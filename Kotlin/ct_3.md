# π§**μ½νλ¦° μ¬ννΈ**

## λλ€(Lamda)

```kotlin
//λλ€ν¨μ - μ΅λͺν¨μ 

fun main() {

    println(sumNumber(1,2))
    println(sumTypeNumber(1,2))
    
    println(sumTypeNumberNull(1,2))
    
    println(sumString("λλ", " μ¬κ³Ό."))
    println(sumString2("λ°λμ", " κ·Έλ λ€"))
}

//λλ€ν¨μ
val sumNumber = {a:Int, b:Int -> a+b}

val sumTypeNumber : (Int, Int) -> Int = {a, b -> a + b}

val sumTypeNumberNull : (Int, Int) -> Int? = {a, b -> null }

val sumString : (String, String) -> String = {a, b -> a+b}

val sumString2 = {a:String, b:String -> a+ b}
```

## κ³ μ°¨ν¨μ(High-order Function)

**[κ³ μ°¨ν¨μ] ν¨μ μμ λ€μ ν¨μκ° λ€μ΄κ°λ κΌ΄** 

```kotlin
//κ³ μ°¨ν¨μ  : ν¨μ μμ ν¨μκ° λ€μ΄κ°λ κΌ΄
//f(x) = x  
// f(f(x)) = x

fun main() {
  	sum(1, 2, {a:Int, b:Int -> a+b})
    
    sum(1,2, ::testSum) 
    
    highPrintTest(::printTest) 
}

fun printTest(str : String) {
    println(str)
}

fun highPrintTest( A : (String) -> Unit) { //Unitμ μλ¬΄κ²λ λ¦¬ν΄ X
    A("bbb") //μ¬κΈ°μ κ·κ²©λ§λ ν¨μ λ€μ΄κ° μ μμ  
}

fun sum(a: Int, b: Int,  operation:(Int, Int) -> Int) {
    println("$a $b")
    println(operation(a,b))
}

fun testSum(a:Int, b:Int) : Int {
    return a+b
}
```

## μ λ€λ¦­(Generic)

[μ λ€λ¦­] : μ λ€λ¦­ νμμ μ»΄νμΌ μ νμμ μ²΄ν¬νλ―λ‘ λ΄μ νμμ μ²μλΆν° μ§μ  X

- μ΄νμ String κ°μ λ£λ , Int κ°μ λ£λ  μλ O

```kotlin
//μ λ€λ¦­(generic)
//μ»΄νμΌ μ νμ μ²΄ν¬ κ°λ₯ 
//νμ μΊμ€ν νμ X

fun main() {
 	val box1 = Box1(10)
    println(box1.value)
    
    val box2 = Box2("μ«μ 10")
    println(box2.value)
    
    //μ λ€λ¦­μ μ»΄νμΌ μ νμμ μ²΄ν¬νλ―λ‘ 
    // Int, String λ± μ μ½μμ΄ νμ λ£μ μ μμ 
    val box3 = Box3(10)
    println(box3.value)
    
    val box4 = Box3("10")
    println(box4.value)
    
    //λ©μλμ μ μ©ν μ λ€λ¦­ 
    println(testFun2("μλ"))
    println(testFun2(1))
    
    println(test(4))
}

//ν΄λμ€μμ μ λ€λ¦­ μ¬μ© 
class Box3<T> (test : T) { 
    var value = test 
}
//λ©μλμμ μ λ€λ¦­ μ¬μ© 
fun <T> testFun2(a: T) {
	println(a)
}

//μΌλ° κ°μ²΄1
class Box1(test : Int ) {
    var value = test
}
//μΌλ° κ°μ²΄2
class Box2(test : String) {
    var value = test 
}
```

## μ€λΈμ νΈ(object) κ°μ²΄

```kotlin
//object κ°μ²΄ -> μ±κΈν€ ν¨ν΄
// κ°μ²΄λ₯Ό ν κ°μ μ’λ₯λ§ μμ±νλ€
// μ¦, λ§€λ² λ€λ₯Έ μ’λ₯μ κ°μ²΄κ° μλλΌ λ κ°μ μ’λ₯μ κ°μ²΄ λ§λ¬ 
fun main() {
 
    val test1 = TestClass()
    val test2 = TestClass()
    test1.count = 10 //test1 κ°μ²΄μ νλ countλ§ κ³ μ³μ§ 
    
    println(test1.count)
    println(test2.count) //test1, test2μ count κ°μ λ€λ¦
    
    val test3 = testObjClass 
    val test4 = testObjClass // μ΄ μ€ νλλ§ μΆλ ₯λ¨ 
    test3.count = 10
    println(test3.count)
    println(test4.count) //test3, test4 μ countκ°μ λμΌ
    
}

//object κ°μ²΄
object testObjClass {
    init {
        println("obj ν΄λμ€ ")
    }
    var count = 0
}

//μΌλ° κ°μ²΄
class TestClass{
    
    init{
        println("TestClass ")
    }
	var count = 0
}
```

```kotlin
fun main() {
    val test5 = TestObjectClass()
    val test6 = TestObjectClass() 
	//λΆλͺ λ€λ₯Έ λ³μμ μ°Έμ‘° μ€μΈλ° 
    
	test5.plusBtn()
    println(TestObjectClass.number)
    
    test5.plusBtn()
    println(TestObjectClass.number)
    
    test6.plusBtn() //μ¬μ ν λμΌν μ’λ₯μ κ°μ²΄μ λν΄ μ²λ¦¬νκ³  μλ€
    println(TestObjectClass.number)
    
}

class TestObjectClass {
    companion object {
        var number = 0
    }
    fun plusBtn() {
        number++
    }
    fun minusBtn() {
		number--
    }
}
```

