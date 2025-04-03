# Dart 객체 지향 정리

## ✅ 1. 클래스

```dart
// class 키워드를 입력 후 클래스 명을 지정해 클래스를 선언.
class Idol {
  // 클래스에 종속되는 변수를 지정
  String name = "블랙핑크";

  // 클래스에 종속되는 함수를 지정
  // 클래스에 종속되는 함수는 메서드라고 부름
  void sayName() {
    // 클래스 내부의 속성을 지칭하고 싶을 때는 this 키워드를 사용하면됨
    // 결과적으로 this.name은 Idol 클래스의 name 변수를 지칭하는 것임.
    print("저는 ${this.name}입니다.");

    // 스코프 안에 같은 속성의 이름이 하나만 존재한다면 this를 생략할 수도 있음.
    print("저는 $name입니다.");
  }
}
```
- `Idol`클래스 안에 종속된 변수 : `name` -> 멤버 변수
- `Idol`클라스 안에 종속된 함수 : `sayName()` -> 메서드
- 클래스 내부 속성을 지칭할 때는 `this`키워드를 사용함. 예를 들어, `this.name`은 `Idol`클래스의 `name`변수를 지칭함. 단, 해당 속성이 유일하면, `this`키워드 생략 가능
- 만약, `sayName()` 함수 내에 `name`이라는 변수가 존재한다면 `this`키워드를 꼭 사용!

### 클래스 사용예시

```dart
void main() {
  // 변수 타입을 Idol로 지정하고 Idol의 인스턴스를 생성할 수 있음.
  // 인스턴스를 생성할 때는 함수를 실행하는 것처럼 인스턴스화 하고 싶은 클래스에 괄호를 열고 닫아주면 됨.
  Idol blackPink = Idol(); // Idol 인스턴스 생성

  // 메서드 실행
  blackPink.sayName();
}

/* 출력값
저는 블랙핑크입니다.
저는 블랙핑크입니다.
*/
```
- 변수 타입을 `Idol`로 지정하여 `Idol`의 인스턴스를 생성
- 인스턴스를 생성할 때는 함수를 실행하는 것처럼 클래스명 뒤에 `()`를 붙여줌.

## ✅ 2. 생성자
생성자는 클래스의 인스턴스를 생성하는 메서드임. 생성자를 사용해서 `name` 변수의 값을 외부에서 입력할 수 있도록 변경할 수 있음!

```dart
// 생성자를 사용해서 활용도 높이기
class Idol {
  // 생성자에서 입력받는 변수들은 일반적으로 final 키워드 사용
  final String name;

  // 생성자 선언
  // 클래스와 같은 이름이어야함
  // 함수의 매개변수를 선언하는 것처럼 매개변수를 지정
  Idol(String name) : this.name = name;

  void sayName() {
    print("저는 ${this.name}입니다.");
  }
}
```
- 생성자에서 입력받을 변수들은 일반적으로 `final`로 선언, 이는 인스턴스화한 후 변수의 값을 변경하는 실수를 방지하기 위함!
- 생성자 선언 시 클래스와 같은 이름을 사용해야함! 이름 뒤에 `()`를 붙이고 원하는 파라미터를 지정함.
- `:`기호 뒤에 입력받은 파라미터가 저장될 클래스 변수를 지정해줌.

### 생성자 사용예시

```dart
void main() {
  // name에 "블랙핑크" 저장
  Idol blackPink = Idol("블랙핑크");
  blackPink.sayName();

  // name에 "BTS" 저장
  Idol bts = Idol("BTS");
  bts.sayName();
}

/* 출력값
저는 블랙핑크입니다.
저는 BTS입니다.
*/
```
- `name`이 `블랙핑크`인 인스턴스와 `name`이 `BTS`인 인스턴스를 생성했음.

## ✅ 3. 네임드 생성자
네임드 생성자는 클래스를 생성하는 여러 방법을 명시하고 싶을 때 사용함.

```dart
class Idol {
  final String name;
  final int membersCount;

  // 생성자
  Idol(String name, int membersCount)
      : this.name = name,
        this.membersCount = membersCount;

  // 네임드 생성자
  // {클래스명.네임드 생성자명} 형식
  // 나머지 과정은 기본 생성자와 동일
  Idol.fromMap(Map<String, dynamic> map)
      : this.name = map["name"],
        this.membersCount = map["membersCount"];

  void sayName() {
    print("저는 ${this.name}입니다. ${this.name} 멤버는 ${this.membersCount}명입니다.");
  }
}
```
- 생성자에서 파라미터 2개를 받아 `this.name`과 `this.membersCount`에 할당함
- 네임드 생성자는 `클래스명.네임드 생성자명` 형식으로 지정함. 위 코드에서는 `Idol.fromMap`과 같이 사용됐음
- 나머지 과정은 기본 생성자와 동일함

### 네임드 생성자 사용 예시

```dart
void main() {
  // 기본 생성자 사용
  Idol blackPink = Idol("블랙핑크", 4);
  blackPink.sayName();

  // fromMap이라는 네임드 생성자 사용
  Idol bts = Idol.fromMap({
    "name": "BTS",
    "membersCount": 7,
  });
  bts.sayName();
}

/* 출력값
저는 블랙핑크입니다. 블랙핑크 멤버는 4명입니다.
저는 BTS입니다. BTS 멤버는 7명입니다.
*/
```

## ✅ 4. 프라이빗 변수
Dart에서 변수나 메서드 앞에 `_`를 붙이면 해당 멤버는 `private`으로 취급받음

```dart
class Idol {
  String _name = "블랙핑크"
}
```
- `_name`은 외부 파일(.dart)에서 접근할 수 없는 private 변수임.

## ✅ 5. 게터와 세터
위 프라이빗 변수를 외부파일에서 간접적으로 접근하게 해줄 수 있는게 게터와 세터인데, 세터는 요즘 거의 사용하지않고 게터는 종종 사용됨

```dart
class Idol {
  String _name = "블랙핑크";
  
  // get키워드를 사용해서 게터임을 명시, 메서드와 다르게 파라미터를 받지 않음.
  String get name {
    return this._name;
  }
  
  // 세터는 set이라는 키워드를 사용해서 선언, 파라미터로 하나의 변수를 받을 수 있음
  set name(String name) {
    this._name = name;
  }
}
```
- 위처럼 `name` 게터나 세터를 사용하면 외부에서도 간접적으로 `_name` 변수를 접근할 수 있음.
- 게터는 파라미터를 정의하지않음
- 세터는 파라미터를 하나만 받음, 이 파라미터는 멤버 변수에 대입되는 값임!

### 게터와 세터 사용 예시

```dart
void main() {
    Idol blackPink = Idol();
    
    blackPink.name = "에이핑크";
    print(blackPink.name);
}
/* 출력값
에이핑크
*/
```
