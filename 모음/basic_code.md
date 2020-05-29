## 📌 Kotlin - Basic Types
<hr/>

## 기본 타입
	- 코틀린에서 모든 것은 객체.
	- 모든 것에 멤버 함수나 프로퍼티를 호출 가능하다는 의미.


## 숫자(Numbers)
	- Java의 숫자형과 거의 비슷하게 처리
	- Kotlin 에서 Number는 Class, java의 primitive type에 접근 불가
	- java에서 숫자형이던 char이 kotlin에서는 숫자형 X
	

## Literal
	- 10진수 : 123 (int, short)
	- Long : 123L
	- Double : 123.5, 123.5e10
	- Float : 123.5f
	- 2진수 : 0b00001011
	- 8진수 : 미지원
	- 16진수 : 0X0F

## Representation
	-Java 플랫폼에서 숫자형은 JVM primitive type으로 저장
	-Nullable이나 generic의 경우 박싱됨
	-박싱된 경우 identity를 유지 X

```
// JVM primitive
val a: Int = 100
print(a === a) // Prints 'true'
```

```
//Boxed
val boxedA: Int? = a
val anotherBoxedA: Int? = a
println("==: ${boxedA == anotherBoxedA}")
println(" ===: $(boxedA === anotherBoxedA}")
```

## Explicit Conversions
	-작은 타입은 큰 타입의 하위 타입이 아니다. 즉 작은타입에서 큰 타입으로 대입 불가능
	-명시적으로 변환 필요

## Characters
	-char 은 숫자로 취급 X

## 배열
	-배열은 Array 클래스로 표현
	-get, set([] 연산자 오버로딩됨)
	-size 등 유용한 멤버 함수 포함

```
var array: Array<String> = arrayOf("코틀린","강좌")
println(array.get(0))
println(array[0])
println(array.size)
```

## 배열 생성
	-Array의 팩토리 함수 이용
	-arrayOf() 등의 라이브러리 함수 이용

val b = Array(5, { i->i.toString() })
val a = arrayOf("0","1","2","3","4")

## 특별한 Array클래스
	-Primitive 타입의 박싱 오버헤드를 없애기 위한 배열
	-IntArray, ShortArray, IntArray
	-Array를 상속한 클래스들은 아니지만, Array와 같은 메소드와 프로퍼티를 가짐
	-size 등 유용한 멤버 함수 포함

```
val x: IntArray = intArryOf(1,2,3)
x[0] = 7
println(x.get(0))
println(x[0])
println(x.size)
```

## 문자열
	-문자열은 String 클래스로 표현
	-String은 characters로 구성
	-s[i] 와 같은 방식으로 접근 가능하다. (변경불가)
```
var x: String = "Kotlin"
println(x.get(0))
println(x[0])
println(x.length)

for (c in x) {
	println(c)
}
```

## 문자열 리터럴
	-escaped string ("Kotlin")
		- 전통적인 방식으로 Java String과 거의 비슷
		- Backslash를 사용하여 escaping 처리
	-raw string("""Kotlin""")
		- escaping 처리 필요 x
		- 개행 이나 어더한 문자 포함이 가능하다.

```
val s = "Hello, world!\n"

val s = """
"'이것은 코틀린의
raw string
입니다.'"
"""
```


 