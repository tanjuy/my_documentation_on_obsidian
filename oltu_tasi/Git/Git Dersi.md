---
tags:
  - git
---
### Git Nedir?
* Git, küçükten çok büyük projelere kadar her şeyi hızlı ve verimli bir şekilde ele almak için tasarlanmış, *ücretsiz ve açık kaynaklı, dağıtılmış bir sürüm kontrol* sistemidir.
* En kısa tanımı ile bir *versiyon kontrol sistemi*dir.

## Git Kurulumu
##### Linux
###### Dabian Temeli Dağıtımlar:
```shell
$ sudo apt install git
```
###### Windows
```powershell
PS C:\Users\tanju> winget install --id Git.Git -e --source winget
```

**Mac**
```shell
(base) ottoman@MacBook-Pro ~ % brew install git
```
## Git Başlatma (Quick Start)
##### Proje Klasörü Oluştuma
```shell
$ mkdir my_project
$ cd my_project
```

#### İlk Ayarlamalar
```shell
$ git config --global user.name "your name"
$ git config --global user.email "youremail@gmail.com"
```
> **Explanation:**
>*  Bir Git deposu başlattıktan sonra, kullanıcının Git yapılandırma ayarlarını yapması gerekebilir. Bu, genellikle kullanıcı adı ve e-posta adresini ayarlamayı içerir, çünkü bu bilgiler *Git commit'lerinde kullanılır.*
> * Bu komutlar, Git yapılandırma dosyasına (genellikle `~/.gitconfig`) bu bilgileri ekler ve tüm projeler için geçerli olur.

```shell
$ git config --local user.name "proje name"
$ git config --local user.email "proje@gmail.com"
```
> **Explanation:**
> Ancak, belirli bir proje için farklı bilgiler ayarlamak istiyorsanız, bu ayarları *yerel (local)* olarak yapabilirsiniz
#### Git Deposu Başlatın
###### Git durum kontrolü:
```shell
$ git status
```
> **Explanation:**
> + git repo'un kurulu olup olmadığına bakılabilir. 
> + Eğer git repo kurulu değil ise `fatal: not a git repository (or any of the parent directories): .git` hata verecektir.
> + Eğer üst üste repo kurulumu yaparsak(`git init`) hatalar meyil verebilir. `git status` komut ile repo'un kurulu olup olmadığını kontrol edebiliyoruz.

```bash
$ echo "# git_test" >> README.md
```
> **Explanation:**
> + Projenin kök dizininde yer alan ve genellikle proje hakkında önemli bilgileri içeren bir dosyadır.
> + Bu dosya, özellikle proje depolarında ziyaretçilere ilk gösterilen belge olup, projenin amacı, nasıl çalıştırılacağı, kurulum talimatları, katkıda bulunma rehberleri gibi bilgileri sunar.

###### Git yerel depoyu başlatma:
```bash
$ git init
```
> **Explanation:**
> Komut başlattığımızda `.git` adında gizli bir dosya oluşacaktır. linux de `ls -al` komut ile görebiliriz. 

