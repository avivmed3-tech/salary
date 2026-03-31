# מחשבון שכר — מדריך העלאה לחנות האפליקציות

## קבצים בחבילה

| קובץ | תיאור |
|---|---|
| `index.html` | האפליקציה הראשית (5,800+ שורות, 130 פונקציות) |
| `sw.js` | Service Worker v10 עם offline מלא + CDN caching |
| `manifest.json` | Web App Manifest מוכן ל-TWA |
| `.well-known/assetlinks.json` | Digital Asset Links (עדכן SHA256 לפני deploy) |

## שלב 1: אירוח (HTTPS — חובה)

### אפשרות א: Netlify (מומלץ, חינם)
1. לך ל-[netlify.com](https://netlify.com) → Sign up
2. גרור את תיקיית הפרויקט ל-Deploy area
3. תקבל דומיין: `your-app.netlify.app`
4. (אופציונלי) חבר דומיין מותאם אישית

### אפשרות ב: GitHub Pages (חינם)
1. צור repo חדש ב-GitHub
2. העלה את כל הקבצים
3. Settings → Pages → Source: main branch
4. תקבל דומיין: `username.github.io/repo-name`

### אפשרות ג: Vercel (חינם)
1. לך ל-[vercel.com](https://vercel.com) → Import project
2. חבר ל-GitHub repo
3. Deploy אוטומטי

## שלב 2: בדיקת Lighthouse

לפני העלאה לחנות, הרץ Lighthouse בכרום:
1. F12 → Lighthouse → Generate report
2. ודא שה-PWA score מעל 80
3. תקן כל בעיה אדומה

## שלב 3: Google Play (TWA)

### דרישות מוקדמות
- חשבון Google Play Console ($25 חד-פעמי)
- האתר חי ב-HTTPS
- Lighthouse PWA score ≥ 80

### הוראות

#### שיטה א: PWABuilder (קלה — מומלץ)
1. לך ל-[pwabuilder.com](https://www.pwabuilder.com)
2. הכנס את ה-URL של האפליקציה שלך
3. לחץ "Package for stores" → Android
4. הורד את ה-APK/AAB
5. העלה ל-Google Play Console

#### שיטה ב: Bubblewrap (CLI)
```bash
npm i -g @nicolo-ribaudo/bubblewrap
bubblewrap init --manifest=https://YOUR-DOMAIN/manifest.json
bubblewrap build
```

### Digital Asset Links
1. אחרי שיש לך signing key, קבל את ה-SHA256:
   ```bash
   keytool -list -v -keystore my-key.keystore | grep SHA256
   ```
2. עדכן את `.well-known/assetlinks.json` עם ה-fingerprint
3. העלה ל-`https://YOUR-DOMAIN/.well-known/assetlinks.json`
4. ודא ש-`https://YOUR-DOMAIN/.well-known/assetlinks.json` נגיש בדפדפן

### הגשה ל-Google Play Console
1. צור אפליקציה חדשה (שם: "מחשבון שכר", קטגוריה: Finance)
2. מלא את כל הפרטים הנדרשים:
   - שם: מחשבון שכר — חישוב משכורת
   - תיאור קצר: חישוב שכר נטו, מעקב שעות, הטבות ארוחות
   - תיאור מלא: (ראה למטה)
   - קטגוריה: Finance
   - תמחור: Free (עם in-app purchases אופציונלי)
3. העלה screenshots (4-8 צילומי מסך)
4. העלה את ה-AAB מ-PWABuilder
5. Start internal testing → הרחב ל-Production

## שלב 4: Apple App Store (אופציונלי)

⚠️ Apple דוחה PWA wraps טהורים. צריך Capacitor עם פיצ'רים native.

```bash
npm init @capacitor/app
npx cap add ios
npx cap copy ios
npx cap open ios
```

מומלץ להוסיף לפחות: Widget, Siri Shortcuts, או Haptics כדי לעבור review.

## תיאור לחנות (copy-paste)

### שם
מחשבון שכר — חישוב משכורת

### תיאור קצר (80 תווים)
חישוב שכר נטו מברוטו, מעקב שעות עבודה, והטבות ארוחות

### תיאור מלא
מחשבון השכר הישראלי המקצועי ביותר — מעודכן לשנת המס 2026.

🔢 חישוב שכר מדויק
• נטו מברוטו בלחיצה אחת
• מדרגות מס הכנסה 2026
• ביטוח לאומי ומס בריאות
• פנסיה וקרן השתלמות
• נקודות זיכוי לפי גיל ילדים

🕐 שעון נוכחות חכם
• כניסה/יציאה בלחיצה
• לוח שעות חודשי עם כניסות ויציאות
• חישוב אוטומטי של שעות נוספות (125% / 150%)
• מעקב גבול 60 שעות נוספות

🍽️ הטבת ארוחות
• סיבוס, תן ביס, פתקי אוכל
• מעקב יתרה ושימוש חודשי
• התראות חכמות

📊 דשבורד מקצועי
• גרף עוגה של הניכויים
• השוואה לחודש קודם
• עלות מעסיק מלאה
• ייצוא לאקסל ותלוש PDF

🔒 פרטיות מלאה
• כל הנתונים נשמרים מקומית על המכשיר שלך
• אין רישום, אין שרתים, אין מעקב
• גיבוי ושחזור בלחיצה

### מילות מפתח (keywords)
מחשבון שכר, חישוב משכורת, נטו ברוטו, מס הכנסה, ביטוח לאומי, שעות עבודה, תלוש שכר, פנסיה, ישראל, 2026
