# Docker
 
DOCKER: Aynı işletim sistemi üzerinde, yüzlerce hatta binlerce birbirinden izole ve bağımsız containerlar sayesinde sanallaştırma sağlayan teknolojidir.
Açık kaynaklıdır. Uygulamaları altyapıdan bağımsız kılar. Böylece yazılım üretim ve dağıtım süreci hızlanır.

DOCKER ENGİNE: işletim sistemi üzerine kurulu server-client mimarisinde bir uygulamadır.

DOCKER DEAMON: image, container, network, volume gibi docker objeleri yaratmamızı, yönetmemizi sağlar.
Deamon, REST API sayesinde dış dünyayla iletişim kurar. Diğer programlar docker deamon ile REST API üzerinden haberleşir.

DOCKER CLI: Kullanıcının Docker Daemon ile konuşmasını sağlayan, docker komutlarının çalıştırıldığı,
docker engine'i yönetmeyi sağlayan CLI(komut satırı arayüzü) ekranıdır.


IMAGE: Bir uygulama ve o uygulamanın çalışması için gerekli ögelerin paketlenmiş halidir. Kernel içermez. Image bir şablondur.

CONTAİNER : Docker Daemon tarafından Linux çekirdeği içerisinde birbirinden izole olarak çalıştırılan process’lerin her birine container denir. 
Image şablonunun çalışır halidir.Container yapısı ile izolasyon sağlanır. Tek fiziksel makine tek işletim sistemi üzerine birçok container kurulabilir.
Container içinde işletim sistemi çekirdeğine ihtiyaç yok.

SANALLAŞTIRMA: 
Fiziksel bir makine üzerine birden fazla sanal makine kurmamıza izin veren sistemdir.
Sanallaştırma ile kaynak israfı azaltılır.
Aynı işletim sistemi üzerine birden fazla uygulama yüklemektten kaçınmamızın sebebi birbirlerine bağımlı olmalarınıı istemememiz.
Windows/Mac üzerine docker kurduğumuzda docker arkada linux yüklü sanal makineyi ayağa kaldırır ve docker deamon'u buraya yükler.

VİRTUAL MACHİNE: Fiziksel makine konusunda tasarruf sağlar ama her uygulama için ayrı işletim sistemi gerekir.

CONTAİNER - VİRTUAL MACHİNE FARKLARI:

Container uygulama izolasyonu sağlar, virtual machine işletim sistemi izolasyonu sağlar.
container virtual machine'e göre çok daha hızlıdır.
Container virtual machine'e göre daha kolay taşınabilir.(image halinde taşınarak her yerde aynı şekilde çalışır.)

----------------------------------------------------**DOCKER 101**--------------------------------------------------------------------------------------

