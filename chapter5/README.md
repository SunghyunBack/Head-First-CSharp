# 데이터 기밀 유지하기(캡슐화)

##캡슐화
- 다른 프로그램 코드로 부터 클래스의 정보를 숨기는것을 의미한다.
- 즉 객체의 세부 구현 내용을 숨기고, 사용자에게 필요한 인터페이스만을 제공하는것을 의미한다.
- 이로인해 객체의 내부 구현이 외부에 노출되지 않으며 객체의 데이터와 메서드를 보호하고 사용자의 실수를 줄이며, 코드의 재상용성과 유지보수성을 높인다.


들어가기 전
Class 는 한개 이상의 필드(field) 또는 메서드(method)로 구성된다.(기본생성자는 자동으로 제공)
ex
```
public class Test {  // 클래스 선언 : 어떠한 객체의 변수, 메서드의 집합

	int a = 1;  // 필드 부분 : 객체 데이터가 저장되는 곳
    
	public void method() {  // 메서드 부분 : 객체의 동작을 수행하는 부분
		
		System.out.println(a);
		
	}
}
```


```
ex
public class Player
{
  public int health;

  public void TakeDamage(int damage)
  {
    health -=damage;
    if(health <=0)
    {
      Die();
    }
  }

  private void Die()
  {
    Debug.Log("Player Died");
  }
}
```
이와 같은 클래스에서 객체를 생서하게 될때 ```Player pl = new Player();``` 하게 된다면 ```pl.health = 100;``` 과 같이 값을 직접 조작할수 있다. 이를 위해 public이 아닌 private로 접근 한정자를 바꾸어 주는것이다.


##생성자
 - 클래스나 구조체가 인스턴스화 될때 자동으로 호출되는 특별한 메서드이다.
 - 주요 목적은 객체를 초기화 하는것이며 필드 또는 속성에 초기 값을 할당하는 작업을 수행할수 있다.
 - 생성자는 클래스 또는 구조체의 이름과 동일하며, 반한 형식을 지정하지 않는다.

1. 기본 생성자
```
public class MyClass
{
    public()
    {
        // 기본 생성자 본문
    }
}
```

2. 매개변수가 있는 생성자
```
public class MyClass
{
    public int Number;

    public MyClass(int number)
    {
        this.Number = number; // 매개변수를 통해 필드 초기화
    }
}
```
3. 생성자 오버로딩
```
public class MyClass
{
    public()
    {
        // 기본 생성자
    }

    public MyClass(int number)
    {
        // 정수 매개변수가 있는 생성자
    }

    public MyClass(string message)
    {
        // 문자열 매개변수가 있는 생성자
    }
}
```
4. 생성자 this 키워드
```
public class MyClass
{
    public MyClass() : this(0) // 다른 생성자 호출
    {
    }

    public MyClass(int number)
    {
        // 매개변수가 있는 생성자 본문
    }
}
```
5. 정적 생성자
```
public class MyClass
{
    static()
    {
        // 정적 생성자 본문
    }
}
```
6. 예시
```
public class BankAccount
{
    public string Owner { get; private set; }
    public decimal Balance { get; private set; }

    // 기본 생성자
    public BankAccount()
    {
        Owner = "Unknown";
        Balance = 0;
    }

    // 매개변수가 있는 생성자
    public BankAccount(string owner, decimal initialBalance)
    {
        Owner = owner;
        Balance = initialBalance;
    }

    // 입금 메서드
    public void Deposit(decimal amount)
    {
        Balance += amount;
    }

    // 출금 메서드
    public void Withdraw(decimal amount)
    {
        if(amount <= Balance)
        {
            Balance -= amount;
        }
        else
        {
            Console.WriteLine("잔액이 부족합니다.");
        }
    }
}
```
 
```
var account1 = new BankAccount();
Console.WriteLine($"소유자: {account1.Owner}, 잔액: {account1.Balance}");
```
기본 생성자에서는 "소유자 : Unknown, 잔액:0" 이라는 값이 나온다.
```
var account2 = new BankAccount("Jane Doe",1000);
Console.WriteLine($"소유자: {account2.Owner}, 잔액: {account2.Balance}");
```
매개변수 생성자일 경우는  "소유자 : Jane Doe, 잔액:1000" 이라는 값이 나온다.



