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

 

