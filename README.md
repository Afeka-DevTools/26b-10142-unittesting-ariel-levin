# פרויקט בדיקות יחידה ב-Java (Unit Testing Exercise)

מערכת בדיקות יחידה אוטומטית מבוססת **JUnit 5** ו-**Gradle** לבדיקת פונקציות הלוגיקה והעזר במחלקה `App`

---

## חברי הצוות / מגיש המטלה
* **אריאל לוין**
---

## מדריך הרצה למשתמש (Getting Started)

כדי להריץ את כל בדיקות היחידה שנכתבו בפרויקט אצלכם במחשב המקומי, יש לעקוב אחר השלבים הבאים לפי הסדר

### דרישות קדם (Prerequisites)
* ודאו שמותקנת אצלכם סביבת ריצה של Java (**JDK 17** ומעלה מומלצת).
* פתחו את הטרמינל (Terminal / PowerShell / CMD) בתיקייה שבה תרצו לשמור את הפרויקט

---

### שלב 1: שכפול הפרויקט (Clone)
העתיקו והריצו את הפקודה הבאה בטרמינל כדי לשכפל את המאגר מ-GitHub למחשבכם האישי
```bash
git clone https://github.com/ariel-levin/26b-10142-unittesting-ariel-levin.git
```

---
### שלב 2: ניווט לתוך תיקיית הפרויקט
לאחר סיום השכפול, היכנסו לתיקיית השורש של הפרויקט בעזרת פקודת הניווט

```bash
cd 26b-10142-unittesting-ariel-levin
```

---
### שלב 3: הרצת בדיקות היחידה (Run Tests)
הפרויקט משתמש ב-Gradle Wrapper ולכן אין צורך להתקין Gradle על המחשב. הריצו את פקודת הבדיקה המתאימה למערכת ההפעלה שלכם

### במערכות Windows (PowerShell / CMD)
```PowerShell
.\gradlew test
```

### במערכות Mac / Linux
```bash
./gradlew test
```

---

### הפקת דוח כיסוי קוד (JaCoCo Code Coverage)
הפרויקט מוגדר להפקת דוחות כיסוי קוד באמצעות תוסף JaCoCo. כדי להריץ את הבדיקות וליצור דוח ויזואלי (HTML), השתמשו בפקודה הבאה

### במערכות Windows
```PowerShell
.\gradlew jacocoTestReport
```

### במערכות Mac / Linux
```bash
./gradlew jacocoTestReport
```

---

### איפה מוצאים את הדוח
לאחר סיום הריצה, הדוח הוויזואלי יישמר בנתיב הבא
build/reports/jacoco/test/html/index.html

ניתן לפתוח את הקובץ index.html ישירות בכל דפדפן כדי לראות אילו שורות קוד נבדקו ובאיזה אחוז
