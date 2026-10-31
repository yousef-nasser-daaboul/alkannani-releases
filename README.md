# alkannani-releases

صفحة تنزيل تطبيق **الكنّاني** (مواقيت الصلاة والأذان) لأجهزة Android، وملف التحديث الذي يقرؤه التطبيق، وسياسة الخصوصية. التطبيق ليس على Google Play بعد، فيُوزَّع ملف APK من هنا.

كل محتوى المستودع منشور عبر GitHub Pages (فرع `main`، المجلد الجذر):

| الرابط | الملف | الغرض |
| --- | --- | --- |
| https://yousef-nasser-daaboul.github.io/alkannani-releases/ | `index.html` | صفحة التنزيل، وهي الرابط الذي يُشارَك مع المستخدمين |
| https://yousef-nasser-daaboul.github.io/alkannani-releases/version.json | `version.json` | يقرؤه التطبيق ليعرف إن كان هناك إصدار أحدث |
| https://yousef-nasser-daaboul.github.io/alkannani-releases/privacy-policy/ | `privacy-policy/index.html` | سياسة الخصوصية، وهي الرابط الذي يوضع في المتجرين |

`icon.jpg` و`favicon.png` نسختان مصغّرتان من أيقونة التطبيق للصفحة. `screenshots/{light,dark}/` لقطات الشاشة في صفحة التنزيل، تظهر منها نسخة الوضع الفاتح أو الداكن حسب جهاز الزائر. كلها لقطات من محاكي Pixel 9a مصغّرة إلى عرض 540 بكسل بصيغة JPEG: من `01` إلى `05` هي لقطات `store/screenshots/android/raw/` في مستودع التطبيق (الإصدار 1.0)، ومن `06` إلى `12` صُوّرت من الإصدار 1.2.0 (الترحيب، والويدجت، وشاشة القفل، واختيار المدينة، وشاشات الإعداد الأول). `07-widgets` و`08-lock-screen` مقصوصتان إلى أعلى الشاشة (540×675). إن أعدت التصوير فاحفظ الصور بالأسماء نفسها. `.nojekyll` يجعل Pages ينشر الملفات كما هي دون Jekyll.

## ملفات APK

ملفات APK لا توضع في المستودع، بل تُرفق بـ GitHub Release لكل إصدار، بوسم مثل `v1.0.0`. اسم الملف المرفق هو دائماً `alkannani.apk`، فيبقى رابطان ثابتان:

- آخر إصدار (زر التنزيل في الصفحة): `https://github.com/yousef-nasser-daaboul/alkannani-releases/releases/latest/download/alkannani.apk`
- إصدار محدد (الحقل `url` في `version.json`): `https://github.com/yousef-nasser-daaboul/alkannani-releases/releases/download/v1.0.0/alkannani.apk`

كل ملفات APK تُبنى بملف البناء `apk` في `eas.json` في مستودع التطبيق، وتُوقَّع بمفتاح EAS نفسه، وإلا لن يستطيع المستخدم التثبيت فوق الإصدار السابق. خطوات النشر بالترتيب في القسم 4 «توزيع APK خارج المتجر» في `store/RELEASE.md` في مستودع التطبيق.

## `version.json`

```json
{
  "latest": 2,
  "minimum": 1,
  "version": "1.0.1",
  "url": "https://github.com/yousef-nasser-daaboul/alkannani-releases/releases/download/v1.0.1/alkannani.apk",
  "notes": "تصحيح وقت الفجر في بعض المدن."
}
```

- `latest` (إلزامي): رقم البناء (`versionCode`) لآخر APK منشور. التطبيق الذي رقم بنائه أقل منه يعرض رسالة «يوجد تحديث» يمكن تأجيلها.
- `minimum` (إلزامي): أقل رقم بناء مسموح به. التطبيق الذي رقم بنائه أقل منه يعرض شاشة تحديث إجبارية. لا يزيد على `latest`.
- `version` (اختياري): الإصدار الظاهر للمستخدم (الحقل `version` في `app.json`)، للعرض فقط في صفحة التنزيل. المقارنة تكون بأرقام البناء وحدها.
- `url` (إلزامي): رابط APK للإصدار المحدد `latest`، لا رابط `latest/download`، حتى لا يتغير الملف الذي يشير إليه.
- `notes` (اختياري): نص عربي قصير يظهر في رسالة التحديث وفي قسم «ما الجديد» في صفحة التنزيل. إن كتبت كل تغيير في سطر (`\n` بين الأسطر)، تعرضه الصفحة قائمة نقطية.

أرقام البناء تديرها خوادم EAS وتزيدها مع كل بناء، ويشترك فيها ملفا البناء `production` و`apk`. اقرأ الرقم الحالي بالأمر `npx eas-cli@latest build:version:get -p android` في مستودع التطبيق، أو من صفحة البناء على expo.dev.

لا تكتب الملف يدوياً: `npm run version-json` في مستودع التطبيق يكتبه من رقم البناء والإصدار والملاحظات، ويرفض القيم التي لا يقبلها التطبيق أو لا معنى لها.

لماذا GitHub Pages وليس jsDelivr: ذاكرة jsDelivr المؤقتة تؤخر وصول التغيير إلى الأجهزة، وهذا لا يناسب التحديث الإجباري. GitHub Pages يُحدَّث خلال دقائق من الدفع.

## سياسة الخصوصية

نُقلت من `store/privacy-policy/` في مستودع التطبيق، وهذا مكانها الوحيد الآن. حدّث تاريخ السريان في ثلاثة مواضع عند كل تعديل: أعلى الصفحة، والملخص الإنجليزي، والتذييل.
