# Unity Test Runner utilities

The Unity Test Runner contains utilities that can be used with `NUnit` constraints for comparing floating point values and some non-primitive objects like `Vector2`, `Vector4` and so on. These classes are placed in the `UnityEngine.TestTools.Utils` namespace.

## Class: Utils
A class that contains utility functions.

### AreFloatsEqual
**Signature** `public static bool AreFloatsEqual(float expected, float actual, float allowedRelativeError)`

**Description**
This method does a *relative epsilon comparison* of two floating point numbers for equality, and takes the relative error as the third parameter. The relative error is the absolute error divided by the magnitude of the exact value.

**Usage**

```csharp
using NUnit.Framework;
using UnityEngine.TestTools.Utils;

[TestFixture]
public class UtilTests
{
    [Test]
    public void FloatsAreEqual()
    {
        float expected = 10e-8f;
        float actual = 0f;
        float allowedRelativeError = 10e-6f;
        Assert.That(Utils.AreFloatsEqual(expected, actual, allowedRelativeError), Is.True);
    }
}
```

### AreFloatsEqualAbsoluteError
**Signature** `public static bool AreFloatsEqualAbsoluteError(float expected, float actual, float allowedAbsoluteError)`

**Description**
This method compares two floating point numbers for equality under the given tolerance.

**Usage**

```csharp
using NUnit.Framework;
using UnityEngine.TestTools.Utils;

[TestFixture]
public class UtilTests
{
    [Test]
    public void FloatsAreAbsoluteEqual()
    {
        float expected = 0f;
        float actual = 10e-6f;
        float error = 10e-5f;
        Assert.That(Utils.AreFloatsEqualAbsoluteError(expected, actual, error), Is.True);
    }
}
```

### CreatePrimitive
**Signature** public static GameObject CreatePrimitive(PrimitiveType type)

**Description**
This is analogous to `GameObject.CreatePrimitive`, but creates a primitive mesh renderer with a fast shader instead of the default built-in shader, optimized for testing performance. It returns a `GameObject` with primitive mesh renderer and collider.

**Usage**

```csharp
var box = Utils.CreatePrimitive(PrimitiveType.Cube);
```

## FloatEqualityComparer
This implements `System.Collections.Generic.IEqualityComparer<float>`. This comparer can be used with `NUnit` constraints to compare two float values for equality using *relative epsilon comparison*. Internally, this comparer uses `Utils.AreFloatsEqual` to compare float values.

**Usage**

```csharp
using NUnit.Framework;
using UnityEngine.TestTools.Utils;

[TestFixture]
public class FloatsTest
{
    [Test]
    public void FloatsAreEqual()
    {
        var comparer = new FloatEqualityComparer(10e-6f);
        var actual = -0.00009f;
        var expected = 0.00009f
        Assert.That(actual, Is.EqualTo(expected).Using(comparer));

        //Default allowed relative error 0.0001f
        var actual = -0.01f;
        var expected = 0.001f
        Assert.That(actual, Is.EqualTo(expected).Using(FloatEqualityComparer.Instance));
    }
}
```

## ColorEqualityComparer

Use this class to compare two `UnityEngine.Color` objects for equality, with `NUnit` constraints. This class implements the `System.Collections.Generic.IEqualityComparer<Color>` interface. It considers `0.01f` as the default error for comparisons if a value is not provided in the `ColorEqualityComparer` constructor.

**Usage**

```csharp
using UnityEngine;
using NUnit.Framework;
using UnityEngine.TestTools.Utils;

[TestFixture]
public class ColorTest
{
    [Test]
    public void ColorsAreEqual()
    {
        //Allowed error 10e-5f
        var comparer = new ColorEqualityComparer(10e-5f);
        var firstColor = new Color(0f, 0f, 0f, 1f);
        var secondColor = new Color(10e-6f, 0f, 0f, 1f);
        Assert.That(firstColor, Is.EqualTo(secondColor).Using(comparer));

        //Using default error
        firstColor = new Color(0f, 0f, 0f, 0f);
        secondColor = new Color(0f, 0f, 0f, 0f);
        Assert.That(firstColor, Is.EqualTo(secondColor).Using(ColorEqualityComparer.Instance));
    }
}
```

## QuaternionEqualityComparer
Use this class to compare two `UnityEngine.Quaternion` objects for equality, with `NUnit` constraints. This class implements the `System.Collections.Generic.IEqualityComparer<Quaternion>` interface. Use the static instance `Instance` to compare with default error `0.00001f`. For any custom error value, use the single argument constructor.

**Usage**

```csharp
using UnityEngine;
using NUnit.Framework;
using UnityEngine.TestTools.Utils;

[TestFixture]
public class QuaternionTest
{
    [Test]
    public void QuaternionsAreEqual()
    {
        var actual = new Quaternion(10f, 0f, 0f, 0f);
        var expected = new Quaternion(1f, 10f, 0f, 0f);
        var comparer = new QuaternionEqualityComparer(10e-6f);
        Assert.That(actual, Is.EqualTo(expected).Using(comparer));
    }
}
```

## Vector2EqualityComparer
Use this class to compare two `UnityEngine.Vector2` objects for equality, with `NUnit` constraints. This class implements the `System.Collections.Generic.IEqualityComparer<Vector2>` interface. Use the static `Instance` member to compare using default error `0.0001f`. You can supply a custom error value while constructing the comparer object. It uses a *relative epsilon comparison* (the absolute error divided by the magnitude of the exact value) of `Utils.AreFloatsEqual` to compare individual coordinates.

**Usage**

