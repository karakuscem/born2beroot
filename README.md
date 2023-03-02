# *Genel Yönlendirmeler*

*VirtualBox (veya VB kullanamıyorsanız UTM) kullanmak zorunludur.*

*Reponuzun içerisinde sadece signature.txt dosyası olmalı, bu dosyanun içerisinde sanal diskinizin kodu(imzası) bulunmalıdır.*

# Virtual Disk Signature nedir ?

Disk imzası, sabit bir disk sürücüsü veya başka bir veri depolama aygıtı için benzersiz, tanımlayıcı bir numaradır. Bir işletim sistemi, bilgisayarınızdaki depolama aygıtları arasında ayrım yapmak için bunu kullanır.

# Host, Guest nedir ?

Sanal makinenin bulunduğu fiziksel olarak var olan bilgisayara Host denir. Bu durumda sanal makineye ise Guest denir.

# “.vdi” Dosyası nedir ?

Açılımı Virtual Disk Image’dır. Disk görüntü dosyası olarak Türkçeye çevrilebilir. Disk görüntü dosyası host sistemde bulunur ve guest sistemler tarafından belirli geometriye sahip sabit diskler olarak görülür. Bir guest sistemi bu sabit diskten okuma yaptığında veya diske yazdığında VirtualBox bu isteği görüntü dosyasına yönlendirir. .vdi formatı yeni bir disk ile sanal makine oluşturulduğunda kullanılır.

# *Zorunlu Kısım*

*İşletim sistemi olarak Debian'ın en son kararlı sürümünü veya CentOS'un en son kararlı sürümünü seçmelisiniz. Sistem yönetiminde yeniyseniz, Debian şiddetle tavsiye edilir.*

# Neden Debian ?

Debian’ın kullanıcı olarak, geliştirici olarak ve hatta kurumsal ortamlarda tercih edilmesinin bir çok sebebi vardır. Çoğu kullanıcı Debian’ın paketlerin ve dağıtımının istikrarlı olmasını ve sorunsuz upgrade yapmasını takdir eder. Debian ayrıca yazılım ve donanım geliştiricileri tarafından yaygın olarak kullanılmaktadır. Ayrıca CentOs’a göre kullanması daha kolaydır.

# CentOS ve Debian Arasındaki Temel Farklar

1. Debian paket yöneticisi apt’dir CentOS’un yum
2. CentOS’un yeni sürümleri genellikle uzun bir aradan sonra yayınlanır bu yüzden genelde daha stabil çalışır, Debian ise CentOS’a göre daha fazla güncelleme aldığı için yeni çıkan sürümleri daha az stabil olabilir.
3. CentOS Red Hat topluluğu tarafından desteklenir, Debian ise bireysel kişiler tarafından.
4. CentOS Selinux adında kendine ait bir güvenlik sistemiyle gelir.
5. CentOS’un arayüzü Debian’a göre daha karmaşıktır.

# Neden En Son Stabil Versiyonu Seçmeliyiz ?

Üretim kullanımı için sadece stabil önerilir. Üretim düzeyinde stabillik ve güvenlik gerektiren uygulamalar (sunucular, güvenlik duvarları vb.) için önerilir ve ayrıca Linux'ta yeni olanlar için önerilir.

# Debian Nasıl Kurulur ?

Güncellenecek…

# LVM nedir ?

Logical Volume Management. LVM modüler disk veri kümesi veya kümeleri oluşturulmasını böyleliklede istenildiğinde mevcut disk alanı üzerinde istenilen boyutlandırmanın yeniden yapabilmesini sağlar. Disk alanının yetersiz kaldığı durumlarda LVM ile oluşturulan disk veri kümesine kolaylıkla yeni disk veya disk bölümleri ilave edilebilir, ihtiyaca göre disk alanı şekillendirilebilir.

Özellikle büyük disk alanı ihtiyacı olan sistemlerde LVM ile disk veri kümeleri oluşturularak ya da sisteme yeni bir disk daha eklenerek toplam disk boyutu arttırılabilir veya sistemde pasif durumda olan bir disk bölümü aktif disk kümesine dahil edilebilir. Aynı zamanda mevcut disk bölümlerinin boyutları değiştirilebilir. Yapılacak fiziksel veri alanı değişikliklerinden sistemin mevcut haritası hiçbir şekilde etkilenmez ve yeni tanımlar yapmaya gerek kalmaz.

Bir örnek ile ifade edilirse; sistemde /home için ayrılmış 100 GB'lık ve /var ****
için ayrılmış 2GB'lık alanlar olsun. Zamanla /var için ayrılan disk alanın yetersiz gelmeye başladığı düşünülsün. Bu durumda  /home alanında kullanılmayan yeterli boş alan varsa bu alan ****
/var bölümüne aktarılabilir ve mevcut alan kolayca yeniden boyutlandırılabilir. Aynı şekilde ****
/home için ayrılan alan yetmemeye başladığı zaman da sisteme eklenecek yeni bir disk ile bu bölüm için kullanılabilir veri alanı arttırabilir. 

LVM, hacim grubu (vp) ve bu grubun içinde fiziksel hacim (pv) ve mantıksal hacimlerden (lv) oluşur.

**Hacim Grubu (VG)**: Hacim grubu, fiziksel ve mantıksal hacimleri içine alan üst düzey bir katmandır.

**Fiziksel Hacim (PV)**: Fiziksel hacim adından da anlaşılacağı üzere fiziksel aygıtlardan (disklerden) veya disk bölümlerinden oluşan kısımdır.

**Mantıksal Hacim (LV)**: Disk bölümlerinin karşılığıdır. Dosya sistemi içerir.

**LVM’nin Avantajları**

- **Ölçeklenebilirlik:** Çok yüksek veri alanı kümelerinin oluşturulabilmesini sağlar. LVM sayesinde Terabyte'lar mertebesinde disk veri alanı dizileri oluşturulabilir.
- **Kullanılabilirlik:** Oluşturulan veri alanlarını dinamik şekilde yönetebilme, istenildiğinde yeni veri alanları ekleyebilme veya fazla veri alanlarını sistemden çıkarabilme gibi imkanları sağlar.
- **Anlık Görüntü (Snapshot):** Özellikle yedekleme işleminde kullanılan önemli bir özelliktir. Üzerinde sürekli işlem yapılan bir veri alanı (veritabanı) ele alınsın. Bu veritabanı tutarlı bir anında yedeklenmek istensin. Bu durumda, snapshot özelliği yapılacak işlemler için kolaylık ve hız sağlar.Bu veritabanı normal yöntemlerle (copy, rsync vb.) bir yerden diğer bir yere yedeklenirken, yedek alınan yerdeki veritabanı o an için tutarlı olmayan bir durumda kalmış olabilir. Bir veri A tablosuna yazıldıktan sonra o veri ile ilişkili başka veriler tam B tablosuna da yazılacağı sırada yapılan bir yedekleme, tutarsız bir yedeklemeye sebep olabilir. Bunu engellemek için yedek almadan önce, veritabanı tutarlı olduğu bir anda durdurulup yedeklenir. Sonra veritabanı kaldığı yerden devam ettirilebilir. Ancak bu durum özellikle yüksek oranda veri yedeklemesi yapılacağı durumlarda ciddi gecikmelere ve sistemin işlemez hale gelmesine sebep olabilir. Bunun önüne geçebilmek için veritabanının tutarlı olduğu bilindiği bir anda LVM ile anlık görüntüsü alınarak veritabanının duraksamasına engel olunur. Snapshot alınmadan önce tutarlı durumu korumayı garanti edebilmek için veritabanı durdurulsa bile görüntü ile yedekleme işlemi çok kısa bir zaman alacağından veritabanının tekrar aktif hale getirilmesi çok uzun sürmeyecektir.

