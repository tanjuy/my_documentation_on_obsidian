---
tags:
  - git
---
**Tanım :** Git, küçükten çok büyük projelere kadar her şeyi hızlı ve verimli bir şekilde ele almak için tasarlanmış, *ücretsiz ve açık kaynaklı, dağıtılmış bir sürüm kontrol* sistemidir.

### Git Kurulumu
##### Linux
###### Dabian Temeli Dağıtımlar:
```shell
$ sudo apt install git
```
###### Windows

### Git Başlatma
###### Proje Klasörü Oluştuma
```shell
$ mkdir my_project
$ cd my_project
```

###### Git Deposu Başlatın
```shell
$ git init
```
> **Explanation:**
> Komut başlattığımızda `.git` adında gizli bir dosya oluşacaktır. linux de `ls -al` komut ile görebiliriz. 
###### İlk Ayarlamalar
```shell
$ git config --global user.name "your name"
$ git config --global user.email "youremail@gmail.com"
```
> **Explanation:**
> Bir Git deposu başlattıktan sonra, kullanıcının Git yapılandırma ayarlarını yapması gerekebilir. Bu, genellikle kullanıcı adı ve e-posta adresini ayarlamayı içerir, çünkü bu bilgiler *Git commit'lerinde kullanılır.*
> Bu komutlar, Git yapılandırma dosyasına (genellikle `~/.gitconfig`) bu bilgileri ekler ve tüm projeler için geçerli olur.

```shell
$ git config --local user.name "proje name"
$ git config --local user.email "proje@gmail.com"
```
> **Explanation:**
> Ancak, belirli bir proje için farklı bilgiler ayarlamak istiyorsanız, bu ayarları yerel (local) olarak yapabilirsiniz


### Git Yapılandırılması(config)

##### Git config

> [!TIP] İpucu:
> Git yapılandırma ayarları belirli bir öncelik sırasına sahiptir:
> 1. **Yerel (Local) Düzey**: En yüksek önceliğe sahiptir ve diğer tüm düzeydeki ayarların üzerine yazar.
> 2. **Kullanıcı (Global) Düzey**: Kullanıcı düzeyindeki ayarlar, sistem düzeyindeki ayarların üzerine yazar.
> 3. **Sistem (System) Düzey**: En düşük önceliğe sahiptir ve tüm kullanıcılar için geçerlidir.


###### Örnek 1:  --list  
```shell
$ git config --list
```
>**Explanation:**
>+ `git config --list` komutu, Git'in yapılandırma ayarlarını listelemek için kullanılır. Bu komut çalıştırıldığında, Git'in hem yerel (proje bazlı), hem global (kullanıcı bazlı), hem de sistem (tüm kullanıcılar için geçerli) yapılandırma ayarlarını gösterir.(chatgpt)
>+ Yapılandırma dosyasıdaki tüm değişken setlerini listeler ve onların değerleri ile birlikte.
>+ Bu komut aşağıda verilenleri komutların çıktısın birleşimi:
>	+ `git config --global --list`
>	+ `git config --system --list`
>	+ `git config --local --list`



###### Örnek 2:  --global
```shell
$ git config --global user.name "username"
$ git config --global user.email "username@gmail.com"
```
> **Explanation:**
> Kullanıcının ev dizininde geçerli olan ayarlar. Ayarlar `~/.gitconfig` veya `~/.config/git/config` dosyasında saklanır.
> Yukarıda girilen değerleri listelemek için: `$ git config --global --list`

###### Örnek3:  --local
```bash
$ git config --local user.name "username"
$ git config --local user.name "username@gmail.com"
```
> **Explanation:**
> Bu işlemi yapabilmemiz için `git init` ile oluşturduğumuz dizinde bulunmamız gerekir.
> `--local` parametresini yazmasak da varsayılan parametredir.
#### Git'in durum ve Geçmişi bakma

##### Git status:
```shell
$ git status
```
> **Explanation:**
> `git status` komutu, bir Git deposunun mevcut durumunu kontrol etmek için kullanılır.
> 1. Şu anda hangi dalda (branch) çalıştığınızı gösterir.
> 2. **Untracked files (İzlenmeyen Dosyalar)**: Git tarafından henüz izlenmeyen dosyaları listeler. Bu dosyalar Git deposuna henüz eklenmemiştir. Bu dosyaları eklemek için `git add <dosya-adı>` komutunu kullanabilirsiniz.

> [!WARNING] Uyarı:
> Eğer boş dosya oluştursanız ve `git status` yaparsanız, herhangi bir değişiklik olmayacaktır. Çünkü; Varsayılan olarak git boş bir dizini kopyalamaz veya size onu sürüm kontrolüne ekleme fırsatı vermez.
##### Git diff:
```shell
$ git diff site.yaml
```

### Git Yapısı ve Çalışması

> [!INFO]
> *Git yapısı* : Local(Yerel Makine) ve  Remote(Uzak Makine) temelde iki yapıdan oluşur.
>  *Local (Yerel Makine)* : 
>  Working Directory  **<--------->** Staging Area **<---------------->**  Local Repo
> *Remote(Uzak Makine)* :
>  Github veya Gitlab
##### Git add:
```shell
$ git add nginx.conf
```
> **Explanation:**
> Working Directoy(Çalışma Dizini) **------>**  Stageing Area(Geçiş Bölgesi) aktarır.
> `git add` komutunu kullanarak belirli dosyaları veya tüm değişiklikleri bu alana ekleyebilirsiniz. Bu, yapılacak olan commit işleminin kapsamını belirlemenizi sağlar.
> Eğer `nginx.conf` dosyasını *Staging Area* eklediyseniz, bu dosya *"Changes to be committed" (commit edilmeye hazır değişiklikler)* altında **listelenecektir**.

##### Git restore:
```shell
$ git restore --staged nginx.conf
```
> **Explanation:**
> Working Directoy(Çalışma Dizini) **<------**  Stageing Area(Geçiş Bölgesi) geri aktarır.
> Dosya, stage alanından çıkarıldığında, `git status` komutunu çalıştırarak bu değişiklikleri görebilirsiniz.
##### Git commit:
```shell
$ git commit -m "nginx.conf dosyasını eklendi veya güncellendi"
```
> **Explanation:**
> Staging Area(Çalışma Dizini) ----------------> Local Repo(Yerel Depo) aktarır.
> **Değişiklikleri Kalıcı Olarak Kaydetmek**: Sahneleme alanına eklenmiş (staged) dosyalar, `git commit` komutuyla kalıcı olarak depoya kaydedilir.