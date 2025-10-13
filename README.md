# BrowserStack Self-Healing Demo (Android - TestNG)

## What is BrowserStack Self-Healing AI Agent?

BrowserStack’s Self-Healing AI Agent automatically detects and repairs broken selectors during test execution. When the application’s UI changes (for example, a button ID changes from `#submit` to `#submit-btn`), traditional tests fail with NoSuchElementException errors. The Self-Healing Agent dynamically identifies these selector failures, finds the correct element in real time, and allows the test to continue, thereby, reducing manual maintenance and improving build stability.

It works on the principle that the test script remains unchanged while DOM changes lead to selector failures. Therefore, the agent utilises past successful run as context to heal broken selectors during test execution.

## Introduction

This repository demonstrates BrowserStack's Self-Healing feature for Android native apps using Appium and TestNG. It includes two Android applications that showcase the power of self-healing in real-world scenarios:

- `BaseAppTest.java` which runs the tests on `BaseApp.apk`(located at `android/testng-examples/BaseApp.apk`). Standard automation tests without UI changes and serves as baseline.
- `SelfHealAppTest.java` which runs the same test script on `SelfHealApp.apk` (located at `android/testng-examples/SelfHealApp.apk`). Demonstrates how Self-Healing recovers from locator failures if agent is turned on.

## How to Run

### Prerequisites
1. Install Java and Maven, if not already installed. Add Java to PATH environment variable.
2. Verify installation: `java -version`, `mvn -version`
3. Move to respective git branch: "testng-automate" for web, "testng-appium-app" for native apps

### Setup
1. Clone the repository
2. Update BrowserStack `username` and `accesskey` in the `browserstack.yml` file. Ensure AI is enabled in your BrowserStack Account.
3. Move to `android/testng-examples` and install dependencies: `mvn compile`.

### Demo Part 1 : Wihout Self-Healing (See tests Fail)

1. Ensure `selfHeal: false` in `browserstack.yml`
2. In `browserstack.yml`, ensure SelfHealApp is selected `app: ./SelfHealApp.apk`
3. Run the tests: `mvn test -P sampleSelfHealAppTest`

### Demo Part 2 : With Self-Healing (See Tests Auto-Fix with Self-Healing AI Agent)
1. Enable self-healing:
   - Set `selfHeal: true` in `browserstack.yml` file
2. In `browserstack.yml`, ensure SelfHealApp is selected `app: ./SelfHealApp.apk`
3. Run the tests: `mvn test -P sampleSelfHealAppTest`

### View Results

- View healed selectors and test results on the [BrowserStack App Automate Dashboard](https://app-automate.browserstack.com/overview?tab=all). The dashboard shows which selectors broke and what the AI agent replaced them with.


## Additional Resources

- [Self-Healing Documentation](https://www.browserstack.com/docs/app-automate/appium/self-healing?fw-lang=java) - Learn more about how self-healing works
- [BrowserStack App Automate Dashboard](https://app-automate.browserstack.com/overview?tab=all) - View test results and healed selectors
