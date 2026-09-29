# Breakout Radar — تطبيق iPhone أصلي

هذه نسخة **SwiftUI Native** من منطق Breakoutz Radar، مهيأة للعمل مباشرة على iPhone بدون Python أو PyQt وبدون Binance API Key.

## ما تم نقله

- محرك التقييم 0–100.
- Bollinger Bandwidth compression (`COILED`).
- Volume Z-Score (`VOL_SPIKE`).
- Delta Open Interest (`OI_EXPANSION`).
- SMA 7 / SMA 25 لتأكيد الاتجاه.
- جودة جسم الشمعة ورفض الـwick (`STRONG_BODY`).
- شرط قرب السعر من قمة/قاع نطاق 50 شمعة؛ وإلا تُخفض النتيجة للنصف.
- LONG وSHORT.
- تصنيفات `SNIPER` و`WATCHLIST` و`SETUP`.
- تحديث تلقائي أثناء فتح التطبيق.

## تحسينات نسخة iOS

1. يعاد فلتر حجم 24 ساعة قبل اختيار العملات، بدل اختيار أول رموز أبجديًا.
2. إعداد لعدد العملات المراد فحصها: 20–120.
3. إعداد للحد الأدنى لحجم التداول اليومي.
4. الوضع الافتراضي يستخدم آخر شمعة 15 دقيقة مكتملة، للحفاظ على سلوك المحرك الحالي.
5. يوجد خيار **Live Candle** لاستخدام شمعة 15 دقيقة الحالية (أسرع لكنه أكثر ضوضاء).
6. واجهة iPhone عربية مع تفاصيل Z-Score وBBW وΔOI والـflags.

## التشغيل على iPhone باستخدام Xcode

المتطلبات:

- Mac عليه Xcode 16 أو أحدث.
- iPhone يعمل iOS 17 أو أحدث.
- Apple ID للتوقيع.

الخطوات:

1. افتح `BreakoutRadar.xcodeproj` في Xcode.
2. اختر Target باسم `BreakoutRadar`.
3. افتح **Signing & Capabilities**.
4. اختر Apple ID / Team الخاص بك.
5. إذا طلب Xcode، غيّر Bundle Identifier من `com.breakoutradar.ios` إلى اسم فريد مثل `com.yourname.breakoutradar`.
6. صِل iPhone بالماك واختره من قائمة الأجهزة.
7. اضغط **Run ▶︎**.
8. إذا طلب iPhone تفعيل Developer Mode فاتبع تعليمات الجهاز ثم شغّل التطبيق مجددًا.

## بناء IPA غير موقّع عبر GitHub Actions

يوجد Workflow جاهز في:

`.github/workflows/build-ios.yml`

بعد رفع المشروع إلى GitHub يمكنك تشغيله يدويًا من تبويب **Actions**. سيُنتج Artifact باسم `BreakoutRadar-unsigned-ipa`. الملف غير موقّع ويحتاج توقيعًا مناسبًا قبل تثبيته على iPhone.

## ملاحظات مهمة

- المسح يعمل أثناء فتح التطبيق. iOS لا يسمح لتطبيق عادي بأن يبقى ماسحًا نشطًا بشكل مستمر في الخلفية.
- التطبيق يستخدم بيانات Binance USD-M Futures العامة فقط؛ لا توجد مفاتيح API داخل المشروع.
- إذا كانت Binance Futures غير متاحة في شبكتك/بلدك فلن يتمكن التطبيق من تحميل البيانات.
- نتيجة 75 أو 90 ليست احتمال ربح 75% أو 90%؛ هي **Score** وفق قواعد المحرك.

## المصدر والترخيص

هذه النسخة مشتقة من:

`https://github.com/dezveda/breakoutz-radar`

المشروع الأصلي منشور تحت MIT License. تم الاحتفاظ بنص الترخيص في `ORIGINAL_LICENSE.txt`.
