#windows 

# Kurulum:

# 1. Distro Listeleme:

## A. Microsoft Store’da mevcut dağıtımları listelemek:

+ Bu komut, Microsoft Store üzerinden yüklenebilecek tüm resmi WSL dağıtımlarını listeler.

```powershell
wsl --list --online
```


> [!TIP]
> + Yukarıdaki komutun kısa kullanımı:
> ```powershell
> wsl -l -o
> ```

## B. Yüklü olan dağıtımları listelemek:

```powershell
wsl --list --verbose
```

> [!TIP]
> + Yukarıdaki komutun kısa kullanımı:
> ```powershell
> wsl -l -v
> ```
# 2. Distro Kurulumu:

## 🧪Örnek 1:

```powershell
wsl.exe --install -d debian
```

# 3. Distro Kaldırma:

```powershell
wsl.exe --
```


# 4. Yedek Alma:

Silmeden önce bir yedek oluşturabilirsin:

```powershell
wsl --export RockyLinux9 D:\Backup\RockyLinux9.tar
```

Daha sonra geri yüklemek için:

```powershell
wsl --import RockyLinux9 C:\WSL\RockyLinux9 D:\Backup\RockyLinux9.tar
```

Bu yöntem, dağıtımını ileride tekrar kullanmak istersen oldukça faydalıdır.

#### Kaynak:
[Wsl Yükleme](https://learn.microsoft.com/en-us/windows/wsl/install)