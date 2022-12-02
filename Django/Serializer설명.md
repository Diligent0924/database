# Serializer의 이해

### Serializer란 왜 쓰는가?
기본적으로 Backend에서 어떠한 로직 처리를 완료한 후 Front로 보낼 때 Json 형태로 보내야 Front에서도 받을 수 있다. 하지만 DB는 보통 RDBMS로 되어 있기 때문에 이 데이터는 RawQueryset/Queryset으로 나타나진다. 그러므로 이러한 부분을 Json으로 변환하기 위해 만들어진 Django만의 개념이다.

### Serializer의 사용방법은?

```python 
# 만약 Model을 그대로 가져다 쓰는 경우 => Model Instance의 속성값과 같을 때를 의미함  
class ArticleListSerializer(serializers.ModelSerializer):
    # 만약 추가적으로 필요한 값이 있다면 여기다 추가

    # 이 아래는 Model의 속성들을 들고오는 곳임
    class Meta:
    model = Article
    fields = "__all__"
            # 만약 1:N, M:N관계로 데이터를 숨기고 싶을 경우
            read_only_fields = ('article',)

#만약 Instace Json형태로 만들고자 할 경우
class ArticleListSerializer(serializers.Serializer):
    id = serializers.CharField(max_length=100)
```