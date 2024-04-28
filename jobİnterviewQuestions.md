# İş Görüşmesinde Çıkabilecek Sorular

## Val ile Val ın farkı nedir? (Kotlin)

## Bir multi-thread projede değişkenleri val olarak kullanmak mı var olarak kullanmak mı daha mantıklıdır?
Akademik camiyada var değişkenlerin val değişkenlere (normalde göz ardı edilebilir seviyede) daha performanslı olduğu söylenir.
Ama eğer bir multi-thread proje için konuşuacak olursak var değişken tanımladığımızda diğer parçacıkların o değişkenin değiştirilip değiştirilmediğini
sürekli kontrol etmesi gerekir ve bu işlem bir yerden sonra çok maliyetli bir hal alır. Bu yüzen val değişkenler kullanmak daha mantıklı olacaktır.
Anlatım: [Kekod Ders4: Kotlin | Basic Types - val vs var](https://youtu.be/-SopbTv37Us?t=2134)


## Bir class'ın üye değişkenini var olarak tanımlayıp değişkenin önündeki var kelimesini değiştirmeden değişkeni nasıl val yapabilirsiniz ?
Bunun yolu val olan değişkenin set değerini private yapmaktır. Örneğin;
```
// Kotlin

Class User{
    val name = "Burak"
    var surName = "Pehlivan"
        private set
}

fun testUser(){
val user = User()

user.name = "Ali"       // Direkt değer ataması ile değerini değiştiremeyiz çünkü name değeri val ve val değişkenler read-only değişkenlerdir.
user.surName = "Can"    // Değerini değiştiremeyiz çünkü değerini değiştirmemizi sağlayan set metodu erşişimimize açık değil (private)

}
```
Anlatım: [Kekod Ders4: Kotlin | Basic Types - how to convert var to val](https://youtu.be/-SopbTv37Us?t=2286)



## const val ile val arasındaki fark nedir?
Çok bilinenin aksine val değişkenler immutable değişkenler değildir. İmmutable değişken demek
değeri hiçbir zaman değişmeyen değişken demektir ama val değişkenlerin değeri aşağıdaki örnekteki gibi
değişen değerler alabilir.


```
// Kotlin

class Box{
    var width: Int = 0
    var height: Int = 0
    var lenght: Int = 0
    var usedSpace: Int = 0

    val availableSpace: Int
        get(){
        return (width * height * lenght) - usedSpace
    }

}

fun calculate () {
    val Box = Box()
    Box.width = 50
    Box.height = 20
    Box.lenght = 30
    Box.usedSpace = 10
    println(Box.availableSpace)  //çıktı: 2990

    Box.width = 20
    Box.height = 10
    Box.lenght = 10
    Box.usedSpace = 30
    println(Box.availableSpace)  //çıktı: 1970
}
```

eğer val değişken immutable olsaydı değeri hiçbir zaman değişmezdi ama parametrelere farklı değerler
girdiğim zaman farklı sonuçlar alabiliyoruz. Bu yüzden val değişkenler immutable değil read-only değişkenlerdir.
Anlatım için: [Kekod Ders4: Kotlin | Basic Types - val is read only not immutable](https://youtu.be/-SopbTv37Us?t=1665)

## `val number = null` kotlinde elimizde böyle bir kod var tipi hakkında ne söleyebilirsiniz
number değişkeni null değer olarak atanmıştır ve null değerin veri tipi belirtilmediği için
kotlin bunu "nothing" veri tipinde bir veri olarak kabul eder.


## Kotlinde === neyi kontrol eder


## Aşağıdaki kod neden bu çıktıyı vermiştir
```
// Kotlin

// 1. Durum
    val number: Int = 100
    val number1: Int? = number
    val number2: Int? = number
    println(number1===number2) //çıktı: ture

// 2. Durum
    val num: Int = 254
    val num1: Int? = num
    val num2: Int? = num
    println(num1===num2) // Çıktı: false
```

kotlinde sayısal değerlerin referans kontrolü yapıldığı zaman 2 değişkenin değeri birbirine eşit
ve byte değer aralığının içinde ise (-128, 127) kotlin yeni bir obje oluşturmadan iki değişkeni de
aynı objeye referans edecek şekilde ayarlar (1. Durum)

byte değer aralığının dışında iki değer atandığında ikisi için de ayrı obje oluşturulup ram'de ayrı eyr tutması sağlanır.
(2. Durum)

## ÇIKTILARIN TİPLERİ NE OLUR
``` 
// Kotlin

val longNumber = 2_100_000_000
val devidedNumber = 2_100_000
val resultNumber1 = longNumber * devidedNumber // işlem 1
val resultNumber2 = longNumber / devidedNumber // işlem 2

val longNumber2 = 1_000_000_000_000L
val devidedNumber2 = 1_000_000_000
val resultNumber3 = longNumber2 * devidedNumber2 // işlem 3
val resultNumber4 = longNumber2 / devidedNumber2 // işlem 4
val resultNumber5 = longNumber2 - devidedNumber2 // işlem 5
val resultNumber5 = longNumber2 - devidedNumber // işlem 6
```

çıktıların tipleri sonuçlara değil işlem yapılan değişkenlerin tipine bağlıdır.

İşlem1, işlem2 -> longNumber ve devidedNumber integer tipinde sayılar o zaman bu sayılarla
bir işlem yaptığımızda sonuç integer tipinde olacak (sonucun değerinin hangi tipin aralığına girdiğine bakılmaksızın)

işlem3, işlem4, işlem5 -> longNumber2 ve devidedNumber2 long tipinde sayılar o zaman bu sayılarla
bir işlem yaptığımızda sonuç long tipinde olacak (sonucun değerinin hangi tipin aralığına girdiğine bakılmaksızın)

işlem6 -> longNumber2 long tipinde ve devidedNumber integer tipinde o zaman bu sayılarla
bir işlem yaptığımızda sonuç long tipinde olacak.
Çünkü eğer işlem yaptığımız sayıların tipleri birbirinde farklı ise en geniş değer aralığına sahip tip sonucun tipi olacak.
(sonucun değerinin hangi tipin aralığına girdiğine bakılmaksızın)

Anlatım: [Kekod Ders4: Kotlin | Basic Types Part2 - Sayısal değişkenlerin etkileşimine göre oluşan tipler](https://youtu.be/U7FfC1NAGHI?t=7688)

## Toplama işleminde değer aralığı
- Eğer iki değişkenin de tipi aynı ise:
  - Değişken tipi int veya long ise sonucun tipi işlem yapılan değişkenin tipi olur. (sonucun değer aralığına bakmaksızın)
  - Değişkenin tipi int ya da long değil ise sonucun tipi integer olur.
- Eğer iki değişkenin tipi farklı ise:
  - Toplanan değişkenler arasında long bir değer var ise sonuç long tipinde olur.
  - Diğer durumlarda sonuç integer olur.

## Kodun Çıktısı nedir?
```
# Kotlin

var numberOne = 2
println("Değer: ${numberOne}")
println("Değer: ${numberOne++}")
println("Değer: ${numberOne}")
println("Değer: ${++numberOne}")
```
çıktı:
  Değer: 2
  Değer: 2
  Değer: 3
  Değer: 4

ilk print numberOne değişkeninin değerini yazdırır. çkt: 2
ikinci print numberOne değişkeninin değerini yazdırır ve sonra değeri bir arttırır. çkt: 2
üçüncü print numberOne değişkeninin değerini yazdırır. çkt: 3
dördüncü print numberOne değişkeninin değerini bir arttırır ve sonra yazdırır. çkt: 4

## Kotlinde + işareti ile plus operatörü aynı işi yapmakta. Peki hangi durumlarda + hangi durumlarda plus operatörü kullanılır?
Eğer işlem yapmak, bu soru özelinde toplamak, istediğimiz değişkenler nullable değişkenler ise operatörün simgesini değil fonksion halini kullanmamız gerekir.
Çünkü operator simgesi kullandığımızda nullable check yapamayız.

## Code Smells çözümü istemek
Bir kod verilerbilir ve "bu koddaki code smells'i çöz" denilebilir. Böyle sorularda genelde tekrar eden kodları tekrardan kurtarma beceriniz sorgulanır.

## Kotlinde infix fonksiyona neden default değer verilemez
infix fonksiyon kullanımı ```classAdı fonksiyonAdı parametreDeğeri``` şeklindedir. Eğer default değer atayabilseydik ```classAdı fonksiyonAdı``` şeklinde bir kullanım olurdu.
Ve bu kullanım class ve fonksiyon isimleri arasında boşluk bulunduğu için kodun anlaşılabilirliği tarafında sıkıntılar yaratacağı için default değer atama kullanılmıyor.