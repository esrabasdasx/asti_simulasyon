# 🚇 Ankara Metro Simülasyonu

Bu proje, Ankara'da bulunan metro istasyonları arasında **en hızlı** (A*) ve **en az aktarmalı** (BFS) yolları bulmayı sağlayan bir simülasyondur.

---

## 📌 Kullanılan Algoritmalar

### 🔹 BFS (En Az Aktarmalı Rota)
- **Amaç:** Bir istasyondan diğerine en az aktarma ile ulaşmak.
- **Kullanılan Veri Yapısı:** `collections.deque` (Kuyruk yapısı - FIFO)
- **Çalışma Prensibi:**
  1. Başlangıç istasyonu kuyruğa eklenir.
  2. Kuyruk boş olana kadar:
     - İlk eleman kuyruğun başından çıkarılır.
     - Eğer hedef istasyona ulaşıldıysa, rota döndürülür.
     - Komşu istasyonlar kuyruğa eklenir.
     - Eğer farklı bir hat gerekiyorsa, aktarma sayısı artırılır.
  3. Ulaşım mümkün değilse `None` döndürülür.

#### 📍 **Neden BFS?**
✅ En az aktarma için uygun bir seçimdir.  
✅ Büyük ölçekli metro ağlarında etkili çalışır.

---

### 🔹 A* (En Hızlı Rota)
- **Amaç:** Toplam seyahat süresini en aza indirmek.
- **Kullanılan Veri Yapısı:** `heapq` (Öncelik kuyruğu)
- **Çalışma Prensibi:**
  1. Başlangıç istasyonu öncelik kuyruğuna eklenir.
  2. Kuyruk boş olana kadar:
     - En düşük maliyetli istasyon seçilir.
     - Hedef istasyon bulunursa, rota ve süre döndürülür.
     - Komşuların toplam tahmini maliyeti hesaplanır ve kuyruğa eklenir.
  3. Hedef istasyon bulunamazsa `None` döndürülür.

#### 📍 **Neden A*?**
✅ **Heuristic** (tahmini mesafe) kullanarak verimli çalışır.  
✅ Trafik ve seyahat süresi gibi değişkenleri hesaba katabilir.

---

## 🔧 Örnek Kullanım

```python
metro = MetroAgi()
metro.istasyon_ekle("M1", "AŞTİ", "Mavi Hat")
metro.istasyon_ekle("K1", "Kızılay", "Kırmızı Hat")
metro.baglanti_ekle("M1", "K1", 5)

rota = metro.en_az_aktarma_bul("M1", "K1")
if rota:
    print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))

```

## ✅ Test Sonucu

```plaintext
**Giriş:** en_az_aktarma_bul("M1", "K1")

**Çıktı:** AŞTİ -> Kızılay
```

## 💡 Proje Geliştirme Fikirleri

- 🎨 **UI tasarımları** ile daha estetik bir görünüm sağlanabilir.
- ⏳ **Hangi durağa kaç dakika kaldığı** bilgisi eklenebilir.
- 🚇 **Alternatif hat önerileri** sunulabilir.
- 💰 **Farklı seferlerin ücretlendirilmesi** hakkında bilgilendirme eklenebilir.
- 🚦 **Mevcut metro doluluk bilgisi** eklenerek, kullanıcıların farklı toplu taşıma alternatiflerini değerlendirmesi sağlanabilir.
