# 🟧**코틀린 기본편**

 📌  [강의] Android 를 위한 Kotlin 문법

## 변수 val, var 설명

---

```kotlin
//** 변수 -> 값을 담아두는 박스
//val => 초기값 변경 불가한 변수
val a = "test box"
a = "modified" <- Error 

//var => 초기값 변경 가능한 변수
var b = "test box"
b = "modified" 
println(b)
```

## 타입과 형변환

---

**[타입 종류]**

```kotlin
[타입 종류]
//자료형 -> 숫자(int, Long, double, Float), 문자(String), boolean(true, false)
//1) 변수 선언 시 할당된 값으로 자동 타입 지정
val test3 = "1234"
println(test3::class.java.simpleName)
//2) 변수 선언 시 명시적으로 타입 지정
val test4 : Int = 1234
println(test4::class.java.simpleName)
```

**[형변환]**

```kotlin
[형 변환] : 중간에 타입을 변경 원할 때
//ex. Int타입을 Sting으로 변경
val test 9 : Int = 1234
val test10 = test9.toString()

//ex. String타입을 Int로 변경
val test11 : String = "1234"
val test12 = Integer.parseInt(test11)
```

**[? 변수 - null 가능한 변수 ]**

```kotlin
[? (물음표)] : 변수 선언 시 해당 변수가 null 가능한 변수임 선언
val test15 : String? = null
```

## 조건문(if else, when)

---

**[조건문]**

```kotlin
[조건문]
// if else
val studentScore1 = 100

if(studentScore1 >= 150) {
    println("150 이상")
}else{
    println("150 미만")
}

// when
val score = 100
when(score){
    100 -> {
        println("100")
    }
    90 -> {
        println("90")
    }
    80 ->{
        println("80")
    }
    else -> {
        println("No")
    }
}

```

## ✅ [활용] 간단한 학점 출력 문제

---

```kotlin
//간단한 조건문 이용한 문제풀이
//학생의 A B C D F  점수판단 출력

val score = 80

if(score > 100) {
    println("A")
}else if(score > 90) {
    println("B")
}else if(score >80) {
    println("C")
}else if(score > 70) {
    println("D")
}else {
    println("F")
}
```

## 리스트/filter/물음표 느낌표/반복문

---

**[리스트]**

```kotlin
//리스트 생성 1
val List = ArrayList<String> ()
List.add("a")
List.add("b")
List.add("c")
println(List[0])

//리스트 생성 2
val testList2 = listOf("a", "b", "c")
println(testList2)

//리스트 생성 3
val testList3 = mutableListOf<String>("a", "b", "c")
println(testList3)
testList3.add("d") //추가

println(testList3)

// filter 사용하여 원하는 리스트 사용하기
    //(1)
  val testList4 = listOf("st1", "st2", "st3", "teacher", "st5")
	println(testList4.filter {it.startsWith("st")} ) //s 로 시작하는 애들 가져와라

    
    //(2) null이 포함된 리스트
    
  val testList5 = listOf("student1","student2","student3","student4", "teacher1", "student5", null)
  println(testList5.filterNotNull().filter { it.startsWith("s")})
```

**[물음표? 변수 대입 , 느낌표!! 붙여야 함]**

```kotlin
var test3 : String = "c"
var test4 : String? = "D" //null일 수 있는 변수
test4 = test4!! //!! 얘는 널이 아님을 표현함
```

**[반복문]**

```kotlin
[반복문]
fun main() {
    
  val testList6 = listOf("a", "b", "c", "d")
  for (i in testList6) {
      println(i)
  }
  
  for (i in 1..10 step 2) { //간격 2
      println(i)
  }
 
  for(i in 1..3) {
       println("i의 값은 : " + i)
  }
   
   //중첩 반복문
   for (i in 1..3) {
       for(j in 1..4) {
           println("i is $i j is $j")
       }
   }
}
```

## ✅ 구구단 출력해보기

---

```kotlin
//구구단 출력해보기 
fun main() {
 	for(i in 2..9) {
        for(j in 1..9) {
            println("$i * $j : " + i*j)
        }
    }
}
```

## List/map/set

---

**[List] - mutableList**

```kotlin
	//List
   // mutable 중간에 변경 가능
    val tL1 = mutableListOf("a", "b", "c") 
    tL1.add("d")
    println(tL1)
    
    tL1.remove("a")
    println(tL1)
```

**[Map]**

```kotlin
//Map : 키값과 value 묶어주기 
	
    // 5 유리 10 철수 15 짱구 22 훈이
	
    val testMap = mutableMapOf<Int, String> ()
    testMap.put(5, "유리")
    testMap.put(10, "철수")
    testMap.put(15, "짱구")
    testMap.put(22, "훈이")
		testMap[33] = "나미리선생"

    for(i in testMap) {
			println(i)
	  }
```

**[Set]**

```kotlin
 //Set : 중복 데이터는 거른다. 
    
    val testSet = mutableSetOf("a", "b", "c")
    println(testSet)
    
    testSet.add("d")
    testSet.add("e")
    testSet.add("e")
    println(testSet)
    
    testSet.remove("e")
    println(testSet)
```

## Iterator

---

