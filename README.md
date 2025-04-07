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

## ✅ 1-2. 생성자
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

## ✅ 1-3. 네임드 생성자
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

## ✅ 1-4. 프라이빗 변수
Dart에서 변수나 메서드 앞에 `_`를 붙이면 해당 멤버는 `private`으로 취급받음

```dart
class Idol {
  String _name = "블랙핑크"
}
```
- `_name`은 외부 파일(.dart)에서 접근할 수 없는 private 변수임.

## ✅ 1-5. 게터와 세터
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
---

## ✅ 2. 상속
상속은 어떤 클래스의 기능을 다른 클래스가 사용할 수 있게 해주는 기법! `extends`키워드를 통해 상속가능!
- 기능을 물려주는 클래스 : 부모 클래스
- 기능을 물려받는 클래스 : 자식 클래스
- 부모 -> 자식

```dart
// 부모 클래스
class Idol {
  final String name;
  final int membersCount;
  
  Idol(this.name, this.membersCount);
  
  void sayName() {
    print("저는 ${this.name}입니다.");
  }
  
  void sayMembersCount() {
    print("${this.name}멤버는 ${this.membersCount}명입니다.");
  }
}

// 자식 클래스
class BoyGroup extends Idol { // extends 키워드를 사용해서 상속받음. class (자식클래스) extends Idol(부모클래스)
  BoyGroup(
  String name,
  int membersCount,
  ) : super( // super는 부모 클래스를 지칭함.
  name,
  membersCount,
  );
  
  void sayMale() { // 상속받지 않는 메서드나 변수를 새로 추가할 수 있음. 
    print("저는 남자 아이돌입니다.");
  }
}

// 두 번째 자식 클래스
class GirlGroup extends Idol {
  GirlGroup(
  String name,
  int membersCount,
  ) : super(
  name,
  membersCount,
  );
  
  void sayFeMale() {
    print("저는 여자 아이돌입니다.");
  }
}

void main() {
  BoyGroup bts = BoyGroup("BTS", 7);
  GirlGroup blackPink = GirlGroup("블랙핑크", 4);
  
  bts.sayName();         // 부모한테 물려받은 메서드
  bts.sayMembersCount(); // 부모한테 물려받은 메서드
  bts.sayMale();         // 자식이 새로 추가한 메서드
  blackPink.sayName();
  blackPink.sayMembersCount();
  blackPink.sayFeMale();
  blackPink.sayMale(); // < 이건 오류! blackPink는 BoyGroup에서 선언한 메서드는 사용 불가!
}
```

---

## ✅ 3. 오버라이드
오버라이드는 부모 클래스 또는 인터페이스에서 정의된 메서드를 재정의할 때 사용됨!
Dart에서는 `override`키워드를 생략할 수 있기 떄문에 키워드를 사용하지 않고도 메서드를 재정의할 수 있음!

```dart
// 부모 클래스
class Idol {
  final String name;
  final int membersCount;
  
  Idol(this.name, this.membersCount);
  
  void sayName() {
    print("저는 ${this.name}입니다.");
  }
  
  void sayMembersCount() {
    print("${this.name}멤버는 ${this.membersCount}명입니다.");
  }
}

// 오버라이드
class GirlGroup extends Idol {
  // 상속에서처럼 super키워드를 사용해도 되고, 아래처럼 생성자의 매개변수로 직접 super키워드를 사용해도 됨.
  GirlGroup (
  super.name,
  super.membersCount,
  );
  
  // override키워드를 사용해 오버라이드
  @override
  void sayName() {
    print("저는 여자 아이돌 ${this.name}입니다.");
  }
}

void main() {
  GirlGroup blackPink = GirlGroup("블랙핑크", 4);
  
  blackPink.sayName(); // 자식 클래스의 오버라이드된 메서드 사용
  
  // sayMembersCount는 오버라이드 하지 않았기 때문에 Idol클래스의 메서드가 실행됨
  blackPink.sayMembersCount();
}
```
- 단! 직접 `override`키워드를 명시하는게 협업 및 유지보수에 유리함!
- 한 클래스에 이름이 같은 메서드가 존재 불가능! -> 부모 클래스나 인터페이스에 이미 존재하는 메서드명이 입력되면 `override`키워드를 생략해도 메서드가 덮어씌워짐! 주의!!

---

