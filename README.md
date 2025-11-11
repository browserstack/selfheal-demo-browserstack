# BrowserStack Self-Healing Demo (Android - TestNG)

## What is BrowserStack Self-Healing AI Agent?

BrowserStack’s Self-Healing AI Agent diagnoses automation failures such as broken selectors due to DOM shifts and automatically recovers tests without masking genuine product bugs. When the application’s DOM shifts (for example, a button ID changes from `#submit` to `#submit-btn`), traditional tests fail with NoSuchElementException errors.  

The Self-Healing Agent dynamically identifies these selector failures, uses contextual signals from past successful run to find the correct element in real time, and allows the test to continue, thereby, reducing manual maintenance and improving build stability.


## Introduction

This repository demonstrates BrowserStack's Self-Healing feature for Android native apps using Appium and TestNG. It includes two Android applications that showcase the power of self-healing in real-world scenarios:

- `BaseAppTest.java` : Runs the test suite on BaseApp.apk (the original app with stable UI). These tests pass and serve as the baseline.
- `SelfHealAppTest.java` :  Runs the same test suite on SelfHealApp.apk (the same app but modified with changed selectors to simulate DOM shift). Without self-healing, these tests fail due to locator changes.

## How to Run

### Prerequisites
1. Install Java and Maven, if not already installed. Add Java to PATH environment variable.
2. Verify installation: `java -version`, `mvn -version`
3. Move to respective git branch: "testng-automate" for web, "testng-appium-app" for native apps

### Setup
1. Clone the repository
2. Update BrowserStack `username` and `accesskey` in the `browserstack.yml` file. Ensure AI is enabled in your BrowserStack Account.
3. Move to `android/testng-examples` and install dependencies: `mvn compile`.

### Demo Part 1 : Without Self-Healing (Tests Fail due to DOM shift & selector failures)

1. Ensure `selfHeal: false` in `browserstack.yml`
2. Run the tests: 
   - In `browserstack.yml`, ensure BaseApp is selected `app: ./BaseApp.apk`. Run the tests: `mvn test -P sampleBaseAppTest`. **Expected: Tests PASS**
   - In `browserstack.yml`, ensure SelfHealApp is selected `app: ./SelfHealApp.apk`. Run the tests: `mvn test -P sampleSelfHealAppTest`. **Expected: Tests FAIL** (app simulates DOM shift & selector changes)

### Demo Part 2 : With Self-Healing (Tests Pass due to Self-Healing AI Agent)
1. Enable Self-healing agent. Ensure `selfHeal: true` in `browserstack.yml`
2. Run the test once so Agent captures success context: 
   - In `browserstack.yml`, ensure BaseApp is selected `app: ./BaseApp.apk`. Run the tests: `mvn test -P sampleBaseAppTest`.  **Expected: Tests PASS** (no selector changes)
   - Note: The Agent needs to learn from a successful test run before it can heal tests.

3. Re-run the failing test:
   - In `browserstack.yml`, ensure SelfHealApp is selected `app: ./SelfHealApp.apk`. Run the tests: `mvn test -P sampleSelfHealAppTest`. **Expected: Tests PASS** (Self-Healing AI agent automatically heals the broken selectors)

### View Results

- View healed selectors and test results on the [BrowserStack App Automate Dashboard](https://app-automate.browserstack.com/overview?tab=all). The dashboard shows which selectors broke and what the AI agent replaced them with.


## Additional Resources

- [Self-Healing Documentation](https://www.browserstack.com/docs/app-automate/appium/self-healing?fw-lang=java) - Learn more about how self-healing works
- [BrowserStack App Automate Dashboard](https://app-automate.browserstack.com/overview?tab=all) - View test results and healed selectors
