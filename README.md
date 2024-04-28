Bu repoda sizlere geliştiricilerin kullandığı ve yazılım ekosistemine ait kavramları açıklıyorum. Repo sürekli güncellenecektir.
## İÇİNDEKİLER:
* 1. [Git](#Git)
* 2. [Bug (Hata)](#BugHata)
* 3. [Debug (Hata Ayıklama)](#DebugHataAyklama)
* 4. [Syntax (Söz Dizimi)](#SyntaxSzDizimi)
* 5. [Parametre](#Parametre)
* 6. [Cache](#Cache)
	* 6.1. [Cache'in faydaları:](#Cacheinfaydalar:)
	* 6.2. [Cache çeşitleri:](#Cacheeitleri:)
	* 6.3. [Cache'in dezavantajları:](#Cacheindezavantajlar:)
* 7. [Overload (Aşırı Yükleme)](#OverloadArYkleme)
	* 7.1. [Fonksiyonlarda Aşırı Yükleme:](#FonksiyonlardaArYkleme:)
	* 7.2. [operatör overload](#operatroverload)
* 8. [IDE (Integrated Development Environment)](#IDEIntegratedDevelopmentEnvironment)
* 9. [SSH](#SSH)
* 10. [command line (tekli çoklu dokümantasyon)](#commandlinetekliokludokmantasyon)
* 11. [technical debt (teknik borç)](#technicaldebtteknikbor)
* 12. [code smell](#codesmell)
* 13. [Shadow naming](#Shadownaming)
* 14. [JVM DİLLLER](#JVMDLLLER)
* 15. [Stand Alone Fonksiyonlar](#StandAloneFonksiyonlar)
* 16. [Native - Cross Platform uygulama geliştirme](#Native-CrossPlatformuygulamagelitirme)
* 17. [Best Practise](#BestPractise)
* 18. [Paralel Programlama](#ParalelProgramlama)
* 19. [Clint - clint development](#Clint-clintdevelopment)
* 20. [Backend](#Backend)
* 21. [Frontend](#Frontend)
* 22. [immutable mutable variable](#immutablemutablevariable)
* 23. [explicit inplicit](#explicitinplicit)
* 24. [Type inference (Tip Çıkarımı)](#TypeinferenceTipkarm)
* 25. [Type Conversion](#TypeConversion)
* 26. [primitive değişken, referans değşken ve nullable](#primitivedeikenreferansdekenvenullable)
* 27. [Boxed Unboxed veri tutma yöntemleri](#BoxedUnboxedveritutmayntemleri)
* 28. [unsigned değişken tipleri](#unsigneddeikentipleri)
* 29. [smart casting](#smartcasting)
* 30. [crash](#crash)
* 31. [Dummy data](#Dummydata)
* 32. [Deadlock Problem](#DeadlockProblem)
* 33. [Edge Case](#EdgeCase)
* 34. [bottlenack](#bottlenack)
* 35. [pitfall](#pitfall)
* 36. [defansive programming](#defansiveprogramming)
* 37. [Deprecated](#Deprecated)
* 38. [Garbage Collector](#GarbageCollector)
* 39. [row string](#rowstring)
* 40. [extention function](#extentionfunction)
* 41. [infix function](#infixfunction)
* 42. [API (Application Program interface)](#APIApplicationPrograminterface)
* 43. [İndent](#ndent)
* 44. [Scrum Metodolojisi](#ScrumMetodolojisi)
* 45. [Sprint](#Sprint)
* 46. [product increment(ürün artımenti)](#productincrementrnartmenti)
* 47. [Product Backlog](#ProductBacklog)
* 48. [Grooming Meeting](#GroomingMeeting)

## Git
Git, yazılım geliştirme alanında kullanılan bir **versiyon kontrol sistemi** (VCS) aracıdır.
Yazılım projelerindeki kodların geçmiş sürümlerini takip etme, değişiklikleri izleme ve
gerektiğinde eski sürümlere geri dönme imkanı sağlar.

**Git'in temel özellikleri şunlardır:**

- **Dağıtık Yapı:** Git, merkezi bir sunucuya bağlı değildir. Her geliştiricinin bilgisayarında kodların tamamının yer aldığı bir yerel depo (repository) bulunur. Bu sayede, internet bağlantısı olmadan da çalışmaya devam edebilirsiniz.
- **Versiyon Takibi:** Git, kodların her değişikliği için bir "commit" oluşturur. Bu commit'lar, tarih ve mesaj gibi bilgilerle birlikte saklanır. Böylece, kodların zaman içinde nasıl değiştiğini takip edebilirsiniz.
- **Branching (Dallanma):** Git, farklı özelliklere veya hataların düzeltilmesine yönelik olarak kod üzerinde aynı anda birden fazla değişiklik yapabilme imkanı sağlar. Bu değişiklikler "branch" (dal) olarak adlandırılır.  Ana kod üzerinde hata yapmadan yeni özellikler denenebilir.
- **Merge (Birleştirme):** Farklı branch'larda yapılan değişiklikleri birleştirme işlemine "merge" denir. Git, merge işlemini kolaylaştırıcı araçlar sunar.
- **Uzak Depolar (Remote Repositories):** Git, genellikle GitHub, GitLab gibi platformlarda yer alan uzak depolar ile de çalışır. Bu sayede, ekipteki diğer geliştiricilerle kod paylaşımı ve ortak çalışma kolaylaştırılır.

**Git'in faydaları:**

- **Kod Geçmişini Takip:** Git, kodların geçmiş sürümlerini takip etmeyi sağlar. Böylece, ihtiyaç duyulduğunda eski bir sürüme geri dönülebilir.
- **Ortak Çalışma:**  Git, birden fazla geliştiricinin aynı proje üzerinde birlikte çalışmasını kolaylaştırır.
- **Hata Düzeltme:**  Git, hataları kolayca bulup düzeltme imkanı sağlar. Yanlış bir commit'ı geri almak mümkündür.
- **Versiyon Kontrolü:**  Farklı versiyonlarda kod stabilitesini korumaya yardımcı olur.

## Bug (Hata)
Bir yazılımdaki hata veya kusurdur.
Bu hatalar, yazılımın işlevini bozabilir veya beklenmedik davranışlara yol açabilir.
Bug Çeşitleri:
- **Syntax error** (Sözdizimi hatası): Bu en basit hata türüdür. Programın yazım kurallarına (syntax) aykırı olması durumunda oluşur. Örneğin, bir noktalı virgül eksikliği veya yanlış yazılmış bir anahtar kelime syntax error'a neden olabilir.
- **Logic error** (Mantık hatası): Kod aslında çalışır durumda olabilir ancak programın mantığında bir hata varsa, yanlış sonuçlar üretebilir. Bu tür hataları bulmak daha zor olabilir.
- **Runtime error** (Çalışma zamanı hatası): Program çalışırken oluşan hatalardır. Örneğin, programın erişmeye çalıştığı bir bellek alanı yoksa veya bir sayısal işlem hata ile karşılaşırsa çalışma zamanı hatası oluşabilir.


## Debug (Hata Ayıklama)
Kodda bulunan hataları düzeltmek için yapılan işleme debug denir.  
Debugging sürecinin genel adımları:

1. **Hatanın belirlenmesi:** Programın beklenen şekilde çalışmadığını fark edersiniz. Hata mesajları varsa bunları inceleyin. 
2. **Hatanın yeniden üretilmesi:** Programı çalıştırarak hatayı tekrarlayın. Hata her zaman mı oluşuyor, yoksa belirli koşullarda mı oluşuyor? 
3. **Debugger kullanımı:** Bir debugger kullanarak programı adım adım çalıştırın. Değişkenlerin değerlerini izleyin ve hata nerede oluştuğunu belirlemeye çalışın. 
4. **Hatanın düzeltilmesi:** Hatanın nedenini bulduktan sonra, program kodunu düzeltin. 
5. **Kodun test edilmesi:** Programı tekrar test edin ve hatanın giderilip giderilmediğini kontrol edin. Gerekirse debugging döngüsüne geri dönün.


## Syntax (Söz Dizimi)
Syntax, bir programlama dilinin nasıl yazılması gerektiğini ve dilin nasıl yorumlanacağını belirleyen kurallarını ifade eder.
Tıpkı bir dilde cümlelerin kurallarla oluşturulması gibi, programlamada da kodlar belirli syntax kurallarına göre yazılır.
Farklı programlama dillerinin farklı syntaxları vardır. Örneğin:

_Python'da girilen sayı'nın pozitif, negatif ya da sıfır olduğunu tespit eden kod:_
```
# Python

firstNumber = int(input("Sayı Giriniz: "))
if firstNumber > 0:
    print(f"{firstNumber} pozitif bir sayıdır.")
elif firstNumber < 0:
    print(f"{firstNumber} negatif bir sayıdır")
else:
    print("Girilen sayı sıfırdır")
```
_C++ girilen sayı'nın pozitif, negatif ya da sıfır olduğunu tespit eden kod:_ 
```
// C++

#include <iostream>

int main() {
int firstNumber;
std::cout << "Sayı Giriniz: ";
std::cin >> firstNumber;

if (firstNumber > 0){
    std::cout << firstNumber << " pozitif bir sayıdır.";
}
else if(firstNumber < 0){
    std::cout << firstNumber << " negatif bir sayıdır.";
}
else{
    std::cout << "Girilen sayı sıfırdır";
}
    return 0;
}
```

Yukarıdaki 2 kod bloğu da birebir aynı işlevi yapmaktadır ama yazıldıkları diller dolayısıyla de syntaxları farklıdır.
Mesela C++ da şart yapılarında ```else if``` syntax'ı kullanılırken Python'da ```elif``` syntax'ı kullanılır.
Siz de yukarıdaki kodlara bakarak dillerin syntax farkını inceleyebilirsiniz.

## Parametre
Fonksiyon çağrılırken parantez içinde yazılan değerlerdir.
Bu değerler fonksiyonun işlevini yerine getirmesi için gerekli olan girdi (input) verileridir.
Fonksiyonlar parametreleri kullanarak işlerini gerçekleştirir ve gerekirse bir sonuç (output) döndürebilir.

```
# Python

def topla(x, y):    # topla fonksiyonu parametre olarak x ve y değerlerini alır.
  """
  İki sayıyı toplar ve sonucu döndürür.
  """
  return x + y

sonuc = topla(5, 3)  # Burada x yerine 5 ve y yerine 3 parametre olarak gönderilir.
print(sonuc)  # Bu kod 8 yazdıracaktır.

```


## Cache
Verileri geçici depolamak için kullanılan bir bellek alanıdır.
Cache, daha yavaş bir kaynaktan veri okuma ihtiyacını azaltarak performansı artırır.

Cache, genellikle daha hızlı bir bellek (örneğin RAM) ile daha yavaş bir bellek (örneğin sabit disk sürücüsü) arasındaki
aracı görevi görür. Sistem, bir veri parçasına erişmeye çalıştığında, önce cache'e bakar.
Eğer veri cache'de bulunuyorsa, hızlı bir şekilde cache'den okunur.
Eğer veri cache'de yoksa, o zaman yavaş olan ana bellekten (örneğin sabit disk) okunur ve aynı zamanda cache'e de kopyalanır.
Böylece, bir daha aynı veriye ihtiyaç duyulduğunda, daha hızlı bir şekilde cache'den erişilebilir.

### Cache'in faydaları:
- Hızlı performans: Cache, sıklıkla erişilen verileri depolayarak, bu verilerin daha hızlı bir şekilde okunmasını sağlar. Bu nedenle, özellikle web sayfaları, uygulamalar ve işletim sistemleri gibi sıklıkla aynı verilere erişen sistemlerde performans artışı sağlar.
- Azaltılmış veri transferi: Cache, sıklıkla erişilen verileri depolayarak, bu verilerin ana bellekten (örneğin sabit disk) tekrar tekrar okunması ihtiyacını azaltır. Bu, özellikle veri transferi bant genişliği sınırlı olan durumlarda faydalıdır.
### Cache çeşitleri:

- **CPU cache:** İşlemcinin içinde yer alan ve işlemci tarafından sıklıkla erişilen verileri depolamak için kullanılır.
- **Disk cache:** Sabit disk sürücüsünde yer alan ve sıklıkla erişilen disk bloklarını depolamak için kullanılır.
- **Web cache:** Web tarayıcılar ve web sunucularında bulunan cache'ler, sıklıkla ziyaret edilen web sayfalarının öğelerini (örneğin resimler, script dosyaları) depolamak için kullanılır.

### Cache'in dezavantajları:

- **Cache tutarsızlığı:** Veri hem cache'de hem de ana bellekte tutuluyorsa, bunların senkron tutulması gerekir. Aksi takdirde, okunan veri güncel olmayabilir.
- **Cache boyutu:** Cache sınırlı bir boyuta sahiptir. Bu nedenle, hangi verilerin cache'de tutulacağı konusunda strateji belirlemek gerekir.

Genel olarak, cache'in avantajları dezavantajlarından daha ağır basar. Cache kullanımı, bilgisayar sistemlerinin performansını önemli ölçüde artırır.

## Overload (Aşırı Yükleme)
Overload (Aşırı Yükleme) birden fazla fonksiyonun veya operatörün aynı adla ancak farklı parametreler veya
farklı geri dönüş değerleri ile tanımlanmasına izin veren bir özelliktir.
Bu özellik, kodun daha okunabilir, anlaşılır ve esnek olmasını sağlar.
### Fonksiyonlarda Aşırı Yükleme:
Fonksiyonlarda aşırı yükleme, aynı adlı fonksiyonların farklı sayıda veya türde [parametre](#parametre) almasına izin verir.
Bu sayede, aynı işlemi farklı veri türleri üzerinden gerçekleştirmek için farklı fonksiyonlar yazmak yerine
tek bir fonksiyonu farklı parametrelerle kullanabilirsiniz.
```


def topla(a, b):
    """
    İki sayıyı toplar.
    """
    return a + b

def topla(a, b, c):
    """
    Üç sayıyı toplar.
    """
    return a + b + c

print(topla(2,3))    # topla fonksiyonu iki parametre aldığı için 1. topla fonksiyonunu çalıştırır.
print(topla(5,4,8))  # topla fonksiyonu üç parametre aldığı için 2. topla fonksiyonunu çalıştırır.
```
### operatör overload
Operatör aşırı yüklemesi, bir operatörün (+, -, *, /, %) ve operatör fonksiyonunun (plus, minus, times, div, rem) farklı veri türleri için farklı anlamlar ve davranışlar tanımlamanıza olanak tanıyan bir özelliktir.





## IDE (Integrated Development Environment)
IDE Tümleşik Geliştirme Ortamı olarak türkçeye çevrilebilir.
IDE'lerin bazı temel özellikleri şunlardır:

- **Kod editörü:** Kod yazmak ve düzenlemek için kullanılan metin editörüdür. [Syntax](#syntax-s-z-dizimi) highlighting (kod vurgulama), otomatik tamamlama ve kod katlama gibi özellikleri sayesinde kod yazmayı kolaylaştırır.
- **Derleyici veya Yorumlayıcı:** Yazdığınız kodu çalıştırılabilir bir programa dönüştürür.
- **Debugger (Hata Ayıklama Aracı):** Kodunuzda [bug](#bug-hata) olup olmadığını bulmanıza ve [debugging](#debug-hata-ay-klama) yardımcı olur. Değişkenlerin değerlerini izleyebilir, programın adım adım nasıl çalıştığını görebilirsiniz.
- 
- **Kod Tamamlama:** Kod yazarken yazmaya başladığınız kelimeleri otomatik olarak tamamlama veya önerme özelliklerini içerir.
- **Sürüm Kontrol Sistemi Entegrasyonu:** Git veya SVN gibi sürüm kontrol sistemleriyle entegre olarak çalışır. Bu sayede kodunuzun geçmiş sürümlerine erişebilir ve değişiklikleri takip edebilirsiniz.
- **Dokümantasyon Araçları:** Yazdığınız kod için otomatik olarak dokümantasyon oluşturmanıza yardımcı olabilir.

## SSH

**SSH**, açılımı **Secure Shell** olan, ağ hizmetlerini güvenli olmayan bir ağ üzerinden güvenli bir şekilde çalıştırmak için kullanılan bir **kriptografik ağ protokolüdür**. En bilinen kullanım alanı bilgisayar sistemlerine **uzaktan oturum açmak** içindir.

**SSH'nin Faydaları:**

* **Güvenlik:** SSH, tüm iletişimi şifreleyerek kullanıcı adları, parolalar ve diğer hassas bilgilerin ele geçirilmesini engeller.
* **Uzaktan Erişim:** SSH, herhangi bir yerden bir bilgisayara veya sunucuya güvenli bir şekilde bağlanmanızı sağlar.
* **Çok Yönlülük:** SSH, dosya aktarımı, port yönlendirme ve daha fazlası gibi çeşitli amaçlar için kullanılabilir.

**SSH Nasıl Çalışır?**

SSH, bir **SSH istemcisini** bir **SSH sunucusuna** bağlayarak **istemci-sunucu mimarisi** çerçevesinde güvenli bir kanal oluşturur. Bağlantı kurulduğunda, tüm iletişim **şifrelenir** ve **kimlik doğrulanması** yapılır.

**Yaygın SSH Kullanımları:**

* **Uzaktan Komut Satırı Girişi:** Bir bilgisayara veya sunucuya uzaktan bağlanmak ve terminal komutları çalıştırmak için.
* **Dosya Aktarımı:** Bilgisayarlar arasında güvenli bir şekilde dosya kopyalamak için.
* **Port Yönlendirme:** Bir bilgisayarda çalışan bir hizmete uzaktan erişmek için.
* **Güvenli Tunneling:** Güvenli olmayan bir ağ üzerinden güvenli bir bağlantı kurmak için.

**SSH Hakkında Ek Bilgiler:**

* **Varsayılan SSH bağlantı noktası 22'dir.**
* **OpenSSH**, en popüler SSH uygulama paketidir.
* **SSH anahtarları**, parolasız kimlik doğrulama için kullanılabilir.
* **SSH, birçok işletim sistemi tarafından desteklenmektedir.**

Umarım bu bilgiler SSH hakkında genel bir fikir vermiştir.

**SSH hakkında daha fazla bilgi edinmek isterseniz, lütfen aşağıdaki kaynaklara bakın:**

 
## command line (tekli çoklu dokümantasyon)
Her fonksiyona yazılmaz karmaşık olabilecek fonksiyonlara eklemek daha doğru olur
## technical debt (teknik borç)
 
## code smell
Yazılan koda bakıldığında daha iyisini de yazabileceğinin düşünülmesi durumudur.
tekrarlanan kod satırlarıyla karşılaşılması gibi durumlarda code smell durumu olabilir.

## Shadow naming
shadow naming genellikle bir değişken, sınıf, veya fonksiyon isminin başka bir değişken, sınıf, veya fonksiyon ismiyle örtüşmesi durumunu ifade eder.
Bu örtüşme genellikle aynı kapsam içinde (örneğin, aynı blokta, aynı sınıfta) gerçekleşir. Örtüşen isimler birbirlerini gizler (gölgelendirir) ve bu durum programın beklenmedik davranışlarına sebep olabilir.
## JVM DİLLLER

## Stand Alone Fonksiyonlar

## Native - Cross Platform uygulama geliştirme 

## Best Practise

## Paralel Programlama

## Clint - clint development

## Backend 
Backend, bir web sitesinin veya uygulamanın kullanıcı arayüzünden (front-end) ayrı olan ve sunucuda çalışan kısmıdır.
Veri tabanı yönetimi, sunucu tarafı mantığı ve iş işleme gibi görevlerden sorumludur.
NodeJs, C#(ASP.NET), PHP, Java gibi diller kullanılır.

## Frontend
Frontend, bir web sitesinin veya uygulamanın kullanıcının gördüğü ve direkt olarak etkileşimde bulunduğu kısmıdır.
Frontend genelde HTML (Programlama dili değil işaretleme dilidir), CSS ve JavaScript ile yazılır. Ek olarak Figma, Sketch gibi
IU/UX tasarım araçları da kullanılır.

## immutable mutable variable

## explicit inplicit

## Type inference (Tip Çıkarımı)
Bir değişken tipinin eşitliğin sağ tarafındaki değere bakarak belirlenmesi işlemine type inference denir.
Eğer sayısal değerler için verilen değer integer değer aralığının (-2^31 , +2^31) içinde ise type inference integer değeri atar.
aralığın dışında ise long veri tipi belirlenir.

# explicit type conversion - inplicit type conversion
explicit type conversion örtülü bir şekilde tip dönüşümü yapmaktır.
```
// Java

val number: Int = (Int)3L
// Bu kodda 3L ifadesi long bir değer (3.0) ve "(Int)" fonksiyonu ile bu long değeri integer bir değere dönüştürüp
// integer bir değere atayabildik. Bu bir explicit type conversion örneğidir.


int ıntValue = 3
double doubleValue = 3.0
float floatValue = 3.0
long longValue = 3
short shortValue = 3
byte byteValue = 3

static void getValue(int value){
pass
}

// getValue fonksyionuna parametre olarak yukarıda tanımladığımız bütün değerler gelebilir.
// Java bu değerleri otomatik olarak int'e dönüştürür. (explicit type conversion)
```

inplicit type conversion





## Type Conversion

## primitive değişken, referans değşken ve nullable

## Boxed Unboxed veri tutma yöntemleri

## unsigned değişken tipleri

## smart casting

## crash

## Dummy data

## Deadlock Problem
iki veya daha fazla işlemin karşılıklı olarak birbirlerinin kilitlediği kaynaklara erişmek istemesiyle oluşur.
Her iki işlem de sürekli birbirlerini beklediği için sistem kaynakları olumsuz yönde etkilenir.

## Edge Case

## bottlenack

## pitfall

## defansive programming

## Deprecated

## Garbage Collector

## row string

## extention function

## infix function

## API (Application Program interface)
Uygulama Programlama Araüyüz demektir. Farklı yazılımların birbirleriyle iletişim kurmasına
ve bilgi paylaşmasına olanak tanıyan bir dizi kural ve tanımlamadır.

## İndent
Kodda satırın solunun sayfanın sonuna uzaklığını ifade eden terimdir. Genelde 1 tab (4 boşluk) indent verilir.
```
for (int=5 ; i<=100; i++){
    if (i == 20){   // indet1
        print("20 ye ulaştınız.") //indent2
    }
}
```
## Scrum Metodolojisi
Scrum, projelere esneklik ve uyumluluk kazandırarak hızlı ve yüksek kaliteli ürün geliştirmeyi amaçlayan bir Agile (çevik yazılım geliştirme) metodolojidir.


- **Kısa ve tekrarlayan döngüler:** Scrum, [sprint](#sprint) adı verilen kısa ve tekrarlayan döngüler halinde çalışır.
- **Kendi kendini organize eden ekipler:** Scrum, ekiplerin kendi kendini organize etmesine ve nasıl çalışacağını kendisinin belirlemesine olanak tanır.
- **Ürün odaklılık:** Scrum, ürünün geliştirilmesine ve müşterinin ihtiyaçlarını karşılamasına odaklanır.
- **Şeffaflık:** Scrum, tüm paydaşların projenin ilerlemesini takip edebilmeleri için şeffaf bir çalışma ortamı sağlar.
- **Uyarlanabilirlik:** Scrum, değişen ihtiyaçlara ve koşullara hızlı bir şekilde uyum sağlayabilir.


## Sprint
Kısa ve sabit zaman dilimleri içerisinde tamamlanması planlanan iş kümelerini ifade eder.

Sprintlerin temel özellikleri:

- **Sabit sürelidir:** Sprint'lerin süresi önceden belirlenir ve genellikle değiştirilmez. Bu, zaman yönetimini ve öngörülebilirliği sağlar.
- **Odaklıdır:** Her sprint'te, [product backlog](#product-backlog)'dan seçilen belirli bir iş kümesi üzerinde çalışılır. Bu, ekibin odaklanmasını ve sprint hedeflerine ulaşma ihtimalini artırır.
- **Takımdır:** Sprint'ler boyunca Scrum ekibi birlikte çalışır. Her gün kısa bir scrum toplantısı yapılarak sprintin durumu değerlendirilir ve sorunlar çözülür.
- **Teslim odaklıdır:** Sprint sonunda, potansiyel olarak kullanılabilir bir ürün artımenti (product increment) ortaya çıkarılmalıdır. Bu artıment, sprint boyunca tamamlanan işlerin çalışır bir parçasıdır.

## product increment(ürün artımenti)
Bir sprint süresince tamamlanan ve kullanılabilir potansiyeli olan bir ürün parçasıdır.
Product increment'in temel özellikleri:

- **Potansiyel olarak kullanılabilir:** Product increment, müşteriler veya kullanıcılar tarafından test edilebilecek ve geri bildirim alınabilecek durumda olmalıdır.
- **Ürüne değer katar:** Her sprint sonunda ortaya çıkan product increment, ürünün değerini artırır ve kullanılabilirliğini genişletir.
- **Şeffaflık sağlar:** Product increment, projenin ilerlemesini ve sprint hedeflerinin ne kadarının tamamlandığını gösteren somut bir kanıt niteliğindedir.
- **Uyarlanabilir:** Scrum metodolojisinin temel ilkelerinden biri olan uyarlanabilirliği destekler. Sprint sonunda elde edilen product increment, değişen ihtiyaçlara veya geri bildirimlere göre sonraki sprintlerde güncellenebilir ve geliştirilebilir.

Product increment'in faydaları:

- **Hızlı geri bildirim:** Sprint sonunda ortaya çıkan product increment sayesinde, müşterilerden ve kullanıcılardan erken aşamada geri bildirim almak mümkündür. Bu geri bildirimler, sonraki sprintlerde ürünün daha doğru bir şekilde geliştirilmesine yardımcı olur.
- **Motivasyon:** Scrum ekibi, sprint sonunda çalışan bir ürün artımenti ortaya koyarak motivasyonlarını ve iş tatminlerini artırabilir.
- **Risk yönetimi:** Sprint sonunda elde edilen product increment, potansiyel sorunların veya hataların erken tespit edilmesine ve çözülmesine yardımcı olur.
- **Şeffaf proje yönetimi:** Product increment, projenin ilerlemesini şeffaf bir şekilde ortaya koyarak tüm paydaşımların proje durumunu takip etmelerini sağlar.

Product increment nasıl oluşturulur:

- Sprint boyunca Scrum ekibi, product backlog'dan seçilen user story'ler ("kullanıcı nasıl yapardı" diye düşünmek) üzerinde çalışır.
- Sprint sonunda, tamamlanan user story'lerden oluşan bir bütün, product increment'i oluşturur.
- Product increment, test edildikten ve onaylandıktan sonra kullanıma sunulabilir veya bir sonraki sprintte geliştirilmeye devam edilebilir.



## Product Backlog
Aigle metodolojilerinde yapılması gereken tüm işlerin önceliklendirildiği bir listedir. Bu liste, bir nevi ürünün yapılacaklar listesidir ve ürünün geliştirilmesi boyunca sürekli olarak güncellenir.

## Grooming Meeting
Ürünü hazırlarken çalışılan aşama bittikten sonra diğer aşamada nasıl bir yol izleneceğini planlamak, işlem önceliklerini belirlemek
, [product backlog](#product-backlog) güncellemesi yapmak gibi ön hazırlıklar için yapılan toplantılardır. Grooming Meeting'lere "[Sprint](#sprint) planlama toplantısı" da denir.
