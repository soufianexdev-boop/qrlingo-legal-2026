# QRlingo — الصفحات القانونية (Legal Pages)

مجلد جاهز للنشر مباشرة يحتوي على سياسة الخصوصية، شروط الاستخدام، وصفحة حذف الحساب والبيانات
لتطبيق QRlingo — بصيغة HTML/CSS فقط بدون أي مكتبات خارجية، متجاوب، ويدعم الوضع الداكن/الفاتح.

## بنية المجلد

```
qrlingo-legal/
├── index.html                 → الصفحة الرئيسية (فهرس الصفحات القانونية)
├── privacy/
│   └── index.html             → /privacy
├── terms/
│   └── index.html             → /terms
├── delete-account/
│   └── index.html             → /delete-account
├── assets/
│   └── style.css              → التنسيق المشترك لكل الصفحات
└── README.md                  → هذا الملف
```

بفضل استخدام `index.html` داخل مجلد فرعي لكل صفحة، ستحصل تلقائيًا على روابط نظيفة بدون
امتداد `.html` عند رفع المجلد على أي استضافة ثابتة (Static Hosting):

- `https://yourdomain.com/privacy`
- `https://yourdomain.com/terms`
- `https://yourdomain.com/delete-account`

## ✅ قبل النشر — العناصر التي يجب تعبئتها

ابحث عن كل النصوص المميّزة بلون برتقالي (`class="placeholder"`) وابدلها ببياناتك الفعلية:

| الملف | ما يجب تعديله |
|---|---|
| `privacy/index.html` | اسم المطوّر/الشركة القانونية، البريد الإلكتروني، رابط الموقع، عدد أيام الاحتفاظ بالبيانات بعد طلب الحذف |
| `terms/index.html` | القانون الحاكم/الدولة المختصة، البريد الإلكتروني، رابط الموقع |
| `delete-account/index.html` | البريد الإلكتروني في رابط `mailto:` (ابحث عن `PRIVACY_EMAIL@yourdomain.com`)، عدد أيام الرد على طلبات الحذف |

> ملاحظة مهمة: زر "حذف الحساب والبيانات" الحالي داخل تطبيق QRlingo نفسه
> (`pages/settings/settings.html` → `deleteAccount()`) يقوم فقط بمسح بيانات
> `localStorage` على الجهاز وإعادة التوجيه — **لا يحذف الحساب أو الصفوف فعليًا من Supabase**.
> قبل الاعتماد النهائي على الخطوات الموضّحة في صفحة `/delete-account`، تأكد من تحديث تلك
> الدالة لاستدعاء حذف حقيقي (حذف صف `auth.users` عبر Admin API من الخادم، أو RPC مخصّصة)
> بحيث تُطابق واجهة التطبيق ما هو موصوف هنا فعليًا — هذا شرط تدقيق أساسي لدى Google Play وApple.

## 🚀 النشر

### GitHub Pages
1. ادفع محتوى هذا المجلد إلى فرع (مثلاً `main`) في مستودع GitHub.
2. من إعدادات المستودع → Pages، اختر الفرع والمجلد الجذري (`/`).
3. ستصبح الصفحات متاحة على `https://<username>.github.io/<repo>/privacy` وهكذا.
   (لرابط جذر نظيف بدون اسم المستودع، استخدم نطاقًا مخصصًا عبر ملف `CNAME`.)

### Cloudflare Pages
1. أنشئ مشروعًا جديدًا واربطه بمستودع Git يحتوي هذا المجلد، أو ارفع المجلد مباشرة (Direct Upload).
2. اترك إعداد Build Command فارغًا (لا حاجة لأي بناء)، ووجّه Output directory إلى جذر المجلد.
3. بعد النشر ستحصل مباشرة على `/privacy`، `/terms`، `/delete-account`.

### أي استضافة ثابتة أخرى
هذه ملفات HTML/CSS ثابتة بالكامل بدون أي اعتماديات بناء (build) — يمكن رفعها كما هي إلى أي
استضافة ثابتة (Netlify، Vercel، Firebase Hosting، خادم Nginx/Apache عادي...).

## استخدام الروابط في نماذج التقديم

- **Google Play Console**: Data Safety → Privacy Policy URL = رابط `/privacy`، وAccount deletion → رابط `/delete-account`.
- **Apple App Store Connect**: App Privacy → Privacy Policy URL = رابط `/privacy`. لتوافق إرشاد
  5.1.1(v) (Account Deletion)، تأكد أن حذف الحساب متاح أيضًا من داخل التطبيق مباشرة، لا الصفحة فقط.
- **Meta App Review (Facebook Login)**: Privacy Policy URL = رابط `/privacy`، وData Deletion
  Instructions URL = رابط `/delete-account` (هذا الحقل مطلوب تحديدًا من Meta عند تفعيل Facebook Login).
