## Kotlin - Packages, Return and Jumps
<hr>

## Package
- 소스 파일은 패키지 선언으로 시작 됨.
- 모든 콘텐츠(클래스, 함수, ...)는 패키지에 포함됨
- 패키지를 명세하지 않으면 이름이 없는 패키지에 포함됨(java와 다른 점 default package)

### 기본 패키지
- 기본으로 import되는 package가 있음
- 플랫폼 별로 다르다

```
kotlin.*
kotlin.annotation.*
kotlin.collections.*
kotlin.comparisons.*
kotlin.io.*
kotlin.ranges.*
```

- 기본으로 포함되는 패키지 외에도, 필요한 package 들을 직접 import할 수 있다.

*자바와 똑같지만 로컬 리네임이 가능하다*

```
import bar.Bar as bBar
```
## Return and Jumps

### 3가지 Jump 표현식
- return : 함수나 익명 함수에서 반환
- break : 루프를 종료시킴
- continue : 루프의 다음 단계로 진행

* Label로 Break and Continue(java와 차이)
+ 레이블 표현 : label@, abc@, fooBar@
- 식별자 + @ 형태로 사용

```
loop@ for (i in 1..10){
    println("--- i : $i ---")

    for(j in 1..10){
        println("j : $j")
        if(i+j>12){
            break@loop
        }
    }
}
//break@loop를 통해서 두개의 loop를 한번에 break함

```

### Label로 Return
* Label로 Return
+ 코틀린에서 중첩 될 수 있는 요소들
- 함수 리터럴(function literals)
- 지역 함수(local fundtion)
- 객체 표현식(object expression)
- 함수(functions)

```
fun foo(){
    var ints=listOf(0,1,2,3)

    ints.forEach(fun(value : int){
        if(value==1) return
        print(value)
    })
    print("End")
}
//result : 023End
//함수가 중첩되면 안쪽 함수만 return 함
```

```
fun foo2(){
    var ints=listOf(0,1,2,3)

    ints.forEach{
        {
            if(it==1) return
            print(it)
        }
    }
    print("End")
}
//result : 0
//람다식 밖 함수까지 return 해버림
```

```
fun foo3(){
    var ints=listOf(0,1,2,3)
    ints.forEach label@{
        if(it==1)return@label
        print(it)
    }
    print("End")
}
//result : 023End
```
- 람다식에서 return시 nearest enclosing 함수가 return 됨
- 람다식에서 대해서만 return 하려면 label을 이용해야 함

### 암시적 레이블
- 람다식에서만 return 하는 경우 label을 이용해서 return 해야 함
- 직접 label을 사용하는 것보다 암시적 레이블이 편리하다
- 암시적 레이블은 람다가 사용된 함수의 이름과 동일함

```
fun foo4(){
    var ints=listOf(0,1,2,3)
    ints.forEach {
        if(it==1)return@forEach
        print(it)
    }
    print("End")
}
//result : 023End
```

### 레이블 return시 값을 반환할 경우
- return@label 1 형태로 사용
- return + @label + 값

```
fun foo():List<String>{
    var ints=listOf(0,1,2,3)
    val result = ints.map{
        if(it == 0){
            return@map "zero"
        }
        "number $it"
    }
    return result
}
```