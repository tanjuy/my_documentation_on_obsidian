#ansible 
###### Örnek 1: Targeting specific Node
```
---

- hosts: all
  become: true

  pre_tasks:
    - name: install updates (RHEL)
      dnf:
        update_only: yes       # 1
        update_cache: yes      # 2
      when: ansible_distribution == "AlmaLinux"

    - name: install update (Ubuntu)
      apt:
        upgrade: dist         # 3
        update_cache: yes     # 4
      when: ansible_distribution == "Ubuntu"


- hosts: web_servers
  become: true

  tasks:
    - name: install apache and php for ubuntu servers
      apt:
        name:
          - apache2
          - libapache-2-mod-php
        state: present
          # update_cache: yes
      when: ansible_distribution == "Ubuntu"

    - name: install apache and php for RHEL servers
      dnf:
        name:
          - httpd
          - php
        state: present
          # update_cache: yes
      when: ansible_distribution == "AlmaLinux"

- hosts: db_servers
  become: true

  tasks:
    - name: install mariadb package (AlmaLinux)
      dnf:
        name: mariadb
        state: latest
      when: ansible_distribution == "AlmaLinux"

    - name: install mariadb package (Ubuntu)
      apt:
        name: mariadb-server
        state: latest
      when: ansible_distribution == "Ubuntu"

- hosts: file_servers
  become: true

  tasks:
    - name: install samba package
      package:              # 5
        name: samba
        state: latest
```

