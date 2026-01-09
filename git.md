Sure 👍
Below are **clear, interview-ready answers** for **Beginner / Zero Level TestNG questions**.

---

## 🟢 Beginner / Zero Level – TestNG Interview Answers

---

### 1. What is TestNG?

TestNG is a **testing framework for Java** inspired by JUnit and NUnit. It is used to **design, execute, and manage automated test cases**, mainly for Selenium, API, and unit testing.

---

### 2. Why is TestNG used in test automation?

TestNG provides:

* Easy **test configuration using annotations**
* **Parallel execution**
* **Data-driven testing**
* **Grouping & dependencies**
* **Powerful reporting**
  These features make automation scalable and maintainable.

---

### 3. What does TestNG stand for?

**Test Next Generation**

---

### 4. Advantages of TestNG over JUnit

* Supports **annotations with more flexibility**
* Allows **parallel execution**
* Supports **test grouping**
* Built-in **HTML reports**
* Supports **data-driven testing**
* Better **dependency management**

---

### 5. How do you install TestNG in Eclipse?

1. Go to **Help → Eclipse Marketplace**
2. Search for **TestNG**
3. Install and restart Eclipse
   OR
   Add TestNG dependency using **Maven**.

---

### 6. What is an annotation in TestNG?

Annotations are **keywords that control test execution flow**, such as before/after methods, tests, or suites.

Example:

```java
@Test
public void testMethod() {}
```

---

### 7. Common TestNG annotations

* `@Test`
* `@BeforeMethod`
* `@AfterMethod`
* `@BeforeClass`
* `@AfterClass`
* `@BeforeTest`
* `@AfterTest`
* `@BeforeSuite`
* `@AfterSuite`

---

### 8. What is `@Test` annotation?

It marks a method as a **test case** that TestNG will execute.

---

### 9. What are `@BeforeMethod` and `@AfterMethod`?

* `@BeforeMethod`: Runs **before every test method**
* `@AfterMethod`: Runs **after every test method**

Used for setup and cleanup (e.g., browser launch & close).

---

### 10. Difference between `@BeforeTest` and `@BeforeMethod`

| @BeforeTest                   | @BeforeMethod                |
| ----------------------------- | ---------------------------- |
| Runs once before `<test>` tag | Runs before each test method |
| Executes less frequently      | Executes multiple times      |

---

### 11. What is a TestNG XML file?

`testng.xml` is a configuration file used to:

* Control test execution
* Define suites, tests, classes
* Enable parallel execution

---

### 12. Why do we need `testng.xml`?

To:

* Run multiple tests together
* Set execution order
* Pass parameters
* Enable parallel execution
* Include/exclude tests

---

### 13. How do you run TestNG tests?

* Right-click test class → **Run As → TestNG Test**
* Using `testng.xml`
* Using Maven or Jenkins

---

### 14. What is the default priority of a TestNG test?

**Priority = 0**

---

### 15. What happens if priority is not specified?

TestNG executes tests in **alphabetical order** by method name.

---

### 16. What is the use of `enabled = false`?

It **disables** a test method so it will not be executed.

Example:

```java
@Test(enabled = false)
public void skipTest() {}
```

---

### 17. How do you skip a test in TestNG?

* Using `enabled = false`
* Throwing `SkipException`

---

### 18. Difference between `@BeforeClass` and `@BeforeSuite`

| @BeforeClass                      | @BeforeSuite                  |
| --------------------------------- | ----------------------------- |
| Runs before first method in class | Runs once before entire suite |
| Class level                       | Suite level                   |

---

### 19. Can TestNG run without `testng.xml`?

✅ **Yes**
You can run tests directly using annotations, but advanced features require `testng.xml`.

---

### 20. Execution order of TestNG annotations

1. `@BeforeSuite`
2. `@BeforeTest`
3. `@BeforeClass`
4. `@BeforeMethod`
5. `@Test`
6. `@AfterMethod`
7. `@AfterClass`
8. `@AfterTest`
9. `@AfterSuite`

---
Below are **clear, interview-ready answers** for **Intermediate Level TestNG questions**. These are written in simple language with **examples where useful**, exactly how interviewers expect.

