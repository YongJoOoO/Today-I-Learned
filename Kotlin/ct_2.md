# ๐ง**์ฝํ๋ฆฐ ๊ธฐ๋ณธ์์ ๋์๊ฐ๊ธฐ**

## ์๋น์ค ์ฐ์ฐ์    ?:

---

[ **์๋น์ค ์ฐ์ฐ์ ( ?: )  ]** 

- **var ๋ณ์๋ช = ๋ณ์ ?: (null์ธ ๊ฒฝ์ฐ์ ๊ธฐ๋ณธ๊ฐ์ง์ )**

```kotlin
//์๋น์ค ์ฐ์ฐ์ ( Elvis Operator)
// ์๋น์ค ์ฐ์ฐ์   ( ?:  ) 
//์๋น์ค์ฐ์ฐ์๋ null๊ณผ null์ด ์๋๊ฐ์ ๊ตฌ๋ณํด์ฃผ๋ ์ฐ์ฐ์

//var ๋ณ์์ด๋ฆ = ๋ณ์ ?: (null์ผ๋ Default๊ฐ์ง์ )
fun main() { 
  	println(findStringLength("avc"))
    println(findStringLength(null))
    
    println(findStringLength3("1234"))
	println(findStringLength3(null))
    
    println(findStringLength4(null))
}

//์๋น์ค ์ฐ์ฐ์ ์ฌ์ฉ ?:
fun findStringLength4(str : String?) :Int {
    return str?.length ?: 0 // str์ด null์ธ ๊ฒฝ์ฐ 0 ๋ฐํ 
    
}

//์๋น์ค ์ฐ์ฐ์ ์ฌ์ฉ X (1)
fun findStringLength(str : String?) : Int? {
    return str?.length
}
//์๋น์ค ์ฐ์ฐ์ ์ฌ์ฉ X (2)
fun findStringLength3(str: String?)	: Int {
    var resultCount = 0
    if(str != null ) {
        resultCount = str.length
    }
    
    return resultCount
}
```

## Anyํ์ / is , as ์ฐ์ฐ์

---

**[Any ํ์] - ์๋ฐ์ Object ํ์๊ณผ ๋น์ทํ ๊ฐ๋**

```kotlin
var str1 : String = "abc"
str1 = 123 
pritnln(str1) //์๋ ์๋ฌ๊ฐ ๋จ 
    
var str2 : Any = "abc"
str2 = 123
println(str2) //์๋ ์ ์ ์ฒ๋ฆฌ๋จ
```

**[is ์ฐ์ฐ์] : ๋ง๋์ง ํ์ธ์ฉ๋**

**is โ ํ์ ๋ง๋์ง ํ์ธ์ฉ**

```kotlin
fun main() {
    var str3: Any = "abc" // Any ํ์๊ฐ์ฒด๋ก ๋ฐ์๋๊ณ  
    
    if(str3 is String) { 
        println("String type")
    }else { 
        println("Not String")
    }

    var str4: Any = "abc" 
    
    when(str4) {
        is Int -> {println("Int")}
        is String -> {println("String")}
        else ->{
			println("this is else ")
        }
    }
```

**[as ์ฐ์ฐ์]**

**as -> type casting ํ์ ๋ณ๊ฒฝ/์ฒดํฌ์ฉ**

```kotlin
  var str5 : String = "abc"
  var str6 : String = str5 as String //as : ์๋ฅผ Stringํ์์ผ๋ก ๋์ํจ

	println(str6)
    
  var str9 : String? = 1 as? String // as?  : ํ์๋งค์นญ ์๋  ๊ฒฝ์ฐ null 
  println(str9)
```

## List  ๊ฐ๊ณต ๋ฐฉ๋ฒ

---

