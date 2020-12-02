## When to inherit Monobehavior class and when not to ?
[C# Question - Do I Have to inherit from MonoBehaviour? What happens if I don't?](https://answers.unity.com/questions/32158/c-question-do-i-have-to-inherit-from-monobehaviour.html)  
>  your classes don't have to inherit from MonoBehaviour, and you can instantiate them in the normal way (using 'new').  
- Inheriting from MonoBehaviour simply gives your scripts extra abilities, such as being able to:
  - be placed on gameobjects
  - have public vars which can be adjusted in the inspector
  - receive Unity events such as Start() Update() FixedUpdate() etc.

> It's worth noting that while you can instantiate other classes using 'new', you shouldn't use 'new' to create new instances of your MonoBehaviour scripts. This is because there are many areas where the functionality of the Monobehaviour relies on assuming that it's attached to a GameObject, and if you create a new one without it being attached to a GO, it can cause it to malfunction and give errors.

For this reason, to create a new instance of a MonoBehaviour at runtime, you should **always use AddComponent** to create and attach it to an existing gameobject at runtime.

## Use public or SerializeField ?
- public - Show up in inspector and accessible by other scripts  
- [SerialiseField] private - Show up in inspector, not accessible by other scripts  
- [HideInInspector] public - Doesn't show in inspector, accessible by other scripts  
- private - Doesn't show in inspector, not accessible by other scripts  
 ```
 /*
                   | available from other classes  |  serialized  |  visible  |
 ------------------------------------------------------------------------------
 [HideInInspector] |               -               |      -       |    No     |
 ------------------------------------------------------------------------------
 [NonSerialized]   |               -               |     No       |    No     |
 ------------------------------------------------------------------------------
 [SerializeField]  |               -               |     Yes      |    Yes    |
 ------------------------------------------------------------------------------
 public modifier   |              Yes              |     Yes      |    Yes    |
 ------------------------------------------------------------------------------
 private,protected |              No               |     No       |    No     |
 internal modifier |                               |              |           |
 ------------------------------------------------------------------------------
 */
```

## Which is the difference between layer and sorting layer ?
[Z-ORDERING SPRITES IN UNITY](http://www.coatbros.com/blog/2015/03/21/z-ordering-sprites-in-unity/)  
[Dynamic draw order or '2D Z-buffer'?](https://forum.unity.com/threads/dynamic-draw-order-or-2d-z-buffer.220231/)
> Sorting Layers are how objects are seen by the camera. This becomes obvious when you remember that sorting layers are attached to the renderer. Therefore, sorting layers (and order in sorting layers) determine how objects are rendered in the scene.  
Layer, up there next to tags, is for grouping objects. Maybe you have a bunch of objects that are similar in that they will be rendered differently from other objects. They would be on different layers. Or, if only certain objects are supposed to be collidable and some are not, they would be on different layers.  
- Sorting layers are visual.  
- Layers are functional.  

## Lifetime of Monobehavior
[Execution Order of Event Functions](https://docs.unity3d.com/Manual/ExecutionOrder.html)  
![](https://docs.unity3d.com/uploads/Main/monobehaviour_flowchart.svg)

## charactor horizontal movement control (with or without inertia)
- 3D
    - **(Recommended)** Component `Character Controller`. Method `Move` or `SimpleMove` 
    - Component `Transform`. Set the value of `transform.position` or use method `Translate`
    - Component `RigidBody` Method `MovePosition`
- 2D
    - Use Component `Transform`
    - Component `Rigidbody2d`. Method `MovePosition`
    - Component `Rigidbody2d`. Set the value of `velocity`

## Input.GetAxis vs Input.GetAxisRaw

## Input.GetButton vs Input.GetButtonDown

## RaycastAll [1]

## Probuilder object is not scriptable

## Instantiate Gameobject use Object.Instantiate

## C sharp multiple key dictionary

[Why is it important to override GetHashCode when Equals method is overridden?](https://stackoverflow.com/questions/371328/why-is-it-important-to-override-gethashcode-when-equals-method-is-overridden)  
Implementations are required to ensure that if the Equals(T, T) method returns true for two objects x and y, then the value returned by the GetHashCode(T) method for x must equal the value returned for y.

## The difference between a field and a property
[What is the difference between a field and a property?](https://stackoverflow.com/questions/295104/what-is-the-difference-between-a-field-and-a-property)  
```c#
public class MyClass
{
    // this is a field.  It is private to your class and stores the actual data.
    private string _myField;

    // this is a property. When accessed it uses the underlying field,
    // but only exposes the contract, which will not be affected by the underlying field
    public string MyProperty
    {
        get
        {
            return _myField;
        }
        set
        {
            _myField = value;
        }
    }

    // This is an AutoProperty (C# 3.0 and higher) - which is a shorthand syntax
    // used to generate a private field for you
    public int AnotherProperty{get;set;} 
}
```

## The difference between struct and class
[Choosing Between Class and Struct](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/choosing-between-class-and-struct)  
Class is a reference type
Struct is a value type

## How to find a prefab via script at RunTime?
```c#
    // Instantiates a prefab named "enemy" located in any Resources
    // folder in your project's Assets folder.
    GameObject instance = Instantiate(Resources.Load("enemy", typeof(GameObject))) as GameObject;
```

## unity get gameobject in scenes
```c#
    public class ExampleClass : MonoBehaviour {
        public GameObject hand;
        void Example() {
            hand = GameObject.Find("Hand");
            hand = GameObject.Find("/Hand");
            hand = GameObject.Find("/Monster/Arm/Hand");
            hand = GameObject.Find("Monster/Arm/Hand");
            // This function only returns active GameObjects. If no GameObject with name can be found, null is returned. If name contains a '/' character, it traverses the hierarchy like a path name.
        }
    }
```

## Awake() vs Start()
[MonoBehaviour.Awake()](https://docs.unity3d.com/ScriptReference/MonoBehaviour.Awake.html)
> Awake is used to initialize any variables or game state before the game starts. Awake is called only once during the lifetime of the script instance. Awake is called after all objects are initialized so you can safely speak to other objects or query them using for example GameObject.FindWithTag. Each GameObject's Awake is called in a random order between objects. Because of this, you should use Awake to set up references between scripts, and use Start to pass any information back and forth. Awake is always called before any Start functions. This allows you to order initialization of scripts. Awake can not act as a coroutine.

[MonoBehaviour.Start()](https://docs.unity3d.com/ScriptReference/MonoBehaviour.Start.html)  

> Start is called on the frame when a script is enabled just before any of the Update methods are called the first time.
Like the Awake function, Start is called exactly once in the lifetime of the script. However, Awake is called when the script object is initialised, regardless of whether or not the script is enabled. Start may not be called on the same frame as Awake if the script is not enabled at initialisation time.
The Awake function is called on all objects in the Scene before any object's Start function is called. This fact is useful in cases where object A's initialisation code needs to rely on object B's already being initialised; B's initialisation should be done in Awake, while A's should be done in Start.
Where objects are instantiated during gameplay, their Awake function is called after the Start functions of Scene objects have already completed.

## SceneManager.sceneLoaded
```C#
public class ExampleCode : MonoBehaviour
{
    // called zero
    void Awake()
    {
        Debug.Log("Awake");
    }

    // called first
    void OnEnable()
    {
        Debug.Log("OnEnable called");
        SceneManager.sceneLoaded += OnSceneLoaded;
    }

    // called second
    void OnSceneLoaded(Scene scene, LoadSceneMode mode)
    {
        Debug.Log("OnSceneLoaded: " + scene.name);
        Debug.Log(mode);
    }

    // called third
    void Start()
    {
        Debug.Log("Start");
    }

    // called when the game is terminated
    void OnDisable()
    {
        Debug.Log("OnDisable");
        SceneManager.sceneLoaded -= OnSceneLoaded;
    }
}
```