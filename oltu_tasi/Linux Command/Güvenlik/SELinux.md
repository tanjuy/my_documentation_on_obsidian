#security

+ `setsebool` ve `getsebool`, **SELinux (Security-Enhanced Linux)** güvenlik modülünün **boolean (mantıksal) değerlerini** yönetmek için kullanılan komutlardır.
# 1. getsebool Komutu:

### 1.1. Tüm SELinux Boolean'ı Listeler:

```shell
sudo getsebool -a
```

**Çıktı:**
```shell
abrt_anon_write --> off
abrt_handle_event --> off
abrt_upload_watch_anon_write --> on
antivirus_can_scan_system --> off
antivirus_use_jit --> off
auditadm_exec_content --> on
authlogin_nsswitch_use_ldap --> off
authlogin_radius --> off
authlogin_yubikey --> off
awstats_purge_apache_log_files --> off
boinc_execmem --> on
cdrecord_read_content --> off
cluster_can_network_connect --> off
cluster_manage_all_files --> off
cluster_use_execmem --> off
cobbler_anon_write --> off
cobbler_can_network_connect --> off
cobbler_use_cifs --> off
cobbler_use_nfs --> off
collectd_tcp_network_connect --> off
colord_use_nfs --> off
condor_tcp_network_connect --> off
conman_can_network --> off
conman_use_nfs --> off
cron_can_relabel --> off
cron_system_cronjob_use_shares --> off
cron_userdomain_transition --> on
cups_execmem --> off
cvs_read_shadow --> off
daemons_dump_core --> off
daemons_enable_cluster_mode --> off
daemons_use_tcp_wrapper --> off
daemons_use_tty --> off
dbadm_exec_content --> on
dbadm_manage_user_files --> off
dbadm_read_user_files --> off
deny_bluetooth --> off
deny_execmem --> off
deny_ptrace --> off
dhcpc_exec_iptables --> off
dhcpd_use_ldap --> off
domain_can_mmap_files --> off
domain_can_write_kmsg --> off
domain_fd_use --> on
domain_kernel_load_modules --> off
entropyd_use_audio --> on
exim_can_connect_db --> off
exim_manage_user_files --> off
exim_read_user_files --> off
fcron_crond --> off
fenced_can_network_connect --> off
fenced_can_ssh --> off
fips_mode --> on
ftpd_anon_write --> off
ftpd_connect_all_unreserved --> off
ftpd_connect_db --> off
ftpd_full_access --> off
ftpd_use_cifs --> off
ftpd_use_fusefs --> off
ftpd_use_nfs --> off
ftpd_use_passive_mode --> off
git_cgi_enable_homedirs --> off
git_cgi_use_cifs --> off
git_cgi_use_nfs --> off
git_session_bind_all_unreserved_ports --> off
git_session_users --> off
git_system_enable_homedirs --> off
git_system_use_cifs --> off
git_system_use_nfs --> off
gitosis_can_sendmail --> off
glance_api_can_network --> off
glance_use_execmem --> off
glance_use_fusefs --> off
global_ssp --> off
gpg_web_anon_write --> off
gssd_read_tmp --> on
guest_exec_content --> on
haproxy_connect_any --> off
httpd_anon_write --> off
httpd_builtin_scripting --> on
httpd_can_check_spam --> off
httpd_can_connect_ftp --> off
httpd_can_connect_ldap --> off
httpd_can_connect_mythtv --> off
httpd_can_connect_zabbix --> off
httpd_can_network_connect --> on
httpd_can_network_connect_cobbler --> off
httpd_can_network_connect_db --> off
httpd_can_network_memcache --> off
httpd_can_network_redis --> off
httpd_can_network_relay --> off
httpd_can_sendmail --> off
httpd_dbus_avahi --> off
httpd_dbus_sssd --> off
httpd_dontaudit_search_dirs --> off
httpd_enable_cgi --> on
httpd_enable_ftp_server --> off
httpd_enable_homedirs --> off
httpd_execmem --> off
httpd_graceful_shutdown --> off
httpd_manage_ipa --> off
httpd_mod_auth_ntlm_winbind --> off
httpd_mod_auth_pam --> off
httpd_read_user_content --> off
httpd_run_ipa --> off
httpd_run_preupgrade --> off
httpd_run_stickshift --> off
httpd_serve_cobbler_files --> off
httpd_setrlimit --> off
httpd_ssi_exec --> off
httpd_sys_script_anon_write --> off
httpd_tmp_exec --> off
httpd_tty_comm --> off
httpd_unified --> off
httpd_use_cifs --> off
httpd_use_fusefs --> off
httpd_use_gpg --> off
httpd_use_nfs --> off
httpd_use_opencryptoki --> off
httpd_use_openstack --> off
httpd_use_sasl --> off
httpd_verify_dns --> off
icecast_use_any_tcp_ports --> off
init_audit_control --> off
init_create_dirs --> on
irc_use_any_tcp_ports --> off
irssi_use_full_network --> off
kdumpgui_run_bootloader --> off
keepalived_connect_any --> off
kerberos_enabled --> on
ksmtuned_use_cifs --> off
ksmtuned_use_nfs --> off
logadm_exec_content --> on
logging_syslogd_append_public_content --> off
logging_syslogd_can_sendmail --> off
logging_syslogd_list_non_security_dirs --> off
logging_syslogd_run_nagios_plugins --> off
logging_syslogd_run_unconfined --> off
logging_syslogd_use_tty --> on
login_console_enabled --> on
logrotate_read_inside_containers --> off
logrotate_use_cifs --> off
logrotate_use_fusefs --> off
logrotate_use_nfs --> off
logwatch_can_network_connect_mail --> off
lsmd_plugin_connect_any --> off
mailman_use_fusefs --> off
mcelog_client --> off
mcelog_exec_scripts --> on
mcelog_foreground --> off
mcelog_server --> off
minidlna_read_generic_user_content --> off
mmap_low_allowed --> off
mock_enable_homedirs --> off
mount_anyfile --> on
mozilla_plugin_bind_unreserved_ports --> off
mozilla_plugin_can_network_connect --> on
mozilla_plugin_use_bluejeans --> off
mozilla_plugin_use_gps --> off
mozilla_plugin_use_spice --> off
mozilla_read_content --> off
mpd_enable_homedirs --> off
mpd_use_cifs --> off
mpd_use_nfs --> off
mplayer_execstack --> off
mysql_connect_any --> off
mysql_connect_http --> off
nagios_run_pnp4nagios --> off
nagios_run_sudo --> off
nagios_use_nfs --> off
named_tcp_bind_http_port --> off
named_write_master_zones --> on
neutron_can_network --> off
nfs_export_all_ro --> on
nfs_export_all_rw --> on
nfsd_anon_write --> off
nis_enabled --> off
nscd_use_shm --> on
openshift_use_nfs --> off
openvpn_can_network_connect --> on
openvpn_enable_homedirs --> on
openvpn_run_unconfined --> off
pcp_bind_all_unreserved_ports --> off
pcp_read_generic_logs --> off
pdns_can_network_connect_db --> off
piranha_lvs_can_network_connect --> off
polipo_connect_all_unreserved --> off
polipo_session_bind_all_unreserved_ports --> off
polipo_session_users --> off
polipo_use_cifs --> off
polipo_use_nfs --> off
polyinstantiation_enabled --> off
postfix_local_write_mail_spool --> on
postgresql_can_rsync --> off
postgresql_selinux_transmit_client_label --> off
postgresql_selinux_unconfined_dbadm --> on
postgresql_selinux_users_ddl --> on
pppd_can_insmod --> off
pppd_for_user --> off
privoxy_connect_any --> on
prosody_bind_http_port --> off
puppetagent_manage_all_files --> off
puppetmaster_use_db --> off
racoon_read_shadow --> off
radius_use_jit --> off
redis_enable_notify --> off
rpcd_use_fusefs --> off
rsync_anon_write --> off
rsync_client --> off
rsync_export_all_ro --> off
rsync_full_access --> off
rsync_sys_admin --> off
samba_create_home_dirs --> off
samba_domain_controller --> off
samba_enable_home_dirs --> off
samba_export_all_ro --> off
samba_export_all_rw --> off
samba_load_libgfapi --> off
samba_portmapper --> off
samba_run_unconfined --> off
samba_share_fusefs --> off
samba_share_nfs --> off
sanlock_enable_home_dirs --> off
sanlock_use_fusefs --> off
sanlock_use_nfs --> off
sanlock_use_samba --> off
saslauthd_read_shadow --> off
secadm_exec_content --> on
secure_mode --> off
secure_mode_insmod --> off
secure_mode_policyload --> off
selinuxuser_direct_dri_enabled --> on
selinuxuser_execheap --> off
selinuxuser_execmod --> on
selinuxuser_execstack --> on
selinuxuser_mysql_connect_enabled --> off
selinuxuser_ping --> on
selinuxuser_postgresql_connect_enabled --> off
selinuxuser_rw_noexattrfile --> on
selinuxuser_share_music --> off
selinuxuser_tcp_server --> off
selinuxuser_udp_server --> off
selinuxuser_use_ssh_chroot --> off
sge_domain_can_network_connect --> off
sge_use_nfs --> off
smartmon_3ware --> off
smbd_anon_write --> off
spamassassin_can_network --> off
spamd_enable_home_dirs --> on
spamd_update_can_network --> off
squid_connect_any --> on
squid_use_tproxy --> off
ssh_chroot_rw_homedirs --> off
ssh_keysign --> off
ssh_sysadm_login --> off
ssh_use_tcpd --> off
sslh_can_bind_any_port --> off
sssd_access_kernel_keys --> off
sssd_connect_all_unreserved_ports --> off
staff_exec_content --> on
staff_use_svirt --> off
swift_can_network --> off
sysadm_exec_content --> on
systemd_socket_proxyd_bind_any --> off
systemd_socket_proxyd_connect_any --> off
telepathy_connect_all_ports --> off
telepathy_tcp_connect_generic_network_ports --> on
tftp_anon_write --> off
tftp_home_dir --> off
tmpreaper_use_cifs --> off
tmpreaper_use_nfs --> off
tmpreaper_use_samba --> off
tomcat_can_network_connect_db --> off
tomcat_read_rpm_db --> off
tomcat_use_execmem --> off
tor_bind_all_unreserved_ports --> off
tor_can_network_relay --> off
tor_can_onion_services --> off
unconfined_chrome_sandbox_transition --> on
unconfined_dyntrans_all --> off
unconfined_login --> on
unconfined_mozilla_plugin_transition --> on
unprivuser_use_svirt --> off
use_ecryptfs_home_dirs --> off
use_fusefs_home_dirs --> off
use_lpd_server --> off
use_nfs_home_dirs --> off
use_samba_home_dirs --> off
use_virtualbox --> off
user_exec_content --> on
varnishd_connect_any --> off
virt_lockd_blk_devs --> off
virt_qemu_ga_read_nonsecurity_files --> off
virt_qemu_ga_run_unconfined --> off
virt_read_qemu_ga_data --> off
virt_rw_qemu_ga_data --> off
virt_sandbox_share_apache_content --> off
virt_sandbox_use_all_caps --> on
virt_sandbox_use_audit --> on
virt_sandbox_use_fusefs --> off
virt_sandbox_use_mknod --> off
virt_sandbox_use_netlink --> off
virt_sandbox_use_sys_admin --> off
virt_transition_userdomain --> off
virt_use_comm --> off
virt_use_execmem --> off
virt_use_fusefs --> off
virt_use_glusterd --> off
virt_use_nfs --> off
virt_use_pcscd --> off
virt_use_rawip --> off
virt_use_samba --> off
virt_use_sanlock --> off
virt_use_usb --> on
virt_use_xserver --> off
webadm_manage_user_files --> off
webadm_read_user_files --> off
wine_mmap_zero_ignore --> off
xdm_bind_vnc_tcp_port --> off
xdm_exec_bootloader --> off
xdm_manage_bootloader --> on
xdm_sysadm_login --> off
xdm_write_home --> off
xen_use_nfs --> off
xend_run_blktap --> on
xend_run_qemu --> on
xguest_connect_network --> on
xguest_exec_content --> on
xguest_mount_media --> on
xguest_use_bluetooth --> on
xserver_clients_write_xshm --> off
xserver_execmem --> off
xserver_object_manager --> off
zabbix_can_network --> off
zabbix_run_sudo --> off
zarafa_setrlimit --> off
zebra_write_config --> off
zoneminder_anon_write --> off
zoneminder_run_sudo --> off
```

