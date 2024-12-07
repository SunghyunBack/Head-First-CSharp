# 객체 소개

![image](https://github.com/user-attachments/assets/d77748b5-54aa-437c-837d-b7a8c992eb17)
- 클래스의 객체는 청산진으로 예를 들수 있다.
- 똑같은 집을 5채를 짓는다고 할때 5개의 청사진은 필요가 없다. 1개의 청사진을 이용해서 5채 모두 적용할수 있다.
- 하나의 클래스로 여러개의 객체를 생성할 수 있다.

 ![image](https://github.com/user-attachments/assets/cd38e87a-5a6f-4e8c-b4f4-e56871806440)

- ex) 객체 생성 ```House house = new House();``` House 타입의 변수이름은 house이면 new 문을 사용해 객체를 생선한다.
- 다음의 그림은 다음과 같이 이야기 할수 있다.
  ```
House PineStreet38 = new House();
House ElemLane26A = new House();
House MapleDrive115 = new House();
  ```
- 생성된 각각의 객체들은 GrowLawn, ReceiveDeliveries, AccurePropertyTaxes, NeedRepairs 메서드를 사용할수 있다.

★객체를 생성한다는 표현은 인스턴스를 생선했다는 표현과 같다.
```House house = new House();```
은 "house 객체를 생성했다" 혹은 "house 인스턴스를 생성했다" 로 표현할수 있다.

##필드를 사용해 인스턴스의 상태 기록하기
![image](https://github.com/user-attachments/assets/730021e8-c2bd-42d1-81a3-f81c09dfafbc)

- 클래스는 크게 필드와 메서드로 내용으로 구성되어 있다.
- 필드 : 객체의 상태를 의미한다.
- 메서드 : 객체의 행동을 의미한다.
- 필드, 메서드를 뭉뚱그려 클래스 멤버(class member)라고 부르곤 한다.
즉 객체의 작동은 메서드로 정의되고, 객체는 필드를 사용해 객체의 상태를 관리한다.


## 선언부 STATIC 키워드
![image](https://github.com/user-attachments/assets/e1c75619-ae7d-4e4a-b83f-09f6ab80e266)

- 다음과 같이 __static__ 키워드를 사용해 클래스의 필드나 메서드르 선언하면 인스턴스 없이 클래스 멤버에 접근할수 있다.
- static일 경우 필드의 사본은 오직 하나만 존재하게 된다. 그래서 모든 인스턴스가 이 필드를 공유할수 있는것이다.
★ 클래스 전체를 static으로 선언하면 클래스의 모든 멤버가 static으로 선언되어야 한다.

즉 기존에 객체 생성을 할대
```CardPicker cardpicker = new CardPicker();``` 과 같이 생성한후 사용했다면 이러한 과정 없이 바로
```CardPicker.PickSomeCards(numberOfCards)```과 같이 사용할수 있다. 왜냐하면 static으로 선언되어 모든 인스턴스가 클래스멤버를 공유하고 있기 때문이다.
