
Sass 是一種CSS 的進階寫法，具有巢狀迴圈、變數、運算、函數、可繼承（Mixins）的語法。但是本身卻無法直接被瀏覽器解讀，因此需要借助“編譯器” 轉換成CSS 才能使用。

簡單說一說為什麼2017 年應該拋棄CSS，而使用Sass(SCSS)、less 來編寫CSS代碼。

變數：

假想一個情境，你使用一種色調在多個不同的styling中etc:

    button.main{

        color: #353535;

    }

    .container-wrapper{

        color:#353535;

    }

可是如果你發現顏色似乎不怎麼搭配時，更改所有色調就要一個一個去調動。這時使用變數就能解救你手動更改所有色碼的厄運。

sass:

    $brown: #353535

    .main

       color: $brown

    .container-wrapper

       color: $brown

更動色碼時，就更改 $brown 的色碼就一次過更改了兩個物件的顏色

其他進階用法請參考：

[http://programmermagazine.github.io/201409/htm/focus2.html](http://programmermagazine.github.io/201409/htm/focus2.html)

[http://sass-lang.com/guide](http://sass-lang.com/guide)

一開始接觸Sass 時，我使用ruby 本身的指令集在Django 開發時編譯Sass:

    sass --watch /Users/theblackcat/style.scss:/Users/theblackcat/style.css

之後寫了一個bash script 幫我處理編譯的指令，可是用起來還有有種在鄉道開法拉利的感覺。

好不容易找到了Django 的sass 自動編譯器： sass-processor

    pip install django-sass-processor==0.5.4

安裝以後更改 settings.py

    SASS_PROCESSOR_AUTO_INCLUDE = False

    SASS_PROCESSOR_INCLUDE_FILE_PATTERN = r’^.+\.scss$’

    SASS_PRECISION = 8

    SASS_OUTPUT_STYLE = ‘compact’

    INSTALLED_APPS = (

       …

       ‘sass_processor’,

       …

    )

    SASS_PROCESSOR_INCLUDE_DIRS = [

       os.path.join(BASE_DIR, ‘extra-styles/scss’),

       os.path.join(BASE_DIR, ‘node_modules’),

    ]

    STATICFILES_FINDERS = [

       ‘django.contrib.staticfiles.finders.FileSystemFinder’,

       ‘django.contrib.staticfiles.finders.AppDirectoriesFinder’,

       ‘sass_processor.finders.CssFinder’,

    ]

    STATIC_ROOT = os.path.join(BASE_DIR, ‘extra-styles/’)

    STATIC_URL = ‘/static/’

    STATICFILES_DIRS = (

         os.path.join(BASE_DIR, ‘assets’),

    )

並且在assets 中建立新的文件夾新增新文件夾：

    mkdir /assets/extra-styles

在extra-styles中新增 scss 文件，用來放置任何sass、 scss 檔案。這裡要注意，如果你用sass 各式在SASS_PROCESSOR_INCLUDE_FILE_PATTERN 的 .scss 改成 .sass。以上參數都設置完畢後，就可以直接在 assets/extra-styles/scss 中存方自己的 sass/ scss 檔案。

當執行runserver 指令以後，這時在 base directory 會自動生成一個 extra-styles 文件夾，裡面就是編譯好的各種sass/ scss 檔案。

在Template 中讀取它們不再像一般使用 static tags 來讀取，而是要 load sass 套件的 tag來讀取編譯的檔案。

base.html

    …

    <link rel=”stylesheet” type=”text/css” href=”\{\% sass_src ‘extra-styles/scss/style.scss’ \%\}”>

    …

這時只要執行開發指令：

    python manage.py runserver

任何 sass/ scss 就會被自動編譯，搭配前一篇的 livereload 設置的話，開發時就可以省去重新刷新瀏覽器的功夫了。
