# שביל הטיול לתאילנד 🌴 — הוראות הקמה

אתר עצמאי לחלוטין: קובץ `index.html` אחד שרץ על GitHub Pages (חינם),
עם שמירת הגשות ותמונות ב-Firebase Firestore (חינם, של Google, הנתונים לא נמחקים).

---

## שלב 1 — העלאה ל-GitHub Pages (5 דקות)

1. היכנסו ל-github.com והתחברו (או פתחו חשבון חינמי).
2. לחצו **New repository** → תנו שם, למשל `thailand-trip` → סמנו **Public** → **Create repository**.
3. לחצו **uploading an existing file** והעלו את `index.html` → **Commit changes**.
4. בתפריט הריפו: **Settings → Pages** → תחת **Branch** בחרו `main` ותיקיית `/ (root)` → **Save**.
5. אחרי דקה-שתיים תקבלו כתובת בסגנון:
   `https://<שם-המשתמש>.github.io/thailand-trip/`

**עריכה עתידית:** פותחים את `index.html` בריפו → כפתור העיפרון ✏️ → עורכים →
Commit. השינוי עולה לאוויר תוך דקה. כל ההגדרות (משפחות, מלונות, טיסות, משימות)
נמצאות באובייקט `CONFIG` בראש הקובץ.

---

## שלב 2 — חיבור Firebase לשמירת תמונות והגשות (10 דקות)

בלי השלב הזה האתר עובד ב"מצב תצוגה מקומי" — הכול נראה ועובד, אבל הנתונים
נשמרים רק במכשיר של כל משתמש. לשיתוף אמיתי בין כולם:

1. היכנסו ל-https://console.firebase.google.com עם חשבון Google → **Add project**.
2. תנו שם (למשל `thailand-trip`) → אפשר לבטל את Google Analytics → **Create project**.
3. במסך הפרויקט: לחצו על סמל ה-**Web** `</>` → תנו כינוי לאפליקציה → **Register app**.
4. יוצג לכם אובייקט `firebaseConfig` — **העתיקו את הערכים** והדביקו אותם
   בראש `index.html` בתוך `FIREBASE_CONFIG` (apiKey, authDomain, projectId וכו').
5. בתפריט הצד: **Build → Firestore Database → Create database** →
   בחרו מיקום (למשל `eur3`) → התחילו ב-**production mode** → **Create**.
6. בלשונית **Rules** של Firestore, הדביקו את החוקים הבאים ולחצו **Publish**:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /submissions/{doc} {
      allow read, write: if true;
    }
    match /photos/{doc} {
      allow read, write: if true;
    }
  }
}
```

> ⚠️ החוקים פתוחים כדי שכל המשפחות יוכלו להעלות בלי התחברות. זה מתאים
> לפרויקט משפחתי קצר-מועד; מי שיש לו את הקישור יכול לכתוב לבסיס הנתונים.
> מומלץ אחרי הטיול לשנות את `if true` ל-`if false` (נעילה) — התמונות יישארו
> שמורות ותוכלו להמשיך להוריד אותן מקונסולת Firebase.

7. עדכנו את `index.html` בגיטהאב עם ה-config → סיימתם. הבאנר הכתום ייעלם.

**מגבלות החינם של Firestore:** ‏1GB אחסון, ‏50,000 קריאות ו-20,000 כתיבות ביום —
הרבה מעבר לצורך של 5 משפחות. התמונות נדחסות אוטומטית לפני שמירה (~200-350KB לתמונה),
כך ש-1GB מספיק לכ-3,000+ תמונות.

---

## שלב 3 — צריבת תגי ה-NFC

לכל משפחה צורבים קישור עם הפרמטר שלה (בחירת המשפחה תיטען אוטומטית):

| משפחה   | קישור לצריבה |
|---------|--------------|
| בוהדנה  | `https://<user>.github.io/thailand-trip/?f=bohadana` |
| עובדיה  | `https://<user>.github.io/thailand-trip/?f=ovadia` |
| משה     | `https://<user>.github.io/thailand-trip/?f=moshe` |
| שדה     | `https://<user>.github.io/thailand-trip/?f=sade` |
| בוזגלו  | `https://<user>.github.io/thailand-trip/?f=buzaglo` |
| **מנהל** | `https://<user>.github.io/thailand-trip/?admin` |

הקישור של המנהל פותח ישר את מסך הזנת הקוד (ברירת מחדל: `2026` —
מומלץ לשנות ב-`CONFIG.adminCode`).

צריבה: כל אפליקציית NFC חינמית (למשל **NFC Tools**) → Write → Add a record →
URL → הדביקו את הקישור → Write והצמידו את התג.

---

## מסך המנהל

- דוח יומי: מי הגיש ומי חסר, וטבלת ✓ לכל הימים שעברו.
- לכל משפחה: תקצירי ההגשות, תצוגת תמונות, וכפתור **⬇️ ZIP** שמוריד את כל
  התמונות של המשפחה + קובץ טקסט עם כל ההגשות שלה.
- מומלץ להוריד ZIP לכל המשפחות אחת לכמה ימים כגיבוי (בכל מקרה הנתונים
  נשמרים ב-Firebase ולא נמחקים מעצמם).

## עריכת משימות

בתוך `CONFIG.tasks` — מוסיפים שורה לכל תאריך:

```js
tasks: {
  "2026-07-26": "צלמו תמונה משפחתית בשדה התעופה...",
  "2026-07-27": "המשימה של היום הראשון בפוקט...",
},
```

תאריך בלי משימה יציג את `defaultTask`.