# Neden Şifrelenmiş Bölümler Kullanıyoruz ?

Verilerinizin gizliliğini garanti etmek için, örneğin bilgisayarınızın veya sabit diskinizin kaybolması veya çalınması durumunda, bazı bölümlerdeki verileri şifrelemek mümkündür. Bu özellik herhangi bir dosya sisteminin altına eklenebilir, çünkü LVM'de olduğu gibi Linux, verileri şifreli bir biçimde depolayacak temel bir bölüme dayalı bir sanal bölüm oluşturmak için Aygıt Eşleyici'yi kullanır.

# APPArmor nedir ?

1. Apparmor, önemli bir güvenlik özelliğidir. Arkaplanda sessizce çalışır. Sisteme zarar verebilecek ayarları, servisleri ve diğer ayarları kontrol edip sınırlandırır. Sistem açılışlarında default olarak aktiftir.
2. Selinux’a benzer bir yapıya sahiptir, her daim çalışmaya devam eder, siz genelde farketmezsiniz. Terminalden durumuna bakmadıkça ne olduğunu hiç araştırmayacak bile olabilirsiniz.
3. AppArmor sisteme verilebilecek zararı sınırlandırır veya yapılan bu işlemi tamamen durdurur.
4. Selinux ve Apparmor ikisi de MAC(MANDATORY ACCESS CONTROL) zorunlu erişim kontrolü güvenliğini sağlamaktadır.
5. Apparmorun sistemdeki durumunu öğrenmek için apparmor-status veya aa-status komutunu girmeniz yeterlidir.
6. Uygulamada çekirdek, verilen işlemi yapmaya yetkili olup olmadığını bilmek için her sistem çağrısından önce AppArmor'u sorgular. Bu mekanizma aracılığıyla AppArmor, programları sınırlı bir kaynak grubuyla sınırlar.
7. AppArmor, her programa bir dizi kural ("profil" olarak bilinir) uygular. Çekirdek tarafından uygulanan profil, yürütülmekte olan programın kurulum yoluna bağlıdır. SELinux'un aksine uygulanan kurallar kullanıcıya bağlı değildir. Tüm kullanıcılar, aynı programı yürütürken aynı kurallar dizisiyle karşılaşır (ancak geleneksel kullanıcı izinleri hala geçerlidir ve farklı davranışlara neden olabilir!).
8. AppArmor profilleri /etc/apparmor.d/ içinde saklanır ve her programın kullanabileceği kaynaklara erişim denetimi kurallarının bir listesini içerir. Profiller, apparmor_parser komutu tarafından derlenir ve çekirdeğe yüklenir. Her profil, enforcing veya  complaining modunda yüklenebilir. İlki, politikayı uygular ve ihlal girişimlerini bildirirken, ikincisi politikayı uygulamaz ancak yine de reddedilecek olan sistem çağrılarını günlüğe kaydeder.
9. AppArmor desteği, Debian tarafından sağlanan standart çekirdeklere yerleştirilmiştir. Bu nedenle, AppArmor'u etkinleştirmek, apt install apparmor apparmor-profiles apparmor-utils'i root ayrıcalıklarıyla yürüterek bazı paketleri kurma meselesidir.

# Mandatory Access Control nedir ?

Bilgisayar güvenliğinde, zorunlu erişim denetimi (MAC), işletim sisteminin veya veritabanının bir öznenin veya başlatıcının bir nesne veya hedefe erişme veya bunlar üzerinde bir tür işlem gerçekleştirme yeteneğini kısıtladığı bir tür erişim denetimi anlamına gelir. İşletim sistemleri söz konusu olduğunda, özne genellikle bir işlem veya iş parçacığıdır; nesneler, dosyalar, dizinler, TCP/UDP bağlantı noktaları, paylaşılan bellek bölümleri, IO cihazları vb. gibi yapılardır. Öznelerin ve nesnelerin her birinin bir dizi güvenlik özniteliği vardır. Bir özne bir nesneye erişmeye çalıştığında, işletim sistemi çekirdeği tarafından uygulanan bir yetkilendirme kuralı bu güvenlik özniteliklerini inceler ve erişimin gerçekleşip gerçekleşmeyeceğine karar verir. Herhangi bir özne tarafından herhangi bir nesne üzerinde yapılan herhangi bir işlem, işleme izin verilip verilmediğini belirlemek için yetkilendirme kurallarına (diğer adıyla politika) karşı test edilir.

# Packet Manager nedir ?

Paket yöneticisi, bilgisayarınızda hangi yazılımların yüklü olduğunu takip eder ve kolayca yeni yazılım yüklemenize, yazılımı daha yeni sürümlere yükseltmenize veya daha önce yüklediğiniz yazılımları kaldırmanıza olanak tanır. 

# APT nedir ?

APT, Advanced Package Tool'un kısaltmasıdır. Bu programı “gelişmiş” yapan, paketlere yaklaşımıdır. Bunları tek tek değerlendirmez, bir bütün olarak ele alır ve mevcut olana ve bağımlılıklara göre uyumlu olana bağlı olarak mümkün olan en iyi paket kombinasyonunu üretir.

APT'ye bir "paket kaynaklarının (havuzlar) listesi" verilmelidir: /etc/apt/sources.list dosyası, Debian paketlerini yayınlayan farklı havuzları listeleyecektir. APT daha sonra bu kaynakların her biri tarafından yayınlanan paketlerin listesini içe aktaracaktır.

# apt nedir ?

apt-get, APT projesi kapsamında geliştirilen komut satırı tabanlı ilk ön uçtur. apt, apt-get'in bazı tasarım hatalarının üstesinden gelen, APT tarafından sağlanan ikinci bir komut satırı tabanlı ön uçtur. Apt'nin varsayılan davranışı, etkileşimli kullanım ve çoğu kullanıcının beklediği şeyi gerçekten yapmak için geliştirildi. APT geliştiricileri, bu aracın genel arayüzünü daha da geliştirmek için değiştirme hakkını saklı tutar. Aksine, apt-get'in genel arayüzü iyi tanımlanmıştır ve geriye dönük olarak uyumsuz bir şekilde değişmeyecektir. Bu nedenle, paket kurulum isteklerini komut dosyası olarak yazmanız gerektiğinde kullanmak istediğiniz araçtır.

# Aptitude nedir ?

aptitude, Debian GNU/Linux sistemleri için ünlü apt paket yönetim altyapısına dayanan özellikli bir paket yöneticisidir. aptitude, dselect ve apt-get işlevlerinin yanı sıra her iki programda da bulunmayan birçok ek özellik sağlar.