---

## 🟡 Intermediate Level – TestNG Interview Answers

---

### 21. What is **priority** in TestNG?

Priority controls the **order of execution** of test methods.

```java
@Test(priority = 1)
public void login() {}
```

Lower priority value executes first.

---

### 22. What happens if two tests have the same priority?

If priorities are the same, TestNG executes them in **alphabetical order** of method names.

---

### 23. What is **dependsOnMethods**?

It makes one test depend on another test method.

```java
@Test
public void login() {}

@Test(dependsOnMethods = "login")
public void dashboard() {}
```

If `login` fails, `dashboard` is skipped.

---

### 24. What is **dependsOnGroups**?

It makes a test depend on an **entire group**.

```java
@Test(groups = "smoke")
public void login() {}

@Test(dependsOnGroups = "smoke")
public void payment() {}
```

---

### 25. What is **grouping** in TestNG?

Grouping allows you to **categorize tests** like smoke, regression, sanity.

```java
@Test(groups = "regression")
public void test1() {}
```

---

### 26. Why do we use groups in TestNG?

* Run specific test sets
* Reduce execution time
* Support CI/CD pipelines
* Better test management

---

### 27. How do you include or exclude groups in `testng.xml`?

```xml
<groups>
  <run>
    <include name="smoke"/>
    <exclude name="regression"/>
  </run>
</groups>
```

---

### 28. What is **DataProvider** in TestNG?

DataProvider is used for **data-driven testing**, running the same test multiple times with different data.

```java
@DataProvider
public Object[][] data() {
    return new Object[][]{{"user1","pass1"},{"user2","pass2"}};
}
```

---

### 29. Difference between DataProvider and Parameters

| DataProvider       | Parameters      |
| ------------------ | --------------- |
| Multiple data sets | Single data set |
| Used inside code   | Passed from XML |
| Dynamic            | Static          |

---

### 30. How do you pass parameters from `testng.xml`?

```xml
<parameter name="browser" value="chrome"/>
```

```java
@Parameters("browser")
@Test
public void test(String browser) {}
```

---

### 31. What is the use of `@Parameters` annotation?

It receives values from `testng.xml` into test methods.

---

### 32. Can a DataProvider return different data types?

✅ Yes
It returns `Object[][]`, so it can hold **any data type**.

---

### 33. What is **invocationCount**?

Runs the same test method multiple times.

```java
@Test(invocationCount = 3)
public void retryTest() {}
```

---

### 34. What is **threadPoolSize**?

Used with `invocationCount` to enable **parallel execution** of the same test.

```java
@Test(invocationCount = 5, threadPoolSize = 2)
```

---

### 35. What is **timeout** in TestNG?

Specifies the **maximum time** a test can run.

```java
@Test(timeout = 5000)
```

If exceeded, test fails.

---

### 36. What is **expectedExceptions**?

Used to validate expected exceptions.

```java
@Test(expectedExceptions = ArithmeticException.class)
```

---

### 37. How do you handle exceptions in TestNG?

* Using `expectedExceptions`
* Try-catch blocks
* Custom listeners

---

### 38. What is **Soft Assert**?

Soft Assert continues execution even if an assertion fails.

```java
SoftAssert sa = new SoftAssert();
sa.assertTrue(false);
sa.assertAll();
```

---

### 39. Difference between Hard Assert and Soft Assert

| Hard Assert       | Soft Assert             |
| ----------------- | ----------------------- |
| Stops execution   | Continues execution     |
| Immediate failure | Failure reported at end |

---

### 40. What happens if an assertion fails?

* **Hard Assert** → Test stops immediately
* **Soft Assert** → Test continues, failure reported at `assertAll()`

---
Absolutely 👍
Below are **Advanced TestNG questions answered with REAL, PRACTICAL EXAMPLES** (code + explanation).
These are **exactly the kind of answers interviewers expect from experienced candidates**.

---

# 🔵 Advanced TestNG – Answers WITH Examples

---

## 41. What is **parallel execution** in TestNG? (With Example)

Parallel execution means running **multiple tests at the same time** to reduce execution time.

### Example: Parallel execution using `testng.xml`

