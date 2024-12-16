
> [!NOTE]
> Django'un [Resmi Site](https://docs.djangoproject.com/en/5.1/intro/tutorial01/)sinden Türkçeye  çevrilmiştir.

# İlk Django uygulamanızı yazma, 1. bölüm:
+ Örnekler ile öğrenelim
+ Bu eğitim boyunca, temel bir anket uygulamasının nasıl oluşturulacağı konusunda size yol göstereceğiz.
+ İki bölümden oluşacak:
	1. İnsanların anketleri görüntüleyip oy kullanmalarına olanak tanıyan halka açık bir site.
	2. Anket eklemenize, değiştirmenize ve silmenize olanak tanıyan bir yönetim sitesi.
+ We’ll assume you have [Django installed](https://docs.djangoproject.com/en/5.1/intro/install/) already.
+ Aşağıdaki komutu bir kabuk isteminde çalıştırarak ($ ​​önekiyle gösterilir) Django'nun kurulu olup olmadığını ve hangi sürümünün yüklü olduğunu anlayabilirsiniz:

```shell
$ python -m django --version
```

+ Django kuruluysa, kurulumunuzun sürümünü görmelisiniz. Değilse, "No module named django" diyen bir hata alırsınız.
+ Bu eğitim Python 3.10 ve üzerini destekleyen Django 5.1 için yazılmıştır. Django sürümü uyuşmuyorsa, bu sayfanın sağ alt köşesindeki sürüm değiştiriciyi kullanarak Django sürümünüze ait eğitime başvurabilir veya Django'yu en yeni sürüme güncelleyebilirsiniz. Daha eski bir Python sürümü kullanıyorsanız, Django'nun uyumlu bir sürümünü bulmak için  [What Python version can I use with Django?](https://docs.djangoproject.com/en/5.1/faq/install/#faq-python-version-support)konusuna bakın.
+ Django'nun eski sürümlerini nasıl kaldıracağınız ve daha yenisini nasıl yükleyeceğiniz konusunda tavsiyeler için  [How to install Django](https://docs.djangoproject.com/en/5.1/topics/install/) başlıklı makaleye bakın.


> [!TIP]
> + **Nerden yardım alırız:**
> + Bu eğitimi tamamlamada sorun yaşıyorsanız lütfen SSS'nin [Getting Help](https://docs.djangoproject.com/en/5.1/faq/help/) bölümüne gidin.

## Bir proje oluşturma:
+ Eğer Django'yu ilk defa kullanıyorsanız, bazı başlangıç kurulumlara dikkat etmeniz gerekecektir.
+ Django projesini kuran bazı kodları otomatik kurmak zorundasınız. Örneğin; django örneği için tüm ayarlar, veritabanın yapılandırmasını(config) dahil etme, Django'ya özgün opsiyonlar ve uygulamaya özgün ayarlar.
+ Komut satırından, kodunuzu depolamak istediğiniz dizine cd ile gidin ve djangotutorial adında yeni bir dizin oluşturun. (Bu dizin adı Django için önemli değildir; istediğiniz herhangi bir isimle yeniden adlandırabilirsiniz.)

```shell
$ mkdir djangotutorial
```

+ Daha sonra yeni bir Django projesini başlatmak için aşağıdaki komutu çalıştırın:

```shell
$ django-admin startproject mysite djangotutorial
```

+ Bu, **djangotutorial** dizininin içinde **mysite** adlı bir proje oluşturacaktır. Eğer işe yaramadıysa, [Problems running django-admin](https://docs.djangoproject.com/en/5.1/faq/troubleshooting/#troubleshooting-django-admin) bakın.


> [!NOTE]
> + Projelerinize yerleşik(built-in) Python veya Django bileşenlerinin adını vermekten kaçınmanız gerekir.
> + Özellikle, bu, django (Django'nun kendisiyle çakışacak) veya test (yerleşik Python paketiyle çakışacak) gibi isimleri kullanmaktan kaçınmanız gerektiği anlamına gelir.

+ Startproject'in ne oluşturduğuna bir bakalım:

```shell
djangotutorial/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```

+ Bu dosyalar şunlardır:
	+ `manage.py` : Bu Django projesiyle çeşitli şekillerde etkileşime girmenizi sağlayan bir komut satırı yardımcı programı. **Manage.py** hakkında tüm detayları [django-admin ve manage.py'da](https://docs.djangoproject.com/en/5.1/ref/django-admin/) okuyabilirsiniz.
	+  `mysite/` : Projeniz için gerçek Python paketi olan bir dizin. Adı, içindeki herhangi bir şeyi içe aktarmak için kullanmanız gereken Python paketi adıdır.  (e.g. `mysite.urls`).
	+ `mysite/__init__.py`: Python'a bu dizinin bir Python paketi olarak değerlendirilmesi gerektiğini söyleyen boş bir dosya. Eğer Python'a yeni başladıysanız, resmi [Python belgelerinde paketler](https://docs.python.org/3/tutorial/modules.html#tut-packages) hakkında daha fazla bilgi edinebilirsiniz.
	+ `mysite/settings.py`: Bu Django projesi için ayarlar/yapılandırma. [Django ayarları](https://docs.python.org/3/tutorial/modules.html#tut-packages) size ayarların nasıl çalıştığı hakkında her şeyi anlatacaktır.
	+ `mysite/urls.py`: Bu Django projesi için URL bildirimleri; Django destekli sitenizin “içindekiler tablosu”.  [URL dispatcher](https://docs.djangoproject.com/en/5.1/topics/http/urls/) da URL hakkında daha fazla bilgi edinebilirsiniz.

## Geliştirme sunucusu:
+ Django projenizin çalıştığını doğrulayalım. Eğer daha önce yapmadıysanız **djangotutorial** dizinine geçin ve aşağıdaki komutları çalıştırın:

```shell
$ python manage.py runserver
```

+ Komut satırında aşağıdaki çıktıyı göreceksiniz:

```shell
Performing system checks...

System check identified no issues (0 silenced).

You have unapplied migrations; your app may not work properly until they are applied.
Run 'python manage.py migrate' to apply them.

November 11, 2024 - 15:50:53
Django version 5.1, using settings 'mysite.settings'
Starting development server at [http://127.0.0.1:8000/](http://127.0.0.1:8000/)
Quit the server with CONTROL-C.
```


> [!NOTE]
> + Uygulanmamış veritabanı geçişleri hakkındaki uyarıyı şimdilik dikkate almayın; veritabanıyla yakında ilgileneceğiz.

+ Artık sunucumuz çalışıyor, web tarayıcınız ile http://127.0.0.1:8000/ adresini ziyaret edin.
+ Bir roketin havalandığı "Tebrikler!" sayfasını göreceksiniz. Çalıştı.
+ Tamamen Python ile yazılmış hafif bir web sunucusu olan Django geliştirme sunucusunu(*development server*) başlattınız.
+ Bunu(*development server*) Django'ya ekledik, böylece *Production ortamı* hazır olana kadar Apache gibi bir *production* sunucusunu yapılandırmakla uğraşmanıza gerek kalmadan, hızla geliştirme yapabilirsiniz.


> [!CAUTION]
> + *Şimdi not almak için iyi bir zaman:* Bu sunucuyu *Production ortamına* benzeyen hiçbir yerde kullanmayın.
> + Sadece geliştirme sırasında kullanılması amaçlanmıştır. (Biz web framework üretme işindeyiz, web sunucuları üretme işinde değiliz.)
> + (Siteyi farklı bir portta sunmak için  [`runserver`](https://docs.djangoproject.com/en/5.1/ref/django-admin/#django-admin-runserver) referansına bakın.)



> [!IMPORTANT]
> + **[Runserver](https://docs.djangoproject.com/en/5.1/ref/django-admin/#django-admin-runserver)'ın otomatik olarak yeniden yüklenmesi:**
> + Geliştirme sunucusu, gerek duyulduğunda her istek için Python kodunu otomatik olarak yeniden yükler.
> + Kod değişikliklerinin etkili olması için sunucuyu yeniden başlatmanıza gerek yok.
> + Ancak dosya ekleme gibi bazı eylemler yeniden başlatmayı tetiklemez, bu nedenle bu durumlarda sunucuyu yeniden başlatmanız gerekir.

## Anketler uygulamasını oluşturma:

+ Artık ortamınız - bir "proje"- kurulduğuna göre, çalışmaya başlamaya hazırsınız.
+ Django'da yazdığınız her uygulama, belirli bir düzene uyan bir Python paketi olarak oluşturulur.
+ Django, bir uygulamanın temel dizin yapısını otomatik olarak oluşturan bir araç ile birlikte gelir, böylece dizinler oluşturmak yerine kod yazmaya odaklanabilirsiniz.


> [!NOTE]
> + **Projeler vs uygulamalar:**
> + Proje ile uygulama arasındaki fark nedir?
> + **Bir uygulama**, belirli bir işlevi yerine getiren bir web uygulamasıdır – örneğin, bir blog sistemi, kamu kayıtları veritabanı veya küçük bir anket uygulaması.
> + **Proje**, belirli bir web sitesi için yapılandırma ve uygulamaların bir toplamıdır.
> + Bir **proje** birden fazla uygulama içerebilir. Bir **uygulama** birden fazla projede olabilir.

+ Uygulamalarınız Python yolunuzun( [Python path](https://docs.python.org/3/tutorial/modules.html#tut-searchpath "(in Python v3.13)")) herhangi bir yerinde yaşayabilir. Bu eğitimde poll(anket) uygulamamızı **djangotutorial** klasörü içerisinde oluşturacağız.
+ Uygulamanızı oluşturmak için *manage.py* ile aynı dizinde olduğunuzdan emin olun ve şu komutu yazın:

```shell
$ python manage.py startapp polls
```

+ Bu, aşağıdaki şekilde düzenlenmiş bir **polls** dizini oluşturacaktır:

```shell
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

+ Bu dizin yapısı poll uygulamasını barındıracaktır.

## İlk view'ınızı yazınız:

+ İlk view'i yazalım. polls/views.py dosyasını açın ve içine aşağıdaki Python kodunu yazın:

```python
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```

+ Bu, Django'da mümkün olan en temel view'dir.
+ Bir tarayıcıda buna erişmek için onu bir URL'ye eşlememiz gerekir - ve bunun için bir URL yapılandırması veya kısaca "URLconf" tanımlamamız gerekir.
+ Bu URL yapılandırmaları her Django uygulamasının içinde tanımlanmıştır ve urls.py adlı Python dosyalarıdır.
+ polls uygulaması için bir `URLconf` tanımlamak üzere, aşağıdaki içeriğe sahip `polls/urls.py` adlı bir dosya oluşturun:

```python
from django.urls import path

from . import views

urlpatterns = [
    path("", views.index, name="index"),
]
```

+ Bir sonraki adım, mysite projesindeki global `URLconf` dosyasını, `polls.urls` içinde tanımlanan `URLconf`'u dahil edecek şekilde yapılandırmaktır.
+ Bunu yapmak için `mysite/urls.py`'ye `django.urls.include` için import ekleyin ve `urlpatterns` listesine bir `include()` ekleyin, böylece şu şekilde olmalıdır::

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path("polls/", include("polls.urls")),
    path("admin/", admin.site.urls),
]
```

+ [`path()`](https://docs.djangoproject.com/en/5.1/ref/urls/#django.urls.path) fonksiyonu en az iki argüman bekler: `route` ve `view`.
+ [`include()`](https://docs.djangoproject.com/en/5.1/ref/urls/#django.urls.include) fonksiyonu diğer `URLconf`'lara referans vermeyi sağlar.
+ Django `include()` ile karşılaştığında, o noktaya kadar eşleşen URL kısmını keser ve kalan dizeyi daha ileri işleme için dahil edilen URLconf'a gönderir.
+ include()'un arkasındaki fikir, URL'lerin *tak-çalıştır özelliğini* (`plug-and-play URLs`) kolaylaştırmaktır.
+ Poll kendi `URLconf`'larında (polls/urls.py) olduğundan, `/polls/` altına veya `/fun_polls/` altına veya `/content/polls/` altına veya başka herhangi bir kök yola(`root path`) yerleştirilebilir ve uygulama yine de çalışacaktır.


> [!TIP]
> + `include()` ne zaman kullanılır?
> + Diğer URL desenlerini dahil ederken her zaman `include()` kullanmalısınız.
> + Tek istisna, Django'nun varsayılan yönetici sitesi için sağladığı önceden oluşturulmuş bir URLconf olan admin.site.urls'dir.

+ Şuan URLconf içerisine `index view`'i bağladınız. Aşağıdaki komutla çalıştığını doğrulayın:

```shell
$ python manage.py runserver
```

+ Tarayıcınızda [http://localhost:8000/polls/]( http://localhost:8000/polls/) adresine gidin, ve `index view` de tanımlamış olduğunuz “Hello, world. You’re at the polls index.” yazısını görmelisiniz.


> [!WARNING]
> + Sayfa bulunamadı?
> + Burada bir hata sayfası alırsanız [http://localhost:8000/polls/](http://localhost:8000/polls/) adresine gittiğinizden ve [http://localhost:8000/](http://localhost:8000/) adresine gitmediğinizden emin olun.

+ Temel istek ve yanıt akışını anladığınızda, veritabanı ile çalışmaya başlamak için bu eğitimin 2. bölümünü okuyun.

# İlk Django uygulamanızı yazma, 2. bölüm
+ Bu eğitim, Eğitim 1'in kaldığı yerden başlıyor.

[Devam Link](https://docs.djangoproject.com/en/5.1/intro/tutorial02/)
