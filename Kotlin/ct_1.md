# ๐ง**์ฝํ๋ฆฐ ๊ธฐ๋ณธํธ**

 ๐  [๊ฐ์] Android ๋ฅผ ์ํ Kotlin ๋ฌธ๋ฒ

## ๋ณ์ val, var ์ค๋ช

---

```kotlin
//** ๋ณ์ -> ๊ฐ์ ๋ด์๋๋ ๋ฐ์ค
//val => ์ด๊ธฐ๊ฐ ๋ณ๊ฒฝ ๋ถ๊ฐํ ๋ณ์
val a = "test box"
a = "modified" <- Error 

//var => ์ด๊ธฐ๊ฐ ๋ณ๊ฒฝ ๊ฐ๋ฅํ ๋ณ์
var b = "test box"
b = "modified" 
println(b)
```

## ํ์๊ณผ ํ๋ณํ

---

**[ํ์ ์ข๋ฅ]**

```kotlin
[ํ์ ์ข๋ฅ]
//์๋ฃํ -> ์ซ์(int, Long, double, Float), ๋ฌธ์(String), boolean(true, false)
//1) ๋ณ์ ์ ์ธ ์ ํ ๋น๋ ๊ฐ์ผ๋ก ์๋ ํ์ ์ง์ 
val test3 = "1234"
println(test3::class.java.simpleName)
//2) ๋ณ์ ์ ์ธ ์ ๋ช์์ ์ผ๋ก ํ์ ์ง์ 
val test4 : Int = 1234
println(test4::class.java.simpleName)
```

**[ํ๋ณํ]**

```kotlin
[ํ ๋ณํ] : ์ค๊ฐ์ ํ์์ ๋ณ๊ฒฝ ์ํ  ๋
//ex. Intํ์์ Sting์ผ๋ก ๋ณ๊ฒฝ
val test 9 : Int = 1234
val test10 = test9.toString()

//ex. Stringํ์์ Int๋ก ๋ณ๊ฒฝ
val test11 : String = "1234"
val test12 = Integer.parseInt(test11)
```

**[? ๋ณ์ - null ๊ฐ๋ฅํ ๋ณ์ ]**

```kotlin
[? (๋ฌผ์ํ)] : ๋ณ์ ์ ์ธ ์ ํด๋น ๋ณ์๊ฐ null ๊ฐ๋ฅํ ๋ณ์์ ์ ์ธ
val test15 : String? = null
```

## ์กฐ๊ฑด๋ฌธ(if else, when)

---

**[์กฐ๊ฑด๋ฌธ]**

```kotlin
[์กฐ๊ฑด๋ฌธ]
// if else
val studentScore1 = 100

if(studentScore1 >= 150) {
    println("150 ์ด์")
}else{
    println("150 ๋ฏธ๋ง")
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

## โ [ํ์ฉ] ๊ฐ๋จํ ํ์  ์ถ๋ ฅ ๋ฌธ์ 

---

```kotlin
//๊ฐ๋จํ ์กฐ๊ฑด๋ฌธ ์ด์ฉํ ๋ฌธ์ ํ์ด
//ํ์์ A B C D F  ์ ์ํ๋จ ์ถ๋ ฅ

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

## ๋ฆฌ์คํธ/filter/๋ฌผ์ํ ๋๋ํ/๋ฐ๋ณต๋ฌธ

---

**[๋ฆฌ์คํธ]**

```kotlin
//๋ฆฌ์คํธ ์์ฑ 1
val List = ArrayList<String> ()
List.add("a")
List.add("b")
List.add("c")
println(List[0])

//๋ฆฌ์คํธ ์์ฑ 2
val testList2 = listOf("a", "b", "c")
println(testList2)

//๋ฆฌ์คํธ ์์ฑ 3
val testList3 = mutableListOf<String>("a", "b", "c")
println(testList3)
testList3.add("d") //์ถ๊ฐ

println(testList3)

// filter ์ฌ์ฉํ์ฌ ์ํ๋ ๋ฆฌ์คํธ ์ฌ์ฉํ๊ธฐ
    //(1)
  val testList4 = listOf("st1", "st2", "st3", "teacher", "st5")
	println(testList4.filter {it.startsWith("st")} ) //s ๋ก ์์ํ๋ ์ ๋ค ๊ฐ์ ธ์๋ผ

    
    //(2) null์ด ํฌํจ๋ ๋ฆฌ์คํธ
    
  val testList5 = listOf("student1","student2","student3","student4", "teacher1", "student5", null)
  println(testList5.filterNotNull().filter { it.startsWith("s")})
```

**[๋ฌผ์ํ? ๋ณ์ ๋์ , ๋๋ํ!! ๋ถ์ฌ์ผ ํจ]**

```kotlin
var test3 : String = "c"
var test4 : String? = "D" //null์ผ ์ ์๋ ๋ณ์
test4 = test4!! //!! ์๋ ๋์ด ์๋์ ํํํจ
```

**[๋ฐ๋ณต๋ฌธ]**

