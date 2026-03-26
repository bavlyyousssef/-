# 🎭 فريق ايل شداي المسرحي — نظام الحضور

## 📁 محتوى الفولدر

```
shadai/
├── index.html          ← صفحة تسجيل الدخول
├── app.html            ← التطبيق الرئيسي (محمي)
├── firebase-config.js  ← إعدادات Firebase (عدّله أولاً)
└── README.md           ← هذا الملف
```

---

## 🔥 خطوات إعداد Firebase

### ١. أنشئ مشروع
- اذهب إلى: https://console.firebase.google.com
- اضغط **Add project** واتبع الخطوات

### ٢. أنشئ Realtime Database
- من القائمة الجانبية: **Build → Realtime Database → Create Database**
- اختر **Start in test mode** (مؤقتاً)

### ٣. انسخ إعدادات المشروع
- اضغط ⚙ **Project Settings → General**
- في **Your apps** اضغط `</>` (Web app)
- انسخ بيانات `firebaseConfig`

### ٤. عدّل ملف `firebase-config.js`
افتح الملف واستبدل القيم الوهمية ببيانات مشروعك.

---

## 🔐 إعداد بيانات الدخول في Firebase

في **Realtime Database** أنشئ هذا المسار يدوياً:

```
settings/
  credentials/
    username: "اسم_المستخدم_هنا"
    password: "كلمة_المرور_هنا"
```

**طريقة الإنشاء:**
1. افتح Realtime Database
2. اضغط **+** بجانب الـ root
3. اكتب `settings` ثم `+` مرة أخرى
4. اكتب `credentials` ثم أضف `username` و `password`

---

## 🔒 تأمين قواعد البيانات (مهم قبل النشر)

في **Realtime Database → Rules** ضع هذه القواعد:

```json
{
  "rules": {
    ".read": false,
    ".write": false,
    "settings": {
      ".read": true,
      ".write": false
    },
    "members": {
      ".read": true,
      ".write": true
    },
    "attendance": {
      ".read": true,
      ".write": true
    }
  }
}
```

> ⚠️ هذه القواعد تسمح بقراءة بيانات الدخول للتحقق منها.
> للمزيد من الأمان، استخدم Firebase Authentication في المستقبل.

---

## 🌐 رفع الموقع (Hosting)

### خيار ١: Firebase Hosting (مجاناً)
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

### خيار ٢: Netlify (مجاناً)
- اذهب إلى https://netlify.com
- اسحب الفولدر كاملاً وأفلته في الموقع

### خيار ٣: GitHub Pages (مجاناً)
- ارفع الملفات على GitHub Repository
- فعّل GitHub Pages من الـ Settings

---

## ✅ ملاحظات

- الجلسة تنتهي عند إغلاق المتصفح (sessionStorage)
- البيانات محفوظة في Firebase وتشترك بين كل الأجهزة
- التصدير CSV يدعم Excel بالعربية مع BOM