```kotlin
// List ๊ฐ๊ณตํ๊ธฐ 

fun main() {
 	val testList1 = mutableListOf<Int>()
		testList1.add(1)
    testList1.add(2)
    testList1.add(3)
    testList1.add(4)
    testList1.add(10)
    testList1.add(11)
    testList1.add(11)
    testList1.add(11)
    testList1.add(14)

// distinct() : ๋ฆฌ์คํธ ์ ์ค๋ณต๊ฐ ์ ๊ฑฐํด์ ๊ฐ์ ธ์ด
    println(testList1.distinct()) 
// maxOrNull() : ๋ฆฌ์คํธ ์ Max๊ฐ
    println(testList1.maxOrNull()) 
// minOrNull() : ๋ฆฌ์คํธ ์ mIn๊ฐ
    println(testList1.minOrNull()) 
// average() : ๋ฆฌ์คํธ ์ ํ๊ท ๊ฐ 
    println(testList1.average()) 
-------------------------------------------------------------------------

//filter{it. startsWith("_") } : _๋ก ์์ํ๋ ๊ฐ ํํฐ๋งํด์ ๊ฐ์ ธ์ค๊ธฐ
	val testList2 = listOf("john", "jay", "minsu", "minji", "bokchi")
    
    val result1 = testList2.filter{
        it.startsWith("j")
    }
    println(result1)
}
------------------------------------------------------------------------
	// filter{ it }  // it์ผ๋ก ์กฐ๊ฑด์ ๋ง๋ ์ ๋ค๋ง ์ถ์ถ
		val testList3 = listOf(1,2,3,4,5,6)
    val result2 = testList3.filter {
        it % 2 == 0
    }
    println(result2)
    
    
    //groupBy : ํด๋น๋๋ ์กฐ๊ฑด์ ๋ง๋ ์ ๋ค๋ผ๋ฆฌ ๊ทธ๋ฃนํ
    
    val testList4 = listOf("a", "aa", "aaa", "aaaa")
    val result3 = testList4.groupBy {
        it.length > 2
    }
    println(result3)
    println(result3[true])
```

## ํด๋์ค(Class)

---

```kotlin
//ํด๋์ค (class)

fun main() {
	var dog = Dog("ํํธ๋ผ์", 20)
    println(dog.getMyDogInfo())
    
    var P1 = Person("์ฌ๋1", 25) 
    
}

class Dog(name : String , age: Int) {
    val dogName = name
    val dogAge = age
    
    fun getMyDogInfo() : String {
    	return "$dogName : $dogAge"    
 	}
}

class Person(var name:String, var age: Int){
    //init() ํจ์ - ๊ธฐ๋ณธ ์์ฑ์ 
    //์์ฑ์ ํ ๋๋ก ๊ฐ์ฒด ์์ฑ ์ ์๋ ํธ์ถ๋๋ ํจ์ 
	init {
        println(" ${this.name} ${this.age} ")
    }
    
    //constructor ํจ์ - ๋ณด์กฐ ์์ฑ์  
    // ๋ฐ๋์ ๊ธฐ๋ณธ์์ฑ์ init์ thisํค์๋๋ก ํธ์ถํ์ฌ ์ด๊ธฐํ ํ์ 
	constructor(name:String) : this(name, 20) {
        println("${this.name} ๋ณด์กฐ์์ฑ์ ์คํ ")
    }
    
}
```

## ์ค๋ฒ๋ก๋ฉ(Overloading)

---

```kotlin
//์ค๋ฒ๋ก๋ฉ : ๊ฐ์ ์ด๋ฆ ๋ฉ์๋ ์ฌ๋ฌ ๊ฐ ์กด์ฌ
//๋ค๋ง ๋งค๊ฐ๋ณ์์ ์ ํ or ๊ฐ์๋ง ๋ค๋ฆ

fun main() {
   val c = Calculator()
   c.sumNumber(1,2)
   c.sumNumber(4,5,6)
   c.sumNumber("๋๋", " ํ๋ณต")
}

class Calculator() {
	//๋ชจ๋ sumNumber() ์ด๋ฆ์ ํจ์ ์ฌ๋ฌ ๊ฐ ์ ์ 
	fun sumNumber(a : Int , b:Int) {
        println(a + b)
    }
    fun sumNumber(a : Int , b: Int, c: Int) {
        println(a + b+ c)
    }
    fun sumNumber(a:String, b:String) {
        println(a+b)
    }
 
}
```