### 1.2. Tek SELinux Boolean Listeleme:

```shell
getsebool httpd_can_network_connect
```

**Çıktı:**
```shell
httpd_can_network_connect --> on
```

# 2. setsebool Komutu:

+ Bir SELinux boolean'ının değerini geçici (`-P` olmadan) veya kalıcı (`-P` ile) olarak değiştirir.


> [!NOTE]
> + `-P` olmadan yapılan değişiklikler **sadece mevcut oturumda** geçerlidir.
> + `-P` ile yapılan değişiklikler **dosya sistemine kaydedilir**

### Geçici Boolean Açma(`on`):

```shell
setsebool httpd_can_network_connect on
```
> **Explanation:**
> + Sistem yeniden başlatıldığında eski haline döner.

### Kalıcı Boolean Açma(`on`):

```shell
setsebool -P httpd_can_network_connect on
```
> **Explanation:**
> + `-P` parametresi, değişikliği kalıcı yapar. Sistem yeniden başlatıldığında ayarlarını korur.


# 3. Boolean:

### 1. httpd_can_network_connect:

+  `httpd_can_network_connect`, **SELinux**'ta Apache/Nginx gibi web sunucularının ağ üzerinden başka servislere bağlanma yetkisini kontrol eden bir boolean değeridir.
+ Bu ayar, özellikle web uygulamalarının harici API'lere, veritabanlarına veya proxy sunucularına erişmesi gereken durumlarda kritik öneme sahiptir.


