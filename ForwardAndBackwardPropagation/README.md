# Yapay Sinir Ağı

# Kişilik Sınıflandırması — Basit Sinir Ağı ile İçedönük/Dışadönük Tahmini

Bu proje, bireylere ait çeşitli özelliklerden yola çıkarak onların içedönük mü yoksa dışadönük mü olduğunu tahmin eden, sıfırdan yazılmış küçük bir yapay sinir ağı (ANN) uygulamasıdır.

Sinir ağı, Python ile yalnızca `numpy` ve `scikit-learn` (performans metrikleri için) gibi temel kütüphaneler kullanılarak manuel olarak uygulanmıştır.

## Problem Tanımı

Veri seti her birey için çeşitli nitelikler içeriyor ve her birey:

* İçedönük (1) veya
* Dışadönük (0) olarak etiketlenmiştir.

Amaç: Bu özellikleri kullanarak bireyin kişilik yönelimini tahmin eden bir model kurmaktır.

## Model Mimarisi

Sinir ağı mimarisi:

* Giriş katmanı: Girdi sayısı = Özellik (feature) sayısı
* Gizli katman 1: 2 nöron + Sigmoid aktivasyon
* Gizli katman 2: 2 nöron + Sigmoid aktivasyon
* Çıkış katmanı: 1 nöron + Sigmoid aktivasyon

Aktivasyon fonksiyonu: `sigmoid(x) = 1 / (1 + e^-x)`

## İleri Yayılım (Forward Propagation)

1. Her katmanda ağırlıklar ve bias ile lineer dönüşüm yapılır: `z = XW + b`
2. Ardından sigmoid aktivasyonu uygulanır: `a = sigmoid(z)`
3. Çıkış katmanı da dahil olmak üzere tüm katmanlarda bu işlem zincirleme uygulanır.
4. Sonuç: `output = olasılık`, yani bireyin dışadönük olma ihtimali.

## Geri Yayılım (Backpropagation)

1. Çıkıştaki hata `loss = y - ŷ` ile hesaplanır.
2. Sigmoid türevi (`sigmoid' = sigmoid * (1 - sigmoid)`) ile zincirleme türev uygulanır.
3. Her katmanın ağırlık ve bias değerleri, hata gradyanı ile güncellenir.
4. Optimizer olarak basit Gradient Descent kullanılmıştır (learning rate sabit).

## Kayıp Fonksiyonu

Eğitim süresince kullanılan kayıp fonksiyonu:

**Binary Cross-Entropy Loss:**

```
L = - (1/N) * Σ [y log(ŷ) + (1 - y) log(1 - ŷ)]
```

Loss değerleri her epoch’ta takip edilip grafiğe dökülür.

## Model Performansı

Test setinde elde edilen metrikler:

* Accuracy: 0.9220
* F1 Score: 0.9216
* Binary Cross-Entropy Loss: 0.2715

## Değerlendirme Grafik ve Metotları

Modeli değerlendirmek için şu yöntemler de kullanıldı:

* ROC eğrisi ve AUC skoru
* Precision-Recall eğrisi
* Confusion Matrix
* Eğitim süreci boyunca Loss eğrisi

## Veri Ön İşleme

* Eksik veriler (NaN) ortalama/mod ile dolduruldu
* Kategorik sütunlar → One-hot encoding ile dönüştürüldü
* Sayısal özellikler → Min-Max normalizasyon (0–1 aralığı)

## Dosyalar

* `ForwardAndBackwardPropagation.ipynb` – Tüm model mimarisi ve eğitim kodları
* `personality_dataset.zip` – Kullanıcı özellikleri ve etiketler
* `README.md` – Bu belge
