#ScriptPlayable and PlayableBehaviour

To create your own custom playable, it must be inherited from the PlayableBehaviour base class.
```
public class MyCustomPlayableBehaviour : PlayableBehaviour
{
    // Implementation of the custom playable behaviour
    // Override PlayableBehaviour methods as needed
}
```
 
To use a PlayableBehaviour as a custom playable, it also must be encapsulated within a ScriptPlayable&lt;&gt; object. If you don’t have an instance of your custom playable, you can create a ScriptPlayable&lt;&gt; for your object by calling:
 
```
ScriptPlayable<MyCustomPlayableBehaviour>.Create(playableGraph);
```
 
If you already have an instance of your custom playable, you can wrap it with a ScriptPlayable&lt;&gt; by calling:
 
```
MyCustomPlayableBehaviour myPlayable = new MyCustomPlayableBehaviour();
ScriptPlayable<MyCustomPlayableBehaviour>.Create(playableGraph, myPlayable);
```
 
In this case, the instance is cloned before it is assigned to the ScriptPlayable&lt;&gt;. As it is, this code does exactly the same as the previous code; the difference is that `myPlayable` can be a public property that would be configured in the inspector, and you can then set up your behaviour for each instance of your script.
 
You can get the PlayableBehaviour object from the ScriptPlayable&lt;&gt; by using the `ScriptPlayable<T> .GetBehaviour()` method.

---

* <span class="page-edit">2017-07-04  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New in Unity [2017.1](../Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>
