# 🟧**코틀린 심화편**

## 람다(Lamda)

```kotlin
//람다함수 - 익명함수 

fun main() {

    println(sumNumber(1,2))
    println(sumTypeNumber(1,2))
    
    println(sumTypeNumberNull(1,2))
    
    println(sumString("나는", " 사과."))
    println(sumString2("반드시", " 그렇다"))
}

//람다함수
val sumNumber = {a:Int, b:Int -> a+b}

val sumTypeNumber : (Int, Int) -> Int = {a, b -> a + b}

val sumTypeNumberNull : (Int, Int) -> Int? = {a, b -> null }

val sumString : (String, String) -> String = {a, b -> a+b}

val sumString2 = {a:String, b:String -> a+ b}
```

## 고차함수(High-order Function)

**[고차함수] 함수 안에 다시 함수가 들어가는 꼴** 

```kotlin
//고차함수  : 함수 안에 함수가 들어가는 꼴
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

fun highPrintTest( A : (String) -> Unit) { //Unit은 아무것도 리턴 X
    A("bbb") //여기에 규격맞는 함수 들어갈 수 있음  
}

fun sum(a: Int, b: Int,  operation:(Int, Int) -> Int) {
    println("$a $b")
    println(operation(a,b))
}

fun testSum(a:Int, b:Int) : Int {
    return a+b
}
```

## 제네릭(Generic)

[제네릭] : 제네릭 타입은 컴파일 시 타입을 체크하므로 담을 타입을 처음부터 지정 X

- 이후에 String 값을 넣든, Int 값을 넣든 작동 O

```kotlin
//제네릭(generic)
//컴파일 시 타입 체크 가능 
//타입 캐스팅 필요 X

fun main() {
 	val box1 = Box1(10)
    println(box1.value)
    
    val box2 = Box2("숫자 10")
    println(box2.value)
    
    //제네릭은 컴파일 시 타입을 체크하므로 
    // Int, String 등 제약없이 타입 넣을 수 있음 
    val box3 = Box3(10)
    println(box3.value)
    
    val box4 = Box3("10")
    println(box4.value)
    
    //메소드에 적용한 제네릭 
    println(testFun2("안녕"))
    println(testFun2(1))
    
    println(test(4))
}

//클래스에서 제네릭 사용 
class Box3<T> (test : T) { 
    var value = test 
}
//메소드에서 제네릭 사용 
fun <T> testFun2(a: T) {
	println(a)
}

//일반 객체1
class Box1(test : Int ) {
    var value = test
}
//일반 객체2
class Box2(test : String) {
    var value = test 
}
```

## 오브젝트(object) 객체

```kotlin
//object 객체 -> 싱글톤 패턴
// 객체를 한 개의 종류만 생성한다
// 즉, 매번 다른 종류의 객체가 아니라 늘 같은 종류의 객체 만듬 
fun main() {
 
    val test1 = TestClass()
    val test2 = TestClass()
    test1.count = 10 //test1 객체의 필드 count만 고쳐짐 
    
    println(test1.count)
    println(test2.count) //test1, test2의 count 값은 다름
    
    val test3 = testObjClass 
    val test4 = testObjClass // 이 중 하나만 출력됨 
    test3.count = 10
    println(test3.count)
    println(test4.count) //test3, test4 의 count값은 동일
    
}

//object 객체
object testObjClass {
    init {
        println("obj 클래스 ")
    }
    var count = 0
}

//일반 객체
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
	//분명 다른 변수에 참조 중인데 
    
	test5.plusBtn()
    println(TestObjectClass.number)
    
    test5.plusBtn()
    println(TestObjectClass.number)
    
    test6.plusBtn() //여전히 동일한 종류의 객체에 대해 처리하고 있다
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

## 지연 초기화(lateinit / lazy)

- lateinit 사용 이유 : 서버에서 데이터 받아올 일 생길 수 있는데,
    서버에서 받아온 데이터를 넣어둘 용도로 여러 변수를 우선 lateinit으로 선언만해놓고
    나중에 서버에서 값을 받아왔을 때 해당 변수에 담는 용도로 많이 사용함

```kotlin
fun main() {
   //lateinit 변수 : 나중에 초기화할 변수임 
   //var 변수로 선언하므로 나중에 초기화O. 나중에 초기값 변경도 가능함 
    lateinit var lateString : String 
   
    lateString = "변경처리"
    println(lateString )
   
   //lazy 
   //val 변수로 선언하므로 나중에 초기화해도 중간에 초기값 변경은 불가함 
   val lazyString : String by lazy {
    	println("이 친구가 만들어질 때 프린트함")   
        
        "lazyTestString"
   }
   lazyString  //사용 시 생성되고 값도 할당됨 
    
   println(lazyString)
   
}
```

## infix function

```kotlin
//infix function 
// 중간에 끼워넣어서 사용하는 함수 
fun main() {
 println(10 sum1 20)
 println(20 sum2 30)
 println("사과" sum2 "포도")
}

infix fun Int.sum1(num:Int) :Int = this + num

infix fun Int.sum2(num:Int) :Int = this + num

infix fun String.sum2(abc:String) : String {
    return this + abc
}
```

## kotlin scope function(let / with / run / apply / also)

```kotlin
//kotlin scope 함수 
// let / with / run / apply / also

//let -> null 아닐 때 사용 
//with -> 람다 결과 제공하지 않고 컨텍스트 내부에서 함수를 호출 
//run -> 객체 초기화와 반환 값 계산 필요할 때 주로 사용 
//apply -> 값 반환하지 않고, 객체 구성에 대해 주로 사용 
//also -> 객체에 대해 추가적인 작업

fun main() {
  val str : String? = "hi"
    
  //let 사용 
  val length = str?.let { //null 아닐 때만 동작함
      println(it) 
      it.length
  }
  println(length)
  
  
  //with 사용
 val numbers = mutableListOf("a", "b", "c", "d")
 println(numbers.first())
 println(numbers.last()) 
 
 val firstAndLast = with(numbers) {
    "${first() } ${last() } "
 }
 
 println(firstAndLast )
 
 //run 사용 
 val service = multiPortService("www.naver.com", 80) 
 val result1 = service.query(service.prepareRequest() + "to port ${service.port} ")
 
 println(result1)
 
 val result2 = service.run {
     port = 8080
     query(prepareRequest() + "to port $port ")
 }
 println(result2)

 //apply 사용 
  val tester2 = Person("Tester2").apply{
        age = 21
        city = "Busan"
   }
   println(tester2)
 
 //also 사용 
 val numbers2 = mutableListOf(1,2,3,4)
 numbers2.also {
     println("$numbers 여기에서 5를 추가한다. ")
 }.add(5)
 
}

class multiPortService(var url : String, var port : Int) {
    fun prepareRequest() : String = "기본 요청 url $url"
    fun query(request : String) = "결과 query $request"
}

data class Person(
    var name : String,
    var age : Int = 0,
    var city : String = ""
)
```

## kotlin enum class

```kotlin
// enum 클래스 

fun main() {
 //일부 사용 
 println(Direction.NORTH)
 //모두 사용 
 Direction.values().forEach {
     println(it)
 }
 
 //필터링해서 사용 
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
//enum 클래스 1
enum class Color (val colorName: String) {
    RED("빨강"), 
    GREEN("초록"),
    BLUE("파랑")
}

//enum 클래스 2
enum class Direction {
    NORTH, SOUTH, WEST, EAST
}
```

