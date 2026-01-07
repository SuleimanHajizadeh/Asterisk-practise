# Asterisk IVR (Sesli Menyu) – İzahlı Dialplan

Bu sənəd **Asterisk IVR (Interactive Voice Response)** sisteminin necə işlədiyini və **dialplan məntiqini addım-addım** izah edir. Məqsəd odur ki, sən yalnız copy‑paste etməyəsən, **nə baş verdiyini tam anlayasan**.

---

## 1. IVR nədir və Asterisk-də harada qurulur?

IVR – zəng edən şəxsə **avtomatik səsli menyu** təqdim edən sistemdir:

* “1-ə bas – Satış”
* “2-yə bas – Texniki dəstək”
* “0-a bas – Operator”

Asterisk-də IVR əsasən **extensions.conf** faylında yazılır.

Dialplan = çağırışın **axın xəritəsidir**.

---

## 2. Ümumi axın məntiqi (logic)

1. Zəng gəlir
2. Salamlayıcı səs faylı səslənir
3. Asterisk istifadəçidən **DTMF** (klaviş) gözləyir
4. Basılan düyməyə görə uyğun istiqamətə yönləndirilir
5. Səhv və ya cavabsızlıq olarsa → menyu təkrarlanır

---

## 3. Context anlayışı

Asterisk-də hər şey **context** içində baş verir.

Məsələn:

* `internal` – daxili zənglər
* `ivr-main` – IVR menyusu

IVR üçün **ayrı context** yaratmaq yaxşı praktikadır.

---

## 4. IVR-in başlanğıcı – zəngin qarşılanması

Zəng IVR-ə düşəndə ilk görülən işlər:

* Cavab verilir (`Answer()`)
* Qısa fasilə verilir (audio üçün)
* Salamlayıcı səs oxudulur

Burada məqsəd:

> Zəng edən şəxs səsi **aydın və kəsilmədən** eşitsin

---

## 5. Fon səsi və menyu oxunuşu

IVR-də səs adətən iki cür verilir:

* **Background()** – fon səsi + düymə gözləmə
* **Playback()** – yalnız səs, düymə qəbul etmir

Menyu üçün adətən **Background()** istifadə olunur, çünki istifadəçi səs gedə-gedə düymə basa bilər.

---

## 6. DTMF (düymə) məntiqi necə işləyir?

Asterisk istifadəçinin basdığı düyməni **extension** kimi qəbul edir:

* `1` → exten 1
* `2` → exten 2
* `0` → exten 0

Bu o deməkdir ki, IVR context-i içində:

* `exten => 1,1,...`
* `exten => 2,1,...`

şəklində istiqamətlər olur.

---

## 7. Timeout (heç nə basılmazsa nə olur?)

Əgər istifadəçi **heç bir düymə basmazsa**:

* `t` extension işə düşür

Bu adətən:

* “Cavab almadıq” mesajı
* Menyunun təkrar oxunması

üçün istifadə olunur.

---

## 8. Invalid input (səhv düymə)

Əgər istifadəçi:

* 9 basdı (menyuda yoxdur)

O zaman:

* `i` extension işə düşür

Bu da adətən:

* “Yanlış seçim” səsi
* Menyunun təkrarı

üçün istifadə olunur.

---

## 9. IVR-dən real istiqamətə çıxış

IVR-in məqsədi zəngi **real hədəfə** ötürməkdir:

* Daxili istifadəçi (1000)
* Queue (support)
* Operator
* Voicemail

Bu nöqtədə IVR bitir və artıq normal call-flow başlayır.

---

## 10. Döngü (loop) məntiqi niyə vacibdir?

Peşəkar IVR:

* 1 dəfə yox
* Bir neçə dəfə cəhd verir

Əgər hər dəfə səhv olarsa:

* Operatora ötürə bilər
* Zəngi bağlaya bilər

Bu **istifadəçi təcrübəsi (UX)** üçün çox önəmlidir.

---

## 11. Səs faylları harada olur?

Asterisk səs faylları adətən buradadır:

```
/var/lib/asterisk/sounds/
```

Dil üçün alt qovluqlar:

* `en/`
* `ru/`
* `tr/`

Məsələn:

* `welcome.wav`
* `main-menu.wav`

---

## 12. IVR test edilərkən nəyə baxmalısan?

CLI-də:

* DTMF görünürmü?
* Düz context-ə düşürmü?
* Timeout və invalid işləyirmi?

Əsas əmrlər:

* `core set verbose 5`
* `core set debug 5`

---

## 13. Növbəti addımlar

Bu IVR əsasdır. Sonra əlavə edə bilərsən:

* Çoxdilli IVR
* Vaxt əsaslı menyu (iş saatı / qeyri‑iş saatı)
* Queue ilə inteqrasiya
* Voicemail fallback

## 9. IVR-dən real istiqamətə çıxış

