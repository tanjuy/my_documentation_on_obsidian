#ansible


> [!CAUTION] Dikkat:
> `ansible -i inventory OR ansible-playbook -i inventory`
> `ansible --ask-become-pass OR ansible-playbook --ask-become-pass`
> Komutları [[ansible.cfg#Ansible.cfg Açıklaması|ansible.cfg]] dosyasında gelmektedir.

### Modül Kullanımı:
```bash
$ ansible all -m ping
```
> **Explanation:**
>  ping modülü ile tüm sunuculara ping atmakdır ve geri dönen pong'dur.

---
> [!CAUTION] Dikkat:
> 

```bash
$ ansible all -a "shutdown now" --become
```
> **Explanation:**
> Tüm sunucuları kapatır