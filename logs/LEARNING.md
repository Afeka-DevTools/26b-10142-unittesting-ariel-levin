🧑‍🎓
תסביר בבקשה על כתיבת בדיקות יחידה בשפת Java

🤖
כתיבת בדיקות יחידה (Unit Tests) היא אחת הפרקטיקות החשובות ביותר בפיתוח תוכנה. המטרה שלהן היא פשוטה: לוודא שרכיב קוד קטן ומבודד (לרוב מתודה בודדת במחלקה) עובד בדיוק כפי שהוא אמור לעבוד, בלי תלות בגורמים חיצוניים כמו בסיסי נתונים או שרתי רשת.

בסביבת Java, כלי הבדיקות הסטנדרטי והפופולרי ביותר הוא JUnit (כאשר הגרסה המודרנית והנפוצה ביותר כיום היא JUnit 5).

מבנה הבדיקה: תבנית ה-AAA
כדי שהבדיקות שלך יהיו קריאות ומסודרות, נהוג לכתוב אותן לפי תבנית קבועה שנקראת AAA:

Arrange (הכנה): מייצרים את האובייקטים ומכינים את הנתונים הדרושים לבדיקה.

Act (פעולה): מפעילים את המתודה שאותה רוצים לבדוק שומרים את התוצאה.

Assert (וידוא): בודקים אם התוצאה שהתקבלה בפועל (Actual) תואמת את התוצאה שציפינו לה (Expected).

האנוטציות (Annotations) המרכזיות ב-JUnit 5
JUnit מבוססת על אנוטציות שמספרות ל-Framework איך להריץ את הקוד:

@Test: מסמנת מתודה כמתודת בדיקה.

@BeforeEach: מתודה שתרוץ לפני כל בדיקה במחלקה (מעולה לאיפוס נתונים או יצירת אובייקטים חדשים).

@AfterEach: מתודה שתרוץ אחרי כל בדיקה (למשל, לניקוי משאבים).

@BeforeAll / @AfterAll: רצות פעם אחת בלבד לפני או אחרי כל קובץ הבדיקות (חייבות להיות מתודות סטטיות).

דוגמה מעשית בקוד
נניח שיש לנו מחלקה פשוטה של מחשבון שאותה נרצה לבדוק:

Java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public double divide(int a, int b) {
        if (b == 0) {
            throw new IllegalArgumentException("Cannot divide by zero");
        }
        return (double) a / b;
    }
}
וכך תיראה מחלקת הבדיקות עבורה בעזרת JUnit 5:

Java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {

    private Calculator calculator;

    // ירוץ לפני כל טסט - מבטיח שנתחיל "דף חלק"
    @BeforeEach
    public void setUp() {
        calculator = new Calculator();
    }

    @Test
    public void testAdd_PositiveNumbers_ReturnsCorrectSum() {
        // 1. Arrange (כבר קרה ב-setUp)
        
        // 2. Act
        int result = calculator.add(5, 3);
        
        // 3. Assert
        assertEquals(8, result, "5 + 3 should equal 8");
    }

    @Test
    public void testDivide_ByZero_ThrowsException() {
        // בדיקה שמוודא שקוד זורק שגיאה כשצריך
        assertThrows(IllegalArgumentException.class, () -> {
            calculator.divide(10, 0);
        });
    }
}
פקודות וידוא נפוצות (Assertions)
החלק של ה-Assert משתמש במתודות סטטיות מהמחלקה Assertions:

assertEquals(expected, actual): בודק ששני הערכים שווים.

assertTrue(condition) / assertFalse(condition): בודק האם תנאי הוא אמת או שקר.

assertNull(object) / assertNotNull(object): בודק האם אובייקט הוא null או קיים.

assertIterableEquals(list1, list2): בודק ששתי רשימות מכילות את אותם איברים ובאותו סדר.

טיפ של מקצוענים: כשאתה כותב בדיקות, תמיד כדאי לבדוק גם את "מקרי הקצה" (Edge Cases) – מספרים שליליים, אפס, מחרוזות ריקות או ערכי null. שם בדרך כלל מסתתרים הבאגים האמיתיים.

האם יש פרויקט ספציפי שאתה עובד עליו כרגע ותרצה שנכתוב עבורו בדיקות יחידה יחד, או שתרצה להעמיק בנושא של "מוקינג" (Mocking) עם Mockito לבדיקת מחלקות מורכבות יותר?

🧑‍🎓
בבקשה תסביר בצורה ברור, כולל מתן הקשר רחב, ודרישה לפורמט מסוים על הנושא

🤖
בדיקות יחידה ב-Java: ההקשר המלא והפורמט המנצח
כדי להבין בדיקות יחידה באמת, לא מספיק לדעת רק את הסינטקס הכללי של JUnit. צריך להבין למה אנחנו עושים את זה, איפה זה פוגש אותנו בתהליך הפיתוח המודרני, ומהו המבנה (הפורמט) המדויק שהופך בדיקה מטקסט מציק לקוד שמציל את הפרודקשן.

1. ההקשר הרחב: פירמידת הבדיקות ו-CI/CD
בעולם התוכנה, בדיקות יחידה הן לא סוג הבדיקות היחיד, אך הן מהוות את הבסיס האיתן ביותר של המוצר. נהוג לתאר זאת באמצעות מודל שנקרא פירמידת הבדיקות (The Testing Pyramid):