```xml
<suite name="ParallelSuite" parallel="tests" thread-count="2">
    <test name="ChromeTest">
        <classes>
            <class name="tests.LoginTest"/>
        </classes>
    </test>

    <test name="FirefoxTest">
        <classes>
            <class name="tests.PaymentTest"/>
        </classes>
    </test>
</suite>
```

👉 Both tests run **simultaneously**.

---

## 42. Types of parallel execution (Example)

### `parallel="methods"`

```xml
<suite parallel="methods" thread-count="3">
```

➡ All test methods run in parallel.

### `parallel="classes"`

```xml
<suite parallel="classes" thread-count="2">
```

➡ Test classes run in parallel.

---

## 45. What is a **Listener** in TestNG? (With Example)

Listeners **listen to test execution events**.

### Example: `ITestListener`

```java
public class TestListener implements ITestListener {

    public void onTestFailure(ITestResult result) {
        System.out.println("Test Failed: " + result.getName());
    }
}
```

### Attach listener:

```java
@Listeners(TestListener.class)
public class LoginTest {
    @Test
    public void loginTest() {}
}
```

---

## 50. How do you capture screenshots on failure? (Real Example)

### Listener code:

```java
public void onTestFailure(ITestResult result) {
    TakesScreenshot ts = (TakesScreenshot) driver;
    File src = ts.getScreenshotAs(OutputType.FILE);
    File dest = new File("screenshots/" + result.getName() + ".png");
    FileUtils.copyFile(src, dest);
}
```

📌 **Very common interview question**

---

## 51. What is **RetryAnalyzer**? (With Example)

Automatically re-runs failed tests.

### Retry class:

```java
public class RetryAnalyzer implements IRetryAnalyzer {
    int count = 0;
    int maxRetry = 2;

    public boolean retry(ITestResult result) {
        if (count < maxRetry) {
            count++;
            return true;
        }
        return false;
    }
}
```

### Apply retry:

```java
@Test(retryAnalyzer = RetryAnalyzer.class)
public void flakyTest() {}
```

---

## 52. How do you re-run failed tests? (Example)

After execution, TestNG generates:

```
test-output/testng-failed.xml
```

👉 Run this XML to execute **only failed tests**.

---

## 53. What is **Factory** in TestNG? (With Example)

Factory creates **multiple instances of a test class**.

```java
public class LoginTest {
    String browser;

    public LoginTest(String browser) {
        this.browser = browser;
    }

    @Test
    public void testLogin() {
        System.out.println(browser);
    }
}
```

### Factory class:

```java
@Factory
public Object[] factoryMethod() {
    return new Object[] {
        new LoginTest("Chrome"),
        new LoginTest("Firefox")
    };
}
```

---

## 55. What is `@Optional`? (Example)

```java
@Parameters("browser")
@Test
public void launch(@Optional("chrome") String browser) {
    System.out.println(browser);
}
```

If browser is not passed → defaults to **chrome**.

---

## 57. Dependencies across classes (Best Practice Example)

❌ Bad practice:

```java
dependsOnMethods="OtherClass.method"
```

✅ Best practice:

```java
@Test(groups = "login")
public void loginTest() {}

@Test(dependsOnGroups = "login")
public void dashboardTest() {}
```

---

## 59. What is `preserve-order`? (Example)

```xml
<suite preserve-order="true">
```

Ensures execution follows **XML order**, not alphabetical.

---

## 62. Custom reports using Extent Reports (Example)

```java
ExtentReports report = new ExtentReports();
ExtentTest test = report.createTest("Login Test");

test.pass("Login successful");
report.flush();
```

Used with listeners.

---

## 64. How do you handle flaky tests? (Real-world Example)

✔ RetryAnalyzer
✔ Explicit waits
✔ Remove test dependencies
✔ Stable test data

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
wait.until(ExpectedConditions.visibilityOf(element));
```

---

## 67. TestNG with Jenkins (Example)

### Jenkins command:

```bash
mvn clean test
```

TestNG:

* Runs via Maven
* Generates reports
* Jenkins archives results

---

## 70. Real-time TestNG Framework Structure

```
src/test/java
 ├── base
 │    └── BaseTest.java
 ├── tests
 │    └── LoginTest.java
 ├── pages
 │    └── LoginPage.java
 ├── utils
 │    └── DataUtil.java
 ├── listeners
 │    └── TestListener.java
