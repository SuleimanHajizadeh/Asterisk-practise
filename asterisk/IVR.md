# Asterisk IVR (Səsli Menyu) Axışı

## 1. Giriş
- IVR, çağırış edən istifadəçilərə avtomatik səsli menyu təqdim edən sistemdir.
- Məqsəd: Çağırışları düzgün bölmələrə yönləndirmək və insan operatorun iş yükünü azaltmaq.

## 2. Əsas Elementlər
- **Dialplan:** `/etc/asterisk/extensions.conf` faylında IVR axışı yazılır.
- **Audio Files:** Səsli mesajlar (`.wav` və ya `.gsm`) menyu seçimlərini elan edir.
- **DTMF Input:** İstifadəçi düymələr vasitəsilə seçim edir (1,2,0…).

## 3. Səsli Menyu Axışı

### Başlanğıc
- Çağırış daxil olur.
- Xoş gəlmisiniz mesajı səsləndirilir.

### Əsas Menü
- **Seçimlər:**
  - 1 → Satış (Sales)
  - 2 → Dəstək (Support)
  - 0 → Operator
- **Yanlış və ya vaxt aşımı:**
  - İstifadəçi düzgün seçim etməzsə və ya cavab verməzsə, əsas menyuya geri dön.

### Axış Nümunəsi
```text
[Incoming Call]
       |
       v
[Play Welcome Message]
       |
       v
[Main Menu: Press 1,2,0]
   /       |       \
  1        2        0
  |        |        |
[Sales] [Support] [Operator]
   ^        ^        ^
   |        |        |
[Invalid/Timeout -> Back to Main Menu]
