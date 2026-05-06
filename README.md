# 🫀 Bulanık Üç Değerli Mantık ile Kalp Hastalığı Risk Analizi

Bu çalışma, makine öğrenmesi süreçlerinde belirsizlikleri yönetmek adına önerilen **Bulanık Üç Değerli Mantık (Fuzzy Three-Valued Logic)** hesaplama çerçevesinin tıbbi bir veri seti (Kardiyovasküler Hastalıklar) üzerindeki uygulamasını içermektedir.

## 📝 Proje Özeti
Geleneksel makine öğrenmesi yöntemleri veriyi genellikle ikili (binary) bir yapıda işlerken, bu projede makalede sunulan teorik altyapı kullanılarak "belirsiz" durumlar (0.5 değeri) sisteme dahil edilmiştir. Bu sayede modelin karar verme kapasitesi ve eğitim süreleri optimize edilmiştir.

## 🛠️ Uygulanan Adımlar
1. **Veri Mimarisi (SQLite):** Veri seti, ilişkisel veritabanı yönetim prensiplerine uygun olarak SQLite tabanlı `kalp_hastaligi.db` dosyasına aktarılmıştır.
2. **Önişleme ve Bulanıklaştırma:** Makaledeki **Tablo 8** ve ilgili denklemler kullanılarak; alkol, sigara ve fiziksel aktivite verileri birleştirilip bulanık değerlere (0, 0.5, 1) dönüştürülmüştür.
3. **Model Karşılaştırmaları:** GaussianNB, SVM, AdaBoost ve Random Forest gibi 7 farklı algoritma üzerinde makaledeki yöntemin doğruluğu test edilmiştir.
4. **Kullanıcı Arayüzü (Streamlit):** Makalenin **Tablo 13** bölümünde yer alan 12 temel kural, interaktif bir Karar Destek Sistemi dashboard'una dönüştürülmüştür.

## 📂 Dosya İçerikleri
- `Untitled.ipynb`: Veri madenciliği, SQL sorguları ve model eğitim aşamalarını içeren ana çalışma dosyası.
- `app.py`: Streamlit kütüphanesi ile yazılmış, kural tabanlı çalışan canlı arayüz kodu.
- `kalp_hastaligi.db`: Projede kullanılan yapılandırılmış veri tabanı dosyası.

## 🚀 Çalıştırma Talimatı
Projeyi yerel ortamda test etmek için:
```bash
pip install pandas scikit-learn streamlit
streamlit run app.py