## ์์(Inheritance)

---

```kotlin
//์์ 
fun main() {
   Job1()
   Job3()
}

// open ๋ถ์ ํด๋์ค๋ง ์์๋ฐ์ ์ ์์
open class AllJobs() {
    init{
        println("์ผ์ ํฉ๋๋ค.")
    }
}
//์์ 1
class Job1() : AllJobs() {
	
    init{
        println("๋ง์ผํ ํฉ๋๋ค. ")
    }

}
//์์ 2 
class Job3() : AllJobs() {
    init{
        println("๊ทผ๋ก๋ฅผ ํฉ๋๋ค.")
    }
}
```

## ์์๊ณผ ์ค๋ฒ๋ผ์ด๋ฉ(Overriding)

---

```kotlin
// ์์๊ณผ ์ค๋ฒ๋ผ์ด๋ฉ 
// ์์ : ์์ ํด๋์ค๊ฐ ๋ถ๋ชจ ํด๋์ค์ ๋ฉค๋ฒ ๋ฌผ๋ ค๋ฐ์
// 
// ์ค๋ฒ๋ผ์ด๋ฉ 
// ๋ถ๋ชจํด๋์ค์ open๋ฉ์๋๋ ์์ ํด๋์ค์์ ์ฌ์ ์ ๊ฐ๋ฅ

fun main() {
   Child().doing()
   Child().disease()
}

open class Parents() {
	fun doing() {
		println("์์ ๋๋ด")
    }    
    open fun disease(){ //๋ถ๋ชจ์ open ๋ถ์ ๋ฉ์๋๋ง ์์์ด ์ฌ์ ์ ๊ฐ๋ฅ
        println("๋น์ผ")
    }
}

class Child() : Parents() {
  	override fun disease() { //๋ถ๋ชจ ๋ฉ์๋ ์ค๋ฒ๋ผ์ด๋ฉ
        //super.disease()
			println("๊ฒ์ด ๋ง์์")
    }
}
```

## ์ถ์ํด๋์ค(Abstract)

---

```kotlin
//์ถ์ํด๋์ค 

fun main() {
   BMW().wheel()
   BMW().engine()
}

abstract class Car { //์ถ์ํด๋์ค 
	//์ถ์๋ฉ์๋ 
    abstract fun wheel()
    
    abstract fun engine()
}

//์ถ์ ํด๋์ค๋ฅผ ์์๋ฐ์ ํ์ํด๋์ค๋ ์ถ์๋ฉ์๋ ์ ๋ถ๋ฅผ ๋ฐ๋์ ์ฌ์ ์ํ์ฌ ์ฌ์ฉํด์ผ ํจ
class BMW() : Car() { 
	override fun wheel() {
        println("BMW ๊ตด๋ฌ๊ฐ")
    }
    override fun engine() {
        println("BMW ์๋๊ฑธ๋ฆผ ")
    }
}
```

## ์ธํฐํ์ด์ค(Interface)

---

```kotlin
// ์ธํฐํ์ด์ค(interface)
// ์ธํฐํ์ด์ค๋ ๋ค์ค ์์ O 

// ํด๋์ค์ ์์ / ์ค๋ฒ๋ผ์ด๋ฉ ์ค๋ฒ๋ก๋ฉ / ์ถ์ํด๋์ค ์ธํฐํ์ด์ค

fun main(){

    BMW().autoParking()
}

//์ถ์ ํด๋์ค 
abstract class Car {

    abstract fun wheel()

    abstract fun engine()

}
//์ธํฐํ์ด์ค 1
interface CarAutoDriving{
    fun autoDriving()
}
์ธํฐํ์ด์ค 2 
interface CarAutoParking{
    fun autoParking()
}

//์ถ์ ํด๋์ค + ์ธํฐํ์ด์ค ๋ค์ค ์์๋ฐ๊ณ  ๊ตฌํํ ๊ฐ์ฒด
class BMW() : Car(), CarAutoDriving, CarAutoParking {

    override fun wheel(){
        println("BMW ๊ตด๋ฌ๊ฐ")
    }

    override fun engine(){
        println("BMW ์์ง์๋")
    }

    override fun autoDriving(){
        println("BMW ์์จ ์ฃผํ")
    }

    override fun autoParking(){
        println("BMW ์๋์ฃผ์ฐจ")
    }

}
//์ถ์ ํด๋์ค๋ง ์์๋ฐ์ ๊ฐ์ฒด 
class Benz() : Car() {

    override fun wheel(){
        println("BMW ๊ตด๋ฌ๊ฐ")
    }

    override fun engine(){
        println("BMW ์์ง์๋")
    }

    fun autoParking(){
        println("BENZ ์๋ ์ฃผ์ฐจ")
    }

}
```