> [!NOTE]
> + **Açık(`on`):**  Web sunucusunun (httpd) **TCP/IP üzerinden dış sunuculara bağlanmasına** izin verir.
> 	- PHP/Python uygulamasının MySQL/MongoDB'ye bağlanması.
> 	- Apache'nin bir REST API'sine istek göndermesi.
> 	- Reverse proxy (örneğin, Nginx → Tomcat) yapılandırmaları.
> + **Kapalı(`off`):**  Web sunucusunun ağ bağlantıları engellenir. Sadece **localhost** veya UNIX soketleri üzerinden iletişime izin verilir.


> [!CAUTION]
> 1. **Güvenlik:**
> 	- SELinux varsayılan olarak web sunucularının ağ erişimini kısıtlar ("**principle of least privilege**").
> 	- Bu, bir saldırganın web uygulaması üzerinden sistemi ele geçirmesini zorlaştırır.
> 2. **Uyumluluk:**
> 	- Eğer web uygulamanız harici servislere bağlanıyorsa, bu boolean'ı açmanız gerekir.
> 	- Aksi halde **"Permission Denied"** hatası alırsınız.

#### Kullanımı:

+ Mevcut durumu öğrenmek için;

```shell
getsebool httpd_can_network_connect
```

**Çıktı:**
```shell
httpd_can_network_connect --> off
```