###### Dosyayı indeksleme:
```bash
$ git add README.md
```
> **Explanation:** 
> + Her git projenin bir README.md olması gerekir. 
> + [[Git Dersi#Git add|Git add]] bakınız.

> [!TIP]
> + Her `git add` komutu kullanımında `git status` komutunu kullanarak teyit ediniz.

###### Dosyayı yerel depoya koyma:
```bash
$ git commit -m "first commit"
```
> **Explanation:**
> + Bu kayıtlar, bir projenin geçmişini izlemeyi, değişiklikleri yönetmeyi ve gerektiğinde önceki sürümlere geri dönmeyi kolaylaştırır.
> + [[Git Dersi#Git commit|Git commit]] bakınız.

> [!TIP] 
> Git kurulumu ve git depo ile bağlantısı sağlandığında en çok kullanılacak 2 komut:
> 1. `git add <file name>`
> 2. ``git commit -m "konu ile ilgi kısa bir açıklama"`

###### Commit'leri listeleme:
```shell
$ git log
```
> **Explanation:**
> + Bulunduğumuz branch de tüm commit'leri ekrana basar.
> + commit içerisinde commit hash, yazarı(Author), tarih(Date) ve mesajı bulunmaktadır.

###### Git'in izlemesinden çıkarma:
```shell
$ touch .gitignore
```
> **Explanation:**
> + `.gitignore` dosyasın içerisine eklediğimiz dosyalar veya klasörler git tarafından izlenmeyecektir.
> + Daha fazla bilgi için [[Git Dersi#Gitignore Dosyası|Gitignore Dosyası]] bakınız.
###### Branch adını değiştirme:
```bash
$ git branch -M main
```
> **Explanation:**
> + Git deposundaki mevcut dalı (branch) **zorunlu (force) olarak yeniden adlandırmak** için kullanılır ve yeni dalın adı **`main`** olur.
> + **`git branch -M`**: Mevcut dalı zorunlu olarak yeniden adlandırır. Buradaki `-M`, **`--move --force`** anlamına gelir, yani yeni dal adıyla aynı ada sahip bir başka dal olsa bile mevcut dal bu isimle değiştirilir.
###### SSH ile bağlanma:
```bash
$ git remote add origin git@github.com:tanjuy/git_test.git
```
> **Explanation:**

```bash
$ git push -u origin main
```
> **Explanation:**
> `-u` parametrenin uzun yazılışı; `--set-upstream`
> + Bu bayrak, yerel dalı bir **upstream dalıyla** ilişkilendirir. Upstream dal, yerel dalın hangi uzak depodaki dalı takip edeceğini belirler.
> + bir dalın uzak depodaki karşılığıyla (upstream branch) sürekli bir ilişki kurmaktır, böylece gelecekte `git push` veya `git pull` komutlarını çalıştırırken her seferinde dal adı belirtmek zorunda kalmazsınız.

###### HTTPS ile bağlama:
```shell
$ git remote add origin https://github.com/tanjuy/git_test.git
```


```shell
git remote add origin git@github.com:tanjuy/git_test.git
git branch -M main
git push -u origin main
```

```shell
$ git add <file_name>
```

```bash
$ git commit -m "message"
```

#### Branch Oluşturma:

> [!TIP]
> +  Genellikle yazılım da özellik için yeni bir branch açıldığında isimlendirme `feat-featureName`  şeklinde olur
> + `featureName` branch için açılacak özellik için verilecek isimdir. Örneğin; `feat-login` veya feat-css gibi.


```shell
$ git branch dev
```
> **Explanation:**
> - `dev` adında yeni bir branch oluşturur.
> - Daha fazla detay için [[Git Dersi#Git branch|Git branch]] başlığına bakınız.

```shell
$ git switch -c prod
```
> **Explanation:**
> - `prod` adında yeni bir branch oluşturur ve üstelik bu branch'e geçiş yapar.
> - Daha fazla detay için [[Git Dersi#Git switch|Git switch]] başlığına bakınız.

```shell
$ git branch
```
> **Explanation:**
> - Oluşturmuş olduğumuz branch'leri görmek için veya listelemek için bu komut kullanılabilir.
> - `-a` parametresi kullanılırsa *hem uzaktaki hemde yereldeki branch'leri listeler.*

#### Branch'ler Arasında Geçiş:
```shell
$ git checkout dev
```
> **Explanation:**
> Eğer `main` branch de iseniz, bu komut ile dev branch'ine geçersiniz.

```shell
$ git switch dev
```
> **Explanation:**
> - Eğer `main` branch de iseniz, bu komut ile dev branch'ine geçersiniz.
> - `switch` git'e yeni gelen bir komuttur bunun nedeni `checkout` bir fazla görevi var ilken `switch` tek görevi branch'ler arasında geçiştir.


> [!CAUTOIN]
> + Eğer **Working Directory** alanında oluşturulmuş bir dosya var iken `git switch dev` komut ile başka branch'e geçiş yapmaya çalışırsak hata verecektir.
> + Eğer oluşturmuş olduğumuz dosyayı **stage(index) area** eklersek ve `git switch dev` komut ile başka branch'e geçiş yaparsak, geçiş yaptığımız branch'e oluşturduğumuz dosyada gelecektir.

#### Branch'leri Birleştirme:
```shell
$ git merge dev 
```
> **Explanation:**
> - Eğer `git branch` komut verirsek ve komut bize *main* branch'ini verirse yukarıda komut uygulayabiliriz.
> - Bu komut `main` branch'i ile `dev` branch'ini birleştirir.


> [!CAUTION]
> Eğer aşağıdaki gibi bir hata alıyorsanız:
> ```
>  Auto-merging test.txt                                                                                                                        CONFLICT (content): Merge conflict in test.txt                                                                                  Automatic merge failed; fix conflicts and then commit the result.
> ```
> Birleştirme aşamasında branch'ler arasında bir fark var demektir.

##### Fast-forward:

> [!NOTE]
> + **main branch:**  commit_1m----commit_2m-----------------------------------commit_3m----
> + **fast branch:**  -----------------------------------commit_1f-----commit_2f--------------------
> + **Nihai Sonuc:** commit_1m----commit_2m-----commit_3m----commit_1f----commit_2f---
> + main branch'deki dosyalar: html ve css  --- fast branch'deki dosyalar: javascript
> + Eğer fark etiyseniz fast branch'inde hem dosya farklı hem de commit aralığı farklı yani main branch'inde yapılmayan commit fast branch'inde yapılmıştır.

###### Örnek: Fast-forward Çıktısına
```shell
╭─ottoman@ottoman ~/gitDerleri ‹main›
╰─$ git merge fastForward
Updating 8de5f50..cca1102
Fast-forward
 fast.txt | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 fast.txt
```
> **Explanation:**
> + Dikkat ederseniz git bize çıktısında bu işlemin bir *Fast-forward* olduğunu sölüyor.

##### Merge Conflict:

> [!NOTE]
> + Git'te **merge conflict** (birleştirme çakışması), iki dalı birleştirirken Git'in otomatik olarak birleştiremeyeceği çelişkili değişiklikler olduğunda ortaya çıkar.
> + Yani, iki dalda aynı dosyanın aynı bölümleri üzerinde farklı değişiklikler yapılmışsa Git bu durumu çözemez ve birleştirme işlemi kullanıcı müdahalesi gerektirir.

###### Örnek 1: main branch ve feat-greeting branch
**main branch ve selamlama.py dosyası**
```python
#!/usr/bin/python3

print("Hello, world")
```

**feat-greeting branch ve selamlama.py dosyası**
```python
#!/usr/bin/python3

print("Merhaba, Git")
```
> **Explanation:**
> + Eğer bu 2 branch'i birleştirdiğimizde, git conflict hatası ekrana basıyor.
> 	 ```
> 	 Auto-merging test.txt
 >	CONFLICT (content): Merge conflict in test.txt
 >	Automatic merge failed; fix conflicts and then commit the result.
> 	 ```
> + Her iki branch de aynı dosya mevcut ve aynı dosya üzerinde değişiklik yapılıyor. Bundan dolayı git de kafa karışıklığı oluşturuyor ve bu işi otomatik gerçekleşemeyeceğini bunun manuel yapılmasını söylüyor.
> + Git'in kendi mesajında da söylediği gibi;
> 	1. Dosyayı kendi talebinize uygun olarak düzenliğin
> 	2. `git add fileName` komut ile index(stage) area gönderin.
> 	3. `git commit -m "short message` komut ile commit ediniz.

#### Takım Çalışması (contributor):
###### Temel Kullanımı:
```shell
git fetch
```
> **Explanation:**
>  + Eğer bir projede birden fazla gelişici var ise ve bu geliştiriciler belli aralıklar ile `git push` ile `repo`'ya kod gönderiyor ise, bundan dolayı çakışmalar olacaktır.
>  + `git fetch` ile `repo`'dan kodlar çekilir ve  daha sonrasında `git merge` ile birleştirilir. Böylelikle çakışmaları manüel olarak düzenleyebiliriz.


> [!CAUTION]
> + **`git fetch`**: Sadece uzak depodaki değişiklikleri indirir, ancak mevcut çalışma dalınıza bu değişiklikleri birleştirmez.
> + **`git pull`**: Hem uzak depodaki değişiklikleri indirir hem de bu değişiklikleri yerel dalınıza birleştirir (fetch + merge yapar).

## Yerel Depoda İşlemler(Local Repository)

#### Gitignore Dosyası
```shell
$ touch .gitignore
```
>**Explanation:**
>Linux komut olan `touch` ile gitingore dosyası oluşturuyoruz. Burada dikkat edilmesi gereken bu dosyanın gizli dosya olduğunu, çünkü bu dosya `notka(.)` ile başlamaktadır.

```vim
# Düzenleyici: vim .gitignore
log.txt         
*.swg
directory/
```
>**Explanation:**
> - `vim .gitignore` komut ile dosyayı açıyoruz:
> - log.txt dosyasını git artık işlemler sokmuyor.
> - `*.swg` ile  swg uzantılı dosyaları git işleme alamayacaktır.  
> - `directory` adlı dizini ve içerisindeki dosyaları kapsayacaktır. 


> [!TIP]
> + İnternet de `gitignore template <progralama adı>` yazıp arattığımızda, o programlamaya uygun hazır gitignore dosyaları listelenecektir. 



> [!CAUTION]
> 1. Eğer `gitignore` dosyasını daha sonra oluşturduysanız, `.gitingore` dosyasında önce oluşturulmuş dosyalar git tarafında izlenmesini göremez. 
> 2. `.gitignore` dosyasından önce oluşturulmuş dosyaları 
> 	+ git'in takibinde çıkarmak için: `git rm --cached <file_name>` veya 
> 	+ tüm dosyaları çıkarmak için: `git rm -r --cached` .

#### Git HEAD:
* Git'te **HEAD**, çalışma dizininde hangi commit'in aktif olduğunu belirten bir referanstır.
* Yani, HEAD, *Git'te şu anda hangi dalda çalıştığınızı ve bu dalın en son commit'ini işaret eder.* Genellikle bir dalın en son commit'ini gösterir
* **Normal durumda**: HEAD genellikle bir dalı işaret eder, yani `HEAD` bir dal adıyla eşleştirilir, ve o dalın en son commit'ini gösterir.
* **Detached HEAD (kopuk HEAD) durumu**: Eğer doğrudan bir commit'e (hash'e) checkout yaparsanız, HEAD artık bir dala değil, doğrudan o commit'e işaret eder. - Bu durumda HEAD kopuktur ve bu şekilde yapılan değişiklikler bir dala bağlı olmadığı için dikkatli olunması gerekir.

#### Git checkout:
+ Git'te **branch**, **commit**'ler, dosyalar veya dizinler arasında geçiş yapmanızı sağlayan bir komuttur.
+ Farklı bir dal veya commit'e geçmek, belirli bir dosyanın daha eski bir versiyonuna dönmek veya yeni bir dal oluşturmak gibi işlemler için kullanılır.

###### 1. Branch Değiştirme:
```shell
$ git checkout dev
```
>**Explanation:**
>+ Bulunduğu branch'den `dev` branch'ine geçiş yapar.


> [!WARNING]
> + `git checkout`'un `branch` değiştirme işlevi, Git 2.23 sürümünden itibaren `git switch` komutuyla değiştirilmiştir.
> + Ancak, `checkout` hâlâ kullanılabilir.

###### 2. Yeni Branch Oluşturma ve Ona(`-b`):
```shell
$ git checkout -b prod
```
>**Explanation:**
>+ Yeni bir dal oluşturup aynı anda o dala geçmek için `-b` seçeneğiyle `git checkout` kullanılabilir.
>+ **Alternatif:** `git switch -c prod`

###### 3. Belirli Bir Commit veya Tag'e Geçme:
```shell
$ git checkout c107365
```
> **Explanation:**
> + Belirli bir commit'in içeriklerine bakmak veya o commit'e geçiş yapmak için commit hash'i ile `checkout` yapılabilir.
> + `c107365` hash'ine sahip commit'e geçiş yapar.
> + Ancak bu, **"detached HEAD"** durumuna yol açar; yani şu an aktif olan HEAD bir *branch* üzerinde değil, belirli bir *commit* üzerindedir.
#### Git diff:


#### Git rm
###### Örnek 1: Temel Kullanımı:
```shell
$ git rm --cached access.log
```
>**Explanation:**
> + `access.log` dosyası `.gitignore` dosyasından daha önce oluşturulmuş ve git tarafında `access.log` izlenmektedir. Bu komut ile `access.log` dosyasını izlenmesini durduruyoruz.
> + Bu komut, `access.log` dosyasını git deposundan çıkarır ancak dosya çalışma dizininde kalmaya devam eder.

###### Örnek 2: -r parametresi
```shell
$ git rm -r --cached directoryName
```
>**Explanation:**
> + Eğer sadece bir dosya yerine bir dizin silmek istiyorsanız, **`-r`** parametresini eklemeniz gerekir. Aksi takdirde, `git rm` sadece tekil dosyalar üzerinde çalışır.
> + `git rm --help` ile -r parametresi ne görevine bakabilirsiniz.


#### Git config

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

##### Git config Özelleştirme:
**İngilizce:** [Basic Client Configuration](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)

###### 1. branch.`<branch-name>`.merge:
```shell
$ git config branch.main.merge "main"
```
> **Explanation:**
> + Git'in, belirli bir dalın hangi uzaktaki dal (remote branch) ile birleştirileceğini tanımlar.
> + Örneğin, `branch.main.merge` ayarı, `main` dalının hangi uzaktaki dal ile birleştirileceğini tanımlar.
> + Bu ayar, genellikle `git pull` komutunun nasıl çalışacağını belirlemek için kullanılır.(**Kullanım amacı**)
> + Eğer `branch.main.merge` ayarı belirli bir uzaktaki dalı işaret ediyorsa, `git pull`, `git push` ve `git fetch` komutu çalıştırıldığında, `main` dalı otomatik olarak bu ayar ile tanımlanan uzak daldan değişiklikleri birleştirir.(**Kullanım amacı**)

```conf
[branch "main"]
    remote = origin
    merge = refs/heads/main
```
> **Explanation:**
> + `.git/config` dosyasındaki bir yapılandırma örneği verilmiştir.
###### 1.  core.editor (set)
```bash
$ git config --global core.editor "vim"
```
> **Explanation:**
> *  Eğer `git` düzenleyici(editor) kullanması gerektiğinde burada ayarlanmış olan `vim` ile açılacaktır.
> * Daha fazla bilgi için [Setup and Config](https://git-scm.com/book/en/v2/Appendix-C%3A-Git-Commands-Setup-and-Config) bakınız.

###### 1.1. core.editor (get)
```shell
$ git config --global core.editor
```
> **Explanation:**
> * `core.editor` ayarlanmışsa ekran değerini basar.

###### 2. remote.origin.url
```shell
$ git config --local remote.origin.url "ssh url veya https url"
```
> **Explanation:**
> + Git repo'unuza giderek `<> Code` yeşil butonu tıklayarak, ssh url veya https url kopya alarak yeniden URL düzenleyebilirsiniz. 

#### Git status:
###### Örnek 1: Temel Kullanımı
```shell
$ git status
```
> **Explanation:**
> 1. `git status` komutu, bir Git deposunun mevcut durumunu kontrol etmek için kullanılır.
> 2. Şu anda hangi dalda (branch) çalıştığınızı gösterir.
> 3. **Untracked files (İzlenmeyen Dosyalar)**: Git tarafından henüz izlenmeyen dosyaları listeler. Bu dosyalar Git deposuna henüz eklenmemiştir. Bu dosyaları eklemek için `git add <dosya-adı>` komutunu kullanabilirsiniz.

###### Örnek 2: -s parametresi
```bash
$ git status -s
```
> **Explanation:**
> * `-s` parametresi durum hakkında kısa bir çıktı verir. short kelimesinin kısatlmasıdır.

> [!WARNING] Uyarı:
> Eğer boş dosya oluştursanız ve `git status` yaparsanız, herhangi bir değişiklik olmayacaktır. Çünkü; Varsayılan olarak git boş bir dizini kopyalamaz veya size onu sürüm kontrolüne ekleme fırsatı vermez.

#### Git branch
###### Örnek 1: Temel Kullanımı
```shell
$ git branch
```
> **Explanation:**
> + Tüm branch'leri listeler ve şu an hangi branch'te olduğunuzu gösterir.
> + Aktif branch, `yıldız (*)` işareti ile belirtilir.

###### Örnek 2: Uzak ve Yerel Branch listeleme
```shell
$ git branch -a
```
> **Explanation:**
> + `-a` parametresi hem yerel (local) hem de uzak (remote) branch'lerin listelenmesini sağlar.
###### Örnek 3: Branch Oluşturma:
```shell
$ git branch prod
```
> **Explanation:**
> + `prod` adında yeni bir branch oluşturacaktır.
> + alternatif olarak: [[Git Dersi#Git switch#Örnek 2: -c parametresi|git switch -c örnek 2]] bakınız.

###### Örnek 4: Branch Silme(local)
```shell
$ git branch -d prod
```
> **Explanation:**
> + Yukarıdaki komut `prod` adındaki branch'i silecektir.
> + Bu işlem yerel depoda gerçekleşecektir ama 
> + eğer uzak depolarda(remote repository) için [[Git Dersi#Uzak Depoda İşlemler(Remote Repository)#Örnek 1 origin de branch silme|Uzak Depoda Branch Silme]] bakınız.

#### Git stash:
+ Git'te **stash**, üzerinde çalıştığınız, henüz commit'lenmemiş değişiklikleri geçici olarak kaydederek (yani "stash"leyerek), çalışma dizininizi temizlemenize ve başka bir dala veya göreve geçiş yapmanıza olanak tanıyan bir özelliktir.
+ Örneğin, bir dosya üzerinde değişiklik yapıyorsunuz ve bu değişiklikleri henüz commit'lemek istemiyorsunuz, ama acilen başka bir dalda çalışmanız gerekiyor.
+ Bu durumda, `stash` komutunu kullanarak geçici olarak bu değişiklikleri saklayabilirsiniz, dal değiştirip gerekli işlemi yaptıktan sonra da bu değişiklikleri geri getirebilirsiniz.
+ `stack` Türkçe karşılığı saklamak, gizlemek anlamındadır.

###### Değişikleri saklamak
```shell
$ git stash
```
> **Explanation:**
> + Üzerinde çalıştığınız değişiklikleri saklar ve çalışma dizinini temizler, yani working directory'i temizler veya saklar.

###### Stash'leri listelemek
```shell
$ git stash list
```
> **Explanation:**
> + Daha önce `stash`lenen değişikliklerin listesini gösterir. Her stash bir isimle (örneğin, `stash@{0}`) etiketlenir.

###### Stash'lenen Değişiklikleri Geri Yüklemek:
```shell
$ git stash apply
```
> **Explanation:**
> + en son `stash`lenen değişiklikleri geri getirir.
> + Ancak, `stash`lenen değişiklikleri listeden silmez, sadece geri yükler.

```shell
$ git stash apply stash@{1}
```
> **Explanation:**
> + Eğer belirli bir stash'i geri yüklemek istiyorsanız, bu şekilde belirtebilirsiniz.
###### Stash'i Geri Yükleyip Listeden Silmek:
```shell
$ git stash pop
```
> **Explanation:**
> + En son yapılan stash'i geri yükler ve aynı zamanda stash listesinden kaldırır.

###### Belirli Bir Stash'i Silmek:
```shell
$ git stash drop stash@{0}
```
> **Explanation:**
> + Belirtilen stash'i listeden siler.

###### Tüm Stash'leri Silmek:
```shell
$ git stash clear
```
> **Explanation:**
> + Tüm stash'leri temizler yani siller.
#### Git log:

> [!TIP] 
> + Git'te **`HEAD`**, şu an **aktif olan branch'te veya commit'te** bulunduğunuz yeri temsil eden bir referanstır.
> + `HEAD`, projenizde hangi branch'te çalıştığınızı ya da belirli bir commit'i işaret eden göstergedir.

###### 1. Temel Kullanımı(local):
```bash
$ git log
```
> **Explanation:**
> 1. Mevcut dalda yapılan tüm commit'leri sıralar
> 2. *Commit hash değeri, Yazar(Author), Tarih(Date), Commit mesajı* ile ekrana basar.

###### 1a. Temel Kullanımı(remote):
```shell
$ git log origin/main
```
> **Explanation:**
> + Uzak daldaki commit'leri görmek için şu komutu kullanabilirsiniz.
> + `origin/main` dalındaki commit'leri listeler. Eğer başka bir dalı incelemek istiyorsanız, dal adını değiştirerek kullanabilirsiniz.
###### 2. --oneline parametresi
```shell
$ git log --oneline
```
> **Explanation:**
> 1. Parametrenin adında anlaşılacağı gibi tek bir satırda(one line) yani daha kısa ile listeler.
> 2. *Kısa Commit hash değeri, Commit mesajı* ile ekrana basar.

###### Örnek 3: --graph parametresi
```shell
$ git log --graph --all 
```
> **Explanation:**
> commit geçmişini dallanmalar ve birleşmelerle birlikte grafiksel olarak gösterir. `--all` seçeneği ise tüm branch'lerdeki commit'leri dahil eder.

###### Örnek 3:  -p parametresi
```bash
$ git log -p -2
```
> **Explanation:**
> + Git'te mevcut dalda yapılan son iki commit'in detaylarını ve bu commit'lerde yapılan değişiklikleri gösterir.
> + hem commit mesajlarını hem de commit'lerdeki *dosya değişikliklerini (patch/diff)* incelemek için kullanılır.

###### Örnek 4: -n parametresi
```shell
$ git log -n 2
```
> **Explanation:**
> Git'te commit geçmişini görüntülerken, sadece belirli bir sayıda commit'i listelemek için kullanılır.

###### Örnek 5: --since parametresi
```shell
$ git log --since=10minutes
```
> **Explanation:**
> 1. 10 dakikadan öncesinden şuana kadar.
> 2. alternatif `since` kullanımı: 
> 	+ `--since=3minutes`  : 3 dakika beri olan tüm commit'ler
> 	+ `--since=3hours` : 3 saatten beri olan tüm commit'ler
> 	+ `--since=3weeks` : 3 haftadan beri olan tüm commit'ler
> 	+ `--since=3days` : 3 günden beri olan tüm commit'ler
> 	+ `--since=3months` : 3 aydan beri olan tüm commit'ler

#### Git show:
###### Örnek 1: 
```bash
$ git show
```
> **Explanation:**
> 1. Son yaptığımız `commit` bize gösterir.
> 2. Git'te bir commit'in detaylarını göstermek için kullanılır. Bu komut, bir commit'in özet bilgilerini ve o commit'te yapılan değişikliklerin ayrıntılarını (diff) görüntüler.

```shell
$ git show <commit-hash>
```
> **Explanation:**
> + Burada `<commit-hash>`, görüntülemek istediğiniz commit'in hash değeri veya referansıdır.
> + Böylelikle istediğimiz `commit` ayrıntılarını inceleyebiliriz.
#### Git diff:
```shell
$ git diff site.yaml
```

#### Git Yapısı ve Çalışması

> [!INFO]
> *Git yapısı* : Local(Yerel Makine) ve  Remote(Uzak Makine) temelde iki yapıdan oluşur.
>  *Local (Yerel Makine)* : 
>  Working Directory  **<--------->** Staging(Index) Area **<---------------->**  Local Repo
> *Remote(Uzak Makine)* :
>  Github veya Gitlab
#### Git add:
###### Örnek 1: Çalışma dizinden geçiş alanına(index)
```shell
$ git add nginx.conf
```
> **Explanation:**
> + Working Directoy(Çalışma Dizini) **------>**  Stageing Area(Geçiş Bölgesi) aktarır.
> + `git add` komutunu kullanarak belirli dosyaları veya tüm değişiklikleri bu alana ekleyebilirsiniz. Bu, yapılacak olan commit işleminin kapsamını belirlemenizi sağlar.
> + Eğer `nginx.conf` dosyasını *Staging Area* eklediyseniz ve `git status` ile baktığımızda, bu dosya *"Changes to be committed" (commit edilmeye hazır değişiklikler)* altında **listelenecektir**.


> [!TIP]
> + Her `git add` komutu kullanımında `git status` komutunu kullanarak teyit ediniz.

###### Örnek 1.1: Tüm dosyaları indeksleme
```shell
$ git add .
```
> **Explanation:**
> Nokta(`.`) karakteri git de tüm dosyaları işaret etmektedir. Tüm dosyaları indekse ekleyecektir.

###### Örnek 1.2: Tüm dosyaları parametre ile indeksleme
```shell
$ git add -A
```
> **Explanation:**
> `-A` parametresi ile tüm dosyaları indeks ekliyoruz.
#### Git restore:
###### Örnek 1:
```shell
$ git restore --staged nginx.conf
```
> **Explanation:**
> 1. Working Directoy(Çalışma Dizini) **<-------**  Stageing Area(Geçiş Bölgesi) geri aktarır.
> 2. Dosya, stage alanından çıkarıldığında, `git status` komutunu çalıştırarak bu değişiklikleri görebilirsiniz.

###### Örnek 2: 
```shell
$ git restore nginx.conf
```
> **Explanation:**
> 1. Working Directoy(Çalışma Dizini) **------->**  Dosyada yazılanları bir geri alır.
> 2. Eğer bu komut kullanırsak çalışma dizinde nginx.conf'daki değişikleri iptal edecektir.
> 3. `git status` komutunu kullandığımızda da yukarıdaki komut önermektedir(DİKKAT).

#### Git checkout
###### Örnek 1: 
```shell
$ git checkout <commit-hash>
```
> **Explanation:**
> 1. Git'te belirli bir commit'e geçmek (checkout yapmak) için kullanılır. Bu komut, depo çalışma dizinini (working directory) o commit'in içeriğine geri döndürür, böylece o commit'in yaptığı değişiklikleri görebilir ve bu durumu inceleyebilirsiniz.
> 2. **Geçmişteki Bir Durumu İnceleme**: Projenizin geçmişindeki bir durumu görmek ve o anda dosyaların nasıl olduğunu incelemek isterseniz, bu komutla ilgili commit'e geçiş yapabilirsiniz.
> 3. **Hata Bulma ve Test Etme**: Projenizdeki bir hatanın hangi commit ile ortaya çıktığını belirlemek veya önceki commit'lerdeki belirli işlevlerin nasıl çalıştığını test etmek için kullanılır.
> 4. **Geçici Çalışma**: Belirli bir commit'e geçip bazı değişiklikler yapmak, ancak bu değişiklikleri kaydetmek istemiyorsanız bu komutu kullanabilirsiniz. Bu, bir tür "sanal zaman makinesi" gibi çalışır, çünkü mevcut durumu kaybetmeden geçmişteki bir anı incelemenize olanak tanır.

###### Örnek 2: Dikkat Edilmesi Gerekenler
```bash
$ git checkout -b yeni_branch_adı <commit-hash>
```
> **Explanation:**
> 1. **Detached HEAD Durumu**: Bir commit'e checkout yaptığınızda "detached HEAD" adı verilen bir duruma girersiniz. Bu, şu anki dalınızın (branch) HEAD'inin herhangi bir dalda değil, direkt olarak bir commit'te olduğu anlamına gelir. Bu durumda yaptığınız değişiklikler, yeni bir dal oluşturmazsanız kalıcı olmaz ve bu commit'in üzerine yeni commit'ler ekleyemezsiniz.
> 2. **Dalı Eski Haline Döndürme**: Eğer commit'lere geri dönüp o commit üzerine yeni bir değişiklik yapmanız gerekiyorsa, bu durumu yönetmek için yeni bir dal oluşturmak iyi bir fikirdir.
> 3. **Bu komut**, eski bir commit'e geçip aynı zamanda yeni bir dal başlatır. Bu sayede mevcut commit'leri koruyarak çalışmaya devam edebilirsiniz. Ayrıca `git switch -c <yeni_branch_adı>` ile de bu işlemi yapabiliriz.

> [!WARNING] 
> `git checkout <commit hash>` komutu, depo çalışma dizinini belirli bir commit'e geri döndürmek için kullanılır. Bu, projenizin önceki durumlarını incelemek, testler yapmak veya hata ayıklamak için kullanışlıdır. Ancak bu işlem sırasında "detached HEAD" durumuna dikkat etmeniz önemlidir, çünkü yaptığınız değişiklikleri kaybetmemek için yeni bir dal oluşturmanız gerekebilir.
#### Git switch:
###### Örnek 1: Basit kullanımı
```shell
$ git switch dev
```
> **Explanation:**
> 1. Git'te dallar arasında geçiş yapmak (checkout yapmak) için kullanılan bir komuttur.

###### Örnek 2: -c parametresi
```shell
$ git switch -c prod
```
> **Explanation:**
> 1. Git'te yeni bir dal (branch) oluşturmak ve bu dala geçiş yapmak (checkout yapmak) için kullanılır.
> 2. **`-c <new-branch-name>`**: Bu seçenek, belirtilen isimde yeni bir dal oluşturur. `-c`, `--create` anlamına gelir ve yeni dal yaratmayı ifade eder.


> [!WARNING]
> + `git switch -c <new-branch-name>` komutu, aslında `git checkout -b <new-branch-name>` komutunun yaptığı işi yapar.
> + Ancak, `git switch` komutu, dallar arasında geçiş yapmak için daha net ve modern bir yol sağlar.
> + `git checkout` komutu, dallar arasında geçiş yapmak, dosyaları geri almak gibi farklı görevler için de kullanıldığı için kafa karıştırıcı olabilir.
> + Bu nedenle, `git switch` ve `git restore` gibi daha spesifik komutlar Git'in yeni sürümlerinde tanıtılmıştır.

#### Git commit:
###### Örnek 1: Yaygın kullanımı
```shell
$ git commit -m "nginx.conf dosyasını eklendi veya güncellendi"
```
> **Explanation:**
> + Staging Area(Çalışma Dizini) **---------------->** Local Repo(Yerel Depo) aktarır.
> + indeksin mevcut içeriğini ve bu içeriğinde ne gibi değişikleri kısaca açıklayan log mesajları oluşturur. *(git commit --help)*
> + **Değişiklikleri Kalıcı Olarak Kaydetmek**: Geçici alana eklenmiş (staged) dosyalar, `git commit` komutuyla kalıcı olarak depoya kaydedilir.

###### Örnek 2:  Editor ile commit
```bash
$ git commit 
```
> **Explanation:**
> - Eğer `-m` parametresini kullanmanda çalıştırsak, git ayarlanmış düzenleyici(editor) açılacaktır.

###### Örnek 3: -am parametresi
```shell
$ git commit -am "short explanation about commit"
```
> **Explanation:**
> 1. `-a` : Daha önce Git tarafından takip edilen (yani, Git'in izlediği) dosyalardaki tüm değişiklikleri otomatik olarak sahneye (stage) ekler. Yeni dosyalar sahneye eklenmez; sadece daha önce commit'lenmiş dosyalardaki değişiklikler eklenir.
> 	- **`-a` parametresi yalnızca takip edilen dosyaları etkiler**: Yani, henüz Git'e eklenmemiş (yeni olan) dosyalar bu komutla sahneye eklenmez. Yeni dosyaları commit'lemek için önce `git add <dosya>` komutunu kullanmanız gerekir.
> 2. `-m "message"`: Commit mesajını doğrudan komut satırında belirtmenizi sağlar.
> 3. Özetlemek gerekirse; hem `git add .` hem de `git commit -m "message"` aynı anda yapar. 


#### Git revert:
###### Örnek 1: Basit Kullanımı
```shell
$ git revert 43bd0f9
```
> **Explanation:**
> - `43bd0f9` git'in commit hash'i ve `git log --oneline` komut ile ekrana basılabilir.
> - Bir commit'i geri almak (tersine çevirmek) için kullanılır.
> - Bu işlem commit'i silmez bunun yerine commit'i tersine çevirir ve yeni commit oluşturur.
> - Böylece proje geçmişi korunmuş olur ve yapılan hatalı bir değişiklik etkili bir şekilde geri alınır.

###### Örnek 2: revert commit'i tekrar revert işlemi
```shell
$ git revert ff0bd9f
```
> **Explanation:**
> + commit hash'i `ff0bd9f` olan ve daha önce revert edilmiş commit'i tekrardan revert işlemi yapıyoruz.
> + Eğer git revert işlemi yapılmış bir commit tekrardan git revert işlemi yaparsak eksi haline geri gelir yani revert türkçe karşılığı tersini almak demek, böylelikle tersin tersi ilk hali olur. 

#### Git reset
**Tanım:** Git'te çalışma dizinini, index'i (staging area) ve commit geçmişini belirli bir commit'e geri almak için kullanılan güçlü bir komuttur. Bu komut, proje geçmişini ve çalışma durumunu geri döndürebilir, yani dosyalarınızı belirli bir commit'teki duruma sıfırlayabilir. 3 farklı modda kullanılabilir:
##### soft modu:
###### Örnek 1: Basit Kullanımı
```shell
$ git reset --soft 487e983fbd6b6c0042f9ec3ff75fc068ac1f2125
```
> **Explanation:**
> - **Commit geçmişi**: Belirtilen commit'e geri döner yani commit geçmişini geriye alır.(+)
> - **Index (Staging Area)**: Etkilenmez, tüm değişiklikler hâlâ sahneye alınmış olarak kalır.(-)
> - **Çalışma dizini**: Dosyalar olduğu gibi kalır.(-)
> - 487e983fbd6b6c0042f9ec3ff75fc068ac1f2125 (commit hash).
##### mixed modu:
###### Örnek 1: Basit Kullanımı:
```shell
$ git reset --mixed 487e983fbd6b6c0042f9ec3ff75fc068ac1f2125
```
> **Explanation:**
> - **Commit geçmişi**: Belirtilen commit'e geri döner yani commit geçmişini geriye alır.(+)
> - **Index (Staging Area)**: staged değişiklikler geri alınır, dosyalar unstaged duruma getirilir.(+)
> - **Çalışma dizini**: Dosyalar olduğu gibi kalır.(-)
##### hard modu:
###### Örnek 1: Basit Kullanımı:
```shell
$ git reset --hard 487e983fbd6b6c0042f9ec3ff75fc068ac1f2125
```
> **Explanation:**
> - **Commit geçmişi**: Belirtilen commit'e geri döner yani commit geçmişini geriye alır.(+)
> - **Index (Staging Area)**: staged değişiklikler geri alınır, dosyalar unstaged duruma getirilir.(+)
> - **Çalışma dizini**: Dosyalar olduğu gibi kalır.(+)
## Uzak Depoda İşlemler(Remote Repository)

##### Origin Nedir?
* Git'te **`origin`**, yerel (local) repository'nizin bağlantılı olduğu **uzaktaki (remote) repository'nin** varsayılan adıdır.
* Git, bir projeyi yerel bilgisayarınıza kopyalarken uzaktaki bir sunucuda veya GitHub, GitLab gibi servislerde barındırılan repository'ye bağlanır.
* Bu uzaktaki repository'ye **remote** denir ve varsayılan ismi **`origin`** olarak atanır.


#### Git fetch:
###### Temel Kullanımı:
```shell
$ git fetch 
```
> **Explanation:**
> + Git'te uzak bir depodaki (`remote`) değişiklikleri yerel depoya indirmenizi sağlayan bir komuttur.
> + Ancak bu komut, indirilen değişiklikleri mevcut çalışma dalınıza (branch) otomatik olarak birleştirmez.
> + Yani, uzak depodan (örneğin, `origin`) en son commit'leri ve referansları (branch, tag vb.) alır, ancak bunları otomatik olarak yerel dalınıza eklemez.
> + Bu sayede uzak depodaki güncellemelerden haberdar olabilir ve daha sonra bu değişiklikleri yerel deponuza birleştirmeyi (merge) veya yeniden uygulamayı (rebase) seçebilirsiniz.

###### --prune parametesi:
```shell
$ git fetch --prune
```
> **Explanation:**
> + Uzak depoda silinen dalları da yerel deponuzdan temizlemek için `--prune` seçeneği kullanılır.

##### Git remote:

##### Git push:
###### 1. origin de branch silme:
```shell
$ git push origin --delete <branch-name>
```
> **Explanation:**
> + Örneğin `prod(<branch-name>)` adında bir uzaktaki depoda bir branch var.
> + Bu komut `prod` adındaki uzak depodaki branch'i silecektir.
> + `origin` burada varsayılan uzaktaki repository'nin adıdır.

###### 2. push -u parametresi:
```bash
$ git push -u origin main
```
### Kaynaklar
+ [Official Git Documantion](https://git-scm.com/book/en/v2)
+ [Resmi Git Belgesi](https://git-scm.com/book/tr/v2)