testng.xml
```

---

## 🎯 FINAL INTERVIEW TIP (IMPORTANT)

When answering **advanced questions**, always mention:

> **“This is how we use it in real projects”**

That’s what separates **manual testers** from **automation engineers**.

---

Here are **🔥 Top 10 Tricky TestNG Interview Questions** with **clear explanations + examples**.
These are **frequently asked for 3–8 years experience** and are meant to **test real understanding**, not memorization.

---

## 🔥 1. What happens if `priority`, `dependsOnMethods`, and `groups` are used together?

### Answer

Execution order is decided in this priority:

1. **dependsOnMethods / dependsOnGroups**
2. **priority**
3. **method name (alphabetical)**

### Example

```java
@Test(priority = 2)
public void login() {}

@Test(dependsOnMethods = "login", priority = 1)
public void dashboard() {}
```

➡ `dashboard()` runs **after login**, even though priority is lower.

---

## 🔥 2. What happens if a dependent method is skipped?

### Answer

If a method depends on another method:

* **FAILED** → dependent test is **SKIPPED**
* **SKIPPED** → dependent test is **SKIPPED**
* **PASSED** → dependent test runs

### Example

```java
@Test
public void login() {
    throw new SkipException("Skipping login");
}

@Test(dependsOnMethods = "login")
public void payment() {}
```

➡ `payment()` will be **skipped**.

---

## 🔥 3. Can we run parallel tests without `testng.xml`?

### Answer

✅ **Yes**, using annotations like `invocationCount` and `threadPoolSize`.

### Example

```java
@Test(invocationCount = 5, threadPoolSize = 3)
public void parallelTest() {}
```

⚠️ But **cross-browser & large suites require `testng.xml`**.

---

## 🔥 4. Why is `ThreadLocal` used in TestNG + Selenium?

### Answer

To avoid **WebDriver conflicts in parallel execution**.

### Example

```java
private static ThreadLocal<WebDriver> driver = new ThreadLocal<>();

public static WebDriver getDriver() {
    return driver.get();
}
```

Each thread gets its **own WebDriver instance**.

---

## 🔥 5. What is the difference between `@BeforeTest` and `@BeforeClass` in parallel execution?

### Answer

| Annotation   | Parallel Impact        |
| ------------ | ---------------------- |
| @BeforeTest  | Runs once per `<test>` |
| @BeforeClass | Runs once per class    |

🚨 `@BeforeTest` can cause **browser sharing issues** in parallel runs.

---

## 🔥 6. Why is `dependsOnMethods` considered bad practice in frameworks?

### Answer

Because:

* One failure causes multiple skips
* Makes tests **not independent**
* Breaks parallel execution

✅ Best practice:

```java
dependsOnGroups = "login"
```

---

## 🔥 7. What happens if a test fails inside `@BeforeMethod`?

### Answer

* The test method is **SKIPPED**
* `@AfterMethod` still executes

### Example

```java
@BeforeMethod
public void setup() {
    Assert.fail();
}
```

---

## 🔥 8. Why is `alwaysRun = true` important?

### Answer

It ensures a method runs **even if dependent tests fail**.

### Example

```java
@AfterMethod(alwaysRun = true)
public void tearDown() {
    driver.quit();
}
```

💡 Critical for **cleanup logic**.

---

## 🔥 9. Difference between `invocationCount` and DataProvider?

### Answer

| invocationCount       | DataProvider                 |
| --------------------- | ---------------------------- |
| Same data             | Multiple data sets           |
| Used for load testing | Used for data-driven testing |

---

## 🔥 10. Why does TestNG sometimes execute tests in alphabetical order even with priority?

### Answer

Because:

* Same priority value
* No dependency defined

### Example

```java
@Test(priority = 1)
public void testB() {}

