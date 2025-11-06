#windows 

# Kurulum:

# Distro Listeleme:

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
# Distro Kurulumu:

## 🧪Örnek 1:

```powershell
wsl.exe --install -d debian
```


#### Kaynak:
[Wsl Yükleme](https://learn.microsoft.com/en-us/windows/wsl/install)