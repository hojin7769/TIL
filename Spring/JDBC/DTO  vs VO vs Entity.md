> ChatGPT의 답변
> DTO(Data Transfer Object), VO(Value Object), 그리고 ENTITY(또는 MODEL)는 모두 데이터를 표현하는 객체입니다. 하지만 이들 객체는 목적과 사용 방식이 다르며, 다음과 같은 차이점이 있습니다.

1. DTO(Data Transfer Object)
  - 데이터 전송을 위한 객체입니다.
  - 여러 개의 필드를 가질 수 있으며, 각각의 필드는 데이터베이스의 테이블 칼럼과 일치합니다.
  - DTO는 주로 비즈니스 계층과 프레젠테이션 계층 간의 데이터 전송을 위해 사용됩니다.
2. VO(Value Object)
- 값을 저장하는 객체입니다.
- DTO와 비슷하지만, 값을 가진 필드는 읽기 전용입니다. 즉, 값이 변경될 수 없습니다.
- VO는 주로 데이터베이스에서 조회한 결과를 저장하기 위해 사용됩니다.
3. ENTITY(또는 MODEL)
- 비즈니스 로직을 담은 객체입니다.
- 데이터베이스의 테이블과 일치하며, ORM(Object-Relational Mapping) 프레임워크에서 사용됩니다.
- ENTITY는 데이터베이스와 연동되어 데이터를 생성, 수정, 삭제하는 작업 등을 수행합니다.

따라서, DTO와 VO는 데이터 전송과 조회를 위한 객체로서 단순히 값을 전달하거나 저장하는 역할을 하며, ENTITY는 비즈니스 로직을 담은 객체로서 데이터를 생성, 수정, 삭제하는 작업 등을 수행합니다. 또한, DTO와 VO는 읽기 전용 필드를 가질 수 있지만, ENTITY는 필드를 수정할 수 있습니다.

# 내가 느낀거
## Entity
실제 DB테이블과 컬럼수와 컬럼의 이름이 일치 되어야 한다

여기에 나온 컬럼은 외부에서 조작이 가해지면 안된다 비즈니스 로직은 가지고 있지 아니하여야 하며 순수 테이블에 관련된 변수만 담고 있어야 한다

DTO와 비슷한 개념이지만 View단과 DB단의 작용된다는 차이점이 존재한다.

Entity클래스는 실제 테이블과 매핑되므로 만일 변경되면 다른 클래스에 영향이 갈 수 있다.

```
import javax.persistence.*;

@Entity
public class User {
   @Id
   @GeneratedValue(strategy = GenerationType.IDENTITY)
   privae Long id;
  
   @Column(nullable = false)
   private String name;
  
   @Column(nullable = false)
   private String email;
  
   @Builder
   public User(String name, String email) {
      this.name = name;
      this.email = email;
   }
  
   public User update(String name, String email) {
      this.name = name;
      this.email = email;
      return this;
   }
}
```

## DTO(Data Transfer Object)
데이터의 전송 객체라는 의미

DTO는 주로 비동기 처리를 할때 사용 된다.

각 개츨간의 데이터 교환을 위한 객체

로직을 갖고 있지 않는 순수한 데이터 객체이며, getter/setter 메소드만을 갖습니다.

```
public class PersonDTO {
 
    private String name;
    private int age;
 
    public String getName() {
        return name;
    }
 
    public void setName(String name) {
        this.name = name;
    }
 
    public int getAge() {
        return age;
    }
 
    public void setAge(int age) {
        this.age = age;
    }
}
```


## VO (Value Object)

*VO는 변하지 않는 데이터 객체를 의미합니다.*

오직 read와getter만 가능하다

VO 는

하나는 **객체의 불변성(객체의 정보가 변경되지 않음)을 보장**
합니다. 즉, 값을 설정한 뒤에는 수정할 수 없습니다.

다른 하나는 **equals()**
와 **hashCode()**
를 **재정의(Override)**
 해서 각 객체의 동일성을 판별할 수 있습니다.
```
class RGBColor {
   private final int red;
   private final int green;
   private final int blue;
  
   public RGBColor(int red, int green, int blue) {
      this.red = red;
      this.green = green;
      this.blue = blue;
   }
  
   public static RGBColor of(int red, int green, int blue){
      return new RGBColor(red, green, blue);
   }
  
   @Override
   public boolean equals(Object o) {
      if (this == o) return true;
      if (o == null || getClass() != o.getClass()) return false;
      RGBColor rgbColor = (RGBColor) o;
      return red == rgbColor.red && green == rgbColor.green && blue == rgbColor.blue;
   }
}
```


## ****DTO와 VO의 차이점****

### DTO는 데이터의 전송만을 위한 객체이고, VO는 특정한 비즈니스 로직을 가질 수 있습니다.

### DTO는 데이터 전달만을 목적으로 하고, VO는 객체 자체를 어떠한 값(Value)으로서 사용합니다.

- (외부 시스템과 데이터 통신을 할 경우 DTO로, DB에서 가져오는 Data는 VO로 정의 후 사용)

### DTO는 목적 자체가 데이터의 전달이므로, 읽고 쓰는 것이 모두 가능해 가변성을 갖고,

### VO는 불변성 및 read-only의 속성을 갖습니다.

VO는  equals()와 hashCode()를 재정의(Override) 해서 각 객체의 동일성을 판별할 수 있습니다.

간단하게
```
DTO a = new DTO(1);

DTO b = new DTO(1);

라고 했을때 a != b 이지만,

VO a = new VO(1);

VO b = new VO(1);
```
라고 했을때 a==b 입니다.


