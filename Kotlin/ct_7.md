# ๐ง**์ฝํ๋ฆฐ ์ฝ๋ฉํ์คํธ ์์ **

## 1. ์ด๋ฉ์ผ ์ฐพ๊ธฐ

**[๋ฌธ์ ]**

// ์ฌ๋ฌ ์ด๋ฉ์ผ์ด ๋ด๊ธด ๋ฆฌ์คํธ๊ฐ ์์ด์!
// ์ ๋ ๊ตฌ๊ธ๋ก ๊ฐ์ํ ์ฌ๋๊ณผ ๋ค์ด๋ฒ๋ก ๊ฐ์ํ ์ฌ๋์ ์ซ์์
// ๊ทธ ์ธ์ ๊ธฐ๋ฉ์ผ๋ก ๊ฐ์ํ ์ฌ๋์ ์ซ์๋ฅผ ๋ณด๊ณ  ์ถ์ต๋๋ค.
// @์ .์ ๊ธฐ์ค์ผ๋ก ์ด๋ ์ฌ์ดํธ์์ ๋ค์ด์จ ์ฌ๋๋ค์ธ์ง ๊ตฌ๋ถ์ ํฉ๋๋ค.
// ์๋์ ๊ฐ์ ํจ์๋ฅผ ๋ง๋ค์ด๋ณด์ธ์.

**[ํ์ด]**

```kotlin
fun main(){

    val emailList1 = arrayListOf<String>("jay@naver.com",
        "john@naver.com",
        "emily@google.com",
        "ken@google.com",
        "minjun@kakao.com")
    val result1 = solution(emailList1)
    println(result1)
    
    // ๊ฒฐ๊ณผ๊ฐ = {naver=2, google=2, else=1}

    val emailList2 = arrayListOf<String>("Aiden@naver.com",
        "Andew@naver.com",
        "Adrian@daum.com",
        "Asher@google.com",
        "Austin@kakao.com",
        "Antonio@google.com")
    val result2 = solution(emailList2)
    println(result2)
    // ๊ฒฐ๊ณผ๊ฐ = {naver=2, google=2, else=2}

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
    //๋ฐํํ  Map<> ํ์์ ์นด์ดํ ์ฎ๊ธฐ๊ณ  
    val resultMap = mutableMapOf<String, Int> () 
    resultMap["naver"] = naverCnt
    resultMap["google"] = googleCnt
    resultMap["else"] = otherCnt
    
    return resultMap //๋ฐํํด์ค 
}
```\
## 2. ๋ฌธ์์ด์ ์ซ์ ๋ฐ ํ์ง ๊ตฌ๋ถ

**[๋ฌธ์ ] ๋ฌธ์์ด์ ์ซ์์ ์ง์(true)์ ํ์(false)๋ฅผ ์๋ ค์ฃผ๋ solution์ ๋ง๋์ธ์**

**[ํ์ด]**

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
    
    if(StringLength % 2 == 0) { // ์ง์์ด๋ฉด 
        TF = true 
    }else {
        TF = false
    }
	
    val returnList = arrayListOf<String> (StringLength.toString(), TF.toString())
    
    return returnList
}
```
