## 📌 Control Flow
<hr/>

## 1. 흐름 제어문

### <span style="color: #2980B9">__1. If else__<br></span> 

*java와 거의 유사하다*

```
var max : int
if(a>b){
	max=a
}else{
	max=b
}
```

kotlin에서는 if문을 식에서 사용 가능하다. 식에서 사용될 때는 반드시 else와 같이 사용되어야 한다.

```
Val max = if(a > b) a else b
```

추가적으로 branches들이 블록을 가질 수 있다. branches = {...}
그리고 블록의 마지막 구문은 return 값을 의미한다.


```
val max = if (a >b) {
    Printf(“Choose a “)
	a //a를 max로 반환
}else{
	Printf(“choose b”)
	b //b를 max로 반환
}
```

※삼항연산자

java에는 삼항 연산자가 있었으나, kotlin에는 삼항 연산자가 없다.

삼항 연산자 //java
```
 int max = (a>b) ? a : b
```

왜냐하면 kotlin에서는 if 문이 삼항연산자 역할을 할 수 있기 때문이다.
```
Val max = if(a > b) a else b
```

### <span style="color: #2980B9">__2. When__<br></span> 

*c계열 언어의 switch문을 대체한다.*

when문은 각각의 branches의 조건문이 만족할 때 까지 위에서부터 순차적으로 인자를 비교함
switch case문과 다른 것은 break문이 필요 없다.

```
when(x){
    1->print(“x == 1”)
    2->print(“x == 2”)
    else->{
	print(“x is neither 1 nor 2”)
    }
}
```

when문도 if 처럼 식으로 사용할 수 있다. 
when 문이 식으로 사용된 경우에는 조건을 만족하는 branch의 값이 전체 식의 결과 값이 된다.
또한 if문과 동일하게 식으로 사용되면 else를 반드시 사용해야 된다.


```
var res = when(x){
    100 -> “A” //x가 100이면 res에 A를 반환
    90 -> “B”
    80 -> “C”
    else -> “F”
}
```

하지만!, when이 식으로 사용된 경우 컴파일러가 else문이 없어도 된다는 것을 입증할 수 있는 경우에는 else를 생략가능
ex) boolean

```
var res= when(x) {
    true -> "맞다"
    false -> "틀리다"
}
```

여러 조건들이 같은 방식으로 처리될 수 있는 경우, branch의 조건문에 콤마를 (,) 사용하여 표기하면 됨

```
When(x) {
    0,1 -> print("x == 0 or x ==1 ")
    else -> print(“otherwise”)
}
```

Branch의 조건문에 함수나 식을 사용할 수 있음

when(x) {
    parseInt(x) -> print("s encodes x")
    1+3 -> print("4")
    else -> print(" s does not encode x ")
}

in !in을 통해서 범위 검사도 조건문에서 가능하다

```
val validNumbers = listOf(3, 6, 9)
when(x){
    in validNumbers -> print("x is valid")
    in 1..10 -> print("x is the range")
    !in 10..20 -> print("x is outside the range")
    else -> print("none of the above")
}
```

in !in를 이용해 타입 검사도 가능
*스마트 캐스트 적용*

fun hasPrefix(x : Any) = when(x){
    is String-> x.startsWith("prefix") //x가 String형이라면 startsWith를 통해서 맨 앞 String 조사
    else -> false
}

when에 인자를 입력하지 않으면, 논리 연산으로 처리하여 if_else if 체인을 대체할 수 있다.

```
when{
    x.isOdd()->print("x is odd")
    x.Even()->print("x is even")
    else->print("x is funny")
}
```

### <span style="color: #2980B9">__3. for__<br></span> 

for문은 iterator을 제공하는 모든 것을 반복할 수 있음
*java에서 쓰던 향상된 for루프문과 비슷*

```
for(item in collection) //collection에 속하는 값이 하나씩 item에 들어가면서 반복됨
    print(item)
```

그리고 iterator에는 조건이 있다.
***1) next()를 가지야 한다.***
***2) hasNext() : Boolean을 가지는 경우***

```
val myData = MyData()
for (item in myData){
    print(item)
}
```

```
class MyData{
    operator fun iterator() : MyIterator{
        return MyIterator()
    }
}
```

```
class MyIterator{
    val data = listOf(1,2,3,4,5)
    var idx=0
    operator fun hasNext() : Boolean {
        return data.size > idx
    }

    operator fun next() : int {
        return data[idx++]
    }
}
```

※ 즉, 어떤 객체가 iterator를 반환하면 next, hasNext 메서드를 구현하면 for문에 들어갈 수 있다는 것.


배열이나 리스트를 반복할 때, index를 이용하고 싶다면 indices를 이용하면 됨

```
val array = arrayOf("가", "나", "다")
for(i in array.indices){//i = {0,1,2}
    println("$i : ${array[i]}") 
}
```


index를 이용하고 싶을 때, withIndex()를 이용할 수도 있음
```
val array = arrayOf("가", "나", "다")
for((index, value) in array.withIndex()){ //index와 value가 모두 반환됨
    println("$index : ${value}")
}
```

### <span style="color: #2980B9">__4. while__<br></span> 

*while, do-while문은 java와 거의 같다.*

do-while문에서 body의 지역변수를 do-while문의 조건문이 참조 할 수 있다.

```
do{
    val y=retrieveData()
}while(y!=null) //y is visible here(kotlin)

```

```
do{
    int b=12++;
}while(b!=null) //b is invisible here(java)

```