#archlinux

## Temel Kurulum:

## BIOS

### 1.Disk Bölümlendirmesi:

```shell
parted /dev/sda mklabel msdos
```
> **Explanation:**
> + `mklabel` : Bu seçenek, bir diskin **bölüm tablosunu** (`partition table`) oluşturur veya değiştirir.
> + `msdos`  : Bu, oluşturulacak bölüm tablosunun türünü belirtir. `msdos`, **MBR (Master Boot Record)** türünde bir bölüm tablosu anlamına gelir. Bu tür, genellikle eski sistemlerde veya BIOS tabanlı önyükleme yöntemlerinde kullanılır.
> + `/dev/sda` diskine bir **MBR tabanlı bölüm tablosu** oluşturur. Diskteki mevcut tüm bölümler ve veriler silinir (uyarı: bu işlem geri alınamaz!). Yeni bir başlangıç noktası sağlanır, bu sayede diskte yeni bölümler oluşturabilirsiniz.


| Yükleme yapılan sistemdeki <br>bağlantı noktası | Bölüm       | Bölüm Tipi | Önerilen Boyut                                                     |
| :---------------------------------------------: | ----------- | ---------- | ------------------------------------------------------------------ |
|                     `/boot`                     | `/dev/sda1` | bootable   | 1GB                                                                |
|                    `[SWAP]`                     | `/dev/sda2` | Linux Swap | En az 4GB                                                          |
|                       `/`                       | `/dev/sda3` | Linux      | Cihazda geriye kalan tüm alan, <br>en az 23-32 GiB arası olmalıdır |

```shell
cfdisk /dev/sda
```
> **Explanation:**

### 2.Bölüm Biçimlendirme:

```shell
mkswap /dev/sda2
```


```shell
swapon /dev/sda2
```


```shell
mkfs.ext4 -L BOOT /dev/sda1 
```

```shell
blid /dev/sda1
```
> **Explanation:**
> + Biçimlendirme işlemi tamamlandıktan sonra etiketi kontrol etmek için `blkid` komutunu kullanabilirsiniz.

```shell
lsblk -o NAME,MAJ:MIN,SIZE,RO,TYPE,MOUNTPOINT,LABEL
```

### 3.Dosya Sistemlerine Bağlanma:

```
```

## UEFI

```shell
parted /dev/sda mklabel gpt
```

## Kaynak:
1. [Resmi Sitesi](https://wiki.archlinux.org/title/Installation_guide_(T%C3%BCrk%C3%A7e))
2. 