## ✅ 4. 인터페이스
- 상속은 공유되는 기능을 이어받는 개념, + 하나의 클래스만 가능
- 인터페이스는 공통으로 필요한 기능을 정의만 해두는 역할!, + 인터페이스는 적용 개수에 제한 없음! 여러 인터페이스를 사용하고싶으면 `,`기호를 사용! 

```dart
// 인터페이스

// 부모 클래스
class Idol {
  final String name;
  final int membersCount;
  
  Idol(this.name, this.membersCount);
  
  void sayName() {
    print("저는 ${this.name}입니다.");
  }
  
  void sayMembersCount() {
    print("${this.name}멤버는 ${this.membersCount}명입니다.");
  }
}

// implements 키워드를 사용하면 원하는 클래스를 인터페이스로 사용 가능!
class GirlGroup implements Idol {
  final String name;
  final int membersCount;
  
  GirlGroup(
  this.name,
  this.membersCount,
  );
  
  void sayName() {
    print("저는 여자 아이돌 ${this.membersCount}명입니다.");
  }
  
  void sayMembersCount() {
    print("${this.name} 멤버는 ${this.membersCount}명 입니다.");
  }
}

// 인터페이스 사용법
void main() {
  GirlGroup blackPink = GirlGroup("블랙핑크", 4);
  
  blackPink.sayName();
  blackPink.sayMembersCount();
}
```
위 코드를 보면 `GirlGroup`클래스는 `Idol`클래스가 정의한 모든 기능을 다시 정의 했음.
상속과 인터페이스의 차이점을 보자면
- 상속 받을 때는 부모 클래스의 모든 기능이 상속되므로 재정의할 필요가 없음
- 인터페이스는 반드시 모든 기능을 다시 정의해줘야함!!
반드시 재정의 할 필요가 있는 기능을 정의하는 용도가 인터페이스임 -> 실수로 빼먹는 일을 방지할 수 있음!

---

## ✅ 5. 믹스인
믹스인은 특정 클래스에 원하는 기능들만 골라서 넣을 수 있는 기능임.
특정 클래스를 지정해서 속성들을 정의할 수 있으며 지정한 클래스는 상속하는 클래스에서도 사용이 가능함!
인터페이스처럼 한 개의 클래스에 여러 개의 믹스인을 적용할 수도 있음. `,`기호로 열거하면 됨.

```dart
// 믹스인

// 부모 클래스
class Idol {
  final String name;
  final int membersCount;
  
  Idol(this.name, this.membersCount);
  
  void sayName() {
    print("저는 ${this.name}입니다.");
  }
  
  void sayMembersCount() {
    print("${this.name}멤버는 ${this.membersCount}명입니다.");
  }
}

mixin IdolSingMixin on Idol {  // mixin키워드로 정의된 믹스인 정의, on Idol은 이 믹스인을 Idol을 상속한 클래스에만 쓸 수 있다는 뜻 (제한 조건을 건 것!)
  void sing() { // sing()은 this.name을 사용 -> 즉, Idol클래스의 속성을 참조함
    print("${this.name}이(가) 노래를 부릅니다.");
  }
}

// 믹스인을 적용할 때는 with 키워드 사용
class BoyGroup extends Idol with IdolSingMixin { // extends Idol -> 부모 클래스로부터 기본 속성과 메서드 상속, with IdolSingMixin -> sing() 메서드도 추가로 섞어 넣음
  BoyGroup( 									 // 즉, BoyGroup은 Idol + IdolSingMixin의 기능을 모두 가짐!
  super.name,									 // sayName, sayMembersCount, sing, sayMale 다 가능!!
  super.membersCount,
  );
  
  void sayMale() {
    print("저는 남자 아이돌입니다.");
  }
}

void main() {
  BoyGroup bts = BoyGroup("BTS", 7);
  
  bts.sayMale(); // BoyGroup의 고유 기능
  bts.sing();    // mixin에서 온 기능!
}
```
- `IdolSingMixin`이라는 믹스인은 `BoyGroup`클래스에 `void sing()`을 섞어 넣은 것
- 그 결과 `BoyGroup`객체는 `sing()` 메서드를 사용할 수 있게 된 것

믹스인을 요약하자면
- 믹스인은 클래스를 상속하지 않고도 기능을 재사용/주입하는 방법
- `with`키워드를 통해 클래스에 기능을 `섞어 넣는`느낌으로 동작함.

---