aptitude, konsolda yarı grafik modunda kullanılabilen bir APT arabirimidir. Kullanıcının çeşitli kategorilere göre (kurulu veya kurulu olmayan paketler, göreve göre, bölüme göre vb.) açıklama vb.). Her paket “yükle” (yüklenecek, + tuşu) veya “kaldır” (kaldırılacak, - tuşu) olarak işaretlenebilir. g tuşuna basarak onayladığınızda bu işlemlerin tümü aynı anda gerçekleştirilecektir (“g”, “go!” anlamına gelir). Bazı programları unuttuysanız üzülmeyin; ilk kurulum tamamlandıktan sonra aptitude'u tekrar çalıştırabileceksiniz.

# Aptitude ve Apt Arasındaki Farklar

1. Apt ve aptitude Debian’ın paket yöneticisidir. İkisini de paket kurma, kaldırma arama vs gibi etkinlikleri gerçekleştirebilir.
2. Apt’nin açılımı “Advanced Packaging Tool”dur.
3. Aptitude işlevsellik açısından aptden daha geniştir. Aptitude get, mark, cache de dahil olmak üzere apt’nin işlevlerini bünyesinde barındırır
4. Aptitude arayüze sahipken apt değildir.
5. Aptitude sisteme yüklediğiniz paketleri otomatik olarak inceler. Diyelim ki A paketini kurdunuz, bu paket kendisine bağımlı olan bir kaç farklı kitaplık ve paket kurdu. Daha sonra bu A paketini sistemden kaldırmak istediğinizde eğer A paketini kurarken sisteme yüklediğiniz kitaplar ve paketler öksüz kalacaksa(yani başka paketler tarafından kullanılmıyorsa) onları da sistemden kaldırır. Apt-get bu konuda yetersizdir. Aptitude paketlerin kurulumunda tavsiye edilen paketleri de kurar. A paketini kurarken, tavsiye edilen B paketi varsa onu da kurar.
6. Aptitude paketlerin ismi, tanımları, bağımlılıkları vs. gibi bir çok bilgiye kolayca ulaşmanızı sağlar, ayrıca çok güçlü filtreleme ve arama özelliklerine sahiptir.
7. Aptitude modası geçmiş paketleri takip eder. Debian bir paketin dağıtımını durdurmuş olabilir. Apt ise bu tür paketleri sisteminizde bulundurmaya devam eder.
8. Aptitude yaptığınız işlemlerin kaydını tutar. Aptitude ile kurulan kaldırılan güncellenen paketlerin kaydını /var/log/aptitude dosyasında tutar. Bu dosya sayesinde geçmişte paketlerle ilgili ne işlem yaptığımızı görebilmemiz çok önemlidir.

# SSH Nedir ?

Secure Shell SSH, ağ hizmetlerini güvenli olmayan bir ağ üzerinden güvenli bir şekilde çalıştırmak için bir kriptografik ağ protokolüdür. SSH, bir SSH istemci uygulamasını bir SSH sunucusuna bağlayarak bir istemci-sunucu mimarisi kullanarak güvenli olmayan bir ağ üzerinden güvenli bir kanal sağlar.

SSH istemcisi, bağlantı kurulum sürecini yürütür ve SSH sunucusunun kimliğini doğrulamak için ortak anahtar şifreleme kullanır. Kurulum aşamasından sonra SSH protokolü, istemci ile sunucu arasında değiş tokuş edilen verilerin gizliliğini ve bütünlüğünü sağlamak için güçlü simetrik şifreleme ve karma algoritmalar kullanır.

Aşağıdaki şekil, güvenli bir kabuk bağlantısının basitleştirilmiş bir kurulum akışını göstermektedir.

![140618919-8617389f-2f37-4b9b-8ec3-64fc6c3447e9.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/62bee92c-124b-4b94-a9b0-28f1769e12be/140618919-8617389f-2f37-4b9b-8ec3-64fc6c3447e9.png)

Kullanımı `ssh {user}@{host} -p 4242` şeklindedir. user ulaşmak istediğiniz hesabı temsil eder. Host ise ulaşmak istediğiniz bilgisayarı simgeler. Bu bir IP (127.0.0.1) veya domain(www.xyzdomain.com) olabilir. Enter’a basıldığında istenilen hesaba erişmek için şifre girmeniz gerekecek. Şifreyi doğru girdiğinizde uzak terminal penceresiyle karşılaşacaksınız.

# Server’daki SSH Port’u Nasıl Değiştirilir ?

Varsayılan olarak, SSH sunucusu 22 numaralı bağlantı noktasında çalışır, ancak farklı bağlantı noktasında çalıştırıldığı durumlar da vardır. Test amaçlı kullanım bunlardan bir tanesidir.

Port numarası /etc/ssh/sshd_config içerisindeki “Port 22” yönergesini düzenleyerek değiştirilebilir.

![140950738-598cd9a4-b41a-4b9c-b68a-495bbb5278ea.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fd0ef506-c704-4ab6-98f6-4b4d53f8ab3e/140950738-598cd9a4-b41a-4b9c-b68a-495bbb5278ea.png)

```bash
cd etc/ssh/
vim sshd_config
**PORTU DEĞİŞTİR VE DOSYAYI KAYDET**
systemctl restart  sshd (sshd servisini yeniden başlat)
sudo systemctl status ssh (ssh servisini kontrol et)
```

# SSH Bağlantılarını Root İçin Neden Varsayılan Olarak Yasaklamalısınız?

SSH hizmeti saldırganlar ve bilgisayar korsanları için oldukça popüler bir hizmettir. Sanki onunla aynı odadaymışsınız gibi sunucu üzerinde doğrudan kontrol sahibi olmasını sağlar. Brute Force saldırılarına karşın SSH hizmeti zayıftır. Brute Force belirli bir kullanıcı için az yada çok rastgele eçilen çok sayıda parolanın test edilmesinden oluşan saldırılardır. Belirli bur noktada kaçınılmaz olarak doğru olan şifreyle karşılaşılmaı ümit edilir.

Sorun şu ki Brute Force saldırısı Root hesabında başarılı olursa saldırılan sunucu için çok tehlikeli hale gelir çünkü bilgisayar tamamen korsanın eline geçer. O yüzden güvenlik sebebiyle root olarak bağlanmak yasaktır. Bir saldırgan SSH erişimini Brute Force ile ele geçirmeye karar verirse önce geçerli bir kullanıcı adını (dünyadaki tüm Linux makinelerinde bulunan tek kullanıcı olan root dışında) bulmalı ve başarılı olursa geçerli bir şifre bulmalıdır. Başarılı olması sonucunda sunucu üzerinde sınırlı gücü olacaktır (root’u ele geçiremediğinden ötürü) ki bu da bizim açımızdan daha iyidir.

# Root’un SSH Kullanarak Giriş Yapıp Yapamayacağı Nasıl Belirlenir?

```bash
vim etc/sshd/sshd_config (bu dosyayı yeniden açın)
```

Dosyanın içerisinde PermitRootLogin kısmını bulun. Bu Root olarak SSH’a giriş yapılıp yapılamayacağını kontrol eder. Argümanlar şunlar olabilir;

```bash
yes
prohibit-password
forced-commands-only
no
```

Varsayılan “prohibit-password” seçeneğidir. Bu seçenek “no” olarak ayarlanırsa root’un oturum açmasına izin verilmez.

