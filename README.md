# 📖 Quran Reels Generator | أداة عمل ريلز القرآن الكريم

[English](#english) | [العربية](#arabic)

---

<a name="arabic"></a>
## 🇪🇬 اللغة العربية

أداة ذكية ومؤتمتة تتيح لك إنشاء مقاطع فيديو قصيرة (Reels/Shorts) للقرآن الكريم بجودة عالية وبضغطة زر واحدة. تقوم الأداة بدمج التلاوة العطرة مع النص القرآني بالرسم العثماني فوق خلفيات طبيعية خلابة.

### 🚀 المميزات
- **أتمتة كاملة:** جلب النصوص والتسجيلات الصوتية تلقائياً من الإنترنت.
- **تنوع القراء:** دعم لأكثر من 10 قراء من مشاهير العالم الإسلامي.
- **خلفيات ديناميكية:** اختيار عشوائي لمقاطع فيديو طبيعية لضمان عدم التكرار.
- **تنسيق ذكي:** ضبط تلقائي لحجم الخط وتوزيعه ليناسب شاشات الجوال.
- **دعم اللغة العربية:** معالجة النصوص العربية وعرضها بشكل صحيح ومشكول.

### ⚙️ كيف تعمل الأداة؟
تعمل الأداة من خلال دورة حياة برمجية منظمة:
1. **الواجهة (UI):** واجهة ويب بسيطة مبنية بـ HTML/JS للتفاعل مع المستخدم.
2. **الخادم (Backend):** مبني باستخدام **Flask** لاستقبال الطلبات ومعالجتها.
3. **البيانات:** يتم جلب النص العثماني من `api.alquran.cloud` والصوت من `everyayah.com`.
4. **المعالجة الصوتية:** استخدام مكتبة `pydub` لقص الصمت في بداية ونهاية كل آية لضمان التزامن المثالي.
5. **المونتاج الآلي:** استخدام محرك **MoviePy** لتركيب طبقات الفيديو (خلفية + نص + صوت) وتنسيقها.
6. **التصدير:** إنتاج فيديو نهائي بصيغة MP4 وبأبعاد طولية مناسبة لمنصات التواصل الاجتماعي.

### 🛠️ المتطلبات التقنية
لتشغيل المشروع يدوياً، يجب توفر:
- **Python 3.10+**: لغة البرمجة الأساسية.
- **FFmpeg**: المحرك المسؤول عن معالجة الفيديو والصوت (ضروري جداً).
- **ImageMagick**: الأداة المسؤولة عن تحويل النصوص إلى صور لدمجها في الفيديو.

### 📥 طريقة التشغيل اليدوي

#### الخطوة 1: تثبيت المتطلبات الأساسية (ضروري جداً)
افتح نافذة الأوامر (PowerShell أو CMD) **كمسؤول** وقم بتنفيذ الأوامر التالية:

```powershell
# تثبيت FFmpeg
winget install Gyan.FFmpeg

# تثبيت ImageMagick
winget install ImageMagick.ImageMagick
```

#### الخطوة 2: التحقق من التثبيت
بعد التثبيت، تأكد من نجاح العملية بتنفيذ الأوامر التالية:

```powershell
# اختبار FFmpeg
ffmpeg -version

# اختبار ImageMagick
magick -version
```

**ملاحظة:** إذا لم تعمل الأوامر، قم بإعادة تشغيل نافذة الأوامر أو الكمبيوتر.

#### الخطوة 3: تثبيت المشروع
1. قم بتحميل المستودع وفك الضغط عنه.
2. افتح نافذة الأوامر (Terminal) في مجلد المشروع.
3. قم بتثبيت المكتبات اللازمة:
   ```bash
   pip install -r requirements.txt
   ```

#### الخطوة 4: تشغيل الأداة
```bash
python main.py
```
سيفتح المتصفح تلقائياً على الرابط `http://localhost:5000`.

---
 المشروع لأهداف تعليمية فقط وجميع الحقوق محفوظة لأصحابها
<a name="english"></a>
## 🇬🇧 English

An automated, intelligent tool designed to allow you to generate high-quality Quran Reels/Shorts with a single click, combining beautiful recitations with Uthmani script overlays on stunning nature backgrounds.

### 🚀 Features
- **Full Automation:** Automatically fetches Quranic text and audio from the web.
- **Reciter Variety:** Supports over 10 world-renowned reciters.
- **Dynamic Backgrounds:** Randomly selects nature videos to ensure unique content.
- **Smart Formatting:** Auto-adjusts font size and alignment for mobile screens.
- **Arabic Support:** Perfectly handles and renders Arabic diacritics (Tashkeel).

### ⚙️ How It Works
The tool follows a structured workflow:
1. **UI:** A sleek web interface built with HTML/JS for user interaction.
2. **Backend:** Built with **Flask** to handle requests and manage the logic.
3. **Data Sourcing:** Fetches Uthmani text via `api.alquran.cloud` and audio from `everyayah.com`.
4. **Audio Processing:** Uses `pydub` to trim silence at the beginning and end of each verse for perfect synchronization.
5. **Auto-Editing:** Utilizes the **MoviePy** engine to composite video layers (Background + Text + Audio).
6. **Exporting:** Outputs a final MP4 video in vertical orientation (9:16), ready for TikTok, Instagram, and YouTube.

### 🛠️ Technical Requirements
For manual execution, you need:
- **Python 3.10+**: The core programming language.
- **FFmpeg**: The engine responsible for audio/video encoding (Essential).
- **ImageMagick**: Responsible for rendering text into video frames.

### 📥 Manual Execution Guide

#### Step 1: Install Essential Dependencies (Required)
Open PowerShell or Command Prompt **as Administrator** and run the following commands:

```powershell
# Install FFmpeg
winget install Gyan.FFmpeg

# Install ImageMagick
winget install ImageMagick.ImageMagick
```

#### Step 2: Verify Installation
After installation, verify that both tools are properly installed:

```powershell
# Test FFmpeg
ffmpeg -version

# Test ImageMagick
magick -version
```

**Note:** If the commands don't work, restart your terminal or computer.

#### Step 3: Install the Project
1. Download and extract the repository.
2. Open a terminal/command prompt in the project folder.
3. Install Python dependencies:
   ```bash
   pip install -r requirements.txt
   ```

#### Step 4: Run the Application
```bash
python main.py
```
The browser will automatically open at `http://localhost:5000`.

---

### 📞 Support | الدعم
Developed by **Arabian AI School**
- YouTube: [@arabianAiSchool](https://youtube.com/@arabianAiSchool)
- Instagram: [@arabianaischool](https://instagram.com/arabianaischool)

---

### 🎥 Tutorial & Download | روابط الشرح والتحميل
- **Watch Tutorial | فيديو الشرح:** https://youtu.be/TL1Gim1VT40
- **Download Portable Version | تحميل النسخة المحمولة:** https://drive.google.com/file/d/12B7vphnf6WLPWScvLIZX7l31Oh4VKDiR/view?usp=sharing

© المشروع لأهداف تعليمية فقط وجميع الحقوق محفوظة لأصحابها




