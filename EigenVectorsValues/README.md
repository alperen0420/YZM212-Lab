# **Matris Manipülasyonu, Özdeğerler ve Özvektörler**
## 1-Matris manipülasyonu: 
Makine öğrenmesindeki hesaplamaların temeli matris manipülasyonuna yani matris ve vektör işlemlerine dayanır. Özellikle özellikleri ölçeklerken, vektörize ederken, özellik çıkarımı yani temel bileşen analizi ve tekil değer ayrışımı gibi yerlerde matris manipülasyonu kullanılır.
## 2-Özdeğer ve Özvektör:
Özdeğer "**Av=λv**" eşitliğini sağlayan A matrisinin skaler bir değeridir. Özvektör ise bu skaler değerle bu eşitliği sağlayan "**v**" vektörüdür.
## 3-Makine öğrenmesi ile ilişkileri:

 1. Boyut indirgeme ve kümeleme gibi analizlerde matrislerin uzayda vektörleri farklı yön ve büyüklüklerde ölçeklerler. Örneğin veri kovaryans veya graf laplasyen matrislerinde bu yön ve büyüklükleri matris manipülasyonu , özdeğerleri ve özvektörleri bularak bu analizleri yapmaya olanak sağlar.
 
 2. Temel bileşen analizi yönteminde verideki varyansı en büyük yani veriyi en iyi açıklayan eksenleri bulurken en büyük özdeğerlere karşılık gelen özvektörleri bulunur.
 
 3. Spektral kümelemede graflardaki en küçük özdeğerlere karşılık gelen özvektörleri bularak düğümler en iyi şekilde kümelenir.
 
 ## 4-Numpy Lineer Algebra Eig fonksiyonu:
### 1. Fonksiyon Tanımı ve Kullanımı (Dokümantasyondan)

   `numpy.linalg.eig(a)` 
    
   `a` parametresi `(..., M, M)` boyutlarında kare matris veya matris yığınıdır.
    
-   **Return**  
    Bir namedtuple:
    
    -   `eigenvalues`: `(..., M)` boyutlu dizi — özdeğerler, çokluklarına göre tekrarlanır.
        
    -   `eigenvectors`: `(..., M, M)` boyutlu dizi — sütunları normalleştirilmiş (birim uzunlukta) sağ özvektörlerdir (sütun `i`, `eigenvalues[i]`’a karşılık gelir).
        
-   **Hata**  
    Hesaplama yakınsamazsa `LinAlgError` yükselir.
   ### 2. Python Seviyesindeki Wrapper (`_linalg.py`)

-   Modül başında `__all__` içinde yer alır; böylece `from numpy.linalg import eig` ile erişilir. 
-   Tipik sarıcı (diğer fonksiyonlarla tamamen aynı desene sahip) şu adımları izler:
    
    1.  **Girdi dönüşümü**
        
        `a, wrap = _makearray(a)` 
        
        — Girdiyi `ndarray`’e çevirir, orijinal tip için `__array_wrap__` fonksiyonunu kaydeder.
        
    2.  **Boyut ve kare kontrolü**
        
        `_assert_stacked_2d(a)
        _assert_stacked_square(a)` 
        
        — En az 2 boyutlu ve son iki boyutun kare olduğunu doğrular.
        
    3.  **Sonuç tipi belirleme**
        
        `t, result_t = _commonType(a)
        signature = 'D->D'  if isComplexType(t) else  'd->d'` 
        
        — Tek ve çift hassasiyetli karmaşık olmayan/tam karmaşık türleri belirler.
    4.  **Ufunc çağrısı**

        `w, v = _umath_linalg.eig(a, signature=signature)` 
        
        — C/C++ seviyesindeki genelleştirilmiş ufunc’a (`gufunc`) iletir.
        
    5.  **Sonucun wrap edilmesi**
        
        `return wrap(EigResult(w.astype(result_t), v.astype(result_t)))` 
        
        — `EigResult` namedtuple’ını, doğru tip dönüşümleriyle paketler.