# Firewall nedir ?

Güvenlik duvarı, gelen ve giden ağ trafiğini önceden belirlenmiş güvenlik kurallarına göre izleyen ve kontrol eden bir ağ güvenlik sistemidir. Bir güvenlik duvarı genellikle güvenilir bir ağ ile Internet gibi güvenilmeyen bir ağ arasında bir engel oluşturur.

# UFW nedir ?

Debian üzerinde kullanılan firewall uygulamasıdır. UFW (Uncomplicated Firewall) ile ipv4 veya ipv6 firewall güvenlik yönetimi yapmamıza imkan verir.

# Debian’da UFW Nasıl Yapılandırılır?

```bash
apt install ufw // ufw'yi yükler
```

Ancak, yalnızca güvenlik duvarını yüklemek onu otomatik olarak açmayacak ve varsayılan olarak ayarlanmış herhangi bir kurala sahip olmayacaktır.

UFW’yi açmak için;

```bash
ufw enable
```

Kurallara izin vermek, komut satırından oldukça basittir ve bazen gereklidir. Örneğin, varsayılan olarak ufw, gelen tüm bağlantıları reddeder, bu da SSH kullanıyorsanız bunu bir sorun haline getirir. Bu nedenle, şunu yazarak SSH bağlantılarına izin veren bir kural oluşturmalısınız:

```bash
ufw allow ssh
```

Port aralıkları da belirtilebilir, basit bir örnek şöyle olabilir:

```bash
ufw allow 4242
```

![140985819-9c52531b-e19a-4c36-9201-d8650fd6eecc.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fe2da7e5-d486-46d5-84ef-30fb34580e79/140985819-9c52531b-e19a-4c36-9201-d8650fd6eecc.png)

Kuralları numarasına göre de silebilirsiniz. Numaralandırılmış bir kural listesi göstermek için:

```bash
ufw status numbered
```

/Bu, numaralandırılmış bir kural listesi çıkarır ve numara, belirli bir kuralı silmek için kullanılabilir:

```bash
ufw delete 2
```

# Makinenin Bilgisayar Adı Nasıl Değiştirilir?

Root’a geçin

```bash
su -
```

Mevcut bilgisayar ismini kontrol edin

```bash
hostnamectl
```

Ana bilgisayar adını değiştirmek için şunları yazın

```bash
hostnamectl set-hostname <yeni_isim>
Örnek;
hostnamectl set-hostname server1
```

# Şifre Politikası

### Kötü

UNIX'in ilk sürümlerinde, parolalar /etc/passwd dosyasında saklanıyordu. Bu dosya, bilgisayarda hesabı olan herkes tarafından kullanılabilirdi. Parolalar 2 karakterlik bir salt ile 11 karakter olarak şifrelenmiş biçimde saklandı. UNIX, parolaları gizlemek için tek yönlü karma algoritma (Crypt) kullanır. Bir dosyaya kopyalamak ve hızlı bir bilgisayarda bir cracker programı kullanarak şifreleri keşfetmek çok kolaydı. UNIX'in bazı sürümleri artık MD5 karma algoritmasını kullanıyor. Günümüzde çoğu sürüm, parolaları yalnızca kök hesabın erişebileceği bir gölge dosyasında tutar.

Şifre kırma için birçok şema var. Farklı parola kırma saldırı türleri arasında şunlar yer alır:

Dictionary Attack - bir sözlükte bulunan kelimelerin çoğunu içeren bir dosya kullanır
Brute Force - olası her harf, sayı ve özel karakter kombinasyonunu dener
Hybrit Attack - ekstra karakterleri sözlük sözcükleriyle birleştirir ve farklı kombinasyonlar dener

### İyi

Kuruluşların bir parola politikasına sahip olması ve bunu uygulaması zorunludur. Politikalar, kuralların ne olduğunu ve bilgisayar kullanıcılarından ne beklendiğini açıklar. Bir ilkeye sahip olmak, parola kurallarını tutarlı bir şekilde uygulamak için bir çerçeve de sağlar.

Güçlü bir parolanın özellikleri şunları içerir:

1. Minimum uzunluk altı-on karakter. Parola ne kadar uzun olursa, kırılması o kadar uzun sürer.
2. Şunlardan en az üçünü içermelidir: küçük harf alfa, büyük harf alfa, rakam ve özel karakter. Parolada ne kadar çok çeşitlilik olursa, kırılması o kadar uzun sürer.
3. Alfa, sayı ve özel karakterler karıştırılmalıdır. Parolanın sonuna yalnızca rakam eklemeyin.
4. "Sözlük" kelimeleri kullanmayın. Bu, ortak özel adların sözlüklerini ve yabancı dil sözlüklerini içerir. Ayrıca rakamların eklendiği "yaygın sözcüklerden" kaçının.
Diğer şifre politikası özellikleri şunları içerir:
5. Önceki beş şifreyi tekrar kullanmayın. Bazı kuruluşlar bir parolanın asla yeniden kullanılmamasını önerir.
6. Minimum şifre yaşı on gündür. Kullanıcıların önceki bir parolaya geri dönmesini engellemek için.
7. Maksimum şifre yaşı 45-60 gündür. Bu, bir bilgisayar korsanının şifreleri kırmasının ne kadar süreceği ile belirlenmelidir.
8. Üç beş başarısız oturum açma girişiminden sonra parolayı kilitleyin. Bu, bilgisayar korsanlarının farklı parola kombinasyonlarını denemek için bir program çalıştırmasını engeller.

# Debian'da Güçlü Bir Parola Politikası Nasıl Kurulur?

Gerekli paket kurulmalıdır.

```bash
apt install libpam-pwquality (şifre kalite kontrol paketi)
```

*Güçlü bir parola politikası oluşturmak için aşağıdaki gereksinimlere uymanız gerekir:*

- [ ]  Parolanızın süresinin her 30 günde bir dolması gerekir.
- [ ]  Parolanın değiştirilmesinden önce izin verilen minimum gün sayısı 2 olarak ayarlanacaktır.
- [ ]  Kullanıcı, şifresinin süresinin dolmasından 7 gün önce bir uyarı mesajı almalıdır.
- [ ]  Şifreniz en az 10 karakter uzunluğunda olmalıdır. Bir büyük harf ve bir rakam içermelidir. Ayrıca, 3'ten fazla ardışık özdeş karakter içermemelidir.
- [ ]  Parola, kullanıcının adını içermemelidir.
- [ ]  Aşağıdaki kural root şifresi için geçerli değildir: Şifre, önceki şifrenin parçası olmayan en az 7 karakterden oluşmalıdır.
- [ ]  Elbette root şifrenizin bu politikaya uygun olması gerekmektedir.

Parola Sona Erme için gün sayısını ayarlayın. Kullanıcıların şifrelerini gün içerisinde değiştirmeleri gerekmektedir. Bu ayar yalnızca bir kullanıcı oluşturulurken etkilenir, mevcut kullanıcıları etkilemez. Mevcut kullanıcılara uygulamak için, [chage -M (days) (user)] komutunu çalıştırın.

![141210102-4f733765-1e8d-48bf-af75-c55893b3a10a.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2a6a41e7-7fc1-4b63-a4f6-993bfe11bb92/141210102-4f733765-1e8d-48bf-af75-c55893b3a10a.png)