Test Pyramid with User Interface Tests, Integration Tests and Unit Tests. Source: Getty Images
מידע נוסף

בדיקות יחידה (Unit Tests): הבסיס הרחב של הפירמידה. הן בודקות פונקציה או רכיב בודד ומבודד. הן רצות באלפיות השנייה, קלות לכתיבה וזולות מאוד לתחזוקה.

בדיקות אינטגרציה (Integration Tests): שכבה אמצעית. בודקות את החיבור בין כמה רכיבים (למשל, האם הקוד שלנו מצליח לדבר בצורה נכונה עם בסיס הנתונים). הן איטיות ומורכבות יותר.

בדיקות קצה לקצה (E2E / UI Tests): השפיץ של הפירמידה. בודקות את המערכת כולה מנקודת המבט של המשתמש (למשל, סימולציה של לחיצה על כפתורים בדפדפן). הן איטיות, "שבירות" ויקרות לתחזוקה.

איפה זה פוגש אותנו ביום-יום? > בדיקות יחידה הן לב לבו של תהליך ה-CI/CD (Continuous Integration). בכל פעם שמפתח מבצע Commit ודוחף קוד ל-GitHub או GitLab, שרת אוטומטי מריץ מיד את כל בדיקות היחידה. אם שינוי קטן שביצעת במקום אחד הרס בטעות לוגיקה במקום אחר – הבדיקות "יצעקו" והבנייה תיכשל מיד, לפני שהבאג יגיע למשתמשי הקצה.

2. הפורמט המבני: עקרונות F.I.R.S.T
כדי שבדיקת יחידה תעמוד בסטנדרט של חברות הייטק מובילות, היא חייבת להיכתב על פי חמשת עקרונות FIRST:

Fast (מהירה): אלפי בדיקות יחידה צריכות לרוץ בכמה שניות. אם הן יהיו איטיות, מפתחים יפסיקו להריץ אותן לפני שהם דוחפים קוד.

Independent (עצמאית): בדיקה אחת לעולם לא תלויה בתוצאה של בדיקה אחרת. אין חשיבות לסדר ההרצה שלהן, וכל אחת צריכה להכין ולנקות את הנתונים של עצמה.

Repeatable (הדירה): בדיקה חייבת להחזיר תמיד, אבל תמיד, את אותה התוצאה. לא משנה אם הרצת אותה על המחשב האישי שלך, ב-1:00 בלילה, או על שרת ה-CI בענן.

Self-Validating (בדיקה עצמית): הבדיקה יודעת לבד אם היא עברה או נכשלה באמצעות Assertions. המפתח לא צריך לקרוא לוגים כדי להבין אם הכל תקין.

Timely (בזמן): בדיקות נכתבות במקביל לכתיבת קוד המוצר (או אפילו לפניו, בגישה שנקראת TDD - Test Driven Development).

3. הפורמט המעשי: תבנית קוד תקנית ב-Java
כשניגשים לכתוב קובץ בדיקות, ישנו פורמט מוסכם (Best Practice) המשלב חלוקה לבלוקים (AAA) וקונבנציית שמות ברורה:

פורמט שמות המתודות
שם המתודה צריך להסביר בדיוק מה נבדק ומה הציפייה, ללא צורך לקרוא את קוד הבדיקה עצמו. הפורמט המקובל ביותר הוא:
should_[ExpectedBehavior]_when_[StateUnderTest]

קוד לדוגמה בפורמט התקני:
Java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class OrderServiceTest {

    private OrderService orderService;

    @BeforeEach
    public void setUp() {
        // אתחול נקי לפני כל בדיקה
        orderService = new OrderService();
    }

    @Test
    public void should_calculateDiscount_when_userIsVIP() {
        // 1. Arrange (הכנת הנתונים והסביבה)
        User vipUser = new User("Yossi", UserRole.VIP);
        double originalPrice = 100.0;

        // 2. Act (ביצוע הפעולה הנבדקת)
        double finalPrice = orderService.calculateFinalPrice(vipUser, originalPrice);

        // 3. Assert (וידוא התוצאה מול הציפייה)
        assertEquals(80.0, finalPrice, "VIP users should get a 20% discount");
    }

    @Test
    public void should_throwException_when_orderPriceIsNegative() {
        // Arrange
        User user = new User("Dana", UserRole.REGULAR);
        double invalidPrice = -50.0;

        // Act & Assert משולבים במקרה של חריגה (Exception)
        assertThrows(IllegalArgumentException.class, () -> {
            orderService.calculateFinalPrice(user, invalidPrice);
        });
    }
}
האם תרצה שנתרגל כעת כתיבת בדיקה לפי הפורמט הזה עבור פונקציה מורכבת יותר, כמו פונקציה שמטפלת במחרוזות (Strings) או לוגיקה עסקית אחרת שאתה עובד עליה?

🧑‍🎓
תודה רבה, לא צריך עוד. הבנתי מספיק

🤖
בשמחה רבה! שמחתי לעזור.

אם תצטרך משהו בעתיד לגבי Java, בדיקות, או כל אתגר תכנותי אחר – אתה יודע איפה למצוא אותי.

המון בהצלחה בהמשך הפיתוח!