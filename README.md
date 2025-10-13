# Self-Healing AI Agent Demo for BrowserStack Automate

## Table of Contents
- [What is BrowserStack Self-Healing AI Agent?](#what-is-browserstack-self-healing-ai-agent)
- [Introduction](#introduction)
- [How to Run](#how-to-run)
- [Additional Resources](#additional-resources)

---

## What is BrowserStack Self-Healing AI Agent?

BrowserStack’s Self-Healing AI Agent automatically detects and repairs broken selectors during test execution. When the application’s UI changes (for example, a button ID changes from `#submit` to `#submit-btn`), traditional tests fail with NoSuchElementException errors. The Self-Healing Agent dynamically identifies these selector failures, finds the correct element in real time, and allows the test to continue, thereby, reducing manual maintenance and improving build stability.

It works on the principle that the test script remains unchanged while DOM changes lead to selector failures. Therefore, the agent utilises past successful run as context to heal broken selectors during test execution.

---

## Introduction

This repository demonstrates BrowserStack's Self-Healing AI Agent for web automation using TestNG and BrowserStack Java SDK. It contains two test scripts:

- **BStackDemoTest.java**: Runs a standard automation flow (control test - should always pass)
- **BStackSelfHealDemoTest.java**: Runs the same flow with "Self-Heal Mode" enabled on the demo website to simulate selector failures (demonstrates healing in action) due to DOM changes.

Both tests run on the demo website: **[https://browserstack.github.io/selfheal-demo-app/](https://browserstack.github.io/selfheal-demo-app/)**

---

## How to Run

### Prerequisites
1. Install Java and Maven, if not already installed. Add Java to PATH environment variable.
2. Verify installation: `java -version`, `mvn -version`
3. Move to respective git branch: "testng-automate" for web, "testng-appium-app" for native apps

### Setup
1. Clone the repository
2. Update BrowserStack `username` and `accesskey` in the `browserstack.yml` file. Ensure AI is enabled in your BrowserStack Account.
3. Install dependencies: `mvn compile`

### Demo Part 1: Without Self-Healing (See Tests Fail)

1. Ensure `selfHeal: false` in `browserstack.yml`
2. Run the tests:
   - `mvn test -P sample-test` → **Expected: Tests PASS** (no selector changes)
   - `mvn test -P sample-selfheal-test` → **Expected: Tests FAIL** with `NoSuchElementException` (website simulates selector changes)

### Demo Part 2: With Self-Healing (See Tests Auto-Fix with Self-Healing AI Agent)

1. Enable self-healing:
   - Set `selfHeal: true` in `browserstack.yml` file
2. Re-run the failing test:
   - `mvn test -P sample-selfheal-test` → **Expected: Tests PASS** (AI agent automatically heals broken selectors)

### View Results

- View healed selectors and test results on the [BrowserStack Automate Dashboard](https://automate.browserstack.com/overview?tab=all). The dashboard shows which selectors broke and what the AI agent replaced them with.

---

## Additional Resources

- [BrowserStack Automate Dashboard](https://automate.browserstack.com/overview?tab=all) - View test results and healed selectors
- [Self-Healing Documentation](https://www.browserstack.com/docs/automate/selenium/self-healing?fw-lang=java) - Learn more about how self-healing works
---