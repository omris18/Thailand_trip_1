# איפוס מלא – Thailand Trip 2026

## 1. GitHub
העלו את `index.html` החדש.
גרסה זו היא 6.0.0 ומנקה אוטומטית מידע מקומי ישן מהדפדפן בלי למחוק נתוני Firebase.

## 2. Firestore – מחיקת נתונים ישנים
ב-Firebase Console:
Firestore Database → Data

מחקו את ה-collections הבאים:
- scans
- uploads
- completions
- familySessions

אין למחוק:
- familyAccess

## 3. Firestore – החלפת Keys
בתוך collection:
familyAccess

פתחו כל document:
- bohadana
- ovadia
- moshe
- sadeh
- buzaglo

החליפו את field בשם `key` לערך החדש מתוך `FAMILY_KEYS_PRIVATE_NEW.txt`.

## 4. Storage – מחיקת כל התמונות
Firebase Console:
Storage → Files

מחקו את התיקייה:
trip-photos

אם Firebase לא מאפשר למחוק תיקייה ריקה/שלמה, פתחו אותה ומחקו את כל התיקיות המשפחתיות שבתוכה.

## 5. Authentication – אופציונלי
Authentication → Users

אפשר למחוק משתמשים אנונימיים ישנים, אך זה לא חובה.
משתמש המנהל עם האימייל omris18@gmail.com צריך להישאר.

## 6. תגי NFC
צרבו מחדש את הקישורים המלאים מתוך:
FAMILY_KEYS_PRIVATE_NEW.txt

הקישורים הישנים יפסיקו לעבוד לאחר החלפת ה-keys ב-Firestore.

## 7. סדר חלקי הפאזל
הסדר הלוגי הוא:
- משימה 1 → חלק 1
- משימה 2 → חלק 2
- ...
- משימה 8 → חלק 8

המיקום הפיזי בתמונה נשאר לפי החלוקה:
שורה עליונה: 1, 3, 8, 6
שורה תחתונה: 5, 7, 2, 4

כלומר מספר המשימה קובע איזה חלק נפתח, ולא המיקום שלו בתמונה.

## 8. בדיקת איפוס
לאחר ההעלאה והמחיקות:
1. פתחו קישור משפחתי חדש.
2. ודאו שאין חותמות, חלקי פאזל, תמונות או משימות שסומנו.
3. בדף המנהל כל המונים צריכים להציג 0.
4. Storage צריך להיות ריק.
