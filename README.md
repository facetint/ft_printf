<div align="center">

![image](https://github.com/user-attachments/assets/7767d343-54d3-429b-93be-9f2194904876)

# "Printf - Because ft_putnbr() and ft_putstr() aren’t enough.”

</div>

# 🌟 ft_printf

`ft_printf`, C programlama dilinde kendi `printf` fonksiyonunuzu yazmanızı sağlayan bir projedir. Bu proje, libc'nin `printf` fonksiyonuna benzer şekilde çalışarak çeşitli format dönüşümlerini destekler.

---

## 📜 İçerik
- [Genel Bakış](#genel-bakış)
- [Proje Gereksinimleri](#proje-gereksinimleri)
- [Fonksiyon Prototipi](#fonksiyon-prototipi)
- [Variadic Fonksiyonlar](#variadic-fonksiyonlar)
  - 
- [Dönüşüm Formatları](#dönüşüm-formatları)
- [Örnek Kullanım](#örnek-kullanım)
- [Kaynaklar](#kaynaklar)

---

## Genel Bakış

  Bu proje, `printf` fonksiyonunun bir taklidini içeren `ft_printf` kütüphanesini oluşturmayı amaçlar. `ft_printf`, standart `printf` fonksiyonu gibi çalışacak ve çeşitli format dönüşümlerini gerçekleştirecektir. Amacımız, C dilinde variadic fonksiyonlarla çalışmayı öğrenmek ve `printf` fonksiyonunun çalışma prensiplerini anlamaktır.


<div align="center">

(![image](https://github.com/user-attachments/assets/b37e5f1b-5a98-4b8c-ac08-6b6f2b50ab37)

</div>

---

## Proje Gereksinimleri

  - **Kütüphane Adı**: `libftprintf.a`
  - **Dosyalar**: `Makefile`, `*.h`, `*/*.h`, `*.c`, `*/*.c`
  - **Harici Fonksiyonlar**: 
    - `malloc`, `free`, `write`, `va_start`, `va_arg`, `va_copy`, `va_end`
  - **Libft Kullanımı**: Evet, `libft` fonksiyonları kullanılabilir.
  - **Kütüphane Oluşturma**: `ar` komutu kullanılmalı; `libtool` yasak.
  - **Buffer Yönetimi**: Gerçek `printf` gibi buffer yönetimi yapılmamalıdır.
    
---

## Fonksiyon Prototipi

```c
int ft_printf(const char *format, ...);
```

**Argümanlar:**

  -  **`format`**: Çıktı biçimini belirten bir dize. Bu dize, ekrana yazdırılacak metin ve değişkenlerin nasıl biçimlendirileceğini belirler. Biçim dizesi, **`%`** işaretleriyle belirtilen biçim belirteçleri içerebilir. Örneğin, **`%d`** bir tamsayıyı, **`%f`** bir ondalık sayıyı gösterir.
  
  - **`...`** (elips): Bu, değişken sayıda argüman almak için kullanılan özel bir işarettir. **`printf`** fonksiyonu, **`format`** dizesinde belirtilen biçim belirteçleri kadar argüman alabilir. Bu argümanlar, biçim dizesindeki sıralamaya göre ekrana yazdırılır.
  
  - **Dönüş Değeri:`printf`** fonksiyonu, ekrana yazdırılan karakter sayısını (yani başarıyla yazdırılan karakterlerin toplamını) döndürür. Eğer bir hata oluşursa, **`-1`** değeri dönecektir.


## Variadic Fonksiyonlar

`printf` gibi fonksiyonlar, değişken sayıda argüman alabilir. Bu tür fonksiyonlara **Variadic Functions** (Değişken Argümanlı Fonksiyonlar) denir. `printf`, aldığı format ve argümanlar sayesinde farklı veri türlerinde veriyi aynı anda işleyebilir.

### Variadic Fonksiyonlarla Çalışmak

C dilinde, variadic fonksiyonları tanımlamak için `<stdarg.h>` başlık dosyası kullanılır. Bu dosyada yer alan bazı önemli fonksiyonla3r:

### 🛠 va_list, va_start, va_arg, va_end

C dilinde variadic fonksiyonlar ile çalışırken, `stdarg.h` kütüphanesinden gelen dört temel makro kullanılır. Bu makrolar, bir fonksiyonun değişken sayıda argümanı işlemesini sağlar.

| **Makro**   | **Açıklama**                                                                                                                                             |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `va_list`   | Variadic fonksiyonun argümanlarını temsil eden bir veri yapısı tanımlar. Bu yapı, argüman listesini tutmak için kullanılır.                              |
| `va_start`  | Argüman listesinin başlangıcını belirler ve ilk argümanın adresini alır. Fonksiyonun değişken sayıda argüman almasını sağlar.                            |
| `va_arg`    | Sıradaki argümanı almak için kullanılır. Her çağrıldığında bir sonraki argümanı döndürür ve elde edilecek veri türü belirtilmelidir (ör. `int`, `char`). |
| `va_end`    | Argüman listesini temizler ve bellek yönetimi açısından işlem tamamlandığında çağrılması gereklidir.                                                     |

Bu makroların kullanımı, `ft_printf` fonksiyonu gibi bir variadic fonksiyonun argümanlarını verimli bir şekilde alıp işlemeyi mümkün kılar.

#### Kullanım Örneği

Aşağıdaki örnek, değişken sayıda argüman alan basit bir variadic fonksiyonun `stdarg.h` makrolarını nasıl kullandığını göstermektedir.

```c
#include <stdio.h>
#include <stdarg.h>

void print_numbers(int count, ...) {
    va_list args;           // Argüman listesini tanımlar
    va_start(args, count);  // İlk argümanın adresini alır

    for (int i = 0; i < count; i++) {
        int number = va_arg(args, int);  // Sonraki argümanı alır
        printf("%d ", number);
    }

    va_end(args);           // İşlem tamamlandığında argüman listesini temizler
    printf("\n");
}

int main() {
    print_numbers(3, 10, 20, 30);  // Çıktı: 10 20 30
    return 0;
}
Bu variadic özellikler, `ft_printf` fonksiyonunda farklı veri türlerini aynı fonksiyon içinde işleyebilmemizi sağlar. Örneğin, `%d`, `%s` ve `%c` gibi dönüşümler için aynı `ft_printf` çağrısında ilgili veri türlerini kullanabiliriz.

### Örnek: Basit Bir Variadic Fonksiyon

Aşağıda basit bir variadic fonksiyon örneği verilmiştir. Bu örnek, bir variadic fonksiyonun nasıl çalıştığını anlamak için iyi bir başlangıçtır.

```c

#include <stdio.h>
#include <stdarg.h>

void print_numbers(int count, ...) {
    va_list args;
    va_start(args, count);

    for (int i = 0; i < count; i++) {
        int number = va_arg(args, int);
        printf("%d ", number);
    }

    va_end(args);
    printf("\n");
}

int main() {
    print_numbers(3, 10, 20, 30);  // Çıktı: 10 20 30
    return 0;
}

```



## 📊 Dönüşüm Formatları

| **Dönüşüm** | **Açıklama**                                           |
|-------------|--------------------------------------------------------|
| `%c`        | Tek bir karakter yazdırır                              |
| `%s`        | Bir karakter dizisi yazdırır                           |
| `%p`        | `void *` pointer’ı hexadecimal olarak yazdırır         |
| `%d`        | 10 tabanında decimal sayı yazdırır                     |
| `%i`        | 10 tabanında integer yazdırır                          |
| `%u`        | 10 tabanında işaretsiz decimal sayı yazdırır           |
| `%x`        | Hexadecimal sayı (küçük harfler ile)                   |
| `%X`        | Hexadecimal sayı (büyük harfler ile)                   |
| `%%`        | Yüzde işareti `%` yazdırır                             |

## Örnek Kullanım

```c

ft_printf("Karakter: %c\n", 'A');
ft_printf("Dize: %s\n", "Merhaba");
ft_printf("Pointer: %p\n", (void *)0x7ffe637541f0);
ft_printf("Decimal: %d\n", 123);
ft_printf("Unsigned: %u\n", 456);
ft_printf("Hexadecimal (küçük harf): %x\n", 0x1a3);
ft_printf("Hexadecimal (büyük harf): %X\n", 0x1A3);
ft_printf("Yüzde İşareti: %%\n");

````

## Kaynaklar

Daha fazla bilgi için man 3 printf ve man 3 stdarg komutlarına göz atabilirsiniz.
