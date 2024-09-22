# Pusula_Abdullah_Dik

VERİ SETİ HAKKINDA

 0   Kullanici_id                            
 1   Cinsiyet                                
 2   Dogum_Tarihi                      
 3   Uyruk                                   
 4   Il                                      
 5   Ilac_Adi                                
 6   Ilac_Baslangic_Tarihi             
 7   Ilac_Bitis_Tarihi                
 8   Yan_Etki                            
 9   Yan_Etki_Bildirim_Tarihi       
 10  Alerjilerim                       
 11  Kronik Hastaliklarim               
 12  Baba Kronik Hastaliklari         
 13  Anne Kronik Hastaliklari             
 14  Kiz Kardes Kronik Hastaliklari     
 15  Erkek Kardes Kronik Hastaliklari     
 16  Kan Grubu                        
 17  Kilo                               
 18  Boy                            

 Değerlere baktığımızda içlerinde eksik değer olan sütunlar var. 
 
 1 int64 , 2 Float, 12 Object ve 4 tane de Datetime64 formatında sütunlarımız var.


Sonradan Verisetine: 
Yaş(Doğum tarihi-2022)
Kullanım Süresi(Gün) (İlaç toplam kaç gün kullanıldı?)
Yan_Etki_Tesir_Süresi (Gün) (Hasta İlacı kullanmaya başladıktan kaç gün sonra yan etki tesir etti)
VKİ(Vücut Kitle Endeksi) (Bu sütunu Kilo kategorisini elde etmek için oluşturdum)
Kilo Kategorisi  

(Zayıf: VKİ < 18.5 )

(Normal: 18.5 ≤ VKİ < 24.9 )

Kilolu: 25.0 ≤ VKİ < 29.9)

(Fazla Kilolu: 30.0 ≤ VKİ < 34.9)

(Obez (Sınıf 1): 35.0 ≤ VKİ < 39.9)

(Obez (Sınıf 2): 40.0 ≤ VKİ < 44.9)

(Morbid Obez (Sınıf 3): VKİ ≥ 45.0))


Ilac Kategorisi(İlaçların hangi alanda işe yaradıklarına dair bir kategori şekli.) 

gibi değişkenler ekleniyor.

Bu bulduğumuz değişkenler sayesinde bazı sütunlara ihtiyacımız olmadığı için dropluyoruz. Bunlar:

Dogum_Tarihi
Ilac_Baslangic_Tarihi
Ilac_Bitis_Tarihi
Yan_Etki_Bildirim_Tarihi

Bütün hastaların uyruğu Türkiye olduğundan Uyruk Sütununu da dropluyoruz.


İLAÇ İSİMLERİNİN ANALİZ İÇİN STANDARDİZE EDİLMESİ

Boş bir liste oluşturuyoruz: İlk adımda, elimizde ilaç isimlerini standart hale getirmek için boş bir liste açıyoruz. Bu listeye birazdan temizleyeceğimiz ilaç isimlerini ekleyeceğiz.

İlaç isimlerini sırayla ele alıyoruz: Daha sonra veri setimizdeki tüm ilaç isimlerine tek tek bakıyoruz. Her bir ilaç ismini alıp işliyoruz.

İlaç ismindeki gereksiz kısımları çıkarıyoruz: İlaç isimlerinin yanında genellikle dozaj (örneğin "500mg") veya form (örneğin "tablet") gibi ek bilgiler olabilir. Biz burada sadece ilacın adını almak istiyoruz. İlaç ismini boşluklardan bölüyoruz ve sadece ilk kısmını alıyoruz. Yani "aspirin 500mg tablet" yazıyorsa, sadece "aspirin" kısmını seçiyoruz.

Standart hale gelen ilaç ismini listeye ekliyoruz: Bu temizlediğimiz ilaç ismini, ilk adımda oluşturduğumuz boş listeye ekliyoruz. Böylece her ilaç ismini teker teker temizleyip listeye eklemeye devam ediyoruz.

Yeni listeyi veri setine ekliyoruz: Bütün ilaç isimlerini bu şekilde temizledikten sonra, elde ettiğimiz listeyi veri setimize yeni bir sütun olarak ekliyoruz. Bu yeni sütun artık standart hale gelmiş, sade ilaç isimlerini içeriyor.

Peki Neden Yapıyoruz?

Tutarlılık Sağlamak

Veriyi Analiz Etmeyi Kolaylaştırmak

Gereksiz Bilgiyi Kaldırmak

Hatalardan Kaçınmak

Sonuç olarak, bu işlemi yaparak veriyi sadeleştiriyor, daha tutarlı ve güvenilir hale getiriyoruz. Bu sayede, ilaç isimlerini daha rahat analiz edebilir ve veriden daha anlamlı sonuçlar çıkarabiliriz.


İLAÇLARIN KATEGORİZE EDİLMESİ

Her bir ilacın alanı neyse, bu alanlar üzerinden kategorize ediyoruz. Bu sayede, ilaçların hangi gruba dahil olduğunu görmek ve ilaçları gruplar halinde analiz etmek daha kolay hale geliyor.


KRONİK HASTALIK SÜTUNLARININ HER BİRİ İÇİN YAPILACAK İŞLEMLER

Model kurulurken modelin bu kısımları daha iyi anlaması için yaptığımız bu işlemde,'Kronik Hastaliklarim' sütununda belirtilen kronik hastalıkları ayrı sütunlara bölüyoruz ve her hastalık için kişinin o hastalığa sahip olup olmadığını 1 ya da 0 ile gösteriyoruz. Örneğin, "Kronik_HastalığımDiabet" gibi bir sütun oluşturulur ve bu sütun 1 (var) veya 0 (yok) değerlerini içerir. Bu, analiz yaparken hastalıkları daha kolay ve düzenli bir şekilde ele almayı sağlar.


LABEL ENCODER KULLANIMI

Burada da Kategorik sütunları, numerik değerlerle kodlayıp modele uygun hale getiriyoruz.(Yan_Etki,Kilo Kategorisi,Yaş Kategorisi,Ilaç Kategorisi,Kan Grubu,Alerjilerim,Il)


VISUAL EDA

Bu alanda kendi çapımda bazı analizler grafikler hazırladım.

CORR HEATMAP

Bu kod parçası veri çerçevesindeki sayısal sütunlar arasındaki korelasyonları hesaplayıp bir ısı haritası olarak görselleştirir. Her hücredeki değer, ilgili iki değişken arasındaki korelasyonu gösterir ve bu, veri analizi sırasında hangi değişkenlerin birbiriyle ilişkili olduğunu anlamak için oldukça faydalıdır.

Sonrasında ki grafiklerde İlaç Kategorileriyle Yan Etkiler arasında grafikler yaptım. En çok yan etki hangilerinde. Hangi yan etkiler hangi alandaki ilaçlarda daha çok çıkıyor? Gibi soruları cevaplamaya çalıştım grafiklerle.

Sonrasında Cinsiyetin kilo dağılımlarına baktım.

Elimden geldiğince veriyi model kurmaya hazır hale getirmeye çalıştım. Buraya kadar okuduysanız hepinize teşekkür ederim. İyi Çalışmalar
