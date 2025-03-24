## Metro Simülasyonu

#Ankara'da bulunan çeşitli istasyonların en hızlı (A*) ve en az aktarmalı (BFS) olacak şekilde arama algoritmaları ile belirtilmesi 

## KULLANILAN ALGORİTMALAR

# Bu projede kullanılan algoritmalar: 

#heapq: A* algoritmasında en hızlı yolu bulmak için kullanılmıştır. 

#collections.deque: BFS algoritmasında kuyruk yapısında en az aktarmalı yolu bulmak için kullanılmıştır.




## ALGORİTMALARIN ÇALIŞMA MANTIĞI 

# BFS (EN AZ AKTARMALI)

- Bu algoritma, en az aktarma ile bir istasyondan diğerine ulaşmayı sağlamaktadır. 

Algoritma basamakları: 

1. Başlangıç istasyonu kuyruğa eklenir

2. Kuyruk boş olasıya kadar işlemler tekrar eder:
	- Kuyruğun başındaki ilk giren kuyruk (FIFO mantığına göre) çıkar.
	- Eğer hedef olan istasyon bulunursa rota döndürülür. 
	- Diğer istasyonların kontrolü sağlanır. 
		- Aynı hat üzerindeki istasyonlar direkt eklenir.
		- Farklı bir hata geçiş lazımsa aktarma sayısında artış gerçekleştirilir.

3. Eğer hedef istasyona ulaşılamazsa None olarak değer döndürülür.


## NEDEN BFS ?

- Aktarma sayısını en az düzeyde tutmak için doğru bir tercih.
- Graph yapılarında kullanımı verimlidir.




# A* (EN HIZLI ROTA)

- Bu algoritma toplam seyahat süresini en aza indirmek için için A* arama algoritmasını kullanır.

Algoritma basamakları: 

1. Öncelik kuyruğu kullanılarak istasyonlar yönetilir.

2. Rotanın başlangıç istasyonu kuyruğa eklenir.

3. Kuyruk boş olana kadar belirtilen işlemler tekrar edilir.
	- En düşük maliyetli (f_score) istasyon çıkartılır.
	- Eğer hedef istasyon bulunursa, rota ve toplam süre döndürülür.
	- Komşuların toplam tahmini maliyet(f_score) ve gerçek mesafe(g_score) değerleri hesaplanır ve kuyruğa eklenir.

4. 	Eğer hedef istasyona ulaşılamazsa None döndürülür. 


## NEDEN A* ?

- Tahmini mesafe (heuristic) kullanılarak daha verimli çalışır.
- Trafik ve yolculuk süresi gibi birçok değişken hesaba katılabilir.




# ÖRNEK KULLANIM 


metro = MetroAgi()
metro.istasyon_ekle("M1", "AŞTİ", "Mavi Hat")
metro.istasyon_ekle("K1", "Kızılay", "Kırmızı Hat")
metro.baglanti_ekle("M1", "K1", 5)

rota = metro.en_az_aktarma_bul("M1", "K1")
if rota:
    print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))


# TEST SONUÇLARI

Giriş: en_az_aktarma_bul("M1", "K1")

Çıktı: AŞTİ -> Kızılay





# PROJE GELİŞTİRME FİKİRİ

Bu projeyi görsel açıdan daha estetik hale getirmek adına UI tasarımları yapılabilir.

Belki hangi durağa kaç dakika kaldığı ya da alternatif olarak kullanılanilecek başka yol hattı gibi özellikler eklenebilir. 

Ek olarak eğer farklı seferlerin ücretleri farklıysa bu konu ile ilgili de bir bilgilendirme içeriği oluşuturulabilir. 

O an metronun mevcut doluluğu gibi bilgilendirmelere yer verilebilir. Bu sayede insanlar başka toplu taşıma kullanma ihtimalini de göz önünde bulundurabilirler.





