```csharp
using UnityEngine;
using NUnit.Framework;
using UnityEngine.TestTools.Utils;

[TestFixture]
public class Vector2Test
{
    [Test]
    public void Vector2AreEqual()
    {
        //Custom error
        var actual = new Vector2(10e-7f, 10e-7f);
        var expected = new Vector2(0f, 0f);
        var comparer = new Vector2EqualityComparer(10e-6f);
        Assert.That(actual, Is.EqualTo(expected).Using(comparer));

        //Default error 0.0001f
        actual = new Vector2(0.01f, 0.01f);
        expected = new Vector2(0.01f, 0.01f);
        Assert.That(actual, Is.EqualTo(expected).Using(Vector2EqualityComparer.Instance));
    }
}
```

## Vector3EqualityComparer
Use this class to compare two `UnityEngine.Vector3` objects for equality, with `NUnit` constraints. This class implements the `System.Collections.Generic.IEqualityComparer<Vector3>` interface. Use the static `Instance` member to compare using default error `0.0001f`. You can supply a custom error value while constructing the comparer object. It uses a *relative epsilon comparison* (the absolute error divided by the magnitude of the exact value) of `Utils.AreFloatsEqual` to compare individual coordinates.

**Usage**

```csharp

using UnityEngine;
using NUnit.Framework;
using UnityEngine.TestTools.Utils;

[TestFixture]
public class Vector3Test
{
    [Test]
    public void Vector3AreEqual()
    {
        //Custom error 10e-6f
        var actual = new Vector3(10e-8f, 10e-8f, 10e-8f);
        var expected = new Vector3(0f, 0f, 0f);
        var comparer = new Vector3EqualityComparer(10e-6f);
        Assert.That(actual, Is.EqualTo(expected).Using(comparer));

        //Default error 0.0001f
        actual = new Vector3(0.01f, 0.01f, 0f);
        expected = new Vector3(0.01f, 0.01f, 0f);
        Assert.That(actual, Is.EqualTo(expected).Using(Vector3EqualityComparer.Instance));
    }
}
```

## Vector4EqualityComparer
Use this class to compare two `UnityEngine.Vector4` objects for equality, with `NUnit` constraints. This class implements the `System.Collections.Generic.IEqualityComparer<Vector4>` interface. Use the static `Instance` member to compare using default error `0.0001f`. You can supply a custom error value while constructing the comparer object. It uses a *relative epsilon comparison* (the absolute error divided by the magnitude of the exact value) of `Utils.AreFloatsEqual` to compare individual coordinates.

**Usage**

```csharp
using UnityEngine;
using NUnit.Framework;
using UnityEngine.TestTools.Utils;

[TestFixture]
public class Vector4Test
{
    [Test]
    public void Vector4AreEqual()
    {
        //Custom error 10e-6f
        var actual = new Vector4(0, 0, 1e-6f, 1e-6f);
        var expected = new Vector4(1e-6f, 0f, 0f, 0f);
        var comparer = new Vector4EqualityComparer(10e-6f);
        Assert.That(actual, Is.EqualTo(expected).Using(comparer));

        //Default error 0.0001f
        actual = new Vector4(0.01f, 0.01f, 0f, 0f);
        expected = new Vector4(0.01f, 0.01f, 0f, 0f);
        Assert.That(actual, Is.EqualTo(expected).Using(Vector4EqualityComparer.Instance));
    }
}
```

## Vector2ComparerWithEqualsOperator
Use this class to compare two `UnityEngine.Vector2` objects for equality, with `NUnit` constraints. This class implements the `System.Collections.Generic.IEqualityComparer<Vector2>` interface. It uses the overload `operator==` of `UnityEngine.Vector2` to compare two `Vector2` objects.

**Usage**

```csharp
using UnityEngine;
using NUnit.Framework;
using UnityEngine.TestTools.Utils;

[TestFixture]
public class Vector2Test
{
    [Test]
    public void VectorsAreEqual()
    {
        var actual = new Vector2(10e-7f, 10e-7f);
        var expected = new Vector2(0f, 0f);
        Assert.That(actual, Is.EqualTo(expected).Using(Vector2ComparerWithEqualsOperator.Instance));
    }
}
```


## Vector3ComparerWithEqualsOperator
Use this class to compare two `UnityEngine.Vector3` objects for equality, with `NUnit` constraints. This class implements the `System.Collections.Generic.IEqualityComparer<Vector3>` interface. It uses the overload `operator==` of `UnityEngine.Vector3` to compare two `Vector3` objects.

**Usage**

```csharp
using UnityEngine;
using NUnit.Framework;
using UnityEngine.TestTools.Utils;

[TestFixture]
public class Vector3Test
{
    [Test]
    public void VectorsAreEqual()
    {
        var actual = new Vector3(10e-7f, 10e-7f, 10e-7f);
        var expected = new Vector2(0f, 0f, 0f);
        Assert.That(actual, Is.EqualTo(expected).Using(Vector3ComparerWithEqualsOperator.Instance));
    }
}
```

## Vector4ComparerWithEqualsOperator
Use this class to compare two `UnityEngine.Vector4` objects for equality, with `NUnit` constraints. This class implements the `System.Collections.Generic.IEqualityComparer<Vector4>` interface. It uses the overload `operator==` of `UnityEngine.Vector4` to compare two `Vector4` objects.

**Usage**

```csharp
using UnityEngine;
using NUnit.Framework;
using UnityEngine.TestTools.Utils;

[TestFixture]
public class Vector4Test
{
    [Test]
    public void Vector4AreEqual()
    {
        var actual = new Vector4(0, 0, 1e-6f, 1e-6f);
        var expected = new Vector4(1e-6f, 0f, 0f, 0f);
        Assert.That(actual, Is.EqualTo(expected).Using(Vector4ComparerWithEqualsOperator.Instance));
    }
}
```

---

* <span class="page-edit">2017-09-13 <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Playmode test framework utilities added in [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20173) <span class="search-words">NewIn20173</span></span>