```kotlin
[๋ฐ๋ณต๋ฌธ]
fun main() {
    
  val testList6 = listOf("a", "b", "c", "d")
  for (i in testList6) {
      println(i)
  }
  
  for (i in 1..10 step 2) { //๊ฐ๊ฒฉ 2
      println(i)
  }
 
  for(i in 1..3) {
       println("i์ ๊ฐ์ : " + i)
  }
   
   //์ค์ฒฉ ๋ฐ๋ณต๋ฌธ
   for (i in 1..3) {
       for(j in 1..4) {
           println("i is $i j is $j")
       }
   }
}
```

## โ ๊ตฌ๊ตฌ๋จ ์ถ๋ ฅํด๋ณด๊ธฐ

---

```kotlin
//๊ตฌ๊ตฌ๋จ ์ถ๋ ฅํด๋ณด๊ธฐ 
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
   // mutable ์ค๊ฐ์ ๋ณ๊ฒฝ ๊ฐ๋ฅ
    val tL1 = mutableListOf("a", "b", "c") 
    tL1.add("d")
    println(tL1)
    
    tL1.remove("a")
    println(tL1)
```

**[Map]**

```kotlin
//Map : ํค๊ฐ๊ณผ value ๋ฌถ์ด์ฃผ๊ธฐ 
	
    // 5 ์ ๋ฆฌ 10 ์ฒ ์ 15 ์งฑ๊ตฌ 22 ํ์ด
	
    val testMap = mutableMapOf<Int, String> ()
    testMap.put(5, "์ ๋ฆฌ")
    testMap.put(10, "์ฒ ์")
    testMap.put(15, "์งฑ๊ตฌ")
    testMap.put(22, "ํ์ด")
		testMap[33] = "๋๋ฏธ๋ฆฌ์ ์"

    for(i in testMap) {
			println(i)
	  }
```

**[Set]**

```kotlin
 //Set : ์ค๋ณต ๋ฐ์ดํฐ๋ ๊ฑฐ๋ฅธ๋ค. 
    
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
   val testList2 = mutableListOf("a", "b", "c") //๋ฆฌ์คํธ
   
   val testIterator = testList2.listIterator() //๋ฆฌ์คํธ๋ฅผ Iterator ํ์์ผ๋ก ๋ณํ 
   println(testIterator.next()) //๋ค์๊ฐ ์ถ๋ ฅ
   println(testIterator.next()) //๋ค์๊ฐ ์ถ๋ ฅ 
   println(testIterator.hasNext()) //๋ค์๊ฐ ์กด์ฌ์ฌ๋ถ ์ถ๋ ฅ 
   println(testIterator.previous()) //์ด์ ๊ฐ ์ถ๋ ฅ 
   
   while(testIterator.hasNext()) { //Iterator๊ฐ ๋ค์๊ฐ ์กด์ฌํ๋ ๋์ ๋ฐ๋ณต
       println(testIterator.next()) //๋ค์ ๊ฐ ์ถ๋ ฅ 
   }
```

## โ ์ํ์ ์ 50์  ์ด์ ์ฐพ๋ ๋ฌธ์ 

---

```kotlin
//์ ์๊ฐ 50์  ์ด์์ธ ์ฌ๋๋ค ์ถ๋ ฅํ๊ธฐ

fun main() {
    val student = mutableMapOf<Int, String>()
    student[99] = "๋ฏผ์ง"
    student[20] = "์ฒ ์"
    student[35] = "๋ฏผ์"
    student[48] = "๊ฐ์"
    student[100] = "ํ์"
    student[22] = "์์ง"
    student[45] = "์๋ฌ"
    student[88] = "์บฅ๊ฑฐ๋ฃจ"
    student[91] = "์ฝ์๋ผ"
    student[87] = "์์ด"
    student[54] = "์ฝ๋ผ๋ฆฌ"
    student[42] = "ํ๋ง"

    // ์ ์๊ฐ 50์  ์ด์์ธ ์ฌ๋๋ค์ ์ด๋ฆ๋ง ๋ฐ๋ณต๋ฌธ๊ณผ ์กฐ๊ฑด๋ฌธ์ ํตํด์ ์ถ๋ ฅํ์ธ์~ :)
	val testList = ArrayList<String>()
    
    for (i in student) {
		//println(i.value) //๊ฐ๋ง ๊ฐ์ ธ์ค๊ธฐ 
    //println(i.key) //ํค๋ง ๊ฐ์ ธ์ค๊ธฐ 
        
        if(i.key >= 50) {
            println(i.value)
            testList.add(i.value)
        }
    }
    
    println(testList)
}
```

## ํจ์(Function) ์ด๋?

---

```kotlin
//ํจ์ (Function)
// ํจ์ = ๊ธฐ๋ฅ

fun main() { //์คํ main() ์์์ ๊ธฐ๋ฅ๋ณ ํจ์ ํธ์ถํ๋ฉด ๋จ 
  sum(10, 20)
  bobMaking(5)
}

fun sum(a :Int, b:Int) {
    println(a + b)
}

fun bobMaking(time : Int) {
    println("$time ๋ถ ํ์ ๋ฐฅ ์๋ฃ๋จ")
}
```

