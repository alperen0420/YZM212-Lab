# **Naive Bayes**
 **Problem Tanımı**: Bir bankanın çeşitli parametrelere bağlı olarak müşterilerinin bankayı terk edip etmedikleridir.
 
 **Kullanılan Veriseti**: Bu veri kümesi, Yeni Zelanda'nın önde gelen finans kuruluşlarından Kiwibank'ın müşteri kaybı kalıpları ve davranışları hakkında içgörü sağlamaktadır. Demografik bilgileri (yaş, cinsiyet, coğrafya gibi), bankacılık metriklerini (kredi puanı, bakiye, ürünler) ve müşteri faaliyet göstergelerini içerir.
 
 **Yöntem**: Bu veriseti üzerinde Gaussian Naive Bayes alogirtması kullanılmıştır. Gaussian Naive Bayes özelliklerin sürekli olması durumunu ve normal dağılıma uyduğunu varsayar.
 
 **Sonuçlar**: Sonuç olarak SKlearn kütüphanesinin kullanıldığı modelde sonuçlar: 
 ```Confusion Matrix:
 [[1531   48]
  [ 376   45]]
 
 Classification Report:
               precision    recall  f1-score   support
 
            0       0.80      0.97      0.88      1579
            1       0.48      0.11      0.18       421
 
     accuracy                           0.79      2000
    macro avg       0.64      0.54      0.53      2000
 weighted avg       0.74      0.79      0.73      2000
 
 Train Time:  0.06769418716430664
 Test Time:  0.024227142333984375
 ```
 
 olarak çıkmıştır.
 
 SKlearn kütüphanesi kullanılmadan yapılan modelde sonuçlar:
 ```Confusion Matrix:
 [[1550   29]
  [ 322   99]]
 
 Classification Report:
               precision    recall  f1-score   support
 
            0       0.83      0.98      0.90      1579
            1       0.77      0.24      0.36       421
 
     accuracy                           0.82      2000
    macro avg       0.80      0.61      0.63      2000
 weighted avg       0.82      0.82      0.79      2000
 
 Train Time:  0.004542112350463867
 Test Time:  0.19118213653564453
 ```
 olarak çıkmıştır.
 **Kişisel Yorum**: Naive Bayes modeli rastgelelik içermediği için genel olarak sonuçların benzer çıkması beklenir ancak hesaplamaların yapıldığı metodlar ve bazı optimizasyonlar sonucu ufak bir miktar değiştirmiştir.
