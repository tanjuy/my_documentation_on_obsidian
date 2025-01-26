
> [!CAUTION]
> + Burada yapılan tüm işlemler `Ubuntu 22.04` üzerinde gerçekleştirilmektedir.


> [!IMPORTANT]
> + Django, **hızlı geliştirmeyi** ve **temiz**, **pragmatik tasarımı** teşvik eden üst düzey bir Python web *framework*'üdür


> [!NOTE]
> + **Web framework nedir?**
> + Web framework, web uygulamaları ve web siteleri geliştirmek için kullanılan yazılım altyapılarıdır.
> + Web framework'leri, temel yapı taşlarını ve çeşitli araçları sağlayarak geliştiricilerin projeleri daha hızlı ve verimli bir şekilde oluşturmasına yardımcı olur.
> + Bu framework'ler, birçok yaygın işlevi ve bileşeni standartlaştırarak geliştiricilerin tekrarlayan kod yazmasını azaltır ve güvenli, sürdürülebilir, ölçeklenebilir web uygulamaları oluşturmayı kolaylaştırır.

## Django nedir? 

+ Django, **battaries included** felsefesini takip etmektedir.
+ Django’nun "batteries included" (pil dahil) felsefesi, Django framework'ünün, bir web uygulaması geliştirmek için gerekli olan temel araçların ve özelliklerin çoğunu kendi bünyesinde sunması anlamına gelir
+ Django, geliştiricilerin ek eklenti veya üçüncü taraf modüllere ihtiyaç duymadan hızlı ve eksiksiz projeler oluşturmasını sağlamak amacıyla kapsamlı bir standart kütüphane içerir.
+ **Kimler Django kullanıyor** soruna cevap olarak; Youtube, Spotify, Instagram ve Mozilla

## Django Yükleme:

```shell
$ python -m venv .venv
```
> **Explanation:**
> + `venv` aracı ile sistemiz de kurulu olan python kütüphaneleri ile bir izolasyon sağlayabiliyoruz. 
> + Eğer sisteminizde  python'un `venv` kütüphanesi yüklü değil ise:  `sudo apt install python3.10-venv` komutu ile yükleme yapabilirsiniz.
> + Ayrıca, Eğer sisteminizde `pip` aracı yani kütüphanesi yüklü değil ise: `sudo apt install python3-pip` komut ile yükleme yapabilirsiniz. 

```shell
$ source .venv/bin/activate
```
> **Explanation:**
> + Bu komut ile sanal ortamımızı aktif ediyoruz.
> + `venv` sanal ortamımızı pasif etmek için yanlızca `deactivate` yazmamız yeterlidir.
> + Sanal ortamı aktif etikten sonra `pip list` veya `python -m pip list` komutuna baktığımızda yalnızca iki kütüphane mevcut olduğunu göreceğiz.

```shell
$(.venv) pip install Django
```
> **Explanation:**
> + Bu komut ile `Django framework` sanal ortama indirmiş yani kurulumunu gerçekleştirmiş bulunuyoruz.
> + `pip list` komut ile kurulumu teyit edebilirsiniz.

