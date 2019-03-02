
# Make Django Great Again (Part 4) : RESTful Framework



當我們將 Django 前端交由React處理後，自然就做到前後端的分割的型態（React render 前端component, 資料由Django 供給）。此時Django 分開成兩部分，也就是在Django template view中不會再出現參數丟到 html 檔案中，而是透過RESTful API 由javascipt獲取資料，再透過react 的props 或 state 呈現出資料數值。此時前端不再需要後端將資料丟進來，也因此另一個作法就是將前端改由NodeJS做後端的 serving, 而Django 角色變成一個RESTful API。這樣專案開發起來，協同性變得非常的好，同時Django views 處理的可以大大的降低。

那麼說到這裡Django 要如何寫自己的RESTful API 呢？

關於什麼是RESTful 知乎上有很好的解釋（注意url 的各式規律）：

[https://www.zhihu.com/question/28557115](https://www.zhihu.com/question/28557115)

回到主題, 先前在Flask 上手刻 RESTful API , 唯一問題是隨著物件越來越多，手動添加的urls 也會越來越繁雜。因此在Django 上有一個很好的套件叫 djangorestframework

安裝指令如下(記得開啟virtual environment)：

(myVENV) pip install djangorestframework==3.6.2

如果你跟過我這系列的第一篇文章教學，那麼你已經安裝過這個套件了～

安裝完畢之後在settings.py 中增加以下參數

    INSTALLED_APPS = [
       …
       ‘rest_framework’,
       …
    ]
    REST_FRAMEWORK = {
        'DEFAULT_PERMISSION_CLASSES': [
            'rest_framework.permissions.IsAdminUser',
        ],
        'PAGE_SIZE': 10
    }

這個教學我會使用Django 專案中原有的Models （Users ）來示範。首先新創一個 app

    django-admin startapp rest_api

並且在settings.py 中再增加這個參數

    INSTALLED_APPS = [
       …
       ‘rest_api’,
       …
    ]

在rest_api 中的views.py 新增新的views 物件，並且import Django 的User class 作為viewset 資料。

    from django.shortcuts import render
    from rest_framework import viewsets
    from django.contrib.auth.models import User
    from rest_api.serializers import UserSerializer

    class UserViewSet(viewsets.ModelViewSet):
          queryset = User.objects.all()
          serializer_class =  UserSerializer

再新增一個檔案叫serializer.py ，這個檔案的目的在於將一般物件serialized, 其目的讓資料不再以記憶形式存在，而是一連串的stream(資料流）呈現，方便網路的傳輸用途。

    from django.contrib.auth.models import User, Group
    from rest_framework import serializers

    class UserSerializer(serializers.HyperlinkedModelSerializer):
        class Meta:
            model = User
            fields = (‘url’,’username’,’email’,’groups’)

且增加一個檔案叫 apps.py

    from django.apps import AppConfig

    class RestApiConfig(AppConfig):
         name = ‘rest_api’

回到 project app 內部的urls.py中，添加以下幾行程式。

    ...
    from django.views.generic.base import TemplateView
    from rest_framework import routers
    from rest_api import views

    router = routers.DefaultRouter()
    router.register(r'users',views.UserViewSet)

    urlpatterns = [
         url(r'^v1/api/', include(router.urls)),
         ...
    ]

此時你就建好自己的Django RESTful API 了（撒花～）。過程可以看到我們完全不需要手動建任何物件的urls, 因為models 本身已經被serialized 了。所以rest_framework 自己可以建出符合RESTful API 規格的urls 樹。

此時，我們新增一個新的rootuser

    (myVENV) python manage.py createsuperuser

接著會跳出一堆要填寫的個人資料。除了使用者名稱與密碼為必要填寫之外，其他都可以enter 跳過。

新增完畢以後就可以開啟server， 執行瀏覽器並開這個網址 [http://localhost:8000/v1/api/](http://localhost:8000/v1/api/)

    (myVENV) python manage.py runserver

![正常的視窗](https://cdn-images-1.medium.com/max/2000/1*QNcoQzz2losIwxrfAJBf6w.png)*正常的視窗*

此時可以登入頁面(Log in) 並且將網址改成 [http://localhost:8000/v1/api/users/](http://localhost:8000/v1/api/users/) 就會看跳出以下結果。

![](https://cdn-images-1.medium.com/max/2000/1*T1y56T1lXhEBgvHUScGZ9Q.png)

再將網址改成 [http://localhost:8000/v1/api/users/1](http://localhost:8000/v1/api/users/1/)/ 就會看跳出以下結果

![](https://cdn-images-1.medium.com/max/2000/1*0lLgtRQyZvo-UQa_3xuWHQ.png)

在terminal 上使用curl 的話，登入指令如下：

    curl -u <你的使用者名字>:<你的密碼> -i [http://localhost:8000/v1/api/](http://localhost:8000/v1/api/)

這時候輸出結果應該會有類似這樣的畫面出現。

![我有兩個users 名字分別叫 django-admin與 theblackcat](https://cdn-images-1.medium.com/max/2000/1*QehJaDZ7J4aC8qecAXAM5Q.png)*我有兩個users 名字分別叫 django-admin與 theblackcat*

最後一篇Make Django Great Again 就到此為止咯。希望透過這系列的文章，能跳脫以往都在教Django MTV (MVC)模式，讓大家認識下不一樣的Django。如果反應好的話，我應該會繼續寫類似系列的文章吧。