## μ§μ° μ΄κΈ°ν(lateinit / lazy)

- lateinit μ¬μ© μ΄μ  : μλ²μμ λ°μ΄ν° λ°μμ¬ μΌ μκΈΈ μ μλλ°,
    μλ²μμ λ°μμ¨ λ°μ΄ν°λ₯Ό λ£μ΄λ μ©λλ‘ μ¬λ¬ λ³μλ₯Ό μ°μ  lateinitμΌλ‘ μ μΈλ§ν΄λκ³ 
    λμ€μ μλ²μμ κ°μ λ°μμμ λ ν΄λΉ λ³μμ λ΄λ μ©λλ‘ λ§μ΄ μ¬μ©ν¨

```kotlin
fun main() {
   //lateinit λ³μ : λμ€μ μ΄κΈ°νν  λ³μμ 
   //var λ³μλ‘ μ μΈνλ―λ‘ λμ€μ μ΄κΈ°νO. λμ€μ μ΄κΈ°κ° λ³κ²½λ κ°λ₯ν¨ 
    lateinit var lateString : String 
   
    lateString = "λ³κ²½μ²λ¦¬"
    println(lateString )
   
   //lazy 
   //val λ³μλ‘ μ μΈνλ―λ‘ λμ€μ μ΄κΈ°νν΄λ μ€κ°μ μ΄κΈ°κ° λ³κ²½μ λΆκ°ν¨ 
   val lazyString : String by lazy {
    	println("μ΄ μΉκ΅¬κ° λ§λ€μ΄μ§ λ νλ¦°νΈν¨")   
        
        "lazyTestString"
   }
   lazyString  //μ¬μ© μ μμ±λκ³  κ°λ ν λΉλ¨ 
    
   println(lazyString)
   
}
```

## infix function

```kotlin
//infix function 
// μ€κ°μ λΌμλ£μ΄μ μ¬μ©νλ ν¨μ 
fun main() {
 println(10 sum1 20)
 println(20 sum2 30)
 println("μ¬κ³Ό" sum2 "ν¬λ")
}

infix fun Int.sum1(num:Int) :Int = this + num

infix fun Int.sum2(num:Int) :Int = this + num

infix fun String.sum2(abc:String) : String {
    return this + abc
}
```

## kotlin scope function(let / with / run / apply / also)

```kotlin
//kotlin scope ν¨μ 
// let / with / run / apply / also

//let -> null μλ λ μ¬μ© 
//with -> λλ€ κ²°κ³Ό μ κ³΅νμ§ μκ³  μ»¨νμ€νΈ λ΄λΆμμ ν¨μλ₯Ό νΈμΆ 
//run -> κ°μ²΄ μ΄κΈ°νμ λ°ν κ° κ³μ° νμν  λ μ£Όλ‘ μ¬μ© 
//apply -> κ° λ°ννμ§ μκ³ , κ°μ²΄ κ΅¬μ±μ λν΄ μ£Όλ‘ μ¬μ© 
//also -> κ°μ²΄μ λν΄ μΆκ°μ μΈ μμ

fun main() {
  val str : String? = "hi"
    
  //let μ¬μ© 
  val length = str?.let { //null μλ λλ§ λμν¨
      println(it) 
      it.length
  }
  println(length)
  
  
  //with μ¬μ©
 val numbers = mutableListOf("a", "b", "c", "d")
 println(numbers.first())
 println(numbers.last()) 
 
 val firstAndLast = with(numbers) {
    "${first() } ${last() } "
 }
 
 println(firstAndLast )
 
 //run μ¬μ© 
 val service = multiPortService("www.naver.com", 80) 
 val result1 = service.query(service.prepareRequest() + "to port ${service.port} ")
 
 println(result1)
 
 val result2 = service.run {
     port = 8080
     query(prepareRequest() + "to port $port ")
 }
 println(result2)

 //apply μ¬μ© 
  val tester2 = Person("Tester2").apply{
        age = 21
        city = "Busan"
   }
   println(tester2)
 
 //also μ¬μ© 
 val numbers2 = mutableListOf(1,2,3,4)
 numbers2.also {
     println("$numbers μ¬κΈ°μμ 5λ₯Ό μΆκ°νλ€. ")
 }.add(5)
 
}

class multiPortService(var url : String, var port : Int) {
    fun prepareRequest() : String = "κΈ°λ³Έ μμ²­ url $url"
    fun query(request : String) = "κ²°κ³Ό query $request"
}

data class Person(
    var name : String,
    var age : Int = 0,
    var city : String = ""
)
```

## kotlin enum class

```kotlin
// enum ν΄λμ€ 

fun main() {
 //μΌλΆ μ¬μ© 
 println(Direction.NORTH)
 //λͺ¨λ μ¬μ© 
 Direction.values().forEach {
     println(it)
 }
 
 //νν°λ§ν΄μ μ¬μ© 
 val direction = Direction.EAST
 when(direction) {
     Direction.NORTH -> {
         println("N")
     }
     Direction.SOUTH -> {
         println("S")
     }
     Direction.WEST -> {
		println("W")
     }
     Direction.EAST -> {
         println( "E")
     }
 }
 

 val color = Color.RED
   
 when(color) {
     Color.RED -> {
         println(Color.RED.colorName)
     }
     Color.GREEN -> {
         println(Color.GREEN.colorName)
     }
     Color.BLUE -> {
         println(Color.BLUE.colorName)
     }
 }
 
}
//enum ν΄λμ€ 1
enum class Color (val colorName: String) {
    RED("λΉ¨κ°"), 
    GREEN("μ΄λ‘"),
    BLUE("νλ")
}

//enum ν΄λμ€ 2
enum class Direction {
    NORTH, SOUTH, WEST, EAST
}
```

