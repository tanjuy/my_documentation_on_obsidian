
# App Arama:

```powershell
winget.exe search pgAdmin
```

```powershell
Name      Id                 Version Match            Source
------------------------------------------------------------
pgAdmin 4 PostgreSQL.pgAdmin 9.3     Moniker: pgadmin winget
```

# App Yükleme:

```powershell
winget.exe install --id "PostgreSQL.pgAdmin" -e
```

# App Güncelleme:

```powershell
winget.exe list flameshot
```

**list Çıktısı:**

```powershell
Name      Id                  Version Available Source
------------------------------------------------------
Flameshot Flameshot.Flameshot 12.1.0  13.1.0    winget
```


```powershell
winget.exe upgrade --id "Flameshot.Flameshot" -e
```

# App Kaldırma:





```powershell
PS C:\Users\userName> winget.exe uninstall --name "pgAdmin 4 version 8.3"  
```
> **Explanation:**
> 

```
PS C:\Users\userName> winget upgrade --all
```
> **Explanation:**
> 