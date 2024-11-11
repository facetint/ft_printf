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
- [Kullanılabilir Fonksiyonlar](#kullanılabilir-fonksiyonlar)
- [Fonksiyon Prototipi](#fonksiyon-prototipi)
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

## Kullanılabilir Fonksiyonlar
`ft_printf` fonksiyonunu yazarken aşağıdaki harici fonksiyonlardan yararlanabilirsiniz:
- **`malloc`**: Bellek tahsisi
- **`free`**: Bellek serbest bırakma
- **`write`**: Çıkışa veri yazma
- **Variadic Fonksiyonlar**:
  - `va_start`, `va_arg`, `va_copy`, `va_end`

---

## Fonksiyon Prototipi
```c
int ft_printf(const char *format, ...);
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
