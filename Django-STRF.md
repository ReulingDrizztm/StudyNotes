# Django-STRF

```python
strftime：日期转字符串
strptime：字符串转日期
loads：字符串转字典
dumps：字典转字符串
如：
startDate = "2018-10-01"
endDate = "2018-10-31"

###字符转化为日期
startTime = datetime.datetime.strptime(startDate, '%Y-%m-%d').time()
endTime = datetime.datetime.strptime(endDate, '%Y-%m-%d').time()

now = datetime.datetime.now()
print(now)

###日期转化为字符串
print("--1---:" + datetime.datetime.strftime(startTime, "%Y-%m-%d"))
print("--2---:" + datetime.datetime.strftime(endTime, "%Y-%m-%d"))
```

```python
python中 将字符串和字典的相互转换
1.首先引入json模块

# 引入json模块
import json
 

2.转换

#JSON到字典转化：
dictinfo = json.loads(json_str) # 输出dict类型
字典到JSON转化：
jsoninfo = json.dumps(dict) # 输出str类型
```
```python
GET ===========> /books ================> 查询所有图书信息
POST ==========> /books ================> 添加图书信息
PUT ===========> /books/id =============> 修改指定的图书信息
DELETE ========> /books/id =============> 删除指定的图书对象
GET ===========> /books/id =============> 查询指定的图书对象
```

```txt
添加、修改数据成功后返回json格式数据的时候，需要指定状态码为201：status=201
删除数据成功后返回json格式数据的时候，需要指定返回状态码为204，返回的数据为一个空字典
添加json格式数据的时候，键的格式注意要使用双引号""
```

序列化与反序列化
```
序列化可以理解为：把python的对象编码转换为json格式的字符串，反序列化可以理解为：把json格式字符串解码为python数据对象

总而言之：
将数据库数据序列化为前端所需要的格式，并返回；
将前端发送的数据反序列化为模型类对象，并保存到数据库中
```

使用REST ：
安装
注册
在子应用中新建serializers.py文件
```python
from rest_framework import serializers
from .models import BookInfo


class BookSerializer(serializers.ModelSerializer):
	'''图书序列化器'''
	calss Meta:
		# 指定模型类
		model = BookInfo
		# 指定字段
		fileds = '__all__'
```

在视图文件中引入
```python
from rest_framework.viewsets import ModelViewSet
from .serializers import BookSerializer


class BookViewSet(ModelViewSet):
	serializers_class = BookInfoSerializer
	queryset = BookInfo.object.all()
```

在urls.py文件中配置路由
```python
from rest_framework.routers import DefaultRouter


router = DefaultRouter()
router.register('books_drf', views.BookViewSet)
urlpatterns += router.urls
```
最后，在浏览器中输入相应地址，就可以访问到Django提供好的可视化界面了

Serializer序列化器
`封装了序列化和反序列化`

基于模型类：
```python
# 定义图书模型类BookInfo
class BookInfo(models.Model):
    btitle = models.CharField(max_length=20, verbose_name='名称')
    bpub_date = models.DateField(verbose_name='发布日期')
    bread = models.IntegerField(default=0, verbose_name='阅读量')
    bcomment = models.IntegerField(default=0, verbose_name='评论量')
    is_delete = models.BooleanField(default=False, verbose_name='逻辑删除')
    image = models.ImageField(upload_to='books', verbose_name='图片', null=True)
```
在serializers.py文件中创建序列化器
```python
# 定义模型类，继承自serializers.Serializer
class BookInfoSerializer(serializers.Serializer):
    """图书数据序列化器"""
    id = serializers.IntegerField(min_value=1, read_only=True)
    btitle = serializers.CharField(label='名称', max_length=20)
    bpub_date = serializers.DateField(label='发布日期', required=False)
    bread = serializers.IntegerField(label='阅读量', required=False)
    bcomment = serializers.IntegerField(label='评论量', required=False)
    image = serializers.ImageField(label='图片', required=False)
```

在视图文件中创建视图
```python
class BookInfoView(View):
    def post(self, request):
        book = BookInfo.objects.get(pk=1)
        book_serializer = BookInfoSerializer(book)
        json_data = book_serializer.data

        return JsonResponse(json_data)
```

在路由中配置路由地址
```python
urlpatterns = [
    url('^bookinfo$', views.BookInfoView.as_view())
]
```

自此，序列化器创建完成，因为是post请求方式，使用postman模拟浏览器操作。最终请求的结果为：
```
{
  "id": 1,
  "btitle": "射雕英雄传",
  "bpub_date": "1980-05-01",
  "bread": 12,
  "bcomment": 34,
  "image": "books/u33700920393638518349fm27gp0.jpg"
}
```
与我数据库中的数据一致

