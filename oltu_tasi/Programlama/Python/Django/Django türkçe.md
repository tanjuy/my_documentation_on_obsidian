
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