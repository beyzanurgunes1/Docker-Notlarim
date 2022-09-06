# Docker
 
DOCKER: Aynı işletim sistemi üzerinde, yüzlerce hatta binlerce birbirinden izole ve bağımsız containerlar sayesinde sanallaştırma sağlayan teknolojidir.
Açık kaynaklıdır. Uygulamaları altyapıdan bağımsız kılar. Böylece yazılım üretim ve dağıtım süreci hızlanır.

DOCKER ENGİNE: işletim sistemi üzerine kurulu server-client mimarisinde bir uygulamadır.

DOCKER DEAMON: image, container, network, volume gibi docker objeleri yaratmamızı, yönetmemizi sağlar.
Deamon, REST API sayesinde dış dünyayla iletişim kurar. Diğer programlar docker deamon ile REST API üzerinden haberleşir.

DOCKER CLI: Kullanıcının Docker Daemon ile konuşmasını sağlayan, docker komutlarının çalıştırıldığı,
docker engine'i yönetmeyi sağlayan CLI(komut satırı arayüzü) ekranıdır.


IMAGE: Bir uygulama ve o uygulamanın çalışması için gerekli ögelerin paketlenmiş halidir. Kernel içermez. Image bir şablondur.

CONTAINER : Docker Daemon tarafından Linux çekirdeği içerisinde birbirinden izole olarak çalıştırılan process’lerin her birine container denir. 
Image şablonunun çalışır halidir.Container yapısı ile izolasyon sağlanır. Tek fiziksel makine tek işletim sistemi üzerine birçok container kurulabilir.
Container içinde işletim sistemi çekirdeğine ihtiyaç yok.

SANALLAŞTIRMA: 
Fiziki bir makine üzerine birden fazla sanal makine kurmamıza izin veren sistemdir.
Sanallaştırma ile kaynak israfı azaltılır.
Aynı işletim sistemi üzerine birden fazla uygulama yüklemektten kaçınmamızın sebebi birbirlerine bağımlı olmalarınıı istemememiz.
Windows/Mac üzerine docker kurduğumuzda docker arkada linux yüklü sanal makineyi ayağa kaldırır ve docker deamon'u buraya yükler.

VIRTUAL MACHINE: Fizikİ makine konusunda tasarruf sağlar ama her uygulama için ayrı işletim sistemi gerekir.

CONTAINER - VIRTUAL MACHINE FARKLARI:

Container uygulama izolasyonu sağlar, virtual machine işletim sistemi izolasyonu sağlar.
container virtual machine'e göre çok daha hızlıdır.
Container virtual machine'e göre daha kolay taşınabilir.(image halinde taşınarak her yerde aynı şekilde çalışır.)

----------------------------------------------------**DOCKER CONTAİNER 101**--------------------------------------------------------------------------------------