```bash
vim /etc/login.defs (şifre politikası için bu dosyayı düzenleyin)
```

![141209040-c9228ba5-eea4-4a1c-a38c-df445380e21a.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ff037925-1dfe-4d7f-bc5f-6a7496de7209/141209040-c9228ba5-eea4-4a1c-a38c-df445380e21a.png)

Parolanın kullanılabileceği minimum gün sayısını ayarlayın. Kullanıcılar şifrelerini değiştirdikten en az bu gün sonra kullanmalıdır. Bu ayar yalnızca bir kullanıcı oluşturulurken etkilenir, mevcut kullanıcıları etkilemez. Mevcut kullanıcılara ayarlamak için, [chage -m (days) (user)] komutunu çalıştırın.

![141210381-aab429af-895d-4826-86c1-336036a74388.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/49e7ded2-e394-47ec-b47c-2b744afb17bb/141210381-aab429af-895d-4826-86c1-336036a74388.png)

Minimum parola uzunluğunu ayarlayın. Kullanıcılar şifre uzunluklarını bu parametreden daha az ayarlayamazlar.

```bash
vim /etc/security/pwquality.conf (ayarlamak için bunu düzenleyin)
```

![141211611-18ebc508-b098-49a9-b8e1-ddb2a4b99e1a.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c36f5af-0f54-4ada-b5c2-ab3c1bd27868/141211611-18ebc508-b098-49a9-b8e1-ddb2a4b99e1a.png)

Yeni parolada en az bir büyük harf gerektir.

![141305935-28eda24c-4621-4a2c-9148-ddfe10db8403.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b0aa14b-bfc7-4686-bbc0-3c554fa80194/141305935-28eda24c-4621-4a2c-9148-ddfe10db8403.png)

Yeni parolada en az bir sayı olmasını zorunlu kılın.

![141212018-43fb81a9-263b-46e1-8fe9-7ae65f7b1b5f.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d71ea8b5-7f0f-4efe-bf9a-b1d03f3d83d1/141212018-43fb81a9-263b-46e1-8fe9-7ae65f7b1b5f.png)

Yeni parolada izin verilen maksimum ardışık aynı karakter sayısını ayarlayın.

![141212139-b069388a-8d6b-4979-8ce1-46d36a2fe8a5.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/875ff956-9228-4378-8612-fe0d55b8aab4/141212139-b069388a-8d6b-4979-8ce1-46d36a2fe8a5.png)

Kullanıcının passwd girişinin GECOS alanından 3 karakterden uzun kelimelerin yeni şifrede bulunup bulunmadığını kontrol edin.

Gecos alanı, Unix ve benzeri işletim sistemlerindeki /etc/passwd dosyasındaki her kaydın alanıdır. UNIX'te, bir kayıttaki 7 alanın 5'idir. Genellikle hesap veya kullanıcıları hakkında gerçek adları ve telefon numaraları gibi genel bilgileri kaydetmek için kullanılır.

![141298683-8cb025a5-8ea4-4284-ac5c-0800560e038a.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/de1d8da5-c8da-4d99-aa04-fb03dc255b49/141298683-8cb025a5-8ea4-4284-ac5c-0800560e038a.png)

![141306286-0fba9b9b-770c-4222-bad7-1cd802fc8755.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b9da9a75-86df-4790-aae6-5092971c8c71/141306286-0fba9b9b-770c-4222-bad7-1cd802fc8755.png)

Yeni parolada, eski parolada olmaması gereken karakter sayısını ayarlayın.

![141301300-e5dd496b-9b07-42d4-8880-c37eed43a519.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/900def8d-cbec-4ae1-9b8a-e3d5a82fa680/141301300-e5dd496b-9b07-42d4-8880-c37eed43a519.png)

Elbette root şifrenizin bu politikaya uygun olması gerekmektedir.

![141306669-2d77c501-551e-4a15-b4e5-a82c0f33a581.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cb7250c3-2f1b-4169-98e8-8d94d44a14b5/141306669-2d77c501-551e-4a15-b4e5-a82c0f33a581.png)

UYARI: Konfigürasyon dosyalarınızı kurduktan sonra, root hesabı da dahil olmak üzere sanal makine üzerinde bulunan tüm hesapların şifrelerini değiştirmeniz gerekecektir.

# Şifre Nasıl Değiştirilir ?

Bir kullanıcı adına şifre değiştirmek için önce oturum açın veya "root" hesabına "su" ile geçin Ardından,

 

```bash
passwd <username>
```

yazın (burada kullanıcı, değiştirmekte olduğunuz parolanın kullanıcı adıdır). Sistem sizden bir şifre girmenizi isteyecektir. 

Ayrıca passwd yazarak (bir kullanıcı adı belirtmeden) kendi şifrenizi değiştirebilirsiniz. Doğrulama için eski şifrenizi ve ardından yeni şifrenizi girmeniz istenecektir.

# Sudo Nasıl Kurulur ?

Sudo’yu kurmak için;

```bash
apt install sudo
```

# Sudo nedir ?