## โ ํจ์ ์ด์ฉ ๊ฐ๋จํ ๊ณ์ฐ๊ธฐ ๋ง๋ค์ด๋ณด๊ธฐ

---

```kotlin
//๊ฐ๋จํ ๊ณ์ฐ๊ธฐ ๋ฌธ์  

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

## ๋ผ๋ฆฌ ์ฐ์ฐ(AND OR)

---

```kotlin
//๋ผ๋ฆฌ์ฐ์ฐ 
//And : ๋ ์กฐ๊ฑด ๋ชจ๋ ๋ง์กฑํด์ผ ํจ 
//OR : ๋ ์กฐ๊ฑด ์ค ํ๋๋ง ๋ง์กฑํ๋ฉด ๋จ 

fun main() {
	val a = "๋จ์"
    val b = 10
    
    //And
    if(a == "๋จ์" && b >= 20) {
      	println("AND ๋ง์กฑ")
    }else{
        println("AND ๋ถ๋ง์กฑ")
    }
    
    //OR
    val c = "๋จ์"
    val d = 30
    
    if(c == "๋จ์" || d >= 30) {
        println("OR ๋ง์กฑ")
    }else {
        println("OR ๋ถ๋ง์กฑ ")
    }
}
```

**[๋ผ๋ฆฌ ์ฐ์ฐ ํ์ฉํ ๊ฐ๋จ ์์ ]**

```kotlin
fun main() {
    
    val student = mutableMapOf<Int, String>()
    student[99] = "๋ฏผ์ง"
    student[20] = "์ฒ ์"
    student[35] = "๋ฏผ์"
    student[48] = "๊ฐ์"
    student[100] = "ํ์"
    student[22] = "์์ง"
    student[45] = "์๋ฌ"
    student[88] = "์บฅ๊ฑฐ๋ฃจ"
    student[91] = "์ฝ์๋ผ"
    student[87] = "์์ด"
    student[54] = "์ฝ๋ผ๋ฆฌ"
    student[42] = "ํ๋ง"
    student[1] = "ํฌ๋ก์ปค๋ค์ผ"

  	//ํ์๋ค ์ค์์ ์ ์ 50 ์ด์์ด๋ฉด์ ํ์ ์ด๋ฆ๊ธธ์ด 3์ด์์ธ ์น๊ตฌ๋ง ์ถ๋ ฅํด๋ผ 
  
    for(i in student ){
        if(i.key>=50 && i.value.length >= 3) {
           println(i)
        }
    }

}
```

## โ ๊ฐ๋จํ ๋ฌธ์์ด ๊ฐ๊ณต

---

 

```kotlin
//๋ฌธ์์ด ๊ฐ๊ณต
// User ์๋ ฅ ๋ฐ์ดํฐ ๊ฐ๊ณต or
// ์๋ฒ์์ ๊ฐ์ ธ์จ ๋ฐ์ดํฐ ์ํ๋ ํํ๋ก ๊ฐ๊ณต

fun main() {
    
    val testString = "๋ํด๋ฌผ๊ณผ ๋ฐฑ๋์ฐ์ด ๋ง๋ฅด๊ณ  ๋ณ๋๋ก"
    
    //split() : ๊ตฌ๋ถ์ ๊ธฐ์ค์ผ๋ก ์๋ผ์ ๋ฆฌ์คํธ ํํ๋ก ๋ฐํํจ
    val newTestString = testString.split(" ") 
    println(newTestString)
    
        //-> ์๋ฆฐ ์ผ๋ถ๋ง ์ถ์ถ ์ํ๋ค๋ฉด ์๋ฆฐ ๋ฆฌ์คํธ ์ [] ์ธ๋ฑ์ค ์ง์ ํจ
        println(newTestString[2])
    
    //substring() : ๋ฒ์ ์ง์  ์ํ๋ ๊ธ์ ๊ฐ์ ธ์ค๊ธฐ 
  	val splitString = testString.substring(1, 3) // ๋ฌธ์์ด ์ 0~2๋ฒ์งธ๊น์ง์ ๊ธ์
    println(splitString)
    
    //replace() ๋ฌธ์์ด ์ผ๋ถ๋ง ๋ณํ
    val replaceValue = testString.replace("๋ฐฑ๋์ฐ", "ํ๋ผ์ฐ")
    println(replaceValue)
}
```

**[๋ฌธ์์ด ๊ฐ๊ณต ์์  ํ๊ธฐ]**

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
    // naver ์ด๋ฉ์ผ ๊ฐฏ์ ์ฐพ๊ณ  ์ถ๋ค๋ฉด ?
    
    //@ ๋ค์ naver. ์ด์ด์ง ์ด๋ฉ์ผ์ ์ฐพ์์ผ ํจ 
    var count = 0
    for(i in testList ) {
	     //@ ๊ธฐ์ค์ผ๋ก ๋ฌธ์์ด ์ชผ๊ฐ๊ธฐ -> ๋ฆฌ์คํธ 2๊ฐ๋ก ๋๋  ๊ฑฐ์
    	 if(i.split("@")[1].split(".")[0] == "naver") {
         count++
     	}
    }
    println(count)
    
}
```