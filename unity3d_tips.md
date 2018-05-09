### When to inherit Monobehavior class and when not to ?
[C# Question - Do I Have to inherit from MonoBehaviour? What happens if I don't?](https://answers.unity.com/questions/32158/c-question-do-i-have-to-inherit-from-monobehaviour.html)  
>  your classes don't have to inherit from MonoBehaviour, and you can instantiate them in the normal way (using 'new').

Inheriting from MonoBehaviour simply gives your scripts extra abilities, such as being able to:

be placed on gameobjects
have public vars which can be adjusted in the inspector
receive Unity events such as Start() Update() FixedUpdate() etc.
It's worth noting that while you can instantiate other classes using 'new', you shouldn't use 'new' to create new instances of your MonoBehaviour scripts. This is because there are many areas where the functionality of the Monobehaviour relies on assuming that it's attached to a GameObject, and if you create a new one without it being attached to a GO, it can cause it to malfunction and give errors.

For this reason, to create a new instance of a MonoBehaviour at runtime, you should always use AddComponent to create and attach it to an existing gameobject at runtime.
