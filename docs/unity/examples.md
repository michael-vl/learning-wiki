# Examples — Unity

Self-contained mini-projects. Each is small enough to build in one sitting and teaches one thing well.

---

## 1. Smooth third-person camera follow

`Assets/Scripts/Camera/SmoothFollow.cs`:

```csharp
using UnityEngine;

public class SmoothFollow : MonoBehaviour {
    [SerializeField] Transform target;
    [SerializeField] Vector3 offset = new(0, 5, -8);
    [SerializeField] float positionLerp = 8f;
    [SerializeField] float rotationLerp = 6f;

    void LateUpdate() {
        if (!target) return;
        Vector3 desiredPos = target.position + target.rotation * offset;
        transform.position = Vector3.Lerp(transform.position, desiredPos, positionLerp * Time.deltaTime);
        Quaternion desiredRot = Quaternion.LookRotation(target.position + Vector3.up * 1.5f - transform.position);
        transform.rotation = Quaternion.Slerp(transform.rotation, desiredRot, rotationLerp * Time.deltaTime);
    }
}
```

Notes: in `LateUpdate` (after the player's `Update` has moved them); decouple position and rotation lerp speeds — both feel different and you'll want them tunable separately.

---

## 2. Object pool for bullets

```csharp
using UnityEngine;
using UnityEngine.Pool;

public class BulletSpawner : MonoBehaviour {
    [SerializeField] Bullet bulletPrefab;
    IObjectPool<Bullet> pool;

    void Awake() {
        pool = new ObjectPool<Bullet>(
            createFunc:    () => { var b = Instantiate(bulletPrefab); b.Pool = pool; return b; },
            actionOnGet:   b => b.gameObject.SetActive(true),
            actionOnRelease: b => b.gameObject.SetActive(false),
            actionOnDestroy: b => Destroy(b.gameObject),
            collectionCheck: false,
            defaultCapacity: 32,
            maxSize: 200
        );
    }

    public Bullet Spawn(Vector3 pos, Quaternion rot) {
        var b = pool.Get();
        b.transform.SetPositionAndRotation(pos, rot);
        return b;
    }
}

public class Bullet : MonoBehaviour {
    public IObjectPool<Bullet> Pool { get; set; }
    [SerializeField] float lifetime = 3f;
    [SerializeField] float speed = 30f;

    void OnEnable() => CancelInvoke(nameof(Recycle));
    void OnEnable() : void => Invoke(nameof(Recycle), lifetime);
    void Update() => transform.position += transform.forward * speed * Time.deltaTime;
    void Recycle() => Pool.Release(this);
}
```

Pattern: pool, prefab knows its pool, returns itself on lifetime expiry.

---

## 3. ScriptableObject inventory

```csharp
[CreateAssetMenu(menuName = "Game/Item")]
public class Item : ScriptableObject {
    public string displayName;
    public Sprite icon;
    public int maxStack = 99;
}

[CreateAssetMenu(menuName = "Game/Inventory")]
public class Inventory : ScriptableObject {
    public List<Slot> slots = new();
    public event System.Action OnChanged;

    [System.Serializable]
    public class Slot { public Item item; public int count; }

    public bool Add(Item item, int n) {
        var slot = slots.Find(s => s.item == item && s.count < item.maxStack);
        if (slot != null) {
            int add = Mathf.Min(n, item.maxStack - slot.count);
            slot.count += add;
            n -= add;
        }
        while (n > 0) {
            int add = Mathf.Min(n, item.maxStack);
            slots.Add(new Slot { item = item, count = add });
            n -= add;
        }
        OnChanged?.Invoke();
        return true;
    }
}
```

The inventory is a *singleton-by-asset-reference*. Drag the same `Inventory` SO into player and UI. They both see the same data; both subscribe to OnChanged. No `Instance` static needed.

---

## 4. State machine via interfaces

For an enemy with idle / chase / attack:

```csharp
public interface IState {
    void Enter();
    void Tick();
    void Exit();
}

public class StateMachine {
    IState current;
    public void Change(IState next) {
        current?.Exit();
        current = next;
        current.Enter();
    }
    public void Tick() => current?.Tick();
}
```

Each state is a small class implementing `IState`, taking the enemy as a constructor arg. Cleaner than nested switch statements.

---

## 5. Animator-driven movement

Setup:
- Player has `Animator` referencing a Controller asset.
- Controller has parameters: `Speed` (float), `Jump` (trigger), `Grounded` (bool).
- A 1D blend tree on the base layer driven by `Speed`: idle (0) → walk (3) → run (6).

Code:

```csharp
void Update() {
    Vector3 horizontal = new(rb.linearVelocity.x, 0, rb.linearVelocity.z);
    animator.SetFloat("Speed", horizontal.magnitude);
    animator.SetBool("Grounded", isGrounded);
    if (jumpPressed && isGrounded) animator.SetTrigger("Jump");
}
```

Animator "Apply Root Motion" is **off** for code-driven movement, **on** for animation-driven (in-place mocap moves the character).

---

## 6. UI Toolkit health bar

UI Toolkit (UXML/USS, similar to HTML/CSS) is the modern UI. uGUI (the Canvas system) still works but UI Toolkit is the path forward for non-world-space UI.

UXML:
```xml
<ui:UXML xmlns:ui="UnityEngine.UIElements">
  <ui:VisualElement name="hud" class="hud">
    <ui:VisualElement name="health-bg" class="bar-bg">
      <ui:VisualElement name="health-fill" class="bar-fill" />
    </ui:VisualElement>
    <ui:Label name="score" text="Score: 0" />
  </ui:VisualElement>
</ui:UXML>
```

C#:
```csharp
using UnityEngine;
using UnityEngine.UIElements;

public class HUD : MonoBehaviour {
    [SerializeField] UIDocument document;
    VisualElement healthFill;
    Label scoreLabel;

    void Awake() {
        var root = document.rootVisualElement;
        healthFill = root.Q<VisualElement>("health-fill");
        scoreLabel = root.Q<Label>("score");
    }

    public void SetHealth01(float t) => healthFill.style.width = Length.Percent(Mathf.Clamp01(t) * 100);
    public void SetScore(int s) => scoreLabel.text = $"Score: {s}";
}
```

USS handles styling. Hot reload in the UI Builder (Window > UI Toolkit > UI Builder).

---

## 7. URP custom shader for dissolve

Shader Graph (URP):
1. Create a Shader Graph (Lit). Assign to a material on a mesh.
2. Add a Texture2D property `_Noise` (a noise texture from PolyHaven works).
3. Add a Float property `_Threshold` (0–1).
4. In the graph: sample `_Noise`. Subtract `_Threshold`. Plug into the master node's *Alpha Clip Threshold* — or to *Alpha* with *Surface = Transparent*, *Alpha Clip* on.
5. Add an *Edge* color: `Step(_Noise - _Threshold, 0.05)` masks a thin band around the dissolve front. Multiply by an emission color.

Drive `_Threshold` from script:

```csharp
material.SetFloat("_Threshold", t); // animate t from 0 to 1
```

This is the bones of every "magic disappear" / Thanos snap effect.

---

## 8. Save and load with JSON

```csharp
[System.Serializable]
public class SaveData {
    public string playerName;
    public int level;
    public Vector3 position;
}

public static class SaveSystem {
    static string Path => Application.persistentDataPath + "/save.json";

    public static void Save(SaveData data) =>
        System.IO.File.WriteAllText(Path, JsonUtility.ToJson(data, true));

    public static SaveData Load() {
        if (!System.IO.File.Exists(Path)) return null;
        return JsonUtility.FromJson<SaveData>(System.IO.File.ReadAllText(Path));
    }
}
```

`Application.persistentDataPath` resolves correctly on every platform (Windows AppData, Mac Application Support, iOS/Android sandboxed paths). `JsonUtility` is fast and Unity-aware (Vector3 etc.) but doesn't support dictionaries; use Newtonsoft.Json (built-in package now) for richer serialization.
