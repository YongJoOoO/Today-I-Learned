# 🟧**코틀린 기본에서 나아가기**

## 엘비스 연산자    ?:

---

[ **엘비스 연산자 ( ?: )  ]** 

- **var 변수명 = 변수 ?: (null인 경우의 기본값지정)**

```kotlin
//엘비스 연산자 ( Elvis Operator)
// 엘비스 연산자   ( ?:  ) 
//엘비스연산자란 null과 null이 아닌값을 구별해주는 연산자

//var 변수이름 = 변수 ?: (null일때 Default값지정)
fun main() { 
  	println(findStringLength("avc"))
    println(findStringLength(null))
    
    println(findStringLength3("1234"))
	println(findStringLength3(null))
    
    println(findStringLength4(null))
}

//엘비스 연산자 사용 ?:
fun findStringLength4(str : String?) :Int {
    return str?.length ?: 0 // str이 null인 경우 0 반환 
    
}

//엘비스 연산자 사용 X (1)
fun findStringLength(str : String?) : Int? {
    return str?.length
}
//엘비스 연산자 사용 X (2)
fun findStringLength3(str: String?)	: Int {
    var resultCount = 0
    if(str != null ) {
        resultCount = str.length
    }
    
    return resultCount
}
```

## Any타입 / is , as 연산자

---

**[Any 타입] - 자바의 Object 타입과 비슷한 개념**

```kotlin
var str1 : String = "abc"
str1 = 123 
pritnln(str1) //얘는 에러가 남 
    
var str2 : Any = "abc"
str2 = 123
println(str2) //얘는 정상 처리됨
```

**[is 연산자] : 맞는지 확인용도**

**is → 타입 맞는지 확인용**

```kotlin
fun main() {
    var str3: Any = "abc" // Any 타입객체로 받아놓고 
    
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

**[as 연산자]**

**as -> type casting 타입 변경/체크용**

```kotlin
  var str5 : String = "abc"
  var str6 : String = str5 as String //as : 얘를 String타입으로 대입함

	println(str6)
    
  var str9 : String? = 1 as? String // as?  : 타입매칭 안될 경우 null 
  println(str9)
```

## List  가공 방법

---

```kotlin
// List 가공하기 

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

// distinct() : 리스트 속 중복값 제거해서 가져옴
    println(testList1.distinct()) 
// maxOrNull() : 리스트 속 Max값
    println(testList1.maxOrNull()) 
// minOrNull() : 리스트 속 mIn값
    println(testList1.minOrNull()) 
// average() : 리스트 속 평균값 
    println(testList1.average()) 
-------------------------------------------------------------------------

//filter{it. startsWith("_") } : _로 시작하는 값 필터링해서 가져오기
	val testList2 = listOf("john", "jay", "minsu", "minji", "bokchi")
    
    val result1 = testList2.filter{
        it.startsWith("j")
    }
    println(result1)
}
------------------------------------------------------------------------
	// filter{ it }  // it으로 조건에 맞는 애들만 추출
		val testList3 = listOf(1,2,3,4,5,6)
    val result2 = testList3.filter {
        it % 2 == 0
    }
    println(result2)
    
    
    //groupBy : 해당되는 조건에 맞는 애들끼리 그룹핑
    
    val testList4 = listOf("a", "aa", "aaa", "aaaa")
    val result3 = testList4.groupBy {
        it.length > 2
    }
    println(result3)
    println(result3[true])
```

## 클래스(Class)

---

```kotlin
//클래스 (class)

fun main() {
	var dog = Dog("파트라슈", 20)
    println(dog.getMyDogInfo())
    
    var P1 = Person("사람1", 25) 
    
}

class Dog(name : String , age: Int) {
    val dogName = name
    val dogAge = age
    
    fun getMyDogInfo() : String {
    	return "$dogName : $dogAge"    
 	}
}

class Person(var name:String, var age: Int){
    //init() 함수 - 기본 생성자 
    //생성자 토대로 객체 생성 시 자동 호출되는 함수 
	init {
        println(" ${this.name} ${this.age} ")
    }
    
    //constructor 함수 - 보조 생성자  
    // 반드시 기본생성자 init을 this키워드로 호출하여 초기화 필수 
	constructor(name:String) : this(name, 20) {
        println("${this.name} 보조생성자 실행 ")
    }
    
}
```

## 오버로딩(Overloading)

---

```kotlin
//오버로딩 : 같은 이름 메서드 여러 개 존재
//다만 매개변수의 유형 or 개수만 다름

fun main() {
   val c = Calculator()
   c.sumNumber(1,2)
   c.sumNumber(4,5,6)
   c.sumNumber("나는", " 행복")
}