## ๋ฐ์ดํฐ ํด๋์ค(Data Class)

---

**[๋ฐ์ดํฐ ํด๋์ค] : ๋ณดํต ์๋ฒ์์ ๋ฐ์ดํฐ์ ๊ฐ์ ธ์ฌ ๋ ์ฌ์ฉ ๅค**

```kotlin
//๋ฐ์ดํฐ ํด๋์ค ( Data Class) : ๋ฐ์ดํฐ ๋ฃ๋ ํด๋์ค 

fun main() {
		//์ผ๋ฐ ํด๋์ค 
	  val justDog = JustDog("ํํธ๋ผ์", 32)
	  println(justDog.name)
    println(justDog.age)
    println(justDog.toString() )  // ์ฃผ์๊ฐ ์ถ๋ ฅ๋จ 
   
    //๋ฐ์ดํฐ ํด๋์ค 
    val dataDog = DataDog("ํตํต", 13)
    println(dataDog.name)
    println(dataDog.age)
    println(dataDog.toString() ) // ๋ฐ์ดํฐ ๊ฐ์ฒด ํํ๊ฐ ์ถ๋ ฅ๋จ 
    //๋ฐ์ดํฐ ํด๋์ค 
    val dataDog2 = DataDog("๊ณฐ๋ฐฉ", 13) 
    println(dataDog2.toString())
    
}

//์ผ๋ฐ ํด๋์ค 
class JustDog(var name : String, var age : Int )

//๋ฐ์ดํฐ ํด๋์ค
data class DataDog(var name : String, var age : Int )
```

## ์ค์ฒฉ ํด๋์ค(Nested Class) / ๋ด๋ถ ํด๋์ค (Inner Class)

---

```kotlin
//์ค์ฒฉ ํด๋์ค (Nested class) -> ๊ฐ์ฒด์งํฅ / ์บก์ํ
//๋ด๋ถ ํด๋์ค (Inner class) -> RecyclerView

fun main() {
	val test1 = Test1.TestNestedClass()
    test1.testFun1()
    
    val test2 = Test2().Test2InnerClass()
    test2.testFun2()
}

//์ค์ฒฉ ํด๋์ค 
class Test1 { 
    
    //ํ๋ ์ ์ธ ์
    //val tempText1 = "tempText1"
    //์ค์ฒฉ๋ ํด๋์ค๋ ์ธ๋ถ ํด๋์ค์ ํ๋ ์ ๊ทผ ๋ถ๊ฐ 
    
   	class TestNestedClass {
        fun testFun1() {
            println("TestFun1")
            //println(tempText1) //Error
        }
    }
}

//๋ด๋ถ ํด๋์ค 
class Test2 {
    
    //ํ๋ ์ ์ธ ์ 
    //Inner ํด๋์ค๋ ์ธ๋ถ ํด๋์ค์ ํ๋ ์ ๊ทผ ๊ฐ๋ฅ 
    
    val tempText2 = "tempText2"
    
    inner class Test2InnerClass {
        fun testFun2() {
            println("TsstFun2")
            println(tempText2) //์ ์ 
        }
    }
    
}
```
