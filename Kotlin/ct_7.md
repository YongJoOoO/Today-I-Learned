# 🟧**코틀린 코딩테스트 예제**

## 1. 이메일 찾기

**[문제]**

// 여러 이메일이 담긴 리스트가 있어요!
// 저는 구글로 가입한 사람과 네이버로 가입한 사람의 숫자와
// 그 외의 기메일로 가입한 사람의 숫자를 보고 싶습니다.
// @와 .을 기준으로 어느 사이트에서 들어온 사람들인지 구분을 합니다.
// 아래와 같은 함수를 만들어보세요.

**[풀이]**

```kotlin
fun main(){

    val emailList1 = arrayListOf<String>("jay@naver.com",
        "john@naver.com",
        "emily@google.com",
        "ken@google.com",
        "minjun@kakao.com")
    val result1 = solution(emailList1)
    println(result1)
    
    // 결과값 = {naver=2, google=2, else=1}

    val emailList2 = arrayListOf<String>("Aiden@naver.com",
        "Andew@naver.com",
        "Adrian@daum.com",
        "Asher@google.com",
        "Austin@kakao.com",
        "Antonio@google.com")
    val result2 = solution(emailList2)
    println(result2)
    // 결과값 = {naver=2, google=2, else=2}

}

fun solution(emailList: ArrayList<String>) : Map<String, Int> {
		var naverCnt = 0
    var googleCnt = 0
    var otherCnt = 0
    
    for(i in emailList ) {
       var name = i.split("@")[1].split(".")[0]
        
        if(name == "naver") {
            naverCnt++
        }else if(name == "google") {
            googleCnt++
        }else{
            otherCnt++
        } 
    }
    //반환할 Map<> 타입에 카운팅 옮기고 
    val resultMap = mutableMapOf<String, Int> () 
    resultMap["naver"] = naverCnt
    resultMap["google"] = googleCnt
    resultMap["else"] = otherCnt
    
    return resultMap //반환해줌 
}
```\
## 2. 문자열의 숫자 및 홀짝 구분

**[문제] 문자열의 숫자와 짝수(true)와 홀수(false)를 알려주는 solution을 만드세요**

**[풀이]**

```kotlin
fun main(){

    val result1 = solution("abcd")
    println(result1)
    // [4, true]

    val result2 = solution("abcde")
    println(result2)
    // [5, false]
}

fun solution(str : String) : ArrayList<String> {

    var StringLength = str.length
    var TF = true
    
    if(StringLength % 2 == 0) { // 짝수이면 
        TF = true 
    }else {
        TF = false
    }
	
    val returnList = arrayListOf<String> (StringLength.toString(), TF.toString())
    
    return returnList
}
```