class Calculator() {
	//모두 sumNumber() 이름의 함수 여러 개 정의 
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

## 상속(Inheritance)

---

```kotlin
//상속 
fun main() {
   Job1()
   Job3()
}

// open 붙은 클래스만 상속받을 수 있음
open class AllJobs() {
    init{
        println("일을 합니다.")
    }
}
//상속 1
class Job1() : AllJobs() {
	
    init{
        println("마케팅 합니다. ")
    }

}
//상속 2 
class Job3() : AllJobs() {
    init{
        println("근로를 합니다.")
    }
}
```

## 상속과 오버라이딩(Overriding)

---

```kotlin
// 상속과 오버라이딩 
// 상속 : 자식 클래스가 부모 클래스의 멤버 물려받음
// 
// 오버라이딩 
// 부모클래스의 open메소드는 자식 클래스에서 재정의 가능

fun main() {
   Child().doing()
   Child().disease()
}

open class Parents() {
	fun doing() {
		println("자식 돌봄")
    }    
    open fun disease(){ //부모의 open 붙은 메소드만 자식이 재정의 가능
        println("비염")
    }
}

class Child() : Parents() {
  	override fun disease() { //부모 메소드 오버라이딩
        //super.disease()
			println("겁이 많아요")
    }
}
```

## 추상클래스(Abstract)

---

```kotlin
//추상클래스 

fun main() {
   BMW().wheel()
   BMW().engine()
}

abstract class Car { //추상클래스 
	//추상메소드 
    abstract fun wheel()
    
    abstract fun engine()
}

//추상 클래스를 상속받은 하위클래스는 추상메소드 전부를 반드시 재정의하여 사용해야 함
class BMW() : Car() { 
	override fun wheel() {
        println("BMW 굴러감")
    }
    override fun engine() {
        println("BMW 시동걸림 ")
    }
}
```

## 인터페이스(Interface)

---

```kotlin
// 인터페이스(interface)
// 인터페이스는 다중 상속 O 

// 클래스의 상속 / 오버라이딩 오버로딩 / 추상클래스 인터페이스

fun main(){

    BMW().autoParking()
}

//추상 클래스 
abstract class Car {

    abstract fun wheel()

    abstract fun engine()

}
//인터페이스 1
interface CarAutoDriving{
    fun autoDriving()
}
인터페이스 2 
interface CarAutoParking{
    fun autoParking()
}

//추상 클래스 + 인터페이스 다중 상속받고 구현한 객체
class BMW() : Car(), CarAutoDriving, CarAutoParking {

    override fun wheel(){
        println("BMW 굴러감")
    }

    override fun engine(){
        println("BMW 엔진시동")
    }

    override fun autoDriving(){
        println("BMW 자율 주행")
    }

    override fun autoParking(){
        println("BMW 자동주차")
    }

}
//추상 클래스만 상속받은 객체 
class Benz() : Car() {

    override fun wheel(){
        println("BMW 굴러감")
    }

    override fun engine(){
        println("BMW 엔진시동")
    }

    fun autoParking(){
        println("BENZ 자동 주차")
    }

}
```

## 데이터 클래스(Data Class)

---

**[데이터 클래스] : 보통 서버에서 데이터셋 가져올 때 사용 多**

```kotlin
//데이터 클래스 ( Data Class) : 데이터 넣는 클래스 

fun main() {
		//일반 클래스 
	  val justDog = JustDog("파트라슈", 32)
	  println(justDog.name)
    println(justDog.age)
    println(justDog.toString() )  // 주소가 출력됨 
   
    //데이터 클래스 
    val dataDog = DataDog("통통", 13)
    println(dataDog.name)
    println(dataDog.age)
    println(dataDog.toString() ) // 데이터 객체 형태가 출력됨 
    //데이터 클래스 
    val dataDog2 = DataDog("곰방", 13) 
    println(dataDog2.toString())
    
}

//일반 클래스 
class JustDog(var name : String, var age : Int )

//데이터 클래스
data class DataDog(var name : String, var age : Int )
```

## 중첩 클래스(Nested Class) / 내부 클래스 (Inner Class)

---

```kotlin
//중첩 클래스 (Nested class) -> 객체지향 / 캡슐화
//내부 클래스 (Inner class) -> RecyclerView

fun main() {
	val test1 = Test1.TestNestedClass()
    test1.testFun1()
    
    val test2 = Test2().Test2InnerClass()
    test2.testFun2()
}

//중첩 클래스 
class Test1 { 
    
    //필드 선언 시
    //val tempText1 = "tempText1"
    //중첩된 클래스는 외부 클래스의 필드 접근 불가 
    
   	class TestNestedClass {
        fun testFun1() {
            println("TestFun1")
            //println(tempText1) //Error
        }
    }
}

//내부 클래스 
class Test2 {
    
    //필드 선언 시 
    //Inner 클래스는 외부 클래스의 필드 접근 가능 
    
    val tempText2 = "tempText2"
    
    inner class Test2InnerClass {
        fun testFun2() {
            println("TsstFun2")
            println(tempText2) //정상 
        }
    }
    
}
```