```shell
$(.venv) django-admin
```
> **Explanation:**
> + Django'un yüklü olup olmadığını gösterir. Bu komut `django-admin` yardım sayfasını ekrana basar.
## blog Proje Başlatma:
```shell
$(.venv) django-admin startproject blog
```
> **Explanation:**
> + *Django'da yeni bir proje başlatmak için kullanılır.* Bu komut, Django'nun temel yapılarını içeren bir klasör yapısı oluşturur.
> + Özellikle, `blog` adında yeni bir proje klasörü oluşturur ve içine aşağıdaki dosya ve klasörleri yerleştirir:
> 1. **manager.py:** Proje yönetim komutlarını çalıştırmak için kullanılan bir betiktir. Bu komutla *sunucuyu başlatabilir*, *veritabanı işlemleri yapabilir* ve diğer Django komutlarını çalıştırabilirsiniz.
> 2. **blog** (proje ana dizini):
> 	+ `__init__.py` : Python'a bu dizinin bir Python paketi olarak değerlendirilmesi gerektiğini söyleyen boş bir dosya.
> 	+ `settings.py`: Projenin tüm ayarlarını içerir (veritabanı ayarları, uygulama yapılandırmaları, dil seçenekleri vb.).
> 	+ `urls.py`: URL yönlendirmeleri için kullanılan ana dosyadır. urls.py dosyası django projesi ile ilgili tüm URL'i içerir.
> 	+ `wsgi.py` : Projenize hizmet verecek WSGI uyumlu web sunucularına yönelik bir giriş noktası. Yani, Django uygulamasını bir WSGI uyumlu web sunucusunda çalıştırmak için kullanılır.
> 	+ `asgi.py`: Django'nun ASGI uyumlu sunucularda çalışabilmesi için bir yapılandırma sağlar (genellikle gerçek zamanlı uygulamalar için kullanılır).
> 	+ Daha fazla bilgi için [Resmi sitesi](https://docs.djangoproject.com/en/5.1/intro/tutorial01/#creating-a-project) bakınız.


```shell
.
└── blog                               # 1
    ├── blog                           # 2
    │   ├── asgi.py
    │   ├── __init__.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    └── manage.py
```
> **Explanation:**
> 0. `tree` komutunu ile `django-admin startproject blog` ile hangi dosyalar ve dizinler oluşturduğumuzu hiyerarşik olarak görebiliyoruz.
> 1. Proje oluşturma komutunda(`django-admin startproject blog`) verdiğimiz isim de klasör oluşturuluyor.
> 2. Bir alt dizinde de komut adındaki ile aynı isimde klasör oluşturuluyor.

### Proje urls.py Dosyası:
#### Basit Kullanımı:
```python
from django.urls import path
from posts import views                           # 1

urlpatterns = [
    path('admin/', admin.site.urls),
    path('post/helloWorld/', views.helloWorld)    # 2
]
```
> **Explanation:**
> 1. `from posts import views` ile `posts` uygulamamızdaki `views.py` dosyasını bu komut ile dahil ediyoruz. 
> 2. **Uyarı:** Uygulama içerisinde `views.py` dosyasına yazmış olduğumuz veya yazacağımız fonksiyonu çağırmıyoruz yani çalıştırmıyoruz. Sadece referans veriyoruz. 
> + Eğer bu kodları kullanıyorsanız, [[Django#posts app Oluşturma#views.py|Basit Kullanımı]] yani *posts app Oluşturma* `->` *views.py* `->` *1.Function-Based Views - FBV* `->` *Basit Kullanımı*  ile devam ediniz! 

#### include fonksiyonu:
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('post/', include('posts.urls'))
]
```

## Geliştirme Sunucusu Çalıştırma:
```shell
$ python3 manage.py runserver
```
> **Explanation:**
> + Yukarıdaki komut çalıştırmak için `cd myblog` komutu ile `blog` dizinine giriş yapmamız gerekmektedir. Çünkü `manage.py` bu dizin içerisindedir.


> [!NOTE]
> + `ss -tuln` komutu ile hangi portların açık olduğunu teyit edebilisiniz!

##### Port Numarasını Değiştirme:
```shell
$ python3 manager.py runserver 8080
```
> **Explanation:**
> + `runserver` parametresi varsayılan olarak 8000 port'u üzerinde yayın yapar.
> + Eğer 8000 port'u dışında farklı bir port'dan yayın yapmak isterseniz port numarasını `runserver` parametresinden sonra belirtmek zorundayız.


##### IP Adresini Değiştirme:
```shell
$ python3 manager.py runserver 192.168.1.132:8000
```
> **Explanation:**
> + `runserver` parametresi varsayılan olarak `127.0.0.1:8000` IP adresinden yayın yapar.
> + Eğer dışarıdaki makinelere yayın yapabilmemiz için hem IP adresini hem de port numarasını belirtmemiz gerekmektedir.
> + Böylelikle herhangi bir tarayıcı ile `http://192.168.1.132` adrese istek atabiliriz.
> + **Uyarı:** `setting.py` dosyasındaki `ALLOWED_HOST = ["192.168.1.132"]` şekillinde IP adresine izin vermeliyiz.  


```shell
curl -X GET -i http://192.168.1.132:8000
```

## posts app Oluşturma:
+ Django'da bir **app** (uygulama), projenin belirli bir işlevselliğini ya da özelliğini sağlayan, modüler bir kod birimidir.
+ Bir Django projesi genellikle birden fazla uygulamadan oluşur ve bu uygulamalar, bağımsız bir şekilde geliştirilebilir ve tekrar kullanılabilir.


> [!CAUTION]
> + Django da oluşturulan uygulamalar(apps) tekrar kullanılabilir(reusable). Yani bir projede oluşturulduğunuz app başka bir projede tekrardan kullanılabilir. 


```shell
$ python3 manage.py startapp posts
```
> **Explanation:**
> + `posts` django da app olarak adlanırılmaktadır.

```shell
.
├── blog                     # proje
│   ├── asgi.py
│   ├── __init__.py
│   ├── __pycache__
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── db.sqlite3
├── manage.py
└── posts                    # app
    ├── admin.py
    ├── apps.py
    ├── __init__.py
    ├── migrations
    ├── models.py
    ├── tests.py
    └── views.py
```

### views.py:
+ Django'da **`views.py`**, web uygulamanızın **mantık katmanını** barındıran dosyadır.
+ Bir kullanıcının belirli bir URL'yi talep ettiğinde, bu isteğe nasıl bir yanıt verileceğini tanımlayan Python kodlarını içerir.
+ Bu yanıtlar genellikle bir HTML sayfası, JSON verisi veya başka türde bir içerik olabilir.
+ `view` istekleri el alır ve cevapları geri döner.

#### 1.Function-Based Views - FBV:
+ Basit ve küçük projelerde yaygındır. Python fonksiyonları kullanılarak tanımlanır.
##### 1.1.Basit Kullanımı:
**view.py dosyası:**
```python
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
def helloWorld(request):
    return HttpResponse("Hello World")
```
> **Explanation:**
> + `helloWorld` adında view yazmış bulunmaktayız. Kodun yapısından da anlaşıldığı üzeri `Function-Based Views` olduğu görünmektedir.
> + `helloWorld` adında bir Django view fonksiyonudur. Bu fonksiyon, bir kullanıcı web tarayıcısından bir istek (örneğin, bir URL'e erişim) gönderdiğinde çalışır ve basit bir "Hello World" yanıtı döner.
> + `request`, Django tarafından otomatik olarak gönderilen bir nesnedir. Bu nesne, istemciden (tarayıcıdan) gelen **HTTP isteği** ile ilgili bilgileri içerir. İstek türü (GET, POST), başlık bilgileri (headers), form verileri ve URL parametreleri gibi bilgileri taşır.
> + `request` aslında bir **HttpRequest** nesnesidir ve şunları içerir:
> 	+ **`request.method`:** İsteğin türü. Örneğin, `"GET"` veya `"POST"`.
> 	+ **`request.GET`:** URL'deki sorgu parametrelerini alır (örneğin: `?name=John`).
> 	+ **`request.POST`:** Formdan gelen verileri alır (eğer `POST` yöntemiyle gönderilmişse).
> 	+ **`request.headers`:** HTTP başlık bilgilerini alır.


> [!NOTE]
> + `request` argümanı `HttpRequest Class`'ın bir `instance`'dır.
> + URL'e bağlı view çağrıldığında `HttpRequest` Sınıfından bir örnek(`instance`) oluşturulur ve view fonksiyona argüman olarak verilir.


**GET isteği:**
```shell
curl -X GET -i http://192.168.1.132:8080/post/helloWorld/
```

```http
HTTP/1.1 200 OK
Date: Sun, 15 Dec 2024 10:21:10 GMT
Server: WSGIServer/0.2 CPython/3.10.12
Content-Type: text/html; charset=utf-8
X-Frame-Options: DENY
Content-Length: 11
X-Content-Type-Options: nosniff
Referrer-Policy: same-origin
Cross-Origin-Opener-Policy: same-origin

Hello World
```
> **Explanation:**
> + Eğer tarayıcıda `http://localhost:8000/hello` adresine gidilirse:
> 1. Django, bu URL’i bu `helloWorld` fonksiyonuna yönlendirir.
> 2. Tarayıcıdan gelen istek bilgileri `request` parametresiyle fonksiyona iletilir.
> 3. Sunucu, `"Hello World"` içeriğini tarayıcıya döner.
##### 1.2.`urls.py` Dosyası oluşturma:
+ Django'da bir **app** içinde ek olarak `urls.py` dosyası oluşturmak, uygulamanızın URL yönlendirmelerini daha modüler ve düzenli hale getirmek için kullanılan bir yöntemdir.

```shell
touch urls.py
```


```shell
.
└── blog
    ├── blog
    │   ├── asgi.py
    │   ├── __init__.py
    │   ├── __pycache__
    │   ├── settings.py
    │   ├── urls.py     # <-------- blog project
    │   └── wsgi.py
    ├── db.sqlite3
    ├── manage.py
    └── posts
        ├── admin.py
        ├── apps.py
        ├── __init__.py
        ├── migrations
        ├── models.py
        ├── __pycache__
        ├── tests.py
        ├── urls.py     # <-------- touch urls.py (posts app)
        └── views.py
```

**urls.py app dosyası:**
```python
from django.urls import path
from . import views

urlpatterns = [
    path('helloWorld/', views.helloWorld)
]
```
> **Explanation:**
> + Bu yukarıdaki işlemleri yapıyorsanız, proje dosyasındaki(blog projesi) `urls.py` dosyasında `include fonksiyonu` ile uygulamadaki `urls.py` dosyasını dahil ediniz.
> + Yani, blog Proje Başlatama `->` Proje urls.py Dosyası `->` include fonksiyonu başlığı altındaki işlemleri yapınız.
> + `curl -X GET -i -L http://192.168.1.132/post/helloWorld/` ile istek gönderdiğimizde `blog` projesin içerisindeki `post` uygulaması içerisindeki `view.py` dosyasında yazılmış olan `helloWorld view fonksiyonu` çalıştırılacaktır.

###### App urls.py Avantajları:
1. **Modülerlik:** Django projeleri genellikle birden fazla uygulamadan oluşur. Her uygulamanın kendi `urls.py` dosyasına sahip olması URL yönetimini modüler hale getir.
2. **Kolay Yönetim:** Uygulama bazlı URL'lerle çalışmak, projedeki URL'leri yönetmeyi kolaylaştırır. Ana `urls.py` dosyası, yalnızca uygulamaların URL'lerini dahil etmekle (örneğin, `include()`) ilgilenir ve bu da karmaşıklığı azaltır.
3. **Yeniden Kullanılabilirlik:** Django uygulamaları modülerdir ve birden fazla projede tekrar kullanılabilir. Eğer bir uygulamanın kendi `urls.py` dosyası varsa bu uygulamayı başka bir projeye entegre ederken URI tanımlamalarını da kolayca beraberinde getirir.


##### 1.3.Veri Çekme:
+ Program içerisinden veya veri tabanından kullanıcıya veya tarayıcıya veri gönderme işlemi.  

**view.py dosyası:**
```python
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.

posts = [
    {
        "id":1,
        "title":'Let\'s expose python',
        "content":'Python Is Intepreted, High level, general purpose \
        programming language. Widely used in the fields of web \
        development, data science and machine learning.'
    },
    {
        "id":2,
        "title": 'Let\'s explore Javascript',
        "content": 'Javascript Is Interpreted, High level, general \
        purpose programming language. Widely used in the fields \
        of web development'
    },
    {
        "id":3,
        "title": 'Django the best web framework',
        "content": 'Django is used by almost every big tech company\
        like facebook, google, youtube, instagram etc.'
    },
]

def helloWorld(request):
    html = ""

    for post in posts:
        html += f'''
            <div>
                <h1>{post['id']} - {post['title']}</h1>
                <p>{post['content']}</p>
            </div>
        '''
    return HttpResponse(html)
```
> **Explanation:**
> + `post` adındaki liste verisini kullanıcı tarafına aktarıyoruz;
> + `for loop` ile liste verilerini `HttpResponse` sınıfına parametre olarak veriyoruz.

#### 2.Class-Based Views - CBV:
+ Daha karmaşık projelerde esneklik sağlar. Python sınıfları kullanılarak tanımlanır.

> [!NOTE]
>  + **Modülerlik ve Yeniden Kullanılabilirlik:**
>  + Bir uygulama, belirli bir işlevselliği kapsar. Bu sayede, bir uygulamayı başka projelere kolayca taşıyabilirsiniz.
>  + Örneğin, bir "kullanıcı doğrulama" uygulaması farklı projelerde yeniden kullanılabilir.
>  + **Proje Yönetimini Kolaylaştırma:**
>  + Büyük projelerde farklı özellikler farklı uygulamalar olarak ayrılır. Örneğin:
>  + **blog**: Blog gönderilerini yönetir.
>  + **e-commerce**: Ürünler ve siparişleri yönetir.
>  + **authentication**: Kullanıcı oturumlarını ve kayıt işlemlerini yönetir.
>  + **Django'nun MVC (Model-View-Controller) Yapısını Destekleme**:
>  + Uygulamalar, Django’nun MVT (Model-View-Template) mimarisini takip ederek projeyi daha düzenli ve okunabilir kılar.





## Proje Ayarları:

**settings.py:**
```python
"""
Django settings for blog project.
Generated by 'django-admin startproject' using Django 5.1.3.

For more information on this file, see
https://docs.djangoproject.com/en/5.1/topics/settings/

For the full list of settings and their values, see
https://docs.djangoproject.com/en/5.1/ref/settings/
"""

from pathlib import Path

# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve().parent.parent

# Quick-start development settings - unsuitable for production
# See https://docs.djangoproject.com/en/5.1/howto/deployment/checklist/

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = 'django-insecure-dy-!h3-l@vbpk6(r9x7syuy(@5##&s2!svxse=0#1r=z8ql@5$'

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True

ALLOWED_HOSTS = []

# Application definition
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'blog.urls'

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'blog.wsgi.application'

# Database
# https://docs.djangoproject.com/en/5.1/ref/settings/#databases

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# Password validation
# https://docs.djangoproject.com/en/5.1/ref/settings/#auth-password-validators

AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },

    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]

# Internationalization
# https://docs.djangoproject.com/en/5.1/topics/i18n/

LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'UTC'

USE_I18N = True

USE_TZ = True


# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/5.1/howto/static-files/

STATIC_URL = 'static/'

# Default primary key field type
# https://docs.djangoproject.com/en/5.1/ref/settings/#default-auto-field

DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'
```

### ROOT_URLCONF:

+ **`ROOT_URLCONF`**, Django projesinin **ana URL yönlendirme(routing) dosyasını** tanımlar. Bu dosya genellikle bir Python modülüne (örneğin, `urls.py`) işaret eder.

#### Varsayılan Ayar:
+  Django da bir proje oluşturduğunuzda, genellikle şu şekilde bir yapı oluşturulur:
+ `settings.py`  içinde;

```python
ROOT_URLCONF = '<Proje_Adı>.urls'
```

+ Örneğin; **blog** adlı django projesinde bu ayar şöyle görünebilir:

```python
ROOT_URLCONF = 'blog.urls'
```

+ Burada `blog/urls.py`, Django'nun tüm URL eşleşmelerini(routing) kontrol ettiği dosyadır.

#### Nasıl Çalışır:
1. **URL İstekleri:** Django'ya bir HTTP isteği geldiğinde, ilk olarak bu istek `ROOT_URLCONF` da belirtilen `urls.py` dosyasına yönlendirilir.
2. **URL Yönlendirmesi:** Django, `urls.py` dosyasındaki URL desenleri(patterns) ve uygun bir eşleşme bulmaya çalışır. Eğer bir eşleşme bulunursa, ilgili `view` fonksiyonu çalıştırılır.
3. **Eşleşme Yoksa:** Eğer bir eşleşme bulunamaz ise, Django otomatik olarak bir `404 Not Found` geri döner.

## Python Sınıfları:
### HttpRequest:

## MVC Yapısı:
+ Python’da MVC (Model-View-Controller), uygulamaların kod yapısını organize etmek için kullanılan bir tasarım desenidir.
+ Bu yapı, uygulamanın farklı bileşenlerini ayırarak daha modüler, okunabilir ve yönetilebilir hale getirir.
+ Özellikle Django gibi Python web framework'lerinde MVC'nin bir varyasyonu kullanılır.
##### MVC Yapısını Bileşenleri:
###### 1. Model:
+ Veritabanı ve veri işlemleriyle ilgilenen kısımdır.
+ Uygulamadaki veri yapısını tanımlar ve veritabanına veri yazma, okuma, güncelleme gibi işlemleri içerir.
+ Python'da bu yapı genellikle ORM (Object-Relational Mapping) aracılığıyla oluşturulur. Django’da `models.py` dosyasında model sınıfları tanımlanır.
###### 2.View:
+ Kullanıcıya gösterilecek arayüzleri, yani görünümü sağlar.
+ Kullanıcıdan gelen istekleri alır, modelden verileri alır ve uygun bir şekilde kullanıcıya sunar.
###### 3.Controller:
+ Model ile View arasında bir köprü görevi görür, iş mantığını yönetir.
+ Gelen kullanıcı isteklerini alır, uygun model ve view bileşenleri arasında veri alışverişini sağlar.
+ Django’da `urls.py` dosyasındaki URL yönlendirmeleri, Controller gibi çalışır ve belirli bir isteği ilgili View’a yönlendirir.
##### Django'da MVC(MVT):
+ Django, klasik MVC yapısını biraz farklı bir yapıda uygular ve buna **MVT (Model-View-Template)** adını verir:
1. **Model:** Veritabanı işlemlerini ve veri yapısını yönetir.
2. **View:** İş mantığını içerir ve kullanıcının isteğine uygun verileri hazırlar.
3. **Template:** Verilerin kullanıcıya nasıl sunulacağını belirler. HTML dosyaları, Django’nun Template diliyle işlenir ve View’dan alınan verilerle birleşerek kullanıcıya sunulur.


> [!IMPORTANT]
>  + **MVT**         <=====>  **MVC**
>  + Model      <=====> Model
>  + Template  <=====> View
>  + View         <=====> Controller

#### Modülleri Oluşturma:

## Kaynak:
1. [Python Django 5.0 Full Course - Beginner to Pro (2024)](https://www.youtube.com/watch?v=hw3Cttc9qZQ)
2. 