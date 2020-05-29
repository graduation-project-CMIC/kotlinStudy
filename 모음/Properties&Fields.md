## 📌 Properties & Fields
<hr/>

## 1. 프로퍼티 선언
    - 코틀린 클래스는 프로퍼티를 가질 수 있다
    - 프로퍼티 사용은 자바의 필드를 사용하듯이 하면 된다.
    ,,
    fun copyAddress(address: Address): Address {
        val result = Address()
        result.name = address.name
        // ....
        return result
    }
    ,,

## 2. 프로퍼티 문법
    - 전체 문법
        var <propertyName>[: <PropertyType>][=<property_initializer>][<getter>][<setter>]

    - 옵션 (생략가능)
        - PropertyType
            - property_initializer에서 타입을 추론 가능한 경우 생략가능
            - property_initializer
            - getter
            - setter


## 3. 프로퍼티 예제
    ,,
    class Address {
        var name = "Kotlin"
    }
    ,,
    ,,
    class Address2 {
        var name: String = "Kotlin"
            get() {
                return field
            }
            set(value) {
                field = value
            }
    }
    ,,

    - var (mutable) 프로퍼티
    ,,
    class Address {
        // default getter와 setter
        // 타입은 int
        var initialized = 1

        // error: 오류 발생
        // default getter와 setter를 사용한 경우
        // 명시적인 초기화 필요
        var allByDefault: Int?

    }
    ,,

    - val (read-only) 프로퍼티
        -var 대신 val 키워드를 사용
        -setter가 없다.
    
    ,,
    class Address {
        // default getter
        // 타입 int
        val initialized = 1

        // error 
        // default getter
        // 명시적 초기화 필요
        val allByDefault: Int?
    }
    ,,


## 4. Custom accessors (getter, setter)
    - custom accessor는 프로퍼티 선언 내부에, 일반 함수 처럼 선언 가능
    - getter
        val isEmpty: Boolean
            get() = this.size == 0

    - setter
        - 관습적으로 setter의 파라매터의 이름은 value임
        ,,
        var stringRepresentation: String
            get() = this.toString()
            set(value){
                setDataFrommString(value)
            }
        ,,

## 5. 타입 생략
    - 코틀린 1.1 부터는 getter를 통해 타입을 추론 가능 한 경우, 프로퍼티 타입 생략 가능
    

## 6. 프로퍼티
    - accessor에 가시성 변경이 필요하거나 어노테이션이 필요한 경우에 기본 accesoor의 수정 없이 body 없는 accessor를 통해 정의 가능하다.

    ,,
    var setterVisibility: String = "abc"
        private set
    var setterWithAnnotation: Any? = null
        @Inject set // annotate the setter with Inject
    ,,

    - Body 작성해도 무관

    ,,
    var setterVisibility: String = "abc"
        private set(value){
            field = value
        }
    ,,

## 7. Backin Fields
    - 코틀린 클래스는 field를 가질 수 없음
    - 'field'라는 식별자를 통해 접근 할 수 있는, automatic backin field 제공
    - field는 프로퍼티의 accessor에서만 사용가능

    - Backin Fields 생성 조건
        - accessor중 1개라도 기본 구현을 사용하는 경우
        - custom accessor에서 field 식별자를 참조하는 경우


## 8. Compile-Time Constants
    - const modifier를 이용하면 컴파일 타임 상수를 만들 수 있음
        - 이런 프로퍼티는 어노테이션 에서도 사용 가능
    - 조건(1가지 조건충족)
        - Top-level
        - object 멤버
        - String이나 preemetive 타입으로 초기화된 경우


## 9. Late-Initialized Properties
    - 일반적으로 프로퍼티는 non-null 타입으로 선언
    - 간혹 non-null 타입 프로퍼티를 사용하고 싶지만, 생성자에서 초기화를 해줄 수 없는 경우가 있다.
        - Dependency injection
        - Butter knife
        - Unit test의 setup 메소드
    - Late-Initialized Properties
        - 객체가 constructor에서는 할당되지 못하지만
        - 여전히 non-null타입으로 사용하고 싶은 경우는
        - Lateinit modifer를 사용 가능
        - 조건
            - 클래스의 바디에서 선언된 프로퍼티만 가능
            - 기본생성자에서 선언된 프로퍼티는 X
            - var 프로퍼티만 가능
            - custom accessor이 없어야함
            - non-null 타입 이어야함
            - preemetive 타입 X
        - lateinit 프로퍼티가 초기화 되기전에 접근되면, 오류 발생
         