### 3. C/C++ Seviyesindeki UFunc Kayıt ve Dağıtımı (`umath_linalg.cpp`)

-   `umath_linalg.cpp` içinde `gufunc_descriptors` dizisinde şöyle tanımlanmış:
    
    `{ "eig", "(m,m)->(m),(m,m)", /* nin=1, nout=2, funcs=FUNC_ARRAY_NAME(eig), types=eig_types */ },` 
    
  - Girdi boyutu `(m,m)`, çıktı boyutları `(m)` (özdeğerler) ve `(m,m)` (özvektörler).
    
-   `FUNC_ARRAY_NAME(eig)` makrosuyla tek ve çift hassasiyetli, karmaşık türler için uygun LAPACK sarmalayıcı fonksiyonlar (`DOUBLE_eig`, `CDOUBLE_eig` vb.) belirlenir.
    
-   Her eleman için döngü yapılarak dizi dilimleri `linearize_matrix` ile düz belleğe taşınır, LAPACK’ın `dgeev`/`zgeev` çağrılır, çıktılar `delinearize_matrix` ile geri yerleştirilir.

## Numpy Lineer Algebra Eig fonksiyonu ve Özel Eigenvalue fonksiyonu karşılaştırması:
 Özel Eigenvalue fonksiyonunu içeren [bu repo](https://github.com/LucasBN/Eigenvalues-and-Eigenvectors) adresindeki koddaki fonksiyonların kısaca açıklaması:
 -   **`get_dimensions(matrix)`**  
    Verilen “liste içinde liste” formatındaki matrisin satır ve sütun sayısını `[rows, cols]` olarak reutrn eder.
    
-   **`find_determinant(matrix, excluded=1)`**  
    Küçük matris (2×2) için doğrudan formülle, daha büyük matrisler için ilk satır üzerinden kofaktör (genişletme) yöntemiyle determinantı hesaplar. `excluded` parametresi, o an çarpılması gereken işaretli katsayıyı (±1) taşır.
    
-   **`list_multiply(list1, list2)`**  
    İki listeyi polinom katsayıları gibi görüp “konvolüsyon” (FOIL’ın genellemesi) yöntemiyle çarpar, sonuç katsayı listesini verir.
    
-   **`list_add(list1, list2, sub=1)`**  
    İki listeyi eleman bazında toplar; `sub=-1` gönderilirse ikinci liste çıkarma olarak uygulanır.
    
-   **`determinant_equation(matrix, excluded=[1, 0])`**  
    Matrisin determinantını “polinom katsayıları” cinsinden (bir bilinmeyenli denklem formunda) bulur. Küçük matrislerde doğrudan, büyüklerde kofaktör açılımı yaparak liste şeklinde katsayı döner.
    
-   **`identity_matrix(dimensions)`**  
    `[rows, cols]` boyutunda birim (köşegeninde 1, geri kalanında 0) matris üretir.
    
-   **`characteristic_equation(matrix)`**  
    Her elemanı `[a, -b]` çifti hâline getirerek `A – λI` matrisini, bir “liste içinde liste” formatında oluşturur; sonrasında determinant denklemine gönderilir.
    
-   **`find_eigenvalues(matrix)`**  
    Önce `characteristic_equation` ile katsayı listesini elde eder, sonra `numpy.roots` ile bu polinomun köklerini (özdeğerleri) bulur ve NumPy dizisi olarak return eder.

## Sonuç:
İlgili dosyadaki main fonksiyonunun çıktısında görüleceği üzere her iki fonksiyon da tam olarak aynı çıktıyı vermiştir. Bu gayet normaldir çünkü her iki fonksiyonun da temelde yaptığı şey tam olarak aynıdır, matrisin karakteristik polinomunu çıkarır ve köklerini yani özdeğerlerini bularak return eder.
