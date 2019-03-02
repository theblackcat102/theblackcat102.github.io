之前在PyCharm 上開發Django有一個插件能在更改任何的文件以後，瀏覽器自動更新的功能。然而，這個功能僅限Chrome （因為只有支援Chrome extension ….) 。這讓習慣使用Safari 的Responsive Mode( cmd + option + R) 的我來說，不怎麼方便啊…..

很久前在看DevTips頻道時，Travis 大大的教學視頻中瀏覽器都會自動更新。而還在手動更新的我 ，簡直自卑到內心深處。還好Django 有一個神奇插件 : django-livereload-server, 本身能監聽任何檔案（包括react ）更新狀態時，自動刷新瀏覽器頁面。更猛的是完全不需要安裝瀏覽器插件。

如果你看過我上一篇文章，我在一開始的安裝指令已經包含 django-livereload-server 。因此如果你半路殺進來看到這篇文章的話，安裝指令如下：

    (myVENV) pip install django-livereload-server==0.2.3

更改settings.py 檔案中設置：

    INSTALLED_APPS = (

    …

    ‘livereload’, #remove this in development

    …

    )

    MIDDLEWARE_CLASSES = [

    …

    ‘livereload.middleware.LiveReloadScript’,#remove this in production

    ]

記得在production時要移除這兩個參數，避免影響了後台效能。

開啟 Livereload Demo :

<iframe src="https://medium.com/media/9fd813ce65eeea6dca6aea95fed28d49" frameborder=0></iframe>

如此以後更改任何檔案都不需要再手動更新了，且搭配屏幕效果更佳～
