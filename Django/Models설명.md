# Model은 어떠한 경우에 사용하는가?

### Model이란 무엇인가?
Django가 DB와 연결하기 위한 장소로 실제로 Django의 기본 DB인 Sqlite3가 아닌 MYSQL과 연동을 혹시 하더라도 Model에는 해당 DB에 맞게 지정을 해줘야한다.실제 View 또는 다른 API에서 트랜잭션(데이터를 저장/조회/삭제/변경)이 발생될 때 Model을 거쳐서 DB로 들어가게 된다.

### Django Model의 특징
Django Model은 기본적으로 Primary Key(Index Column)이 없다면 id(pk)라고 하는 PrimaryKey를 스스로 생성한다. 해당 Index는 나중에 해당 모델에 따로 Primary Key를 넣게 된다면 해당 값은 사라진다.

### Model의 사용방법
```python
class Usermodel(models.Model):
    username = models.CharField(max_length=50)
    email = models.CharField(max_length=50)
```

### Model에서 사용할 수 있는 것들 
1. ModelField의 종류 (매우 다양함)
   1. CharField : 문자열
   2. TextField : TextArea와 같은 개념
   3. DatetimeField : 날짜/시간
   4. DateField : 날짜
   5. BooleanField : Bool
   6. AutoField : 자동으로 증가하는 IntegerField
   7. IntegerField : 정수만 가능!
   8. EmailField : 이메일
   9. FileField : 파일 업로드 필드!
   10. ImageField : 이미지 필드!
   11. 등등.... 매우 많음
2. 부가적인기능
3. ForeignKey를 사용할 경우
   1. on_delete = models.[CASCADE, PROTECT]
      1. CASCADE : Primary Table 삭제 시 같이 삭제
      2. PROTECT : 해당 요소가 같이 삭제되지 않음
      3. related_name : 원래 기본적으로 Primary Table에서 역참조 시 [역참조테이블]_set.~~ 방식으로 사용해야하는데 이것을 이름으로 바꿔주는 역할

### ManyToManyField 시 주의사항
1. related_name을 꼭 적어넣자(이름이 꼬일 수도 있으므로)
2. 역참조/참조 개념과 같은 개념이라고 생각하고 써야한다. 해당 Field가 있는 곳이 참조이기 때문에 그냥 사용해서 쓰면 된다. 역참조는 반대에서 사용해서 쓰는 것과 같다.