@Test(priority = 1)
public void testA() {}
```

➡ Execution order:

```
testA
testB
```

---

## 🎯 FINAL INTERVIEW ADVICE (VERY IMPORTANT)

Interviewers often follow up with:

> “Have you used this in real projects?”

Always reply with:

> “Yes, in our framework we use this to handle parallel execution / flaky tests / cleanup.”

---

Here are the **🔥 MOST COMMON TestNG MISTAKES** seen in **real projects and interviews**, with **why they are dangerous** and **how to fix them**.
Interviewers LOVE asking these because they reveal **practical experience**.

---

# 🔥 Most Common TestNG Mistakes (With Fixes)

---

## 🔴 1. Overusing `priority` to control execution order

### ❌ Mistake

```java
@Test(priority = 1)
@Test(priority = 2)
@Test(priority = 3)
```

### Why it’s bad

* Tests become **dependent**
* Breaks parallel execution
* Hard to maintain

### ✅ Best Practice

Use **independent tests** and **groups**:

```java
@Test(groups = "smoke")
```

---

## 🔴 2. Using `dependsOnMethods` across test classes

### ❌ Mistake

```java
@Test(dependsOnMethods = "LoginTest.login")
```

### Why it’s bad

* Tight coupling
* Causes cascading skips
* Not scalable

### ✅ Best Practice

```java
dependsOnGroups = "login"
```

---

## 🔴 3. Not making WebDriver thread-safe in parallel execution

### ❌ Mistake

```java
WebDriver driver;
```

### Why it’s bad

* Browser crashes
* Random failures

### ✅ Fix (ThreadLocal)

```java
ThreadLocal<WebDriver> driver = new ThreadLocal<>();
```

---

## 🔴 4. Putting browser launch in `@BeforeTest`

### ❌ Mistake

```java
@BeforeTest
public void setup() {
    driver = new ChromeDriver();
}
```

### Why it’s bad

* Same browser shared across threads

### ✅ Best Practice

```java
@BeforeMethod
public void setup() {
    driver = new ChromeDriver();
}
```

---

## 🔴 5. Forgetting `alwaysRun = true` in cleanup methods

### ❌ Mistake

```java
@AfterMethod
public void tearDown() {
    driver.quit();
}
```

### Problem

If test fails → cleanup may not run.

### ✅ Fix

```java
@AfterMethod(alwaysRun = true)
```

---

## 🔴 6. Mixing TestNG and JUnit assertions

### ❌ Mistake

```java
org.junit.Assert.assertTrue(true);
```

### Why it’s bad

* Confusing failure reporting
* Inconsistent behavior

### ✅ Best Practice

Use **TestNG assertions only**:

```java
org.testng.Assert.assertTrue(true);
```

---

## 🔴 7. Forgetting `assertAll()` in SoftAssert

### ❌ Mistake

```java
SoftAssert sa = new SoftAssert();
sa.assertTrue(false);
```

### Result

Test passes even though assertion failed ❗

### ✅ Fix

```java
sa.assertAll();
```

---

## 🔴 8. Hardcoding data instead of using DataProvider

### ❌ Mistake

```java
login("admin", "admin123");
```

### Why it’s bad

* No data-driven testing
* Poor coverage

### ✅ Fix

Use `@DataProvider`

---

## 🔴 9. Ignoring `testng-failed.xml`

### ❌ Mistake

Re-running full suite after failure

### ✅ Best Practice

Run only failed tests using:

```
testng-failed.xml
```

---

## 🔴 10. No listener for screenshots & reporting

### ❌ Mistake

* No screenshots on failure
* Poor debugging

### ✅ Fix

Implement `ITestListener`:

```java
onTestFailure()
```

---

## 🔴 11. Not using groups for test selection

### ❌ Mistake

Running entire suite every time

### ✅ Fix

```java
@Test(groups = "regression")
```

Run selectively via XML.

---

## 🔴 12. Making tests dependent on test data order

### ❌ Mistake

```java
@Test
public void test1() {
    createUser();
}

