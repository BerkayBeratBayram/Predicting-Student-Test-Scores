# Öğrenci Sınav Sonuçlarını Tahmin Etme (Predicting Student Test Scores)

Bu projede ben `data/` klasöründeki veri setini kullanarak öğrencilerin sınav puanlarını tahmin etmeye çalışıyorum. 

## Dosyalar
- `main.ipynb` — Benim hazırladığım uçtan uca notebook: veri yükleme, EDA, feature engineering, K-Fold güvenli target encoding, LightGBM ile model eğitimi (5-fold CV) ve submission oluşturma.
- `data/train.csv`, `data/test.csv`, `data/sample_submission.csv` — Kullanılan veri seti dosyaları.
- `submission.csv` — Notebook'u çalıştırdığımda ürettiğim örnek çıktı.

## `main.ipynb` içinde ne yaptım (adım adım)
1. Ortam ve kütüphaneler
   - Gerekli kütüphaneleri (`pandas`, `numpy`, `scikit-learn`, `lightgbm`, `xgboost`, `catboost`, `matplotlib`, `seaborn`, vb.) import ediyorum.

2. Veri yükleme ve ön inceleme (EDA)
   - `data/train.csv` ve `data/test.csv` dosyalarını okudum; boyutları, sütun isimlerini ve ilk birkaç satırı inceledim.
   - Eksik değerlerin sayısını kontrol ettim ve sayısal sütunların korelasyon matrisi ile `exam_score` ilişkisine baktım.

3. Basit feature engineering
   - `study_efficiency` (çalışma verimliliği), `study_sleep_ratio`, `study_x_attendance`, `sleep_x_study` gibi oran/etkileşim özellikleri oluşturdum.

4. Kategorik sütunları belirleme
   - Veri tipi `object` olan sütunları kategorik olarak aldım ve target encoding uygulamak üzere listeledim.

5. K-Fold güvenli Target Encoding (OOF)
   - K-fold out-of-fold target encoding ile kategorik değişkenleri `_te` suffix'li düzenlenmiş ortalamalara çevirdim.
   - Her fold için yalnızca train fold'u kullanarak OOF encode hesapladım; test için ise tüm eğitim verisi üzerinden smooth edilmiş ortalamayı uyguladım.
   - Target encoding sonrası ham kategorik sütunları düşürdüm; böylece yalnızca sayısal ve `_te` sütunlarla model eğittim.

6. Modelleme: 5-Fold CV ve LightGBM
   - 5-Fold ile modelleri eğittim, her fold için doğrulama setinde RMSE hesapladım ve fold'lar arası ortalama ile standart sapmayı raporladım.
   - Son adımda tüm eğitim verisiyle tek bir LightGBM modeli eğittim ve test seti için tahminler üreterek `submission.csv` dosyasını oluşturdum.

7. Tekrar üretilebilirlik (reproducibility)
   - Çalışmalarımda `random_state` değerleri kullandım. 

8. Notlar ve öneriler
   - Target encoding uyguladıktan sonra ham kategorik sütunları kullanmamak veri sızıntısını azaltır; notebook'ta bunu uyguladım.
   - Performansı düşürmek veya yükseltmek için şunları deneyebilirsiniz: hiperparametre optimizasyonu (GridSearch/Optuna), CatBoost/XGBoost denemeleri, stacking/ensemble yöntemleri, daha kapsamlı feature engineering.

## Nasıl çalıştırırım (kısa)
1. Sanal ortam oluşturun veya etkinleştirin.

2. Gerekli paketleri yükleyin (örnek):

```powershell
pip install pandas numpy scikit-learn lightgbm xgboost catboost matplotlib seaborn
```

3. `main.ipynb`'yi açın ve hücreleri sırayla çalıştırın. Notebook `data/` klasöründeki dosyaları okur ve kök dizine `submission.csv` yazar.



