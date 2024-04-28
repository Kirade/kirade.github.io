---
description: https://kotlinlang.org/docs/arrays.html
---

# Arrays

array 는 정해진 개수 만큼의 동일한 타입 혹은 서브타입의 데이터를 모아둔 데이터구조이다. 코틀린에서 가장 보편적인 array 구현은 object-type array 인 [Array](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-array/) 클래스이다.

> 만약 원시 타입을 가진 object-type array 를 생성하는 경우, [Boxing](https://app.gitbook.com/o/Oc6vjlzg842PDkWq4YI2/s/Wwemy0ptrx1onUUxiCfZ/\~/changes/16/piece-of-knowledge/java/boxing) 이 발생하여 성능에 영향이 있을 수 있다. 이런 경우 [primitive-type arrarys](https://kotlinlang.org/docs/arrays.html#primitive-type-arrays) 를 사용하는것을 권장한다.

### 언제 Array 를 사용할까?

코틀린에서는 Array 를 특수한 상황의 요구조건을 만족하기 위해서 사용한다. 예를 들어 일반적인 어플리케이션에서 필요하지 않은 성능 적인 요구조건이 있거나, 커스텀 데이터 구조를 만드는 경우 이다. 이런 종류의 제약이 존재하지 않는다면 [collections](https://kotlinlang.org/docs/collections-overview.html) 을 사용하는것을 권장한다.

collections 는 array 에 비해 다음과 같은 장점을 갖는다.

* Collections 는 읽기 전용으로 정의가 가능하여 코드의 제어를 쉽게 하고 제작자의 의도를 명확히 표시할 수 있다.
* 원소들을 쉽게 추가하거나 제거할 수 있다. 반면 array 는 크기가 고정되어 있다. 그래서 원소를 추가하거나 제거하기 위해서는 매번 새로운 array 를 만들어야 한다. 이는 매우 비효율적이다.
* 동등 연산자 ( `==` ) 를 활용하여 collections 이 구조적으로 일치하는지 확인할 수 있다. array 에 대해서는 불가능하다. 대신 [다른 방법](https://kotlinlang.org/docs/arrays.html#compare-arrays)을 활용해야 한다.

### Array 를 생성하는 방법

* `arrayOf()`, `arrayOfNulls()`, `emptyArray()`
* `Array` 생성자

<pre class="language-kotlin"><code class="lang-kotlin">// arrayOf()
// Creates an array with values [1, 2, 3]
val simpleArray = arrayOf(1, 2, 3)
println(simpleArray.joinToString())
// 1, 2, 3

// arrayOfNulls()
// Creates an array with values [null, null, null]
val nullArray: Array&#x3C;Int?> = arrayOfNulls(3)
println(nullArray.joinToString())
// null, null, null

// emptyArray()
var exampleArray = emptyArray&#x3C;String>()

<strong>/**
</strong> * Array Constructor
 */
// Creates an Array&#x3C;Int> that initializes with zeros [0, 0, 0]
val initArray = Array&#x3C;Int>(3) { 0 }
println(initArray.joinToString())
// 0, 0, 0

// Creates an Array&#x3C;String> with values ["0", "1", "4", "9", "16"]
val asc = Array(5) { i -> (i * i).toString() }
asc.forEach { print(it) }
// 014916
</code></pre>

#### Nested Array

```kotlin
// Creates a two-dimensional array
val twoDArray = Array(2) { Array<Int>(2) { 0 } }
println(twoDArray.contentDeepToString())
// [[0, 0], [0, 0]]

// Creates a three-dimensional array
val threeDArray = Array(3) { Array(3) { Array<Int>(3) { 0 } } }
println(threeDArray.contentDeepToString())
// [[[0, 0, 0], [0, 0, 0], [0, 0, 0]], [[0, 0, 0], [0, 0, 0], [0, 0, 0]], [[0, 0, 0], [0, 0, 0], [0, 0, 0]]]
```

### Array 접근과 수정

Array 는 언제나 수정이 가능하다. 접근을 위해서는 [indexed access operator](https://kotlinlang.org/docs/operator-overloading.html#indexed-access-operator) `[]` 를 사용한다.

```kotlin
val simpleArray = arrayOf(1, 2, 3)
val twoDArray = Array(2) { Array<Int>(2) { 0 } }

// Accesses the element and modifies it
simpleArray[0] = 10
twoDArray[0][0] = 2

// Prints the modified element
println(simpleArray[0].toString()) // 10
println(twoDArray[0][0].toString()) // 2
```

코틀린에서의 array 는 불변한다. `String`은 `Any`의 하위타입이 이기 때문에 `Array<Any>` 로 정의된 Array 에 `Array<String>`의 원소를 할당 할 수 있을것 처럼 보이지만 불가능하다.

### Array 사용 예시

코틀린에서는 array 를 함수에 여러 개의 인자를 넘기기 위한 수단으로 활용하거나 array 자체에 어떤 연산을 활용하곤한다. 예를들면 array 끼리 비교하거나, 원소를 변환하거나 혹은 collection 으로 변경하는데 활용한다.

#### 여러개의 인자 넘기기

코틀린에서는 `vararg`를 통해 여러개의 인자를 넘길 수 있다. 이것은 사전에 몇개의 인자를 넘기게 될지 알 수 없는 경우에 유용하게 사용된다. 예를들면 SQL 문을 표현할 문자열을 포매팅 하는경우가 있다.

함수에 array 를 활용해 여러 인자를 넘기기 위해서는 spread operator `*` 를 활용한다. 이것을 활용하면 함수의 인자로 array 의 각 원소들을 넘길 수 있다.

```kotlin
fun main() {
    val lettersArray = arrayOf("c", "d")
    printAllStrings("a", "b", *lettersArray)
    // abcd
}
​
fun printAllStrings(vararg strings: String) {
    for (string in strings) {
        print(string)
    }
}

```

#### Array 비교

두 개의 array 가 같은 원소를 가지고 같은 순서로 이루어져있는지 확인하기 위해서는 `.contentEquals()`와 `.contentDeepEquals()`를 사용한다.

```kotlin
val simpleArray = arrayOf(1, 2, 3)
val anotherArray = arrayOf(1, 2, 3)

// Compares contents of arrays
println(simpleArray.contentEquals(anotherArray))
// true

// Using infix notation, compares contents of arrays after an element 
// is changed
simpleArray[0] = 10
println(simpleArray contentEquals anotherArray)
// false
```

#### Array 변형

코틀린에서는 여러 변형 함수를 제공한다. 매우 많아서 모두 소개하지 않고 [문서](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-array/) 를 참고하면 좋다.

```kotlin
// Sum
val sumArray = arrayOf(1, 2, 3)

// Sums array elements
println(sumArray.sum())
// 6

// Shuffle
val simpleArray = arrayOf(1, 2, 3)

// Shuffles elements [3, 2, 1]
simpleArray.shuffle()
println(simpleArray.joinToString())

// Shuffles elements again [2, 3, 1]
simpleArray.shuffle()
println(simpleArray.joinToString())
```

#### Collection 으로 변환

Collection 과 Array 를 혼용해서 사용하는 환경에서는 서로 적절히 변환을 할 수 있다.

```kotlin
val simpleArray = arrayOf("a", "b", "c", "c")

// Converts to a Set
println(simpleArray.toSet())
// [a, b, c]

// Converts to a List
println(simpleArray.toList())
// [a, b, c, c]


// Converts to a Map
val pairArray = arrayOf("apple" to 120, "banana" to 150, "cherry" to 90, "apple" to 140)

// The keys are fruits and the values are their number of calories
// Note how keys must be unique, so the latest value of "apple"
// overwrites the first
println(pairArray.toMap())
// {apple=140, banana=150, cherry=90}
```

### 원시타입 Array

| Primitive-type array                                                                  | Equivalent in Java |
| ------------------------------------------------------------------------------------- | ------------------ |
| [`BooleanArray`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-boolean-array/) | `boolean[]`        |
| [`ByteArray`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-byte-array/)       | `byte[]`           |
| [`CharArray`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-char-array/)       | `char[]`           |
| [`DoubleArray`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-double-array/)   | `double[]`         |
| [`FloatArray`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-float-array/)     | `float[]`          |
| [`IntArray`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-int-array/)         | `int[]`            |
| [`LongArray`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-long-array/)       | `long[]`           |
| [`ShortArray`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-short-array/)     | `short[]`          |

원시 타입을 위한 Array 를 활용하는 경우 위의 표에서 제공하는 arrary 를 활용해서 Boxing 오버헤드를 피할 수 있다.&#x20;

만약 원시 타입 array 를 object-type array 로 변경하려고 하면 `.toTypedArray()` 를 사용해 변경할 수 있다. 반대의 경우 `.toBooleanArray()`, `.toByteArray()`, `.toCharArray()` 등의 함수를 활용하면된다.





