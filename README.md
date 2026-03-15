# 🔒 Block Cipher Lab — مختبر التشفير الكتلي

> منصة تعليمية تفاعلية لمادة التشفير الكتلي  
> الجامعة التكنولوجية — كلية علوم الحاسوب  
> أ.د. هالة بهجت عبد الوهاب | الفصل الثاني 2025-2026

---

## 📋 نظرة عامة

**Block Cipher Lab** موقع HTML تفاعلي مبني بالكامل من ملف واحد (`index.html`) بدون أي مكتبات خارجية أو backend. صُمِّم خصيصاً لطلاب قسم أمن الحاسوب والمعلومات لفهم خوارزميات التشفير الكتلي **نظرياً وعملياً** في نفس الوقت.

---

## ✨ المميزات

- **عربي بالكامل** مع دعم RTL
- **تصميم Cyberpunk داكن** مع تأثيرات Neon
- **لا يحتاج إنترنت** بعد تحميل الخطوط (يعمل محلياً)
- **لا يحتاج server** — افتح الملف مباشرة في المتصفح
- **كل خوارزمية قابلة للتنفيذ** مع إدخال بياناتك الخاصة

---

## 📂 هيكل المشروع

```
block-cipher-lab/
└── index.html      ← الملف الوحيد — يحتوي HTML + CSS + JS
```

---

## 🚀 طريقة التشغيل

```bash
# الطريقة الأبسط: افتح الملف مباشرة في المتصفح
open index.html

# أو عبر Python server محلي (اختياري)
python3 -m http.server 8080
# ثم افتح: http://localhost:8080
```

> **ملاحظة:** يحتاج اتصال إنترنت للمرة الأولى فقط لتحميل خطوط Google Fonts.  
> بعدها يعمل بدون إنترنت.

---

## 📚 محتوى الموقع

### القسم النظري

| الصفحة | المحتوى |
|--------|---------|
| **المفاهيم الأساسية** | التشفير المتماثل، نموذج Shannon، المعادلات الأساسية، Stream vs Block |
| **هجمات التشفير** | Ciphertext-only، Known-plaintext، Chosen-plaintext، Chosen-ciphertext |
| **أوضاع التشغيل** | ECB، CBC، CFB، OFB — مزايا وعيوب كل وضع |
| **Feistel & Shannon** | Diffusion، Confusion، S-boxes، P-boxes، شبكة Feistel |

### المختبرات التفاعلية

| المختبر | الخوارزمية | ما يمكنك تجربته |
|---------|------------|----------------|
| 🔑 **DES Lab** | Data Encryption Standard | تشفير/فك تشفير، عرض 16 جولة، S-Box lookup، مثال المحاضرة كاملاً |
| 🔁 **Modes Lab** | ECB / CBC / CFB | مقارنة الأوضاع، إظهار ضعف ECB عملياً |
| 🐡 **Blowfish Lab** | Blowfish (Schneier 1993) | دالة F خطوة بخطوة، 16 جولة Feistel |
| 🔢 **RC5 Lab** | RC5-W/R/B (Rivest 1994) | Key expansion، تشفير بمعاملات متغيرة |
| ☭ **GOST Lab** | GOST 28147-89 | جولة واحدة + 32 جولة كاملة |

### أدوات إضافية

| الأداة | الوصف |
|--------|-------|
| 📊 **مقارنة الخوارزميات** | جدول شامل: DES vs GOST vs Blowfish vs RC5 vs FEAL vs Serpent |
| 🧮 **حاسبة Brute Force** | احسب زمن كسر أي مفتاح بالقوة الغاشمة |
| 🔍 **تحليل التكرار** | Frequency Analysis + Caesar Cipher decoder |
| 👁️ **مُصوِّر البتات** | نص → بتات → Hex → XOR بصرياً |

---

## 🛠️ التقنيات المستخدمة

| التقنية | الاستخدام |
|---------|----------|
| **HTML5** | هيكل الصفحة |
| **CSS3** | تصميم Cyberpunk، CSS Variables، Grid، Flexbox، Animations |
| **Vanilla JavaScript** | كل المنطق البرمجي — بدون أي framework |
| **Google Fonts** | Tajawal (عربي)، JetBrains Mono (كود)، Orbitron (عناوين) |

---

## 🔐 الخوارزميات المُنفَّذة