IVR-in məqsədi zəngi **real hədəfə** ötürməkdir:

* Daxili istifadəçi (1000)
* Queue (support)
* Operator
* Voicemail

Bu nöqtədə IVR bitir və artıq normal call-flow başlayır.

---

## 10. Döngü (loop) məntiqi niyə vacibdir?

Peşəkar IVR:

* 1 dəfə yox
* Bir neçə dəfə cəhd verir

Əgər hər dəfə səhv olarsa:

* Operatora ötürə bilər
* Zəngi bağlaya bilər

Bu **istifadəçi təcrübəsi (UX)** üçün çox önəmlidir.

---

## 11. Səs faylları harada olur?

Asterisk səs faylları adətən buradadır:

```
/var/lib/asterisk/sounds/
```

Dil üçün alt qovluqlar:

* `en/`
* `ru/`
* `tr/`

Məsələn:

* `welcome.wav`
* `main-menu.wav`

---

## 12. IVR test edilərkən nəyə baxmalısan?

CLI-də:

* DTMF görünürmü?
* Düz context-ə düşürmü?
* Timeout və invalid işləyirmi?

Əsas əmrlər:

* `core set verbose 5`
* `core set debug 5`

---

## 13. Tam real işlək dialplan – IVR → Queue → Operator (izahlı)

Bu hissədə **real işlək məntiq** izah olunur. Məqsəd: zəng → IVR → uyğun Queue → lazım gələrsə Operator.

### Məntiq axını

* Zəng daxil olur
* Sistem iş saatını yoxlayır
* Gündüz isə əsas IVR
* Gecə isə fərqli mesaj
* Seçimə görə Queue
* Queue cavab verməsə → Operator

Burada əsas anlayış **vaxt + menyu + fallback** kombinasiyasıdır.

---

## 14. İş saatına görə IVR necə işləyir?

Asterisk vaxtı bu formada oxuyur:

* Həftənin günü
* Saat aralığı

Məsələn:

* Bazar ertəsi – Cümə
* 09:00 – 18:00 → iş saatı
* Qalan vaxt → gecə rejimi

Bu yoxlama **zəng gələn anda** edilir.

Əgər iş saatıdırsa → əsas IVR
Əgər deyilsə → gecə mesajı + operator və ya voicemail

Bu yanaşma şirkət IVR-lərinin 90%-də istifadə olunur.

---

## 15. Çoxdilli IVR məntiqi (AZ / RU / EN)

Çoxdilli IVR-in əsas prinsipi:

1. Əvvəlcə dil seçimi
2. Seçilən dil yadda saxlanılır
3. Bütün səslər həmin dilə görə oxunur

Asterisk bunu **kanal dəyişəni** ilə edir.

Məsələn:

* İstifadəçi 1 basdı → AZ
* 2 → RU
* 3 → EN

Sonra IVR eyni məntiq ilə davam edir, sadəcə fərqli səs faylları oxunur.

Bu o deməkdir ki:

* Menyu eynidir
* Dil dəyişir

Bu dizayn **ölçülə bilən və genişlənən** sayılır.

---

## 16. Queue nədir və IVR ilə necə bağlanır?

Queue:

* Bir neçə agenti eyni nömrədə toplayır
* Kim boşdursa ona zəng ötürür

IVR-də Queue:

* Satış
* Texniki dəstək
* Müştəri xidməti

IVR sadəcə qərar verir:

> "Bu zəng hansı Queue-ya getsin?"

Əgər Queue-da cavab olmazsa:

* Operator
* Voicemail
* Yenidən IVR

istiqamətlərindən biri seçilir.

---

## 17. Operator fallback niyə vacibdir?

Peşəkar sistemlərdə:

* Heç vaxt zəng boş qalmaz

Əgər:

* Queue doludur
* Heç kim cavab vermir

O zaman:

* Canlı operator
* Və ya səsli mesaj

Bu müştəri məmnuniyyəti üçün kritikdir.

---

## 18. Call‑flow diaqramı – məntiqin vizual izahı

Axın belədir:

1. Incoming Call
2. İş saatı yoxlanır
3. Dil seçimi
4. Əsas IVR menyusu
5. Queue
6. Operator fallback
7. Zəng bitir

Bu ardıcıllıqda **heç bir boşluq yoxdur**.

---

## 19. Test edərkən nələrə baxmalısan?

CLI-də:

* Zəng hansı context-ə düşür?
* Dil dəyişəni dəyişirmi?
* Queue daxil olurmu?

Ən vacib məqam:

> Hər addımın məntiqini başa düşmək

Əgər burada hər şey aydındırsa:

* Sistem real mühitə hazırdır

---

## 20. Nəticə

Bu sənəddə sən:

* Real IVR məntiqini
* İş saatına görə yönləndirməni
* Çoxdilli dizaynı
* Queue və operator fallback anlayışını

**copy‑paste etmədən** öyrəndin.
