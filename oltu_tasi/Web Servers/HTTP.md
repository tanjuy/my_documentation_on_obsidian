
> [!INFO] Bilgi:
> **HTTP** kısaltmasının açılımı *Hypertext Transfer Protocol*
> Http bize tarayıcılar ile Web sunucuların konuşmasını sağlar.
> **HTTP/0.9** da yalınca GET isteği destekliyordu Header'ı yoktu. Yanlıca Http dosyasını gönderiyordu ve durum kodu da yoktu.
> 


> [!INFO] Bilgi: 
> **HTTP/1.0** 1996 da tanıtıldı.
> + HTTP/1 ile başlık (header) durum kodları ve yeni metotlar geldi
> + Her isteğin kendi bağlantısı vardı. Her bağlantı için yapar:
> 1. Client ------------- TCP SYN -------------------> Server
> 2. Client <-----------  TCP SYN + ACK ------------ Server
> 3. Client ------------> TCP ACK ------------------> Server
> 4. Client --------------- Http Request ------------> Server
> 5. Client <------------- Http Response ------------ Server
> + ilk 3 aşama TCP Handshake(Üçlü el sıkışması)




> [!INFO] Bilgi: HTTPS
> + HTTP/1.0 de TLS/SSL ile bağlantılarda:
> 1. Client ------------- TCP SYN -------------------> Server
> 2. Client <----------- TCP SYN + ACK ------------ Server
> 3. Client ------------> TCP ACK ------------------> Server
> 4. Client ------------- Client Hello ---------------> Server
> 5. Client <-----------  Server Hello --------------- Server
> 6. Client <----------- Certificate ------------------ Server
> 7. Client <---------- Server Hello Done ---------- Server
> 8. Client ------------ Client Key Exchange -------> Server
> 9. Client ------------ Client Cipher Spec ---------> Server
> 10. Client ----------- Finished --------------------> Server
> 11. Client <---------- Change Cipher Spec ------- Server
> 12. Client <---------- Finished -------------------- Server
> 13. Client ------------ Encrypted Data -----------> Server
> 14. Client <----------- Encrypted Data ------------ Server

### HTTP 1.1
> http 1.1 kalıcı bağlantıları tanıttı. Bağlantılar kapatılamadıkça açık kalır. Böylelikle çok fazla TCP handshake yapmaya gerek kalmıyordu.  *Bir bağlantı üzerinden çok fazla istek sağlanabiliyordu(buna pipelining denir).* Cevap için beklemek zorunda değiller idi.

Kaynak: [ByteByteGo](https://www.youtube.com/watch?v=UMwQjFzTQXw)
Kaynak: [Vertical Moustache Academy](https://www.youtube.com/watch?v=CkEQ0sJ6uJw)