### DES (Data Encryption Standard)
```
Block Size : 64-bit
Key Size   : 56-bit فعلي (64-bit مع parity bits)
Rounds     : 16 جولة Feistel
Structure  : IP → 16×(Expansion+XOR+S-boxes+P-box) → IP⁻¹
```

**مكونات دالة f:**
1. **Expansion E** — توسيع 32-bit إلى 48-bit
2. **Key Mixing** — XOR مع subkey 48-bit
3. **S-Box Substitution** — 8 S-boxes، كل منها 6-bit → 4-bit
4. **P-Box Permutation** — إعادة ترتيب 32-bit

### Blowfish
```
Block Size : 64-bit
Key Size   : 32 إلى 448-bit (متغير)
Rounds     : 16 جولة Feistel
Structure  : Key-dependent S-boxes (مشتقة من المفتاح)
```

**دالة F:**
```
F(XL) = ((S1[a] + S2[b] mod 2³²) XOR S3[c]) + S4[d] mod 2³²
حيث a,b,c,d هي أرباع XL الأربعة (8-bit لكل منها)
```

### RC5
```
Designation: RC5-W/R/B
W (word)   : 16، 32، أو 64 bit
R (rounds) : 0-255 (الموصى به: 12)
B (key)    : 0-255 byte
Magic:       P₃₂ = 0xB7E15163، Q₃₂ = 0x9E3779B9
```

**خطوات Key Expansion:**
1. تحويل المفتاح من bytes إلى words (L array)
2. تهيئة S array بالثوابت السحرية Pw/Qw
3. خلط المفتاح: `3 × max(t, c)` مرة

### GOST 28147-89
```
Block Size : 64-bit
Key Size   : 256-bit (+610-bit مع S-boxes السرية)
Rounds     : 32 جولة (ضعف DES)
P-Box      : 11-bit left circular shift (بدل P-box)
```

**جدول subkeys GOST:**
- الجولات 1-24: k1, k2, ..., k8 (مكرر 3 مرات)
- الجولات 25-32: k8, k7, ..., k1 (معكوس)

---

## ⚠️ حالة الأمان الحالية

| الخوارزمية | الوضع | السبب |
|------------|-------|-------|
| DES | 🔴 **مكسور** | مفتاح 56-bit قصير جداً |
| FEAL | 🔴 **مكسور** | هشّ أمام التحليل التفاضلي والخطي |
| GOST | 🟡 **تاريخي** | آمن نظرياً لكن قديم |
| Blowfish | 🟢 **آمن** | لكن block size 64-bit صغير للبيانات الكبيرة |
| RC5 | 🟢 **آمن** | مع اختيار r ≥ 12 |
| AES | 🟢 **المعيار الحالي** | بديل DES منذ 2001 |

---

## 🗒️ ملاحظات للامتحان

> هذه النقاط الأهم من الملزمة للامتحان:

**DES:**
- الـ S-boxes هي مصدر الأمان الحقيقي في DES (اللاخطية)
- نفس الخوارزمية للتشفير وفك التشفير (فقط ترتيب subkeys معكوس)
- `Lᵢ = Rᵢ₋₁` و `Rᵢ = Lᵢ₋₁ ⊕ f(Rᵢ₋₁, Kᵢ)`

**ECB vs CBC:**
- ECB: نفس النص → نفس التشفير (ضعف كبير!)
- CBC: `Cᵢ = Ek(Mᵢ ⊕ Cᵢ₋₁)` — يكسر الأنماط المتكررة

**Diffusion vs Confusion (Shannon):**
- Diffusion (P-boxes): كل bit في النص يؤثر على بتات كثيرة في التشفير
- Confusion (S-boxes): يجعل العلاقة بين المفتاح والتشفير معقدة

**GOST vs DES الفروق:**
- GOST: 32 جولة، 256-bit key، S-boxes سرية، circular shift بدل P-box
- DES: 16 جولة، 56-bit key، S-boxes ثابتة ومعروفة

---

## 👨‍💻 المطوِّر

**CYBER FORCE_280**  
طالب — قسم أمن الحاسوب والمعلومات  
الجامعة التكنولوجية، بغداد

---

## 📄 الترخيص

هذا المشروع للأغراض التعليمية فقط.  
المحتوى النظري مستند إلى ملزمة أ.د. هالة بهجت عبد الوهاب.