+ **Nasıl değiştirilir?**

```shell
sudo setsebool httpd_can_network_connect on
```


> [!WARNING]
> + Eğer `-P` parametresini kullanırsanız, Sistem yeniden başlatıldığında ayarlar korunur: 
> 	- `sudo setsebool -P httpd_can_network_connect on`
> + Yukarıdaki gibi `-P` parametresi kullanılmadığında sistem yeniden başlatıldığında ayar sıfırlanır.

#### Sorun Giderme:
##### A. Nginx Reverse Proxy Sorunu:
+ Eğer REHL(Alma linux, Rocy Linux) işletim sisteminizi `Nginx Reverse Proxy` sunucusu olarak kullanmak istiyorsanız ve 
+ `nginx.conf` dosyası da herhangi bir sorun  yoksa
+ `sudo ausearch -m avc -ts recent` komut çıktısı: 

```shell
----
time->Sat Apr 19 04:44:59 2025
type=PROCTITLE msg=audit(1745027099.043:459): proctitle=6E67696E783A20776F726B65722070726F63657373
type=SYSCALL msg=audit(1745027099.043:459): arch=c000003e syscall=42 success=no exit=-13 a0=8 a1=55afde171db8 a2=10 a3=7ffc46e1d60c items=0 ppid=36255 pid=37721 auid=4294967295 uid=992 gid=988 euid=992 suid=992 fsuid=992 egid=988 sgid=988 fsgid=988 tty=(none) ses=4294967295 comm="nginx" exe="/usr/sbin/nginx" subj=system_u:system_r:httpd_t:s0 key=(null)
type=AVC msg=audit(1745027099.043:459): avc:  denied  { name_connect } for  pid=37721 comm="nginx" dest=80 scontext=system_u:system_r:httpd_t:s0 tcontext=system_u:object_r:http_port_t:s0 tclass=tcp_socket permissive=0
```
> **Explanation:**
> + `avc: denied` olduğuna dikkat ediniz.

