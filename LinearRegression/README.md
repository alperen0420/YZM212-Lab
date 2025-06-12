## Lineer Regresyon ve Veri Seti:
Lineer regresyon için kullanılan bu veri seti bazı öğrencilerin çeşitli özelliklerine göre aldığı puanı gösterir. Bu veri üstünde lineer regresyon iki şekilde uygulanmıştır; birisi sıfırdan yani sadece numpy kütüphanesi kullanılarak, diğeri de scikit-learn kütüphanesinden entegre edilerek uygulanmıştır.
## Sonuç :
| From Scratch | Sklearn     |
|--------------|-------------|
| 7.80972946   | 7.80972946  |
| 0.54616359   | 0.54616359  |
| -0.02353613  | -0.02353613 |
| -0.01593587  | -0.01593587 |
| 0.00313561   | 0.00313561  |
| 0.01739190   | 0.01739190  |
| -0.03896222  | -0.03896222 |
| -0.01841907  | -0.01841907 |
| -0.00464729  | -0.00464729 |
|MSE:0.255401  |MSE:0.255401 |

Her iki model de aynı veriseti, aynı özellikler ve aynı maliyet fonksiyonunu (En küçük kareler yaklaşımı) kullandığı için sonuçlar tamamen aynı çıkmıştır. Bu ağırlık hesaplamasının doğrudan matris işlemleriyle yapılmasından dolayı beklenen bir durumdur.

Alperen Aydın 22290435
