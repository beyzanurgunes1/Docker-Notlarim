# Docker
 
DOCKER: Aynı işletim sistemi üzerinde, yüzlerce hatta binlerce birbirinden izole ve bağımsız containerlar sayesinde sanallaştırma sağlayan teknolojidir.
Açık kaynaklıdır. Uygulamaları altyapıdan bağımsız kılar. Böylece yazılım üretim ve dağıtım süreci hızlanır.

DOCKER ENGİNE: işletim sistemi üzerine kurulu server-client mimarisinde bir uygulamadır.

DOCKER DEAMON: image, container, network, volume gibi docker objeleri yaratmamızı, yönetmemizi sağlar.
Deamon, REST API sayesinde dış dünyayla iletişim kurar. Diğer programlar docker deamon ile REST API üzerinden haberleşir.

DOCKER CLI: Kullanıcının Docker Daemon ile konuşmasını sağlayan, docker komutlarının çalıştırıldığı CLI ekranıdır.

IMAGE: Bir uygulama ve o uygulamanın çalışması için gerekli ögelerin paketlenmiş halidir. Kernel içermez. Image bir şablondur.

CONTAİNER : Docker Daemon tarafından Linux çekirdeği içerisinde birbirinden izole olarak çalıştırılan process’lerin her birine container denir. 
Image şablonunun çalışır halidir.Container yapısı ile izolasyon sağlanır. Tek fiziksel makine tek işletim sistemi üzerine birçok container kurulabilir.
Container içinde işletim sistemi çekirdeğine ihtiyaç yok.

SANALLAŞTIRMA: 
Fiziksel bir makine üzerine birden fazla sanal makine kurmamıza izin veren sistemdir.
Sanallaştırma ile kaynak israfı azaltılır.
Aynı işletim sistemi üzerine birden fazla uygulama yüklemektten kaçınmamızın sebebi birbirlerine bağımlı olmalarınıı istemememiz.

VİRTUAL MACHİNE: Fiziksel makine konusunda tasarruf sağlar ama her uygulama için ayrı işletim sistemi gerekir.

CONTAİNER - VİRTUAL MACHİNE FARKLARI:

Container uygulama izolasyonu sağlar, virtual machine işletim sistemi izolasyonu sağlar.
container virtual machine'e göre çok daha hızlıdır.
Container virtual machine'e göre daha kolay taşınabilir.(image halinde taşınarak her yerde aynı şekilde çalışır.)