@Test
public void test2() {
    useSameUser();
}
```

### Why it’s bad

* Fails in parallel
* Not reusable

### ✅ Fix

Create **data independently per test**

---

## 🔴 13. Running UI tests without waits

### ❌ Mistake

```java
Thread.sleep(5000);
```

### Why it’s bad

* Slow
* Flaky

### ✅ Fix

Use **Explicit Waits**

---

## 🔴 14. Using single testng.xml for everything

### ❌ Mistake

One XML for smoke + regression + cross-browser

### ✅ Best Practice

* smoke.xml
* regression.xml
* crossbrowser.xml

---

## 🎯 INTERVIEW GOLD TIP

If interviewer asks:

> “What TestNG mistakes have you seen in projects?”

Say:

> “Overusing priority, not making WebDriver thread-safe, and tight dependencies using dependsOnMethods.”

That answer **instantly shows experience**.

---
Here’s a **📘 One-Page TestNG – Advanced Cheat Sheet** you can **revise in 5–10 minutes before an interview**.
It’s concise, practical, and focused on **what interviewers actually test**.

---

# 📘 TestNG – Advanced Cheat Sheet (Interview Ready)

---

## 🔹 Core Execution Rules

* **Execution priority order**

  1. `dependsOnMethods / dependsOnGroups`
  2. `priority`
  3. Alphabetical method name

* **Default priority**: `0`

* Same priority → **alphabetical order**

* Failed dependency → dependent test **SKIPPED**

---

## 🔹 Annotation Execution Flow

```
@BeforeSuite
@BeforeTest
@BeforeClass
@BeforeMethod
@Test
@AfterMethod
@AfterClass
@AfterTest
@AfterSuite
```

---

## 🔹 Parallel Execution

```xml
<suite parallel="tests" thread-count="3">
```

Types:

* `methods`
* `classes`
* `tests`
* `suites`

⚠️ Parallel UI tests → **ThreadLocal WebDriver required**

---

## 🔹 Thread-Safe WebDriver (Parallel Runs)

```java
ThreadLocal<WebDriver> driver = new ThreadLocal<>();
driver.set(new ChromeDriver());
driver.get();
```

---

## 🔹 Dependencies (Best Practice)

❌ `dependsOnMethods` across classes
✅ `dependsOnGroups`

```java
@Test(groups="login")
@Test(dependsOnGroups="login")
```

---

## 🔹 Groups (Selective Execution)

```java
@Test(groups={"smoke","regression"})
```

```xml
<include name="smoke"/>
<exclude name="regression"/>
```

---

## 🔹 Data-Driven Testing

### DataProvider

```java
@DataProvider
Object[][] data()
```

✔ Multiple datasets
✔ Dynamic

### Parameters

```java
@Parameters("browser")
```

✔ Single value
✔ Static

---

## 🔹 Retry Failed Tests

```java
@Test(retryAnalyzer = RetryAnalyzer.class)
```

OR
Run:

```
testng-failed.xml
```

---

## 🔹 Listeners (Must-Know)

Common listeners:

* `ITestListener`
* `ISuiteListener`
* `IRetryAnalyzer`

Use cases:

* Screenshots on failure
* Custom reports
* Logging

---

## 🔹 Screenshot on Failure (Listener)

```java
onTestFailure(ITestResult result)
```

---

## 🔹 Assertions

### Hard Assert

* Stops execution immediately

### Soft Assert

```java
SoftAssert sa = new SoftAssert();
sa.assertAll(); // MUST
```

---

## 🔹 `alwaysRun = true`

Ensures cleanup runs even if test fails:

```java
@AfterMethod(alwaysRun = true)
```

---

## 🔹 Common XML Attributes

```xml
parallel="tests"
thread-count="3"
preserve-order="true"
```

---

## 🔹 Reports

Default:

* `index.html`
* `emailable-report.html`

Advanced:

* Extent Reports (via Listener)

---

## 🔹 CI/CD (Jenkins)

```bash
mvn clean test
```

✔ Parallel execution
✔ Headless mode
✔ Reports archived

---

## 🔹 Common Mistakes (Remember These!)

* Overusing `priority`
* Tight method dependencies
* No ThreadLocal WebDriver
* Forgetting `assertAll()`
* No listeners for failures

---

## 🎯 FINAL INTERVIEW POWER LINE

> “In our framework, we use TestNG for parallel execution, retry logic, grouping, and listener-based reporting.”

Say this confidently — it **signals real project experience**.

---



