# **Logistic Regression:**
## 1-Problem ve Veriseti:
Bu veriseti bazı hastaların çeşitli faktörler ve sağlık durumlarını içeren bir verisetidir. Bu modelde bu faktörlere bağlı olarak hastaların kardiyovasküler hastalık durumu incelenmiştir. Bunun için lojistik regresyon algoritması kullanılmıştır.
## 2-Veri Önişleme:
Bu veriseti 18 sütun 319.796 adet satır içermektedir. Örnek sayısı fazla olduğundan 10.000 örneğe indirilmiştir, bu sırada etiket sınıfındaki değerlerin eşit dağılması için her bir değerden 5000 örnek seçilmiştir. Verilerden faydasız olarak değerlendirilen özellikler çıkarılmıştır ve tüm kategorik sütunlara one-hot encoding yöntemi uygulanmıştır. BMI sütununun dağılımının log-norm dağılıma uyduğu belirlenmiştir; bu yüzden log-normal dönüşümü uygulanıp dağılım normal dağılıma benzetilmiş, standartizasyon kullanılarak verilerin ortalaması "0" standart sapması "1" olacak şekilde düzenlenmiştir.
## 3-Yöntem:
Bu verisetinde için kullanılacak model lojistik regresyon olarak belirlenmiştir. Lojistik regresyon, bir sınıflandırma algoritmasıdır. Bu verisetinde çeşitli özelliklere bakarak hastada kardiyovasküler hastalığa sahip olup olmadığı tahmin edilmeye çalışılmıştır.
## 4-Sonuçlar:

 - Scikit Learn ile Logistic Regression:

|              | precision | recall | f1-score | support |
|--------------|-----------|--------|----------|---------|
| 0.0          | 0.79      | 0.74   | 0.77     | 1012    |
| 1.0          | 0.75      | 0.80   | 0.78     | 988     |
|       -      |           |        |          |         |
| accuracy     |           |        | 0.77     | 2000    |
| macro avg    | 0.77      | 0.77   | 0.77     | 2000    |
| weighted avg | 0.77      | 0.77   | 0.77     | 2000    |
```
Eğitim süresi:  0.22160601615905762
Test süresi:  0.006459474563598633
[[753 259]
 [195 793]]
```
- Scikit Learn olmadan Logistic Regression:

|              | precision | recall | f1-score | support |
|--------------|-----------|--------|----------|---------|
| 0.0          | 0.79      | 0.74   | 0.77     | 1012    |
| 1.0          | 0.75      | 0.80   | 0.77     | 988     |
|       -      |           |        |          |         |
| accuracy     |           |        | 0.77     | 2000    |
| macro avg    | 0.77      | 0.77   | 0.77     | 2000    |
| weighted avg | 0.77      | 0.77   | 0.77     | 2000    |
```
Eğitim süresi: 7.870607376098633 saniye
Test süresi: 0.00029087066650390625 saniye
[[752 260]
 [201 787]]
```
## 5-Yorum / Tartışma:
Yeterli miktarda iterasyon olduğundan dolayı iki model arasında karmaşıklık matrisinde kayda değer bir fark oluşmamıştır, bu yüzden performans metrikleri de hemen hemen aynıdır. İki modelin test süresindeki fark çok düşük derecede olsa da eğitim süresinde büyük bir fark olduğu açıktır. Bu Scikit Learn kütüphanesinin hesaplamalarda kullandığı optimizasyon algoritmaları, bellek yönetimi optimizasyonları ve iterasyon sayısından kaynaklanmaktadır. Scikit Learn kütüphanesinde öğrenme oranı hiperparametresi optimize edilip sürekli değişirken Scikit Learn kütüphanesi kullanılmadığı modelde sabittir, ayrıca Scikit Learn kütüpühanesi kullanılan modelde iterasyon sayısı model en yüksek doğruluğa ulaştığında otomatik olarak durur.

**-Değerlendirme metrikleri seçiminde problem ve sınıf dağılımı önemli midir?**
Evet oldukça önemlidir, problem dağılımı için problem tipi önemlidir eğer sınıflandırma ikiden fazla farklı örnek içeriyorsa her farklı değer için performans metrikleri ayrı ayrı hesaplanıp değerlendirilmesi gerekir. Sınıf dağılımı için de tüm performans metriklerini dikkate almak önemlidir çünkü tek başına doğruluk modelin başarısını ölçmede yetersiz kalır. Bunun sebebi sınıf dağılımı düzensiz ise örneğin ikili sınıflandırma problemi için "0" değerinin dağılımı tüm sınıfın %95ini oluşturuyorsa tüm değerleri "0" olarak tahmin etmek %95 bir doğruluk sağladığı halde "1" tahmini yoktur yani model başarısızdır, bu durumda diğer parametreler örneğin hassasiyet bu modelin başarısız olduğunu gösterecektir.