```kotlin
//Iterator
   val testList2 = mutableListOf("a", "b", "c") //리스트
   
   val testIterator = testList2.listIterator() //리스트를 Iterator 타입으로 변환 
   println(testIterator.next()) //다음값 출력
   println(testIterator.next()) //다음값 출력 
   println(testIterator.hasNext()) //다음값 존재여부 출력 
   println(testIterator.previous()) //이전값 출력 
   
   while(testIterator.hasNext()) { //Iterator가 다음값 존재하는 동안 반복
       println(testIterator.next()) //다음 값 출력 
   }
```

## ✅ 시험점수 50점 이상 찾는 문제

---

```kotlin
//점수가 50점 이상인 사람들 출력하기

fun main() {
    val student = mutableMapOf<Int, String>()
    student[99] = "민지"
    student[20] = "철수"
    student[35] = "민수"
    student[48] = "가영"
    student[100] = "하영"
    student[22] = "수진"
    student[45] = "수달"
    student[88] = "캥거루"
    student[91] = "코알라"
    student[87] = "악어"
    student[54] = "코끼리"
    student[42] = "하마"

    // 점수가 50점 이상인 사람들의 이름만 반복문과 조건문을 통해서 출력하세요~ :)
	val testList = ArrayList<String>()
    
    for (i in student) {
		//println(i.value) //값만 가져오기 
    //println(i.key) //키만 가져오기 
        
        if(i.key >= 50) {
            println(i.value)
            testList.add(i.value)
        }
    }
    
    println(testList)
}
```

## 함수(Function) 이란?

---

```kotlin
//함수 (Function)
// 함수 = 기능

fun main() { //실행 main() 안에서 기능별 함수 호출하면 됨 
  sum(10, 20)
  bobMaking(5)
}

fun sum(a :Int, b:Int) {
    println(a + b)
}

fun bobMaking(time : Int) {
    println("$time 분 후에 밥 완료됨")
}
```

## ✅ 함수 이용 간단한 계산기 만들어보기

---

```kotlin
//간단한 계산기 문제 

fun main() {
   sumTwo(3,4)
   sumThree(3, 4, 5)
   minus(2, 1)
   division(4,2)
   remainder(9,3)
}

fun sumTwo(num1 : Int, num2 : Int) {
    println(num1 + num2)
}
fun sumThree(a1 : Int, a2:Int, a3 :Int) {
    println(a1 + a2 + a3)
}
fun minus(a:Int, b:Int) {
    println(a - b)
}
fun division(a:Int, b:Int) {
    println(a / b)
} 
fun remainder(a:Int, b:Int) {
    println(a % b)
}
```

## 논리 연산(AND OR)

---

```kotlin
//논리연산 
//And : 두 조건 모두 만족해야 함 
//OR : 두 조건 중 하나만 만족하면 됨 

fun main() {
	val a = "남자"
    val b = 10
    
    //And
    if(a == "남자" && b >= 20) {
      	println("AND 만족")
    }else{
        println("AND 불만족")
    }
    
    //OR
    val c = "남자"
    val d = 30
    
    if(c == "남자" || d >= 30) {
        println("OR 만족")
    }else {
        println("OR 불만족 ")
    }
}
```

**[논리 연산 활용한 간단 예제]**

```kotlin
fun main() {
    
    val student = mutableMapOf<Int, String>()
    student[99] = "민지"
    student[20] = "철수"
    student[35] = "민수"
    student[48] = "가영"
    student[100] = "하영"
    student[22] = "수진"
    student[45] = "수달"
    student[88] = "캥거루"
    student[91] = "코알라"
    student[87] = "악어"
    student[54] = "코끼리"
    student[42] = "하마"
    student[1] = "크로커다일"

  	//학생들 중에서 점수 50 이상이면서 학생 이름길이 3이상인 친구만 출력해라 
  
    for(i in student ){
        if(i.key>=50 && i.value.length >= 3) {
           println(i)
        }
    }

}
```

## ✅ 간단한 문자열 가공

---

 

```kotlin
//문자열 가공
// User 입력 데이터 가공 or
// 서버에서 가져온 데이터 원하는 형태로 가공

fun main() {
    
    val testString = "동해물과 백두산이 마르고 닳도록"
    
    //split() : 구분자 기준으로 잘라서 리스트 형태로 반환함
    val newTestString = testString.split(" ") 
    println(newTestString)
    
        //-> 잘린 일부만 추출 원한다면 잘린 리스트 속 [] 인덱스 지정함
        println(newTestString[2])
    
    //substring() : 범위 지정 원하는 글자 가져오기 
  	val splitString = testString.substring(1, 3) // 문자열 속 0~2번째까지의 글자
    println(splitString)
    
    //replace() 문자열 일부만 변환
    val replaceValue = testString.replace("백두산", "한라산")
    println(replaceValue)
}
```

**[문자열 가공 예제 풀기]**

```kotlin
fun main() {
	val testList = ArrayList<String>()
    testList.add("abc1@naver.com")
    testList.add("abc2@google.com")
    testList.add("abc3@daum.com")
    testList.add("abc4@kakao.com")
    testList.add("abc5@naver.com")
    testList.add("abc6@kakao.com")
    testList.add("abc7@naver.com")
    // naver 이메일 갯수 찾고 싶다면 ?
    
    //@ 뒤에 naver. 이어진 이메일을 찾아야 함 
    var count = 0
    for(i in testList ) {
	     //@ 기준으로 문자열 쪼개기 -> 리스트 2개로 나뉠 거임
    	 if(i.split("@")[1].split(".")[0] == "naver") {
         count++
     	}
    }
    println(count)
    
}
```