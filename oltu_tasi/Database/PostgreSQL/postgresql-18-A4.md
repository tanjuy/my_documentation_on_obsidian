# Önsöz

Bu kitap, PostgreSQL'in resmi belgesidir. PostgreSQL yazılımının geliştirilmesiyle eş zamanlı olarak PostgreSQL geliştiricileri ve diğer gönüllüler tarafından kaleme alınmıştır. PostgreSQL'in mevcut sürümünün resmi olarak desteklediği tüm işlevselliği açıklamaktadır.

PostgreSQL hakkındaki bu büyük miktardaki bilginin yönetilebilir olmasını sağlamak adına, bu kitap birkaç bölüme ayrılmıştır. Her bir bölüm, farklı bir kullanıcı kitlesini veya PostgreSQL deneyimlerinin farklı aşamalarındaki kullanıcıları hedeflemektedir:

+ **Bölüm I**, yeni kullanıcılar için resmi olmayan (gayriresmî) bir giriş niteliğindedir.
+ **Bölüm II**, veri tipleri ve fonksiyonların yanı sıra kullanıcı seviyesindeki performans ayarlamalarını da içeren SQL sorgu dili ortamını belgelemektedir. Her PostgreSQL kullanıcısının bu bölümü okuması gerekir.
+ **Bölüm III**, sunucunun kurulumunu ve yönetimini açıklar. İster kişisel kullanım için ister başkaları için olsun, bir PostgreSQL sunucusu çalıştıran herkes bu bölümü okumalıdır.
+ **Bölüm IV**, PostgreSQL istemci programlarına yönelik programlama arayüzlerini açıklar.(Bir uygulama yazdığınızda (örneğin Python, Java, C ile), o uygulamanın PostgreSQL ile nasıl "konuşacağını" — bağlantı kurma, sorgu gönderme, sonuç alma gibi işlemleri — anlatan programlama arayüzleri (API'ler, kütüphaneler, sürücüler) Bölüm IV'te açıklanmaktadır.)
+ **Bölüm V**, sunucunun **genişletilebilirlik** özellikleri hakkında ileri düzey kullanıcılara yönelik bilgiler içermektedir. Konular arasında kullanıcı tanımlı veri türleri ve fonksiyonlar yer almaktadır.(**PostgreSQL'i özelleştirmek isteyen ileri düzey kullanıcılara** yönelik bir bölümü tanıtıyor.)
	- **"Genişletilebilirlik"** şu anlama geliyor: PostgreSQL, varsayılan olarak gelen özelliklerle sınırlı kalmak zorunda değilsiniz; sisteme kendi eklemelerinizi yapabilirsiniz. Örneğin:
		- **Kullanıcı tanımlı veri türleri** → PostgreSQL'in sunduğu `integer`, `text` gibi standart türlerin yanı sıra kendi veri türünüzü oluşturabilirsiniz. Mesela "coğrafi koordinat" veya "para birimi" gibi özel bir tür tanımlayabilirsiniz.
		- **Kullanıcı tanımlı işlevler** → Kendi fonksiyonlarınızı yazıp SQL sorgularında kullanabilirsiniz.
+ **Bölüm VI**, SQL komutları ile istemci ve sunucu programları hakkında **başvuru bilgileri** içermektedir. Bu bölüm, komutlara veya programlara göre sıralanmış **yapılandırılmış** bilgilerle diğer bölümleri desteklemektedir.
	- **"Başvuru bilgileri"** → Bir şeyi öğrenmek için değil, **ihtiyaç duyduğunuzda bakıp hızlıca bilgi almak** için kullanılan bölüm. Tıpkı bir sözlük gibi — baştan sona okunmaz, gerektiğinde açılır.
	- **"Komut veya programa göre sıralanmış"** → Bilgiler alfabetik ya da kategorik olarak düzenlenmiştir. Örneğin `SELECT` komutunu ya da `psql` programını aradığınızda doğrudan o maddeye gidip tüm ayrıntılarını bulabilirsiniz.
	- **"Diğer bölümleri destekler"** → Diğer bölümlerde bir kavram veya komut geçtiğinde, ayrıntılı teknik bilgi için Bölüm VI'ya yönlendirilirsiniz. Yani bu bölüm kitabın **arka planındaki teknik zemin** gibi çalışır.
	- Özetle: Bölüm VI, kitabın geri kalanını okurken ya da PostgreSQL kullanırken **"bu komut tam olarak ne yapar?"** diye sorduğunuzda başvuracağınız yapılandırılmış bir referans bölümüdür.
+ **Bölüm VII**, PostgreSQL geliştiricileri için yararlı olabilecek çeşitli bilgiler içermektedir.

> [!TIP]
> #### yapılandırılmış(structured)
> + Burada "yapılandırılmış" kelimesi **"belirli bir düzene göre organize edilmiş, sistematik biçimde düzenlenmiş"** anlamında kullanılmıştır.
> + Yani bilgilerin rastgele değil, **önceden belirlenmiş bir iskelet/şema dahilinde** sunulduğunu ifade ediyor. Her komut veya program için aynı başlıklar altında aynı tür bilgiler veriliyor — örneğin: açıklama, sözdizimi, parametreler, örnekler gibi. Böylece okuyucu nerede ne bulacağını önceden biliyor.


https://www.postgresql.org/files/documentation/pdf/18/postgresql-18-A4.pdf