##get(getter)와 set(setter)
- 필드처럼 보이지만 메서드 처럼 실행되는 클래스의 멤버이다.
- 필드처럼 타입과 이름을 사용하지만 중괄호 안에 속성접근자가 존재한다.
- get : 속성 값을 반환한다.
- set : 속성 값을 설정한다.
- 클래스는 지원필드(backing field)라는 private 필드를 사용해 속성을 통한 접근으로부터 데이터를 캡슐활 한다.

필드는 접근제한자인해 외부에서 접근이 불가능하지만 속성(property)로써는 접근이 가능하다. 

다음의 3가지 예를 통해 확인해보자!

[프로퍼티(Property) 예제 코드]
```
class Person
{
  private string age; // field
  public string Age   // property
  {
    get { return age; }
    set { age = value; }
  }
}

class Program
{
  static void Main(string[] args)
  {
    Person personObj = new Person();
    Console.WriteLine("personObj.Age 값 설정 전 : " + personObj.Age);
    personObj.Age = "29";
    Console.WriteLine("personObj.Age 값 설정 후 : " + personObj.Age);
  }
}
```
결과로는 "설정 전: 0 / 설정 후 : 20"이다.

[set 접근 제어 예제 코드]
```
class Person
{
  private string age; // field
  public string Age   // property
  {
    get { return age; }
    set { 
      if(value == "29") {
        age = "";
      } else { 
        age = value;
      }
    }
  }
}

class Program
{
  static void Main(string[] args)
  {
    Person personObj = new Person();
    Console.WriteLine("personObj.Age 값 설정 전 : " + personObj.Age);
    personObj.Age = "29";
    Console.WriteLine("personObj.Age 값 설정 후 : " + personObj.Age);
  }
}
```
결과로는 "설정 전: 0 / 설정 후 : 0"이다.

[get 접근 제어 예제 코드]
```
class Person
{
  private string age; // field
  public string Age   // property
  {
    get 
    { 
      if(age == "29") { 
        return "접근불가";
      } else {
        return age;
      } 
    }
    set { age = value; }
  }
}

class Program
{
  static void Main(string[] args)
  {
    Person personObj = new Person();
    Console.WriteLine("personObj.Age 값 설정 전 : " + personObj.Age);
    personObj.Age = "29";
    Console.WriteLine("personObj.Age 값 설정 후 : " + personObj.Age);
  }
}
```
결과로는 "설정 전: 0 / 설정 후 : 접근불가"이다.


헤드퍼스트c# 내용의 예제를 통해 난이도는 어려워 지지만 생각의 폭을 넓힐수 있다.
```
 internal class PaingtballGun
 {
     public const int MAGAZINE_SIZE = 16;
     private int balls = 0;
    
     public int BallsLoaded { get; private set; }

     //public int GetBalls() { return balls; }

     //public void SetBalls(int numberOfBalls)
     //{
     //    if (numberOfBalls > 0)
     //        balls = numberOfBalls;
     //    Reload();
     //}

     public int GetBallsLoaded()
     {
         return BallsLoaded;
     }

     public bool IsEmpty()
     {
         return BallsLoaded == 0;
     }
     public int Balls
     {
         get { return balls; }
         set
         {
             if (value > 0)
             {
                 balls = value;
                 Reload();
             }
         }
     }

     public void Reload()
     {
         if (balls > MAGAZINE_SIZE)
             BallsLoaded = MAGAZINE_SIZE;
         else
             BallsLoaded = balls;
     }


     public bool Shoot()
     {
         if (BallsLoaded == 0) return false;
         BallsLoaded--;
         balls--;
         return true;
     }
     static void Main(string[] args)
     {
         PaingtballGun gun = new PaingtballGun();
         while (true)
         {
             Console.WriteLine($"{gun.Balls} balls, {gun.GetBallsLoaded()} loaded");

             if (gun.IsEmpty()) Console.WriteLine("WARING: You're out of ammo");
             Console.WriteLine("Space to shoot, r to reload, + to add ammo, q to quit");
             char key = Console.ReadKey(true).KeyChar;
             if (key == ' ') Console.WriteLine($"Shooting returned {gun.Shoot()}");
             else if (key == 'r') gun.Reload();
             else if (key == '+') gun.Balls += PaingtballGun.MAGAZINE_SIZE;
             else if (key == 'q') return;

         }
     }
 }
```