Sudo (bazen Super-user do'nun kısaltması olarak kabul edilir), sistem yöneticilerinin bazı kullanıcıların bazı komutları root (veya başka bir kullanıcı) olarak yürütmesine izin vermek için tasarlanmış bir programdır. Temel felsefe, mümkün olduğu kadar az ayrıcalık vermek ama yine de insanların işlerini yapmasına izin vermektir. Sudo ayrıca kimin hangi komutu ne zaman çalıştırdığını kaydetmenin etkili bir yoludur.

# Sudo Neden Kullanılır ?

Sudo kullanmak, aşağıdakiler de dahil olmak üzere çeşitli nedenlerle bir oturumu root olarak açmaktan daha iyidir (daha güvenlidir):

1. Kimsenin root şifresini bilmesine gerek yoktur (sudo mevcut kullanıcının şifresini ister).
2. Bireysel kullanıcılara geçici olarak ekstra ayrıcalıklar verilebilir ve daha sonra şifre değişikliğine gerek kalmadan geri alınabilir.
3. Sudo aracılığıyla yalnızca özel ayrıcalıklar gerektiren komutları çalıştırmak kolaydır; geri kalan zamanlarda ayrıcalıksız bir kullanıcı olarak çalışırsınız, bu da hataların neden olabileceği zararı azaltır.
4. Denetim/günlüğe kaydetme: bir sudo komutu yürütüldüğünde, orijinal kullanıcı adı ve komut günlüğe kaydedilir.

Debian'ın varsayılan yapılandırması, sudo grubundaki kullanıcıların herhangi bir komutu sudo aracılığıyla çalıştırmasına izin verir.

# Sudo Üyeliğini Kontrol Etmek

Bir kullanıcı olarak oturum açtıktan sonra, kullanıcının group=sudo'ya ait olup olmadığını

```bash
id
groups
```

 id veya groups komutlarını kullanarak doğrulayabilirsiniz.

### Mevcut kullanıcıyı komut satırından sudo’ya ekleme

id=kullanıcıadı olan mevcut bir kullanıcıyı group=sudo'ya eklemek için:

```bash
sudo adduser username sudo
```

Alternatif olarak, önce root’a geçilip (örneğin, sudo su -) ardından aynı komutları önek=sudo olmadan çalıştırabilirsiniz:

Yeni bir gruba eklendikten sonra, yeni grubun etkili olması için kullanıcının oturumu kapatması ve ardından tekrar oturum açması gerekir. Gruplar, yalnızca oturum açma sırasında kullanıcılara atanır. En yaygın kafa karışıklığı kaynağı, insanların kendilerini yeni bir gruba eklemeleri, ancak daha sonra oturumu kapatıp tekrar açmamaları ve ardından grup atanmadığı için sorun yaşamalarıdır; grup üyeliğini doğruladığınızdan emin olun.

# Grup Nasıl Yaratılır

“groupadd” komutu, komut satırında belirtilen değerler ile sistemdeki varsayılan değerleri kullanarak yeni bir grup hesabı oluşturur. Yeni grup gerektiği gibi sistem dosyalarına girilecektir.

# Kullanıcı Nasıl Yaratılır

useradd - yeni bir kullanıcı oluşturun veya varsayılan yeni kullanıcı bilgilerini güncelleyin

# Sudo Grubu Nasıl Yapılandırılır?

Sudoers ilkesi eklentisi, bir kullanıcının sudo ayrıcalıklarını belirler. Varsayılan sudo politikası eklentisidir. Politika, /etc/sudoers dosyası tarafından veya isteğe bağlı olarak LDAP'de yürütülür.

![141489375-505810eb-4f68-4b32-9c1f-e5cf4cdfac7f.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0f706044-e2bd-41ca-85f8-340536cf6585/141489375-505810eb-4f68-4b32-9c1f-e5cf4cdfac7f.png)

![141491250-19d9abbe-ea60-46c2-b58b-caa18968a311.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/728ee45a-3ff1-4581-a889-24ebb32f04ac/141491250-19d9abbe-ea60-46c2-b58b-caa18968a311.png)

# Visudo nedir ?

visudo, sudoers dosyasını güvenli bir şekilde düzenler. visudo, sudoers dosyasını birden fazla eşzamanlı düzenlemeye karşı kilitler, temel kontrolleri sağlar ve ayrıştırma hatalarını kontrol eder. Sudoers dosyası şu anda düzenleniyorsa, daha sonra tekrar denemek için bir mesaj alacaksınız.

*Sudo grubunuz için güçlü bir yapılandırma ayarlamak için aşağıdaki gereksinimlere uymanız gerekir:*

*Sudo kullanılarak yapılan kimlik doğrulama, yanlış parola durumunda 3 denemeyle sınırlandırılmalıdır.*

1. passwd_tries: Sudo başarısızlığı günlüğe kaydedip çıkmadan önce bir kullanıcının parolasını girme deneme sayısı. Varsayılan 3'tür.

*Sudo kullanılırken yanlış parola nedeniyle bir hata oluşursa, seçtiğiniz özel bir mesajın görüntülenmesi gerekir.*

1. baddpass_message: Bir kullanıcı yanlış bir parola girerse görüntülenen mesaj. Varsayılan Üzgünüz, tekrar deneyin şeklindedir. hakaretler etkinleştirilmedikçe.
    
    ![141497000-425bd100-8eea-4be2-9362-a109e90d0092.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/41627465-8357-4dbd-be10-9b6913b32e89/141497000-425bd100-8eea-4be2-9362-a109e90d0092.png)
    

*Sudo kullanan her eylem, hem girdiler hem de çıktılar olarak arşivlenmelidir. Günlük dosyası /var/log/sudo/ klasörüne kaydedilmelidir.*

![143683138-5ee3bc66-1175-43d2-bdc5-77de5b46e3a8.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f17e5d80-3ccd-451e-9b93-30170fa980ae/143683138-5ee3bc66-1175-43d2-bdc5-77de5b46e3a8.png)

*Güvenlik nedeniyle TTY modu etkinleştirilmelidir.*

1. requiretty: Ayarlanırsa, sudo yalnızca kullanıcı gerçek bir tty'de oturum açtığında çalışır. Bu bayrak ayarlandığında, sudo yalnızca bir oturum oturumundan çalıştırılabilir ve cron(8) veya cgi-bin betikleri gibi başka yollarla çalıştırılamaz. Bu bayrak varsayılan olarak kapalıdır

Requiretty ayarlandığında, sudo oturum açmış bir terminal oturumundan (bir tty) çalıştırılmalıdır. Bu, sudo'nun arka plan programlarından veya cronjobs veya web sunucusu eklentileri gibi diğer bağımsız işlemlerden kullanılmasını engeller. Ayrıca, bir terminal oturumu kurmadan doğrudan bir ssh çağrısından çalıştıramayacağınız anlamına da gelir.

Bu, belirli türdeki yükseltme saldırılarını önleyebilir. Örneğin, NOPASSWD sudo izinlerine sahip bir kullanıcı için crontab'ı değiştirmek için bir yolum varsa, bunu root olarak bir işi başlatmak için kullanabilirim. Requiretty ile bunu yapamam...

...kolayca. Bu kısıtlamayı aşmak özellikle zor değildir ve bu nedenle, bozduğu geçerli kullanım durumlarıyla karşılaştırıldığında genellikle o kadar da yararlı değildir. Red Hat bunu kullanırdı, ancak birkaç yıl önce kaldırdı.

*Güvenlik nedeniyle de sudo tarafından kullanılabilecek yollar kısıtlanmalıdır. Örnek: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin*

***Dosyanın son şekli bu şekilde olmalıdır***

![x.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ca459620-531d-48b9-b2fc-ee1ae2b391c2/x.png)

# Script nedir ?

Bir shell scriptii, tekrar tekrar kullandığınız bir komutlar dizisidir. Bu sıra genellikle komut satırına komut dosyasının adını girerek yürütülür. Alternatif olarak, cron özelliğini kullanarak görevleri otomatikleştirmek için scriptleri kullanabilirsiniz.

# Script Nasıl Yaratılır ?

Kabuk komut dosyası oluşturmak için düzenleyicinizde yeni bir boş dosya açın. Bununla birlikte, vim veya emacs gibi daha gelişmiş bir düzenleyici seçmek isteyebilirsiniz, çünkü bunlar kabuk ve Bash sözdizimini tanıyacak şekilde yapılandırılabilir ve parantezleri ve noktalı virgülleri unutmak gibi yeni başlayanların sıklıkla yaptığı hataları önlemede çok yardımcı olabilir. .

### Script’i hangi shell çalıştıracak ?

Bir scripti bir alt shellde çalıştırırken, scripti hangi kabuğun çalıştıracağını tanımlamanız gerekir. Komut dosyasını yazdığınız shell türü sisteminizde varsayılan olmayabilir, bu nedenle girdiğiniz komutlar yanlış shell tarafından yürütüldüğünde hatalara neden olabilir.

Komut dosyasının ilk satırı, başlatılacak kabuğu belirler. İlk satırın ilk iki karakteri #! olmalıdır, ardından takip eden komutları yorumlaması gereken shell giden yolu izler. Boş satırlar da satır olarak kabul edilir, bu nedenle betiğinize boş bir satırla başlamayın.

monitoring.sh #!/bin/bash komutuyla başlayacak

Daha önce belirtildiği gibi bu, Bash yürütülebilir dosyasının /bin içinde bulunabileceği anlamına gelir.

Bir dosyayı yürütülebilir yapmak için eXecutable bitini ayarlamanız gerektiğini ve bir kabuk komut dosyası için Okunabilir bitin de ayarlanması gerektiğini unutmayın:

*Sunucu başlangıcında, komut dosyası her 10 dakikada bir tüm terminallerde bazı bilgileri (aşağıda listelenmiştir) gösterecek bir script gerekiyor*

*Komut dosyanız her zaman aşağıdaki bilgileri görüntüleyebilmelidir:*

1. *İşletim sisteminizin mimarisi ve kernel versiyonu. (uname —all)*
2. *Fiziksel işlemci sayısı. ( Örneğin, kaç tane işlemciniz olduğunu öğrenmek için /proc/cpuinfo'da "fiziksel kimlik" dizesini içeren satırlara bakın. Bunu grep ile yakalayabilir ve ardından bu bilgiyi, bir sayım elde etmek için bunun gibi birkaç kullanışlı filtreden geçirebilirsiniz:*

```bash
grep "physical id" /proc/cpuinfo | sort | uniq | wc -l
```

Bu size sisteminizde kaç tane fiziksel işlemci olduğunu söyler, ancak kaç tane çekirdek olduğu veya sisteminizin hyper-threading kullanıp kullanmadığı hakkındaki soruları yanıtlamaz. Herhangi bir fiziksel kimliğin dosyada bir defadan fazla görünebileceğini unutmayın; bu nedenle, her birinin yalnızca bir kez sayıldığından emin olmak için o dizeyi (ör. "fiziksel kimlik : 0") içeren satırları sıralamak isteyebilirsiniz.

1. *Sanal işlemci sayısı. (İşlemcileriniz çok çekirdekli ise, kaç tane sanal işlemciniz olduğunu bilmeniz gerekir. "İşlemci" ile başlayan satırları arayarak bunları sayabilirsiniz.)*

```bash
grep "^processor" /proc/cpuinfo | wc -l
```

*İşlemcileriniz çok çekirdekli olduğundan, işlemcileriniz hiper iş parçacıklı olduğundan veya her ikisi birden olduğundan, fiziksel işlemcilerden daha fazla sanal işlemciniz olabilir. Ne kadar çekirdeğe sahip olduğunuzu söylemenin yolu, /proc/cpuinfo dosyanızda "işlemci çekirdeği" aramaktır. Bu satır her sanal işlemci için görünecektir. Gösterilen çekirdek sayısı, sanal işlemci sayısından azsa, sisteminiz çok iş parçacıklıdır.*

1. *Sunucunuzdaki mevcut kullanılabilir RAM ve yüzde olarak kullanım oranı.*

*free, çekirdek tarafından kullanılan arabellekler ve önbelleklerin yanı sıra sistemdeki toplam boş ve kullanılan fiziksel ve takas belleği miktarını görüntüler. Bilgiler /proc/meminfo ayrıştırılarak toplanır.*

```bash
free --mega | grep Mem | awk '{printf("Memory Usage: %i/%iMB (%.2f%%)\n", $3, $2, $3/$2*100}'
```

1. *Sunucunuzdaki mevcut kullanılabilir bellek ve yüzde olarak kullanım oranı.*

*df, her dosya adı bağımsız değişkenini içeren dosya sisteminde kullanılabilir disk alanı miktarını görüntüler. Herhangi bir dosya adı verilmezse, halihazırda bağlı olan tüm dosya sistemlerinde bulunan alan gösterilir.*

```bash
df --total --human-readable | grep "total" | awk '{printf("Disk Usage: %s\%s (%.1f%%)\n", $3, $2, $3/2*100)}'
```

1. *Yüzde olarak işlemcilerinizin mevcut kullanım oranı.*

```bash
top -bn1 | grep "%Cpu" | awk '{printf("CPU load: %.1f%%\n", (100.0-$8)%100)}'
```

*top programı çalışan bir sistemin dinamik gerçek zamanlı bir görünümünü sağlar. Sistem özeti bilgilerinin yanı sıra şu anda Linux çekirdeği tarafından yönetilen işlemlerin veya iş parçacıklarının bir listesini görüntüleyebilir.* 

*-n : Yineleme sayısı sınırı: -n sayı*

*Top'un sona ermeden önce üretmesi gereken maksimum yineleme veya çerçeve sayısını belirtir.*

1. *Son yeniden başlatmanın tarihi ve saati.*

```bash
who --boot | awk '{printf("Last boot: %s %s", $3, $4)}'
```

1. *LVM'nin aktif olup olmadığı.*

```bash
if [ $(lsblk | grep "lvm" | wc -l) -eq 0 ]; then echo "no"; else echo "yes"; fi
```

1. Etkin bağlantıların sayısı.

*ss soket istatistiklerini dökümü için kullanılır. Netstat'a benzer bilgilerin gösterilmesine izin verir. Diğer araçlardan daha fazla TCP ve durum bilgisi görüntüleyebilir.*

*-s, --summary*

*Özet istatistikleri yazdırın. Bu seçenek, çeşitli kaynaklardan özet alan soket listelerini ayrıştırmaz. /proc/net/tcp çözümlemesini zahmetli hale getirecek kadar çok sayıda yuva olduğunda kullanışlıdır.*

```bash
ss -s | grep "TCP:" | tr ',' ' ' | awk '{printf("Connections TCP : %s ESTABLISHED\n", $4)}'
```

1. *Sunucuyu kullanan kullanıcı sayısı.*

```bash
who --count
```

tüm oturum açma adları ve oturum açan kullanıcıların sayısı

```bash
who --count | grep "users" | tr '=' ' ' | awk '{printf("User log: %s\n", $3)}'
```

1. *Sunucunuzun IPv4 adresi ve MAC (Medya Erişim Kontrolü) adresi.*

```bash
hostname -I
```

*hostname sistemin geçerli ana bilgisayarını, etki alanını veya düğüm adını ayarlamak veya görüntülemek için kullanılan programdır. Bu adlar, ağ programlarının çoğu tarafından makineyi tanımlamak için kullanılır.*

```bash
-I, --all-ip-addresses
```

*Ana bilgisayarın tüm ağ adreslerini görüntüleyin. Bu seçenek, tüm ağ arayüzlerinde yapılandırılmış tüm adresleri numaralandırır. Geridöngü arabirimi ve IPv6 yerel bağlantı adresleri atlanmıştır. -i seçeneğinin aksine, bu seçenek ad çözümlemesine bağlı değildir. Çıktının sırası hakkında herhangi bir varsayımda bulunmayın.*

*MAC adresini bulmak için*

```bash
ip link | grep "ether" | awk '{print($2)}'
```

1. *Sudo programı ile yürütülen komutların sayısı.*

```bash
sudo ls var/log/sudo/00/00 | wc -l
```

# Cron Nedir ?

cron, planlanmış ve yinelenen komutları (her gün, her hafta, vb.) yürütmekten sorumlu arka plan programıdır.

Varsayılan olarak, tüm kullanıcılar görevlerin yürütülmesini planlayabilir. Böylece her kullanıcı, programlanmış komutları kaydedebilecekleri kendi crontab'ına sahiptir. crontab -e çalıştırılarak düzenlenebilir (içeriği /var/spool/cron/crontabs/user dosyasında saklanır).

# crontab nedir?

Bir crontab dosyası, genel formun cron(8) için yönergeler içerir: "bu komutu bu tarihte bu saatte çalıştır". Her kullanıcının kendi crontab'ı vardır ve herhangi bir crontab'taki komutlar, crontab'ın sahibi olan kullanıcı olarak yürütülür.

# Her 10 dakikada bir tüm terminallerde bazı bilgiler nasıl görüntülenir?

Crontab'ın her 10 dakikada bir görev çalıştırmasını sağlamak için aşağıdaki gibi yazabilirsiniz:

```bash
*/10 * * * * /path/to/script
```

/10, aralıklarla birlikte kullanılır. Örneğin, her saat başı komut yürütmeyi belirtmek için saat alanında 0-23/2 kullanılabilir. Yıldız işaretinden sonra adımlara da izin verilir, bu nedenle her iki saatte bir demek istiyorsanız */2 kullanın. Bu örnekte, her 10 dakikada bir komut yürütülmesini belirtmek için dakika alanında */10.

![144088241-0a2c0131-d4d0-40fd-9d8f-a5061c1bb259.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d5eb9420-ca53-4e0b-a200-ade31694b071/144088241-0a2c0131-d4d0-40fd-9d8f-a5061c1bb259.png)

# Komut dosyasını değiştirmeden nasıl kesilir?

Cron tarafından programlanan bir görevi iptal etmek için, crontab -e komutunu çalıştırın ve crontab dosyasındaki ilgili satırı silin.

---

# BİTTİ

---

# CHECK LIST

- [ ]  İlk makinenizi VirtualBox'ta (veya VirtualBox kullanamıyorsanız UTM'de) belirli talimatlar altında oluşturacaksınız. Ardından, bu projenin sonunda katı kurallar uygularken kendi işletim sisteminizi kurabileceksiniz.
- [ ]  Reponuzun içerisinde sadece signature.txt dosyası olacak ve içinde sanal makinenizin imzası bulunacak.
- [ ]  İşletim sistemi olarak Debian'ın en son kararlı sürümünü veya CentOS'un en son kararlı sürümünü seçmelisiniz. Sistem yönetiminde yeniyseniz, Debian şiddetle tavsiye edilir.
- [ ]  Sanal makinenizin ana bilgisayar adı, 42 ile biten oturum açma bilgileriniz olmalıdır (örneğin, ckarakus42). Değerlendirmeniz sırasında bu ana bilgisayar adını değiştirmeniz gerekecektir.
- [ ]  Root kullanıcıya ek olarak, kendi kullanıcı adınızla oturum açtığınız bir kullanıcının bulunması gerekir. // ckarakus
- [ ]  Diskinizin şifreli olması gerekir.
- [ ]  Kurulumda herhangi bir arayüz kurmamanız gerekir, eğer kurulursa 0 alırsınız
- [ ]  Lvm nedir ?
- [ ]  APPArmor nedir ? / Çalıştığı nasıl kontrol edilir ?
- [ ]  Mandatory Access Control (MAC) nedir ?
- [ ]  Paket Yöneticisi nedir / Apt ve Aptitude Arasındaki Farklar ?
- [ ]  SSH nedir ? / Port nasıl değiştirilir ?
- [ ]  İşletim sisteminizi UFW güvenlik duvarı ile yapılandırmanız ve böylece yalnızca 4242 numaralı bağlantı noktasını açık bırakmanız gerekir.
- [ ]  UFW nedir ? / Nasıl kurulur / Nasıl ayarlanır
- [ ]  Şifre politikası nedir / Güçlü Şifre politikası nedir / Nasıl uygulanır ?
- [ ]  Sudo'yu katı kurallara göre kurmanız ve yapılandırmanız gerekir.
- [ ]  Sudo nedir / Yararı nedir ?
- [ ]  Kullanıcı adı olarak oturum açtığınız bir kullanıcının user42 ve sudo gruplarına ait olması gerekir.
- [ ]  Grup nasıl yaratılır
- [ ]  Yeni kullanıcı nasıl yaratılır
- [ ]  Sudo nasıl ayarlanır
- [ ]  Script nedir / Nasıl yaratılır / Monitoring.sh’da neler gösteriliyor ?

# Önemli Komutlar

su - : root kullanıcıya geçer.

sudo service ufw status : ufw’nin durmunu kontrol eder.

sudo service ssh status : ssh’ın durumunu kontrol eder.

sudo service “servis ismi” restart : yazılan servisi yeniden başlatır.

find / -iname “dosya-ismi” : yazılan dosya ismini bulur ve konumunu döndürür.

uname -a : işletim sistemini gösterir.

sudo adduser “kullaniciadi” : kullanıcı ekler.

sudo deluser “kullaniciadi” : kullanıcı siler.

sudo chage -l "kulaniciadi” : kullanıcının şifre politikasını gösterir.

sudo deluser —remove-home “kullaniciadi” : kullanıcıyı ana diziniyle beraber kaldırır

sudo deluser —remove-all-files “kullaniciadi” : kullanıcıyı tüm dosyalarıyla beraber siler.

sudo addgroup “grupismi” : grup ekler.

sudo delgroup “grupismi” : grup siler.

groups “kullanıcı adı” : kullanıcının üye olduğu grupları gösterir.

compgen -u : Tüm kullanıcıları gösterir.

sudo hostnamectl : bilgisayar adını gösterir.

sudo hostnamectl set-hostname “hostismi” : host adını değiştirir.

lsblk : disk bölümlerini gösterir.

dpkg -l | grep “paketismi” : paket bilgilerini gösterir. Kurulu mu değil mi vs.

sudo ufw status : ufw kurallarını gösterir.

sudo ufw status numbered : ufw kurallarını numaralı gösterir, böylece silebilirsin.

sudo ufw allow 8080 : 8080 portunu kurallara ekler.

sudo ufw delete “numara” : belirtilen numaralı kuralı siler.

**sudo vim /etc/ssh/sshd_config : ssh config dosyasını vim ile açar, port göstermek için**

ssh kullaniciadi@127.0.0.1 -p 4242 : 4242 portundan 127.0.0.1 ağına kullanıcı adıyla ssh aracılığıyla bağlanmayı sağlar.

sudo crontab -e : crontab dosyasını açar.

sudo service cron stop : Cron’u dosyayı editlemeden durdurur.

sudo service cron start : Cron’u dosyayı editlemeden başlatır.

sudo service cron status : Cron durumunu gösterir.

# Önemli Dosyalar

login.defs : Şifre değiştirme günlerini ayarladığımız dosya.

common-password : Şifre politikası ayarladığımız dosya.

sudoers : Sudo yapılandırmasını yaptığımız dosya.

sudo.log : Sudo loglarının tutulduğu dosya.

sshd_config : Ssh yapılandırmasının tutulduğu dosya.

monitoring.sh : 10 dakikada 1 bilgi gösteren dosya.

crontab -e : bu komutla crontab dosyasına ulaşılır.