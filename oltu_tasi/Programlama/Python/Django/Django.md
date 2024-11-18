
> [!CAUTION]
> + Burada yapılan tüm işlemler `Ubuntu 22.04` üzerinde gerçekleştirilmektedir.


> [!IMPORTANT]
> + Django, **hızlı geliştirmeyi** ve **temiz**, **pragmatik tasarımı** teşvik eden üst düzey bir Python web *framework*'üdür


> [!NOTE]
> + **Web framework nedir?**
> + Web framework, web uygulamaları ve web siteleri geliştirmek için kullanılan yazılım altyapılarıdır.
> + Web framework'leri, temel yapı taşlarını ve çeşitli araçları sağlayarak geliştiricilerin projeleri daha hızlı ve verimli bir şekilde oluşturmasına yardımcı olur.
> + Bu framework'ler, birçok yaygın işlevi ve bileşeni standartlaştırarak geliştiricilerin tekrarlayan kod yazmasını azaltır ve güvenli, sürdürülebilir, ölçeklenebilir web uygulamaları oluşturmayı kolaylaştırır.

#### Django nedir? 

+ Django, **battaries included** felsefesini takip etmektedir.
+ Django’nun "batteries included" (pil dahil) felsefesi, Django framework'ünün, bir web uygulaması geliştirmek için gerekli olan temel araçların ve özelliklerin çoğunu kendi bünyesinde sunması anlamına gelir
+ Django, geliştiricilerin ek eklenti veya üçüncü taraf modüllere ihtiyaç duymadan hızlı ve eksiksiz projeler oluşturmasını sağlamak amacıyla kapsamlı bir standart kütüphane içerir.
+ **Kimler Django kullanıyor** soruna cevap olarak; Youtube, Spotify, Instagram ve Mozilla

#### Django Yükleme:

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
#### Bir Proje Oluşturma:
```shell
$(.venv) django-admin startproject blog
```
> **Explanation:**
> + *Django'da yeni bir proje başlatmak için kullanılır.* Bu komut, Django'nun temel yapılarını içeren bir klasör yapısı oluşturur.
> + Özellikle, `blog` adında yeni bir proje klasörü oluşturur ve içine aşağıdaki dosya ve klasörleri yerleştirir:
> 1. **manager.py:** Proje yönetim komutlarını çalıştırmak için kullanılan bir betiktir. Bu komutla sunucuyu başlatabilir, veritabanı işlemleri yapabilir ve diğer Django komutlarını çalıştırabilirsiniz.
> 2. **myblog** (proje ana dizini):
> 	+ `__init__.py` : Python'a bu dizinin bir Python paketi olarak değerlendirilmesi gerektiğini söyleyen boş bir dosya.
> 	+ `settings.py`: Projenin tüm ayarlarını içerir (veritabanı ayarları, uygulama yapılandırmaları, dil seçenekleri vb.).
> 	+ `urls.py`: URL yönlendirmeleri için kullanılan ana dosyadır.
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
#### Geliştirme Sunucusu:
```shell
$ python3 manage.py runserver
```
> **Explanation:**
> + Yukarıdaki komut çalıştırmak için `cd myblog` komutu ile `myblog` dizinine giriş yapmamız gerekmektedir. Çünkü `manage.py` bu dizin içerisindedir.

#### blog app Oluşturma:
```shell
$ python3 manage.py startapp blog
```
> **Explanation:**
> + 

> [!NOTE] Title
> Contents
##### MVC Yapısı:
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
