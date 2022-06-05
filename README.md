# Kotlin standard coding guidelines and naming convention

A style guide for Android developers writing in Kotlin. These guidelines are based on the official Kotlin [coding conventions](https://kotlinlang.org/docs/reference/coding-conventions.html).

## Naming rules

### Package Name

1. Names of packages are always lowercase and do not use underscores its should be __(lowerCamelCase)__

__BAD__:

```kotlin
com.lirisoft.message_plus
```

__GOOD__:

```kotlin
com.lirisoft.message
```


2. Using multi-word names is generally discouraged, but if you do need to use multiple words, you can either just concatenate them together or use camel case __(lowerCamelCase)__

__BAD__:

```kotlin
com.lirisoft.message_plus
```

__GOOD__:

```kotlin
com.lirisoft.messagePluse
```

### Class Name 

Names of classes and objects start with an uppercase letter and use camel case __(UpperCamleCase)__

__BAD__:

```Kotlin
open class Declaration_Processor { /*...*/ }

object EmptyDeclaration_Processor : DeclarationProcessor() { /*...*/ }

```

__GOOD__:

```Kotlin
open class DeclarationProcessor { /*...*/ }

object EmptyDeclarationProcessor : DeclarationProcessor() { /*...*/ }

```

### Function names

Funcation Name should be written in __(lowerCamelCase)__ and no underscores

```Kotlin
fun processDeclarations() { /*...*/ }
```

### Property names

1. Generally property name should be  written in as start with lower case and the use camel case __lowerCamelCase__

Example field names:

```kotlin
class MyClass {
  var publicField: Int = 0
  val person = Person()
  private var privateField: Int?
}
```
2. Names of constants properties marked with const, or top-level or object val propertiesshould use uppercase underscore-separated names:

```Kotlin
 val MAX_COUNT = 8
```

```Kotlin
companion object {
 const val USER_NAME_FIELD = "UserName"
}
```

3.  Names of properties holding references to singleton objects can use the same naming style as object declarations:

```Kotlin
val PersonComparator: Comparator<Person> = /*...*/
```

### backing properties Name 

If a class has two properties which are conceptually the same but one is part of a public API and another is an implementation detail, use an underscore as the prefix for the name of the private property:

```Kotlin
class C {
    private val _elementList = mutableListOf<Element>()

    val elementList: List<Element>
         get() = _elementList
}
```

### Use Good Name for Propertis 

__BAD:__

```kotlin
XMLHTTPRequest
URL: String? 
findPostByID
```
__GOOD:__

```kotlin
XmlHttpRequest
url: String
findPostById
```
## Declarations

### Visibility Modifiers

Only include visibility modifiers if you need something other than the default of public.

**BAD:**

```kotlin
public val wideOpenProperty = 1
private val myOwnPrivateProperty = "private"
```

**GOOD:**

```kotlin
val wideOpenProperty = 1
private val myOwnPrivateProperty = "private"
```

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and member variables.

### Fields & Variables

Prefer single declaration per line.

__GOOD:__

```kotlin
username: String
twitterHandle: String
```

### Classes

Exactly one class per source file, although inner classes are encouraged where scoping appropriate.

### Data Type Objects

Prefer data classes for simple data holding objects.

__BAD:__

```kotlin
class Person(val name: String) {
  override fun toString() : String {
    return "Person(name=$name)"
  }
}
```

__GOOD:__

```kotlin
data class Person(val name: String)
```

### Enum Classes

Enum classes without methods may be formatted without line-breaks, as follows:

```kotlin
private enum CompassDirection { EAST, NORTH, WEST, SOUTH }
```


## Formatting

### Indentation

Use four spaces for indentation. Do not use tabs.

For curly braces, put the opening brace in the end of the line

```Kotlin
if (elements != null) {
    for (element in elements) {
        // ...
    }
}
```

### Class headers

class with primary constructor should be written in one line 

```Kotlin
class Person(id: Int, name: String)
```

if line length is longer then 100 characters then wrap the line 

```Kotlin

class Person(
    id: Int,
    name: String,
    surname: String
) 
```

if class inherite the other class then supperclass constructor call should be on the same line as paranthesis 

```Kotlin

class Person(
    id: Int,
    name: String,
    surname: String
) : Human(id, name) { /*...*/ }
```

If class implements  multiple interfaces, the superclass constructor call should be located first and then each interface should be located in a different line:


```Kotlin

class Person(
    id: Int,
    name: String,
    surname: String
) : Human(id, name),
    KotlinMaker { /*...*/ }
    
```

#### Line Wraps

Indentation for line wraps should use 4 spaces (not the default 8):

__BAD:__

```kotlin
val widget: CoolUiWidget =
        someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line)
```

__GOOD:__

```kotlin
val widget: CoolUiWidget =
    someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line)
```

## Semicolons

semicalon is optional in kotlin.  you should be avoid use of semicolon

__BAD:__

```Kotlin
val numberOfElement = 10;
```


__GOOD:__

```Kotlin
val numberOfElement = 10
```

## Functions

## Long funtion parameter
When a function signature does not fit on a single line, break each parameter declaration onto its own line


```Kotlin
fun longMethodName(
    argument: ArgumentType = defaultValue,
    argument2: AnotherArgumentType,
): ReturnType {
    // body
}
```

### Expression functions

When a function contains only a single expression it can be represented as an expression function.

__BAD:__

```Kotlin
fun foo(): Int {     // bad
    return 1
}
```


__GOOD:__

```Kotlin

fun foo() = 1 
```
### Omit a type of return value

we can omit a type of return value as declaration variables using type interface.

```Kotlin 
fun createIntent(context: Context, foo: Int, bar: Boolean) = 
Intent(context, HogeActivity::class.java).apply {    
   putExtra("foo", foo)
   putExtra("bar", bar)
}

fun hoge(value: Int): String = when (value) {
   in 0..10 -> "foo"
   in 100..500 -> "bar"
   else -> "else"
}
```

## Named Arguments

Use named arguments for function overloading

__BAD:__

```Kotlin
class Person {
   fun personName() {
      print("Anurag")
   }

   fun PersonName(prefix: String) {
       print(prefix + "Anurag")
   }
}

```


__GOOD:__

```Kotlin
class Person {
   fun PersonName(prefix: String = "") {
      print(prefix + "Anurag")
   }
}
```

## Braces

Braces are not required for __when__ and __if__ statement  which have no else if/else branches and which fit on a single line.

```Kotlin
if (string.isEmpty()) return

when (value) {
    0 -> return
    // …
}

```

Conditional statements are always required to be enclosed with braces

__BAD:__

```kotlin
if (someTest)
  doSomething()
if (someTest) doSomethingElse()
```

__GOOD:__

```kotlin
if (someTest) {
  doSomething()
}
if (someTest) { doSomethingElse() }
```

### Non-empty blocks

No line break before the opening brace.
Line break after the opening brace.
Line break before the closing brace.
Line break after the closing brace, only if that brace terminates a statement or terminates the body of a function, constructor, or named class. For example, there is no line break after the brace if it is followed by else or a comma.

```Kotlin

return Runnable {
    while (condition()) {
        foo()
    }
}

return object : MyClass() {
    override fun foo() {
        if (condition()) {
            try {
                something()
            } catch (e: ProblemException) {
                recover()
            }
        } else if (otherCondition()) {
            somethingElse()
        } else {
            lastThing()
        }
    }
}
```

### Empty blocks

Empty blocks

__BAD:__

```Kotlin
try {
    doSomething()
} catch (e: Exception) {} // WRONG!
```


__GOOD:__

```Kotlin
try {
    doSomething()
} catch (e: Exception) {
} // Okay
```

### Expressions

An if/else conditional that is used as an expression may omit braces only if the entire expression fits on one line.

```Kotlin
val value = if (string.isEmpty()) 0 else 1  // Okay

```

__BAD:__

```Kotlin
val value = if (string.isEmpty())  // WRONG!
    0
else
    1
```


__GOOD:__

```Kotlin
val value = if (string.isEmpty()) { // Okay
    0
} else {
    1
}
```

### Companion Objects

Companion objects, such as those for Fragment newInstance methods, should be defined at the bottom of a class declaration

```Kotlin 
class MyFragment : Fragment() {

    init {
        Injector.INSTANCE.inject(this)
    }

    @Inject
    lateinit var dataManager: DataManager

    fun doSomething() {
        // ...
    }

    companion object {
        const val BUNDLE_VALUE_ONE = "bundle_value_one"

        fun newInstance(value1: String, value2: String): MyFragment {
            // ...
        }
    }
}

```

## Modifiers order

If a declaration has multiple modifiers, always put them in the following order:

```Kotlin 
public / protected / private / internal
expect / actual
final / open / abstract / sealed / const
external
override
lateinit
tailrec
vararg
suspend
inner
enum / annotation / fun // as a modifier in `fun interface`
companion
inline / value
infix
operator
data
```

There many more in kotlin guide line....


## Credits

- [coding conventions](https://kotlinlang.org/docs/reference/coding-conventions.html).
- [kotlin style Guide](https://developer.android.com/kotlin/style-guide)







