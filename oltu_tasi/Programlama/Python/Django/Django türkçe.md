
> [!NOTE]
> Django'un [Resmi Site](https://docs.djangoproject.com/en/5.1/intro/tutorial01/)sinden Türkçeye  çevrilmiştir.

## İlk Django uygulamanızı yazma, 1. bölüm:
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
+ Tamamen Python ile yazılmış hafif bir web sunucusu olan Django geliştirme sunucusunu başlattınız.