+ `sudo grep "denied" /var/log/audit/audit.log`

```shell
type=AVC msg=audit(1745027099.043:459): avc:  denied  { name_connect } for  pid=37721 comm="nginx" dest=80 scontext=system_u:system_r:httpd_t:s0 tcontext=system_u:object_r:http_port_t:s0 tclass=tcp_socket permissive=0
```


> [!CAUTION]
> + Sadece `nginx reverse proxy` de bu sorunu yaşıyorsanız `httpd_can_network_connect` yerine `httpd_can_network_relay`'yi kullanınız. 

### 2. httpd_can_network_relay:

+ `httpd_can_network_relay`, **SELinux** politikalarında Apache/Nginx gibi web sunucularının **proxy (veya relay) görevi üstlenmesine** izin veren bir boolean değeridir.
+ Bu ayar, özellikle reverse proxy, load balancer veya gateway yapılandırmalarında kritik öneme sahiptir.


> [!NOTE]
> + **Açık(`on`):** Web sunucusunun (httpd) **istemci adına başka sunuculara istek iletmesine** (relay/proxy) izin verir.
> 	- Reverse Proxy (örneğin, Nginx → Tomcat arası iletişim veya Nginx → Nginx).
> 	- Load Balancer yapılandırmaları (Apache → Backend sunucular veya Nginx → Apache, Nginx).
> 	- API Gateway'lerin yönlendirme yapması.
> + **Kapalı(`off)`:** Web sunucusu sadece **doğrudan kendisine gelen isteklere yanıt verebilir**, başka sunuculara istek iletemez.

#### 2.1. `httpd_can_network_connect` vs `httpd_can_network_relay`:

|Boolean|Kapsam|
|---|---|
|**`httpd_can_network_connect`**|Web sunucusunun **doğrudan harici bir sunucuya bağlanmasına** izin verir (örneğin, MySQL API'sine erişim).|
|**`httpd_can_network_relay`**|Web sunucusunun **istemci adına başka bir sunucuya istek iletmesine** izin verir (proxy/gateway davranışı).|

#### Kullanımı:

+ Mevcut durumu öğrenmek için;

```shell
getsebool httpd_can_network_relay
```

**Çıktı:**
```shell
httpd_can_network_relay --> on
```

+ **Nasıl değiştirilir?**

```shell
sudo setsebool httpd_can_network_relay on
```


> [!CAUTION]
> + Sistem yeniden başlatıldığında kalıcı olmasını istiyorsanız: `sudo setsebool -P httpd_can_network_relay on`
> + Yani, `-P` parametresini kullanınız.


> [!WARNING]
> 1.  **Minimum Ayrıcalık Prensibi:**
> 	- Sadece proxy gerekiyorsa `httpd_can_network_relay`'i açın.
> 	- Eğer sadece doğrudan bağlantı gerekiyorsa, `httpd_can_network_connect` yeterlidir.
> 2. **SELinux Loglarını İzleme:**
> 	```shell
> 	sudo tail -f /var/log/audit/audit.log | grep AVC
> 	```
> 3. **Proxy Yapılandırmasını Test Etme:**
> 	```shell
> 	curl -I http://192.168.1.132/api
> 	```

#### 2.2 Ne Zaman Kullanılmalı?

1. **Reverse Proxy Sunucularda:** Nginx, `example.com` üzerinden gelen istekleri `localhost:8080`'de çalışan bir Tomcat uygulamasına veya nginx sunucularına yönlendiriliyorsa.
2. **API Gateway: ** Apache veya nginx, `/api` yolundaki istekleri arka planda bir microservice'e (`backend:3000`) iletiyorsa.

#### Sorun Giderme:
##### A. Nginx Reverse Proxy Sorunu:
+ Eğer REHL(Alma linux, Rocy Linux) işletim sisteminizi `Nginx Reverse Proxy` sunucusu olarak kullanmak istiyorsanız ve 
+ `nginx.conf` dosyası da herhangi bir sorun  yoksa
+ `sudo ausearch -m avc -ts recent` komut çıktısı: 

```shell
----
time->Sat Apr 19 04:44:59 2025
type=PROCTITLE msg=audit(1745027099.043:459): proctitle=6E67696E783A20776F726B65722070726F63657373
type=SYSCALL msg=audit(1745027099.043:459): arch=c000003e syscall=42 success=no exit=-13 a0=8 a1=55afde171db8 a2=10 a3=7ffc46e1d60c items=0 ppid=36255 pid=37721 auid=4294967295 uid=992 gid=988 euid=992 suid=992 fsuid=992 egid=988 sgid=988 fsgid=988 tty=(none) ses=4294967295 comm="nginx" exe="/usr/sbin/nginx" subj=system_u:system_r:httpd_t:s0 key=(null)
type=AVC msg=audit(1745027099.043:459): avc:  denied  { name_connect } for  pid=37721 comm="nginx" dest=80 scontext=system_u:system_r:httpd_t:s0 tcontext=system_u:object_r:http_port_t:s0 tclass=tcp_socket permissive=0
```
> **Explanation:**
> + `avc: denied` olduğuna dikkat ediniz.

+ `sudo grep "denied" /var/log/audit/audit.log`

```shell
type=AVC msg=audit(1745027099.043:459): avc:  denied  { name_connect } for  pid=37721 comm="nginx" dest=80 scontext=system_u:system_r:httpd_t:s0 tcontext=system_u:object_r:http_port_t:s0 tclass=tcp_socket permissive=0
```

# 4. `audit.log` Dosyasını Yorumlama:

### Nginx Reverse Proxy Sorunu:

```shell
type=AVC msg=audit(1745027099.043:459): avc:  denied  { name_connect } for  pid=37721 comm="nginx" dest=80 scontext=system_u:system_r:httpd_t:s0 tcontext=system_u:object_r:http_port_t:s0 tclass=tcp_socket permissive=0
```

+ Bu AVC (Access Vector Cache) kaydı, **SELinux** tarafından engellenen bir bağlantı denemesini gösteriyor.

|Bileşen|Açıklama|
|---|---|
|**`denied { name_connect }`**|Nginx'in **TCP bağlantısı kurma** (`name_connect`) isteği reddedildi.|
|**`pid=37631 comm="nginx"`**|İşlemi yapan uygulama: **Nginx** (PID 37631).|
|**`dest=80`**|Hedef: **80 portu** (HTTP).|
|**`scontext=...:httpd_t:s0`**|Kaynak (Nginx) SELinux context'i: `httpd_t`.|
|**`tcontext=...:http_port_t:s0`**|Hedef (80 portu) SELinux context'i: `http_port_t`.|
|**`tclass=tcp_socket`**|Erişim denenen nesne türü: **TCP soketi**.|
|**`permissive=0`**|SELinux **enforcing modda** (kesin reddedildi).|

### Sorunun Nedeni?

+ Nginx (`httpd_t` context'inde çalışan bir proses), **80 portuna** (`http_port_t`) bağlanmaya çalıştı, ancak SELinux politikası buna izin vermedi.
+ Nginx **reverse proxy** olarak çalışıyor ve başka bir sunucuya bağlanmaya çalışıyor.
+ Nginx'in **80 portunu dinlemesi** engellenmiş olabilir (ancak bu durumda genellikle `name_bind` hatası alırsınız).

### AVC nedir?