> **Explanation:**
> 1. dnf modülündeki ==update_only== argümanı [[Linux Paket Komutları#check-update|check-update]] komut ile aynıdır.
> 2. dnf modülündeki ==update_cache== argümanı [[Linux Paket Komutları#makecache|makecache]] komut ile eş değerdir.
> 3. apt modülündeki ==upgrade: dist== argümanı [[Linux Paket Komutları#dist-upgrade|dist-upgrade]] aynıdır.
> 4. apt modülündeki ==update_cache== argümanı [[Linux Paket Komutları#update|update]] ile aynıdır.
> 6. [[Inventory Config#Örnek 1|Inventory]] dosyası 
> 7. Video Bağlantısı: [Learn Linux TV](https://www.youtube.com/watch?v=EraC1AuWEF8&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70&index=11)

> [!TIPS] İpucu:
> 5. package modülü kullanıldı çünkü hem ubuntu da hem de almalinux de paket isimleri aynı.


>[!CAUTION] Dikkat:
>*pre-task kullanımı:*
>Eğer işlerin belirli bir sırayla gerçekleşmesini istediğiniz bir noktaya gelirseniz, aynı zamanda belirli Task'ları her zaman diğer play'lerden önce çalıştırılmasını zorunlu kılacak bir yola sahip olmak istersiniz.

###### Örnek 2: Tags
```yaml
---

- hosts: all
  become: true

  pre_tasks:
    - name: install updates (RHEL)
      tags: always               # 1
      dnf:
        update_only: yes      
        update_cache: yes
      when: ansible_distribution == "AlmaLinux"

    - name: install update (Ubuntu)
      tags: always                                   # 1
      apt:
        upgrade: dist
        update_cache: yes
      when: ansible_distribution == "Ubuntu"

- hosts: web_servers
  become: true

  tasks:
    - name: install apache and php for ubuntu servers
      tags: apache,php,ubuntu     
      apt:
        name:
          - apache2
          - libapache-2-mod-php
        state: present
          # update_cache: yes
      when: ansible_distribution == "Ubuntu"

    - name: install apache and php for RHEL servers
      tags: apache,php,almalinux   
      dnf:
        name:
          - httpd
          - php
        state: present
          # update_cache: yes
      when: ansible_distribution == "AlmaLinux"

- hosts: db_servers
  become: true

  tasks:
    - name: install mariadb package (AlmaLinux)
      tags: almalinux,db,mariadb                     # 2
      dnf:
        name: mariadb
        state: latest
      when: ansible_distribution == "AlmaLinux"

    - name: install mariadb package (Ubuntu)
      tags: ubuntu,db,mariadb                        # 2
      apt:
        name: mariadb-server
        state: latest
      when: ansible_distribution == "Ubuntu"

- hosts: file_servers
  become: true
  tags: samba
  tasks:
    - name: install samba package
      package:        
        name: samba
        state: latest
```
> **Explanation:**
> Tags anahtarı büyük playbook'larda kullanışlı olabilir, tüm playbook'u çalıştırmaktansa sadece etiketli alanı çalıştırılabilir. Özelikle playbook'daki spesifik sunucuyu test etmek istersek.
> 1. `tags: always` etiketi, playbook hangi etiketlerle çalıştırılırsa çalıştırılsın, o görevin her zaman çalıştırılmasını sağlar.
> 2. Buradaki etiketler(tags) kendi ama doğrultusunda etiketlenmiştir; 
> 	+ Örneğin: `ansible-playbook --tags db site.yamk` ile sadece ==db== ile etiketlenmiş olan play içerisindeki task'lar etkilenecektir.
> 	+ *Birden fazla etiket eklemek*: `ansible-playbook --tags "apache,db" site.yamk`
> 3. Video: [Learn Linux TV](https://www.youtube.com/watch?v=gH_A-0zYLyw&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70&index=10)

```
$ ansible-playbook --list-tags site.yaml
```
> **Explanation:**
> Yukarıdaki(örnek 2) ansible playbook olan site.yaml dosyasındaki tüm etiketleri(tags) listeliyecektir.

###### Örnek 3: Bir Dosyayı Sunucuya Kopyalama
```yaml
---

- hosts: all
  become: true

  pre_tasks:
    - name: install updates (RHEL)
      tags: always               
      dnf:
        update_only: yes      
        update_cache: yes
      when: ansible_distribution == "AlmaLinux"

    - name: install update (Ubuntu)
      tags: always               
      apt:
        upgrade: dist
        update_cache: yes
      when: ansible_distribution == "Ubuntu"

- hosts: web_servers
  become: true

  tasks:
    - name: install apache and php for ubuntu servers
      tags: apache,php,ubuntu     
      apt:
        name:
          - apache2
          - libapache-2-mod-php
        state: present
          # update_cache: yes
      when: ansible_distribution == "Ubuntu"

    - name: install apache and php for RHEL servers
      tags: apache,php,almalinux   
      dnf:
        name:
          - httpd
          - php
        state: present
          # update_cache: yes
      when: ansible_distribution == "AlmaLinux"
    
	- name: copy default html file for site 
	  tags: apache, apache2, httpd
	  copy:                                        # 1
	    src: default_site.html                     # 2
	    dest: /var/www/html/index.html             # 2
	    owner: root                                # 4
	    group: root                                # 4
	    mode: 0644                                 # 5

- hosts: db_servers
  become: true

  tasks:
    - name: install mariadb package (AlmaLinux)
      tags: almalinux,db,mariadb    
      dnf:
        name: mariadb
        state: latest
      when: ansible_distribution == "AlmaLinux"

    - name: install mariadb package (Ubuntu)
      tags: ubuntu,db,mariadb      
      apt:
        name: mariadb-server
        state: latest
      when: ansible_distribution == "Ubuntu"

- hosts: file_servers
  become: true
  tags: samba
  tasks:
    - name: install samba package
      package:        
        name: samba
        state: latest
```
> **Explanation:**
> 1. Kopyalama işlemini gerçekleştirmek için `copy` modülünü kullanıyoruz.
> 2. `src` yönergesi bizim kaynağımız(source) göstermektedir. Öncelikle playbook dosyamızın bulunduğu dizinde `mkdir files` komut ile *files* adında bir dizin oluşturmamız gerekmektedir. Daha sonrasında files dizin içerisine kaynaklarımız verebiliriz. files klasörün içerisine **default_site.html** var. 
> 	+ `scp files/default_site.html 192.168.1.X:/var/www/html/index.html` aynı işlemi yapıyor.
> 3. Hedefteki dosyanın(*index.html*) sahibini **root** yapıyoruz ve grubunu **root** yapıyoruz. 
> 	+ `chown root:root index.html` ile aynı işlemi yapıyor.
> 4. `chmod 644 index.html` ile aynı işlemi yapıyor.
