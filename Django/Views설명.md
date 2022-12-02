# Views는 어떠한 경우에 사용하는가?

### Views이란 무엇인가?
다른 여러가지 방법이 있지만 여기서는 api_view를 이용하여 나타낸다. Views는 모든 논리적인 알고리즘들을 나타내는 곳으로 가장 중요한 부분임  

### Views의 사용방법
```python
@api_view["GET","POST"] # 반드시 써줘야한다.
def article_list(request):
    if request.method == 'GET':
        # articles = Article.objects.all()
        # articles = get_list_or_404(Article)
        articles = Article.objects.raw('select * from [DB내에서의 이름]')
        serializer = ArticleListSerializer(articles, many=True)
        return Response(serializer.data)

    elif request.method == 'POST':
        serializer = ArticleSerializer(data=request.data)
        if serializer.is_valid(raise_exception=True):
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)

```

### ORM vs SQL
ORM은 기본적으로 해당 프레임워크에서 SQL을 처리하기 위해 만들어진 방법이다. 하지만 결국 ORM으로 사용된 방법도 SQL문으로 변경된 후에 DB에 들어가게 된다.  
SQL은 DB에서 사용하는 문법으로 어떤 프레임워크던지 SQL을 사용할 수 있게끔 만들어놓았다.(애초에 ORM이 SQL의 쉬운 처리를 위해 만들어졌으므로...)

=> 개인적인 생각으로는 SQL문을 사용하는 것이 어떤 언어를 사용하든 가능하므로 좋을 것 같다.(실제로 좀 더 빠르기도 하고..)