CMIC Kotlin에 대한 스터디 기록 파일입니다
=======================================

**Commit convention rule** : 날짜-[주제]-내용-상태

## 📌 Basic Syntax

1. 함수정의

함수는 fun 키워드로 정의한다.

```
fun sum(a: Int, b: Int):Int{
    return a+b
}
```

paramter에서 data type이 먼저 나오는 Java와는 달리, kotlin에서는 data type이 뒤에 나온다. 그리고 제일 마지막에 return type이 나온다.

※ return type을 생략할 수 있는데, 함수 몸체가 식(Expression)인 경우 return 생략 가능하다.

즉 위와 같은 sum func의 경우에는 return이 생략 가능하다. 

```
fum sum(a:Int, b:Int) = a+b  // return type이 '추론'된다.
```