Docker version: sistemde yüklü olan docker CLI ve docker deamon versiyonlarını listeler.
(server'dan sonuç alamazsak ya docker deamon çalışmıyor ya da client deamon'a bağlanamıyordur.)

 `Docker info`: Temel bütün bilgilere erişmemizi sağlar. (Kaç container ve kaç image var gibi)
 
 `Docker`: Docker CLI'da kullanabileceğimiz komutları listeler.
 
 `Docker --help`: Bir şeyi nasıl kullanacağımızı hatırlamamıza yardım eder. (Daha detaylı aramak için ör; Docker image --help)
 
 `Docker build --tag imageADI`: image oluşturur.(Docker build image --tag'da aynı işlemi yapar.)
 
 ![docker1](https://user-images.githubusercontent.com/55952111/187977167-c312e98e-66d0-4ab6-8c3d-32d92dee3d0d.JPG)
 
 `Docker images`: image'ları listeler ("docker image ls" de aynı işlevi görür.)
 
 ![docker3](https://user-images.githubusercontent.com/55952111/187977732-8928fe2a-4517-4cab-8bc9-47d87060726e.JPG)

 `Docker image rm`: image'ı siler.
 
 
 `Docker container create`: yeni bir container yaratır.
 
 `Docker container start`: container'ı başlatır.
 
 `Docker container run`: Container yaratıp başlatır.(create ve start'ı ayrı ayrı kullanmaktan daha pratik)
 
 `Docker container run -d`: Container'ı arka planda çalıştırır(detach olarak)
 
 `Docker container ls`: çalışan container'ları listeler.
 
 `Docker container ls -a`: tüm container'ları listeler.
 
 
 ![docker11](https://user-images.githubusercontent.com/55952111/187976205-64ea4b84-72cd-4908-b428-a9e0179d27ae.JPG)

 `Docker container rm <containerID>`: container'ı siler.
 
 `Docker container rm -f <containerID>`: çalışan container'ı zorla siler.
 
 
 `Docker container exec -it <ContainerADI> sh`: çalışan container'a bağlanır.
 
 `exit` komutu container'dan çıkmamızı sağlar.(container çalışmaya devam eder.)
 
 `PS`: Container'a bağlıyken çalışan uygulamaları gösterir.
 
 PID 1 olan uygulama container başladığı anda çalışır.
 
 **RUN - CMD - ENTRYPOINT**
 
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

`Docker container prune`: çalışmayan containerları siler.

`Docker image prune`: çalışmayan image'ları siler.

`Docker image pull alpine`: docker hub'daki alpine image'ını sisteme çeker.

![alistirma1 2](https://user-images.githubusercontent.com/55952111/188207748-59e59b56-09ae-4f2e-adab-618f36a91e6f.JPG)


**DOCKER CONTAINER YAŞAM SÜRESİ**

Container'da tüm ayarlamalar image kısmında yapılır.

Container tek uygulama çalıştırması için dizayn edilir.

Sorun durumunda saniyeler içerisinde kopya oluşturulabilir.(aynı image'dan)

Sorun container'a bağlanarak çözülmez. Yeni container yaratılır. Eğer sorun ayarlar/config ile ilgiliyse image aşamasında çözülür.

Sürekli yeni veriler eklenen bir uygulamayı image haline getirip container çalıştırdığımızı düşünelim. container'da sorun oldu ve yeni container oluşturduk. Bu durumda eski veriler yazılabilir katmana kaydedildiği için yeni container üzerinde bu verilere erişemem. Bu yüzde container yaşam süresinden daha uzun süre saklamam gereken verileri container dışında erişilebilir ve paylaşılabilir olarak ayarlamam gerekir. Bunu volume ile sağlarız. Container silinse bile volume silinmeyeceğinden veriler kaybolmaz.

`Docker volume create`: yeni volume yaratır.

`Docker volume inspect <volumeAdı>`: volume detaylarını görüntüler.

`Docker container run -it -v <volumeAdı:/dosyaAdı> <imageAdı>`: Container oluşturup volume bağlanır. (mount işlemi)


![volumeCreate](https://user-images.githubusercontent.com/55952111/188570245-954ff1e9-f43b-4394-91fc-b896b9810770.JPG)


![DockerVolume](https://user-images.githubusercontent.com/55952111/188208187-373b0255-d448-4872-9d86-96345f899160.JPG)



Bir volume birden fazla container bağlayabilirim. Bu iki container'dan da volume verilerine erişebilirim.

Volume'un mount edildiği klasör mevcut değilse;
-klasörü yaratır ve volume'de hangi dosyalar varsa klasörde de o görünür.(Volume boş ise boş görünür)

Volume, image'da mevcut bir klasöre mount edilirse;
-Klasör boşsa volume içindeki dosyalar klasörde görünür.
-Klasörde dosya var ve volume boş ise klasördeki doyalar volume'e kopyalanır.
-Klasörde dosya var ya da yok volum'de varsa klasörde volumdeki dosyalar görünür.

BIND MOUNTS:

Host üzerindeki bir klasör ya da dosyayı container içine map etme işlemi. (örnek bind mound komutu aşağıdadır.)

`Docker container run -d -p 80:80 -v <Bilgisayarımdaki klasör adresi>:<oluşturduğum container içindeki klasör adresi> <imageAdı>`
Bu komut ile bilgisayarımda belirttiğim klasördeki dosyaları oluşturduğum containerdaki klasöre mount et diyorum.
Yani container'daki klasörde benim bilgisayarımdaki klasör görünsün.)

![alistirma7](https://user-images.githubusercontent.com/55952111/188207921-f90e2c49-1893-44d4-a079-7672e2573292.JPG)


Bind mounds- volume farkı:

Bind mounds'da volume adı girilen yere bilgisayarımdaki klasörün adresini giriyorum. Volume'ler docker'ın kendi objesiyken bind mounds ile bilgiayarımdaki klasörü volume olarak ayarlayabiliyorum.

----------------------------------------------------**DOCKER CONTAİNER 102**--------------------------------------------------------------------------------------

DOCKER PLUGIN-DRIVER SİSTEMİ:

Docker bize varsayılan olarak driver'lar ve pluginler sunar.  Dışarıdan da plugin ve driver yükleyebiliriz.
Ayrıca kendi driver'larımızı yazmamıza da imkan sağlar.

`Volume Driver`: volume yaratıp kullanmamızı sağlar.(Local driver ile local ortamda volume yaratılır.)

`Network Driver`: Ağ altyapısının nasıl davranacağını ve ağa bağlı container'ların ne şekilde haberleşeceğini belirler.

Docker'da container'ların birbirleriyle ve dış dünyayla haberleşmeleri, dışarıdan container'lara erişim sağlanması gibi tüm iletişim altyapısı docker network objeleriyle sağlanır. Network objeleri de çeşitli driver'lar ile yaratılır. Driver'lar sayesinde network'lere değişik özellikler kazandırılabilir.
Docker üzerinde network driver yaratabileceğimiz 5 farklı driver mevcuttur.

1) Bridge Driver: 

   - Birden fazla ağdan tek, birleşik bir ağ yaratır.
   - Varsayılan driver'dır (Network obj. yaratırken spesifik olarak belirtmezsem bridge driver ile yaratır.)
   - Her docker kurulu sistemde üzerinde bridge driver ile yaratılmış aynı isimli network bulunur.
   - Container yaratırken farklı bir şey belirtmediğim sürece bridge driver'a bağlanır.
   
   
2) Host Driver:

   - Her docker kurulu sistemde üzerinde host driver ile yaratılmış aynı isimli network bulunur.
   - Host network'e bağlı container'da network izolasyonu olmaz. Sanki o host üzerinde çalışan bir uygulama gibi host'un ağ kaynaklarını kullanır.
   - Container'ın bağlı olduğu host'un network'ü ile görüşmek istersem host driver kullanırım.
   
   
3) MacVlan:

   - MacVlan ile oluşturulan bir docker network objesine bağlı docker container'lara direkt birer mac adresi atayarak mevcut ağa bağlı
    birer fiziki cihaz gibi davranmaları sağlanır.
   - Docker network trafiğini container'a mac adresi üzerinden yönlendirir
    (Ip routing yapmadan container'ın direkt olarak ağ ile haberleşmesi sağlanır.)
    
    
4) None:

   - Container'ın hiçbir şekilde ağ bağlantısının olmamasını sağlamak için container, none driver'la yaratılan network'e bağlanır.
   
   
 5) Overlay:
 
    - Ayrı sistemler (hostlar) üzerindeki container'ların aynı ağda çalışıyor gibi davranmasını sağlar.
   
 
 
 
 
 Docker kurulduğunda otomatik olarak bridge, host ve none network objeleri yaratılır.
 
 `Docker Network ls`: Sistemdeki network objelerini listeler.
 
 `Docker network inspect bridge`: Bridge network objesinin tüm özelliklerini listeler.
 
 
 ![alistirma2 1inspect](https://user-images.githubusercontent.com/55952111/188512233-7f80d8b8-39b2-4906-bca5-ee6c99ae9208.JPG)


 `CTRL + PQ`: Container ile bağlantıyı keser ancak container'ı kapatmaz.
 
 `Ifconfig`: Container içerisnde ağ ayarlarını gösterir.
 
 Bir container'dan diğer container'a erişmek için container içerisinden ping atılır.(Ping + bağlanmak istenen container ip adresi ile)
 
 `Docker container run -it --name <containerAdı> --net host <imageAdı> sh`: Bir container oluşturup host network'üne bağlar.
 
 `Docker container run -it --name <containerAdı> --net none imageAdı sh`: Bir container oluşturup none network'üne bağlar.
 
 
 PORT PUBLISH:
 
 Aynı bridge network'e bağlı conttainer'lar birbirleriyle haberleşebilir ancak dışarıdan container içindeki servise erişmek için bu container'ın dış dünyaya açık         olması gerekir. Bu da port publish ile sağlanır. (-p veya --publish komutu ile)
 
 `Docker container run -d -p 8080:80 <imageAdı>`: Host üzerinde container yaratıp hostun 8080 portuna gelen bütün istekleri yaratılan container'ın 80 portuna gönderir.
 
 ![alistirma2 3](https://user-images.githubusercontent.com/55952111/188512288-cfda8588-91ce-464f-a352-73a66a43c5aa.JPG)

 
 Aynı container içerisinde birden fazla port publish edebilirim.
 Varsayılan olarak açılan port TCP'dir (UDP port açmak için ör; 53:53/udp şeklinde belirtilir.)
 
 
 
Docker'da birden fazla container ile çalışırken daha karmaşık network topolojilerine ihtiyaç duyulabilir. Bunun için de yeni bridge network'ler oluşturulabilir.
Ör; bir makine (host) üzerinde birbirleriyle iletişim kurması gereken 2 container ve bunlardan tamamen bağımsız 5 container çalışıyor olsun. Hepsi varsayılan bridge network üzerinde olduğundan bütün container'lar birbirleriyle haberleşebilecek ancak bu istediğimiz bie durum değil. Birbirleriyle haberleşmesi gerekmeyen container'ları farklı bridge neetwork'lere bağlayarak network izolasyonu sağlarım.

Docker bridge network'ün ip aralığı vb. her şey default olarak gelir. Bridge network için farklı bir ip adres aralığı seçmem mümkün değil. Bu nedenle farklı bir subnet ihtiyacı duyarsam yeni bridge network yaratmam gerekir.


KULLANICI TANIMLI BRIDGE:

-Varsayılan bridge network'te tanımlı container'lar birbirlerini isimleriyle tanıyamaz (ortamda DNS hizmeti olmadığından). Eğer yeni bir bridge network yaratıp   container'ları buna bağlarsam container'lar artık birbirlerini isimleriyle de tanıyabilir (Docker kullanıcı tanımlı bridge networklerde basit DNS hizmeti de sağlar.)

-Bir container bridge network' bağlıysa bu container'ın bridge network ile bağlantısı kesilemez ancak kullanıcının yarattığı bridge networklere bağlıysa bağlantısını kesebilirim (container çalışıyor olsa bile).

`Docker network create <networkAdı>`: Network yaratır (default olarak bridge network oluşturur.)

`Docker network create --driver host` : host network yaratır.

`Docker container run -dit --name <containerAdı> --net <networkAdı> <imageAdı> sh`: Container'ı detached + interaktif olarak yaratıp network'e bağlar.

`Docker attached <containerAdı>`: container içine girmemizi sağlar.

`Docker network create --driver = bridge -subnet 10.10.0.0/16 --ip range = 10.10.10.0/24 --gateway = 10.10.10.10 <networkAdı>`:
Kullanıcı tanımlı bridge network yaratılarak kendi ip adres aralıklarımı belirlememi sağlar. 


![Alistirma2 1](https://user-images.githubusercontent.com/55952111/188512132-a2c7ba3d-5989-4627-935e-a440f0414f61.JPG)


`Docker network connect <networkAdı> <containerAdı>` : container kullanıcı tanımlı network'e bağlanır.

`Docker network disconnect <networkAdı> <containerAdı>` : container network bağlantısı kesilir.

`Docker network rm <networkAdı>`: Bağlı container yoksa network'ü siler.



LOGGING:

Uygulama ve servisler adım adım hangi işlemleri gerçekleştirdiğini, hataları kaydeder. Bu işleme logging denir.
Linux'da loglar dosyalara kaydedilir. Windows'da ise eventviewer altından erişilebilecek şekilde windows native logs altyapısına kaydedilir. Bunlar sistem loglarıdır.
Bir de kullandığımız servis/uygulamaların oluşturduğu loglar var.
(ör; nginx serviste access.log: her erişim denemesini kaydederken error.log: hataları kaydeder)


Eğer fiziki/sanal linux sistem kullanıyorsak loglara o makineye bağlanarak ulaşırız. Container içerisindeki loglara erişme işlemini docker logs management komut sağlar.



STDIN-STDOUT-STDERR:


`Stdin`: Klavyeden veya başka bir uygulamadan giriş içerebilen akış

`Stdout`: Uygulamanın normal çıktısı (Terminal üzerinde)

`Stderr`: Uygulamanın hata mesajı göndermek için kullanılan çıktısı (Terminal üzerinde)

Docker log altyapısı da stdout-stderr akışlarını izler ve mesajları gösterir.

`Docker logs <containerAdı>`: container çalıştığı andan bu komut girilene kadar oluşan bütün loglar listelenir.

![alistirma2 4](https://user-images.githubusercontent.com/55952111/188512362-a503f90f-d3e1-4e31-a444-c84d0bab1788.JPG)


`Docker logs --details <containerAdı>`: Bazı uygulamalar logları kısıtlı olarak gösterir. Detaylı olarak görmek için bu komut kullanılır.

`Docker logs -t <containerAdı>`: Bazı uygulamalar logların zamanlarını göstermez. Log zamanlarını görmek için bu komut kullanılır.

`Docker logs --until <zaman> <containerAdı>`: Belirtilen zamana kadar oluşan loglar listelenir.

`Docker logs --since <zaman> <containerAdı>`: Belirtilen zamandan beri oluşan loglar listelenir.

`Docker logs --tail 3 <containerAdı>`: son 3 log satırını listeler (3 yerine kaç gelirse sondan o kadar satır listelenir)

`Docker logs -f <containerAdı>`: Logları canlı olarak anında listeler (-f: follow anlamında)

![alistirma2 5](https://user-images.githubusercontent.com/55952111/188512390-8bc2e6e6-fe20-4095-aaef-1e10d0c74585.JPG)


`Docker container run --log -driver splunk <imageAdı>`:  Container'daki bütün logları splunk'ın merkezi sunucusuna gönderir.
(Loglarla daha gelişmiş işlemler için)



DOCKER STATS VE TOP:



`Docker top <containerAdı>`: container içine girmeden çalışan uygulamalar listelenir.

`Docker stats`: Docker host'un üzerinde çalışan bütün container'ları listeler ve yeniler (refresh). 
Container'ın kullandığı memory, cpu gibi durumlara erişim sağlar. Sistemde oluşan yükü gözlemler. (CTRL + C ile çıkılır)


![DockerStats](https://user-images.githubusercontent.com/55952111/188512711-c38871bf-1edf-48a7-8488-986dfa5d51e0.JPG)




`Docker stats <containerAdı>`: sadece belirtilen container'ın oluşturduğu yük, memory, cpu bilgileri listelenir.



CONTAINER CPU VE MEMORY LİMİTLERİ:


Container'lar varsayılan olarak üzerinde çalıştıkları host sistemin cpu ve memory kaynaklarını bir kısıtlama olmadan kullanır. Birden çok container ile çalışırken bir container'dan diğerine cpu/memory kalmaması hataya neden olur.

 `--memory =<limit>`: Container'a belirtilen limit kadar memory limiti verir.
 
 `docker container run -d --memory = <limit> <imageAdı>`: Container oluşturup memory limiti verilir.
 
 Container'a memory'e ek olarak swap alanı da tanıyabiliriz. Swap sayesinde memory'i tüketirse kullanabileceği ek bir alan daha olmuş olur.
 
 `--memory -swap = <limit>`: Container' swap limiti verilmesini sağlar.
 
 `docker container run -d --memory = <limit> --memory -swap = <limit> <imageAdı>` : Container oluşturup swap limiti verilir.
 
 Cpu'da sınırlama yapmak için gereken hesaplama ve dağıtım işlemi karmaşık ve zahmetlidir. Bu yüzden sistemde işlemci (core) sayısından kısıtlama yapılır.
 
 `--cpus = <core sayısı>`: Core sayısı kısıtlaması yapar.
 
 `docker container run -d --cpus = <core sayısı> <imageAdı>`: Container oluşturup cpu yani core sayısı limiti verilir.
 
 `--cpuset -cpus = <aralık>`: özel olarak bir aralık belirterek kullanılacak cpu'ları belirtir( `--cpuset -cpus = "0,3"`: cpu 0 ve cpu 3'ü kullan)
 
 `docker container run -d --cpus = <core sayısı> --cpuset -cpus "<aralık>" <imageAdı>`: Container oluşturup core sayısı (cpu) kısıtı verip kullanılacak cpu'ları belirtiriz.
 
 
 ENVIRONMENT VARIABLES (ORTAM DEĞİŞKENLERİ):
 
 Sistem bazında yani işletim sisteminin tamamında geçerli olan, her yerden erişebilir/çağırılabilir olan değişkenlerdir.
 
 Windows için;
 
 -`get-childItem env`: Sistemdeki bütün environment değişkenleri görüntüler.
 
 -`$Env: <değişkenAdı>` : Belirtilen değişkenin değerini gösterir.
 
 -`$Env: <atananDeğer>`: Ortam değişkeni oluşturup değer atanır.
 
 Linux için;
 
 Bir container yaratıp `bash` komutuyla içine geçtikten sonra şu işlemler yapılabilir:
 
 -`printenv`: Sistemde tanımlı tüm ortam değişkenlerini listeler.
 
 -`echo $<ortam değişkeni>`: Belirtilen ortam değişkenini listeler.
    
 -`export <ortam değişkeni> = <değer>`: Ortam değişkeni oluşturulup değer atandı.
    
 DOCKER ENVIRONMENT VARIABLES (DOCKER ORTAM DEĞİŞKENLERİ):
 
 Container ortamlarında image/container yaratılırken tanımlanan değerlerdir.
 
 -`docker container run -it --env <değişkenAdı> = <değer> <imageAdı> bash` : Container yaratılırken ortam değişkeni oluşturuldu ve değer atandı.
 
 Sistemde tanımlı ortam değişkeni değerini container'a aktarabilirim.
 
 -`docker container run -it --env <ortam değişeni> <imageAdı> bash` : Host üzerinde yer alan ortam değişkeni continer içine atandı.
     
 Docker bütün ortam değişkenlerini dosyaya aktarıp o doya üzerinden tek seferde tanımlamamıza izin verir.
 
 -`docker container run -it --env -file <dosya adı> <imageAdı> bash` : Docker belirtilen dosya içindeki tüm değerleri ortam değişkeni olarak container'a tanımlar.
     
     
     
     
     
 ![alistirma2 11](https://user-images.githubusercontent.com/55952111/188512570-dbca3084-a14e-4cb0-891c-a6aa3d348bb9.JPG)
     
     


     
 IMAGE VE REGISTRY :
 
 Docker image registry: Docker image'larını depolayan sistemlerdir. En büyüğü docker hub'dır. Docker varsayılan image registry olarak docker hub ile haberleşir. Docker hub kendi repository'lerimizi yaratıp kendi yarattığımız docker image'larını depolamamızı sağlar.
 
 Docker image'larına verilen isimler /tag'ler o image'ın depolandığı yeri de belirtir.
 
 Docker'da her objenin ID'si vardır ve bunlarla tanınırlar.
 
 
 Docker image isimlendirme yapısı: 
 
 -image'lar `registry url/ repository: tag` şeklinde isimlendirilir (ör; docker.io/ubuntu: 18.04).
      
 -Eğer image registry varsayılan olan docker hub ise belirtilmesi gerekmez.
     
 -Tag kısmında versiyon belirtilir. Bir repository içinde birden fazla image versiyonu saklanabilir. Uygulamaya tag atamazsak docker varsayılan olarak latest tagını atar. Uygulama çağırırken de tag belirtilmezse varsayılan olarak latest'i çağırır.
      
      
DOCKER IMAGE OLUŞTURMA 1)

Docker image'ı oluşturmak için ilk önce dockerfile oluşturulur.

Dockerfile talimatları: 

FROM: 
            
- Her dockerfile'da bulunmak zorundadır.
               
- Oluşturulacak image'ların hangi image'dan oluşturulacağını belirler.
               
- ` FROM <image>: tag `şeklinde kullanılır.
               
       
RUN: 
      
- image oluşturulurken shell'de komut çalıştırmak için kullanılır.
             
- `RUN <komut>`şeklinde kullanılır.(ör; RUN apt-get update)
             
      
WORKDIR:
      
      
- Cd komutuyla aynı işlevi görür ancak cd komutundan farkı workdır ile belirttiğimiz klasör yoksa oluşturulur.
              
- Bir klasöre geçmek için kullanılır.
              
- `WORKDIR <klasör_lokasyonu>` şeklinde kullanılır.
              
              
 COPY:
      
      
 - image içine dosya/klasör kopyalamak için kullanılır.
              
 - `COPY <dosya_lokasyonu>` şeklinde kullanılır.
              
              
 EXPOSE:
      
      
  - Bu image'dan oluşturulacak container'ların hangi portlar üzerinden erişilebileceğini yani hangi portların yayınlanacağını belirtir.
              
              
  - `EXPOSE port` şeklinde kullanır. (Ör; EXPOSE 80/tcp)
              
              
              
  CMD: 
      
      
  - image'den container yaratıldığında varsayılan olarak çalıştırmasını istediğimiz komutu belirtir.
              
  - `CMD <komut>` şeklinde kullanılır.
              
              
              
  HEALTHCHECK:
       
       
  - Docker'a container'ın hala çalışıp çalışmadığını kontrol etmesini healthcheck ile söyleriz. Docker varsayılan olarak çalışan ilk prosesi izler. O çalııştığı süreece container çalışır. Docker container'ın düzgün çalışıp çalışmadığına bakmaz.
             
             
  - `HEALTHCHECK <komut>` şeklinde çalışır.
             
      
 
 
              
              
      
               
 
 
 
 
 
 
 

 

 



 
 






 

