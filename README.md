# İran–İsrail Çatışmasında Deepfake ve Yanlış Bilgi Yayılımının Sosyal Ağ Analizi

> Sosyal medya hesapları arasındaki hashtag bağlantıları üzerinden deepfake ve yanlış bilgi yayılımının ağ teorisi yöntemleriyle incelenmesi.

---

## İçindekiler

- [Proje Hakkinda](#proje-hakkinda)
- [Veri Seti](#veri-seti)
- [Kurulum](#kurulum)
- [Kullanım](#kullanım)
- [Analiz Adımları](#analiz-adımları)
- [Görseller](#görseller)
- [Sonuçlar](#sonuçlar)
- [Gereksinimler](#gereksinimler)
- [Proje Yapısı](#proje-yapısı)

---

## Proje Hakkinda

Bu proje, İran–İsrail çatışması bağlamında çeşitli sosyal medya platformlarından (Twitter/X, Instagram, TikTok vb.) toplanan herkese açık içerikleri sosyal ağ analizi yöntemleriyle incelemektedir.

İçerikler dört sınıfa ayrılmıştır:
- **Deepfake / Yanlış bilgi** – doğrulanmamış, yanıltıcı içerik
- **Kanıtlanmış deepfake** – sahte olduğu doğrulanmış içerik
- **Doğru bilgi** – güvenilir ve doğrulanmış içerik
- **Eski bilginin yanlış bağlamda paylaşılması** – gerçek ama yanlış bağlamda sunulan içerik

Bu içerikler, **platform**, **hesap**, **hashtag** ve **etiket** ilişkileri üzerinden bir sosyal ağ yapısına dönüştürülmüş; merkeziyet ölçümleri ve topluluk analizi ile yanlış bilgi yayılımının ağ içindeki yapısı ortaya konmuştur.

---
## Veri Seti

| Özellik | Açıklama |
|--------|----------|
| Dosya | `İranİsraelWarDataset.csv` |
| Konu | İran–İsrail çatışmasıyla ilgili sosyal medya paylaşımları |
| Alanlar | `account_name`, `platform`, `hastags`, `views`, `likes`, `shares`, `comments`, `possible_label` |
| Ön işleme | Sayısal sütunlar temizlendi; platform bazında z-skoru standardizasyonu uygulandı |

---

## Kurulum

```bash
# Depoyu klonlayın
git clone https://github.com/kullanici_adi/repo_adi.git
cd repo_adi

# Gerekli kütüphaneleri yükleyin
pip install networkx matplotlib pandas numpy scipy python-louvain seaborn plotly
```

Jupyter Notebook ortamında çalıştırmak için:

```bash
jupyter notebook social_network_analysis_standardized.ipynb
```

---

## Kullanım

1. `İranİsraelWarDataset.csv` dosyasının notebook ile aynı dizinde bulunduğundan emin olun.
2. Notebook'u açın: `social_network_analysis_standardized.ipynb`
3. Tüm hücreleri sırasıyla çalıştırın (Kernel → Restart & Run All).

---

## Analiz Adımları

### 1. Keşifsel Veri Analizi (EDA)
- Platformlara göre gönderi dağılımı
- İçerik etiketlerine göre dağılım
- Platform × etiket çapraz analizi ve ısı haritası
- En sık kullanılan 20 hashtag

### 2. Ağ Modelleme — G = (V, E, W)
- **Düğümler (V):** Sosyal medya hesapları
- **Kenarlar (E):** Ortak hashtag kullanımı
- **Ağırlıklar (W):** Ortak hashtag sayısı × standartlaştırılmış etkileşim skoru ortalaması
- Ağ türü: Yönsüz (undirected), ağırlıklı (weighted)

### 3. Temel Ağ Ölçütleri
- Düğüm/kenar sayısı, yoğunluk, ortalama derece
- Kümelenme katsayısı, ağ çapı, ortalama en kısa yol
- Bağlı bileşen analizi

### 4. Derece Dağılımı Analizi
- Histogram ve log-log grafik ile power-law dağılım incelemesi

### 5. Merkezilik Analizi

| Ölçüt | Anlamı |
|-------|--------|
| Degree Centrality | En çok bağlantıya sahip hesaplar |
| Betweenness Centrality | Bilgi akışında köprü rolündeki hesaplar |
| Closeness Centrality | Ağa en hızlı erişen, en hızlı yayıcı hesaplar |
| Eigenvector Centrality | Etkili hesaplara bağlı, dolayısıyla güçlü hesaplar |
| PageRank | Ağ içindeki otorite/önem skoru |

### 6. Topluluk Analizi (Louvain Algoritması)
- Modülarite tabanlı topluluk tespiti
- Topluluk başına deepfake içerik oranı
- Platform dağılımı ve içerik profili

### 7. Dayanıklılık Analizi
- Hedefli kaldırma (merkezi düğümler) vs. rastgele kaldırma
- Ağın kırılganlık noktaları
- Farklı saldırı stratejilerinin karşılaştırması

---

## Görseller

`görseller/` klasöründe aşağıdaki analizlere ait görselleştirmeler yer almaktadır:

| Görsel | Açıklama |
|--------|----------|
| `İran_israil_Çatışması_Sosyal_Medya_Hesap_Ağı` | Genel ağ yapısı |
| `NetworkX_Ag_Gösterimi` | NetworkX ile ağ gösterimi |
| `Derece_Dağılımı_Analizi` | Derece dağılımı histogramı |
| `Merkezilik_ölçütlerine_Göre_Ağ_Görselleştirmesi` | Degree / Betweenness / Closeness / Eigenvector |
| `Betweenness_Centrality_Haritası_Köprü_Hesaplar` | Köprü hesapların ağ üzerindeki konumu |
| `Louvain_Topluluk_Analizi` | Topluluk yapısı |
| `Topluluklara_Göre_Renklendirilmiş_Ağ` | İlk 180 merkezi düğüm |
| `Topluluk_Başına_Deepfake_İçerik_Oranı` | Toplulukların içerik profili |
| `Hashtag_Eş_Görünüm_Ağı` | Birlikte kullanılan hashtag ilişkileri |
| `İçerik_Etiketi_Bazlı_Ağ` | Ağ üzerinde içerik türü dağılımı |
| `Platform_Bazlı_Ağ` | Platform bazında ağ yapısı |
| `Yanlış_Bilgi_vs_Doğru_Bilgi_Ağdaki_Konum` | Yanlış bilgi ile doğru bilginin ağdaki konumu |
| `Ağ_Dayanıklılık_Analizi` | Hedefli vs. rastgele düğüm kaldırma |
| `Platformlara_Göre_Gönderi_Dağılımı` | EDA: Platform dağılımı |
| `Etiketlere_Göre_İçerik_Dağılımı` | EDA: İçerik etiket dağılımı |
| `En_Sık_Geçen_20_Hashtag` | EDA: Hashtag frekansı |
| `Plafform_ve_Etiket_İlişkisi` | Platform × etiket çapraz analizi |
| `Plafform_Etiket_Isı_Haritası` | Isı haritası görselleştirmesi |

---

## Sonuçlar

- Yanlış bilgi ve deepfake içerikler ağ içinde **rastgele dağılmamakta**; belirli hesaplar, topluluklar ve merkezi bağlantılar etrafında yoğunlaşmaktadır.
- Yüksek **betweenness** ve **weighted degree** değerine sahip hesaplar, hem güçlü etkileşim bağlantılarına sahip olmaları hem de farklı topluluklar arasında geçiş noktası oluşturmaları nedeniyle bilgi yayılımında kritik konumdadır.
- Topluluk analizinde bazı **TikTok ve Instagram** ağırlıklı topluluklarda riskli içerik oranlarının diğerlerine kıyasla daha yüksek olduğu görülmüştür.
- Dayanıklılık analizi, **rastgele hesap kaldırmanın** ağı sınırlı etkilediğini; buna karşın **merkezi veya köprü hesapların** kaldırılmasının ağı çok daha hızlı parçaladığını ortaya koymuştur.

---

## Gereksinimler

```
networkx
matplotlib
pandas
numpy
scipy
python-louvain
seaborn
plotly
```

Python 3.8 veya üzeri önerilir.

---

## Proje Yapısı

```
.
├── social_network_analysis_standardized.ipynb   # Ana analiz notebook'u
├── İranİsraelWarDataset.csv                     # Ham veri seti
├── Sosyal Ağ Analizi Final Proje Raporu.pdf     # Proje raporu
├── sunum.pptx                                   # Sunum dosyası
└── görseller/                                   # Analiz çıktısı görseller
    ├── İran_israil_Çatışması_Sosyal_Medya_Hesap_Ağı.png
    ├── Louvain_Topluluk_Analizi.png
    ├── Betweenness_Centrality_Haritası_...png
    └── ...
```
