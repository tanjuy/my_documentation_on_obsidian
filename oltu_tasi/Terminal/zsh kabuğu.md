
+ Linux makinenizde hangi kabuklar(`shells`) yüklü olduğunu kontrol ediyoruz:

```shell
cat /etc/shells
```

**cat çıktısı:**

```shell
# /etc/shells: valid login shells
/bin/sh
/usr/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/usr/bin/dash
/usr/bin/screen
/usr/bin/tmux
```

+ Eğer linux makinenizde `zsh shell` yüklü değil ise aşağıdaki komut ile yüklemesini gerçekleştirebilirsiniz:

```shell
sudo apt install zsh
```

```shell
cat /etc/shells
```

**cat çıktısı:**

```shell
# /etc/shells: valid login shells
/bin/sh
/usr/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/usr/bin/dash
/usr/bin/screen
/usr/bin/tmux
/bin/zsh
/usr/bin/zsh     # <---- 
/usr/bin/zsh     # <----
```

```shell
chsh
```

