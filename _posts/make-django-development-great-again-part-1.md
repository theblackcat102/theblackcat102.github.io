
# Make Django Development Great Again (Part 1) : Webpack + React + Django



2017 年，身為Django 粉絲，心情百感交集。雖然碰過React, Angular 各種前端框架，可是都僅在NodeJS 上跟這教程寫。內心難免因為背叛Django而感覺小內疚。

在實習面試時，幾乎每位主管聽了我的自我介紹以後都一定問說“你的技能到底偏向後段還是前端？”

關於這問題，我內心也小糾結。主要因為多數的專案都在Django 上開發，使用的是傳統HTML, Sass + JQuery 的寫法，偶爾會配上Angular。說自己是前端工程師又有些牽強，畢竟前端框架實戰經驗不多。說自己是後端工程師，對於各種資料庫使用又不怎麼熟悉（抱歉，我都用Sqlite, 偶爾用用MySQL ) ，進階Redis、 RESTful API的使用也僅僅只有皮毛等級。然而再說自己是Django 後端工程師，業界使用Django 的公司真的不多（在台灣大概十根手指可以數完吧）。許多公司依舊使用Laravel , 年輕點的就直接使用 NodeJS 或 Rails。

於是趁著一星期的連假索性將 Webpack, Sass, RESTful API , Live reload 整合到Django 中。勢必要：MAKE DJANGO GREAT AGAIN。

開始建立專案前，確定要確定環境已經安裝了以下的配件：

1. Virtualenv

1. Python 3.4 (Django 1.9 在 2.7 似乎有bug )

1. 偉大的 npm

1. 偉大的 pip

**建立Django + Npm 專案：**

在某文件夾中執行以下指令：

    virtualenv -p python3.4 myVENV

    source myVENV/bin/source

    (myVENV)pip install django==1.9.7 django-webpack-loader==0.3.3 django-sass-processor==0.5.4 djangorestframework==3.6.2 django-livereload-server==0.2.3 django-compressor==2.1.1

    (myVENV)django-admin startproject django-webpack

    cd django-webpack

    npm init

    npm install — save react react-dom babel webpack webpack-dev-server

npm install — save-dev babel-core babel-loader babel-preset-react babel-preset-es2015 webpack webpack-dev-server webpack-bundle-tracker

以上指令執行內容順序大意如下：

1. 建立虛擬環境

1. 開啟Python虛擬環境

1. 安裝所需的套件

1. 建立Django 專案

1. 到專案文件夾內

1. 初始npm

1. 安裝各種套件

接著我們建立webpack 存放的路徑

    mkdir -p assets/js

    touch webpack.config.js

    touch assets/js/index.js

Index.js 為webpack 的entry point ，之後如果添加react component 則在 assets/js 中添加components 的文件夾即可

添加webpack.config.js 檔案，位置就在Django 專案的第一層內。

    var path = require(“path”);

    var webpack = require(‘webpack’);

    var BundleTracker = require(‘webpack-bundle-tracker’);

    module.exports = {

       context: __dirname,

       entry: ‘./assets/js/index.js’,

       output: {

          path: path.resolve(‘./assets/bundles/’),

          filename: “[name]-[hash].js”

      },

      plugins: [

          new BundleTracker({filename: ‘./webpack-stats.json’})

      ],

      module: {

       loaders: [

         { 
          test: /\.js$/, exclude: /node_modules/, loader: ‘babel-loader’,

          query:{

              cacheDirectory: true,

              presets: [‘es2015’, ‘react’]

            }

            }

         ]

        } 
    }; 

在index.js 中添加以下的code

    import React from ‘react’;

    import ReactDOM from ‘react-dom’;

    class App extends React.Component{

       render(){

        return(

           <div><h1>Make Django Great Again, Duh</h1></div>

        );

       }

    }

    ReactDOM.render( <App/>,document.getElementById(‘app’) );

執行指令 webpack — config webpack.config.js

如果沒有錯誤，結果應該如圖所示 ( TLDR; 沒有紅字就對了 XD )：

![](https://cdn-images-1.medium.com/max/2422/1*wdtB5zCUdwUsePG7IpFX3A.png)

如果一切沒有問題，接下就設置django-webpack/settings.py 檔案:

    TEMPLATES = [

    …

    ‘DIRS’: [os.path.join(BASE_DIR, ‘templates’)], # Add this

    …

    ]

    STATICFILES_DIRS = (

    os.path.join(BASE_DIR, ‘assets’),

    )

    WEBPACK_LOADER = {

    ‘DEFAULT’: {

    ‘BUNDLE_DIR_NAME’: ‘bundles/’,

    ‘STATS_FILE’: os.path.join(BASE_DIR, ‘webpack-stats.json’),

    }

    }

    INSTALLED_APPS = (

    …

    ‘webpack_loader’,

    ‘sass_processor’,

    ‘rest_framework’,

    ‘livereload’, #remove this in development

    )

其中，sass_processor , rest_framework, livereload, 的設置我會在接下來三篇文章逐一講解。( 前提是沒有突發狀況發生，例如：電腦爆炸 )

弄到這裡你應該已經沒什麼耐心了。如果你沒出現什麼奇葩的bug, webpack 設置就完畢了。

接著我們建立template/index.html

    mkdir template

    vim template/index.html

index.html 內容如下：

    {% load render_bundle from webpack_loader %}

    <!DOCTYPE html>

    <html>

    <head>

    <meta charset=”UTF-8">

    <title>Django is Great</title>

    </head>

    <body>

    <div id=”react-app”><h1>Opps something went wrong</h1></div>

    {% render_bundle ‘main’ %}

    </body>

    </html>

在django-webpack/urls.py 中添加路徑：

    from django.conf.urls import url

    from django.views.generic.base import TemplateView

    urlpatterns = [

    url(r’^$’, TemplateView.as_view(template_name=’index.html’), name=’index’),

    ]

這時，你可以執行

    webpack --watch --config webpack.config.js 

讓後台不斷compile 最新的js 檔案

在開啟Python 虛擬環境下執行

    (myVENV) python manage.py runserver

在瀏覽器輸入localhost:8000，輸出正確結果如下：

![](https://cdn-images-1.medium.com/max/2000/1*HP7zNCLTyJRFLAmXFa1AgQ.png)

錯誤結果如下：

![](https://cdn-images-1.medium.com/max/2000/1*qTRfk65zlDZp1D32e7w4Aw.png)

參考：[https://medium.com/@urangurang/react-on-django-boilerplate-3c3735df41f2](https://medium.com/@urangurang/react-on-django-boilerplate-3c3735df41f2)