Docker version: sistemde yüklü olan docker CLI ve docker deamon versiyonlarını listeler.
(server'dan sonuç alamazsak ya docker deamon çalışmıyor ya da client deamon'a bağlanamıyordur.)

 Docker info: Temel bütün bilgilere erişmemizi sağlar. (Kaç container ve kaç image var gibi)
 
 Docker: Docker CLI'da kullanabileceğimiz komutları listeler.
 
 Docker --help: Bir şeyi nasıl kullanacağımızı hatırlamamıza yardım eder. (Daha detaylı aramak için ör; Docker image --help)
 
 Docker build --tag imageADI: image oluşturur.(Docker build image --tag'da aynı işlemi yapar.)
 
 ![docker1](https://user-images.githubusercontent.com/55952111/187977167-c312e98e-66d0-4ab6-8c3d-32d92dee3d0d.JPG)
 
 Docker image: image'ları listeler.
 
 ![docker3](https://user-images.githubusercontent.com/55952111/187977732-8928fe2a-4517-4cab-8bc9-47d87060726e.JPG)

 Docker image rm: image'ı siler.
 
 
 Docker container create: yeni bir container yaratır.
 
 Docker container start: container'ı başlatır.
 
 Docker container run: Container yaratıp başlatır.(create ve start'ı ayrı ayrı kullanmaktan daha pratik)
 
 Docker container run -d: Container'ı arka planda çalıştırır(detach olarak)
 
 Docker container ls: çalışan container'ları listeler.
 
 Docker container ls -a: tüm container'ları listeler.
 
 
 ![docker11](https://user-images.githubusercontent.com/55952111/187976205-64ea4b84-72cd-4908-b428-a9e0179d27ae.JPG)

 Docker container rm containerID: container'ı siler.
 
 Docker container rm -f containerID: çalışan container'ı zorla siler.
 
 
 Docker container exec -it ContainerADI sh: çalışan container'a bağlanır.
 
 exit komutu container'dan çıkmamızı sağlar.(container çalışmaya devam eder.)
 
 PS: Container'a bağlıyken çalışan uygulamaları gösterir.
 
 PID 1 olan uygulama container başladığı anda çalışır.
 
 **RUN - CMD - ENTRYPOİNT**
 
 Dockerfile içinde kaç cmd olursa olsun hep en sonuncu çalışır.(ekrana o yazılır)
 
 ![docker6](https://user-images.githubusercontent.com/55952111/187979466-a075ec6e-acd1-40ef-83ae-54b02138d0f0.JPG)
 
 ![docker5](https://user-images.githubusercontent.com/55952111/187979521-5c5b4375-0a2f-4887-bbac-29544ce24f0a.JPG)

 Run ile yazılanlar derlerken çalışır.
 
 Entrypoint ilk çalışan uygulamadır. Entrypoint ezilemez.
 Entrypoint ve cmd var ise entrypoint + cmd ekrana yazılır.
 
 
 ![docker7](https://user-images.githubusercontent.com/55952111/187979640-a5e501e5-d1cd-4be2-8896-7fdf48724009.JPG)
 
 ![docker8](https://user-images.githubusercontent.com/55952111/187979728-bb8606e6-5ec2-4cfc-aa36-a2d206d4bbf1.JPG)

**DOCKER KATMANLI DOSYA SİSTEMİ YAPISI**

Docker depolama yapısında union file system kullanır.

Docker image'ları mevcut bir base image üzerine inşaa edilir. Yapılan her değişiklik katman olarak eklenir. Katmanlar ayrı dosya olarak depolanır.
Docker image'den container oluştururken image'ın kopyasını oluşturup container yaratmaz. Image readonly olarak yüklenir.
Bunun üzerine boş bir yazılabilir katman ekler ve container bu şekilde çalıştırılır. Container'da yapılan değişiklikler yazılabilir katmanda yapılır ve sadece o container için geçerlidir.

![dockerUnionFile](https://user-images.githubusercontent.com/55952111/188208058-21bca815-6353-4846-a5d7-78e5814e33c9.JPG)



Docker tüm image'leri katmanlar halinde tuttuğundan aynı katmanı iki kez barındırmak/transfer etmek zorunda kalmıyor.

Docker container prune: çalışmayan containerları siler.

Docker image prune: çalışmayan image'ları siler.

Docker image pull alpine: docker hub'daki alpine image'ını sisteme çeker.

![alistirma1 2](https://user-images.githubusercontent.com/55952111/188207748-59e59b56-09ae-4f2e-adab-618f36a91e6f.JPG)


**DOCKER CONTAİNER YAŞAM SÜRESİ**

Container'da tüm ayarlamalar image kısmında yapılır.

Container tek uygulama çalıştırması için dizayn edilir.

Sorun durumunda saniyeler içerisinde kopya oluşturulabilir.(aynı image'dan)

Sorun container'a bağlanarak çözülmez. Yeni container yaratılır. Eğer sorun ayarlar/config ile ilgiliyse image aşamasında çözülür.

Sürekli yeni veriler eklenen bir uygulamayı image haline getirip container çalıştırdığımızı düşünelim. container'da sorun oldu ve yeni container oluşturduk. Bu durumda eski veriler yazılabilir katmana kaydedildiği için yeni container üzerinde bu verilere erişemem. Bu yüzde container yaşam süresinden daha uzun süre saklamam gereken verileri container dışında erişilebilir ve paylaşılabilir olarak ayarlamam gerekir. Bunu volume ile sağlarız. Container silinse bile volume silinmeyeceğinden veriler kaybolmaz.

Docker volume create: yeni volume yaratır.

Docker volume inspect volumeAdı: volume detaylarını görüntüler.

Docker container run -it -v volumeAdı:/dosyaAdı imageAdı: Container oluşturup volume bağlanır. (mount işlemi)

![DockerVolume](https://user-images.githubusercontent.com/55952111/188208187-373b0255-d448-4872-9d86-96345f899160.JPG)



Bir volume birden fazla container bağlayabilirim. Bu iki container'dan da volume verilerine erişebilirim.

Volume'un mount edildiği klasör mevcut değilse;
klasörü yaratır ve volume'de hangi dosyalar varsa klasörde de o görünür.(Volume boş ise boş görünür)

Volume, image'da mevcut bir klasöre mount edilirse;
Klasör boşsa volume içindeki dosyalar klasörde görünür.
Klasörde dosya var ve volume boş ise klasördeki doyalar volume'e kopyalanır.
Klasörde dosya var ya da yok volum'de varsa klasörde volumdeki dosyalar görünür.

BİND MOUNTS:

Host üzerindeki bir klasör ya da dosyayı container içine map etme işlemi. (örnek bind mound komutu aşağıdadır.)

Docker container run -d -p 80:80 -v (Bilgisayarımdaki klasör adresi):(oluşturduğum container içindeki klasör adresi) imageAdı
Bu komut ile bilgisayarımda belirttiğim klasördeki dosyaları oluşturduğum containerdaki klasöre mount et diyorum.
Yani container'daki klasörde benim bilgisayarımdaki klasör görünsün.)

![alistirma7](https://user-images.githubusercontent.com/55952111/188207921-f90e2c49-1893-44d4-a079-7672e2573292.JPG)


Bind mounds- volume farkı:

Bind mounds'da volume adı girilen yere bilgisayarımdaki klasörün adresini giriyorum. Volume'ler docker'ın kendi objesiyken bind mounds ile bilgiayarımdaki klasörü volume olarak ayarlayabiliyorum.








 

