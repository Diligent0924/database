# Override의 개념 및 설명

### Override란 무엇인가?
부모 클래스에 있는 것을 자식 클래스에서 재정의하는 것을 의미한다. 자식 클래스에서 재정의하지 않는 것은 부모 클래스의 메소드를 그대로 가져온다.  
Django 기준 : Class Customizing 하는것과 같은 개념이라고 생각하면 된다.  

### 부모 - 자식 관계는 어떻게 연결하는가?
public class Person2 extends Person{ ... } 와 같이 extends로 부모/자식 관계를 연결할 수 있다.  

### Super의 개념
한 단계 상위 클래스에서 Method 값을 들고 오는 것을 의미함. 보통 자식 메소드로 변경하기 전에 부모 메소드를 한번 사용하고 바꿀 때 많이 쓰이는 것 같음.
public class Person {
    void jump(){
        System.out.println("저어어엄프!!");
    }

    void jump2(){
        System.out.println("점프 2222");
    }
}

public class Person2 extends Person{
    void jump(){
        super.jump(); 
        System.out.println("Child Jump!");
    }
}

### @Override 사용 개념
만약 해당 Class가 부모가 있으나 어떤 부분을 Customizing 했는지를 알고 싶으면 위에서부터 전체를 확인하는 불상사가 발생함.  
또한 Override 시에 이름/변수/타입/return 타입 등이 모두 같아야만 Override가 가능한데 상위 클래스에서 하나하나씩 확인하는 것이 어려움.  

위와 같은 어려움을 해소하기 위해 @Override를 위에 써줌  
@Override 사용 시 상위 클래스 이름/변수/타입/return 타입이 다르면 아래에 빨간줄을 쳐줌(개꿀)
내가 어떤걸 Override 했는지 알 수 있음

### JAVA는 상속이 몇개나 되는가?
Java에서는 다중 상속이 불가하다. => 만약 부모 2개가 같은 메소드명을 가지고 있다면 어떤 메소드를 쓸지 자식은 알 수 없기에 이러한 문제 때문에 1개만 지원  
자바는 딱딱한 언어이다. (원칙주의자)  

### final 개념
어떤 자바 파일에 public final class ... 와 같이 쓰게 된다면 해당 class는 상속 및 오버라이드를 금지한다는 것을 의미한다.  
=> 해당 부분은 해당 파일에서만 쓰이는 클래스일 때 쓰면 좋을 것 같다.
