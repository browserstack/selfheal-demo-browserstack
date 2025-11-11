# Self-Healing AI Agent Demo for BrowserStack Automate

## Table of Contents
- [What is BrowserStack Self-Healing AI Agent?](#what-is-browserstack-self-healing-ai-agent)
- [Introduction](#introduction)
- [How to Run](#how-to-run)
- [Additional Resources](#additional-resources)

---

## What is BrowserStack Self-Healing AI Agent?

BrowserStack’s Self-Healing AI Agent diagnoses automation failures such as broken selectors due to DOM shifts and automatically recovers tests without masking genuine product bugs. When the application’s DOM shifts (for example, a button ID changes from `#submit` to `#submit-btn`), traditional tests fail with NoSuchElementException errors.  

The Self-Healing Agent dynamically identifies these selector failures, uses contextual signals from past successful run to find the correct element in real time, and allows the test to continue, thereby, reducing manual maintenance and improving build stability.

---

## Introduction

This repository demonstrates BrowserStack's Self-Healing AI Agent for web automation using TestNG and BrowserStack Java SDK. It contains two test scripts:

- **BStackDemoTest.java**: Runs a standard automation flow (tests should pass and serve as the baseline).
- **BStackSelfHealDemoTest.java**: Runs the same flow with "Self-Heal Mode" enabled. Simulates selector failures due to DOM shifts.

Tests run on the demo website: **[https://browserstack.github.io/selfheal-demo-app/](https://browserstack.github.io/selfheal-demo-app/)**

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

### Demo Part 1: Without Self-Healing (Tests Fail due to DOM shift & selector failures)

1. Ensure `selfHeal: false` in `browserstack.yml`
2. Run the tests:
   - `mvn test -P sample-test` → **Expected: Tests PASS** (Serves as baseline)
   - `mvn test -P sample-selfheal-test` → **Expected: Tests FAIL** with `NoSuchElementException` (website simulates DOM shift & selector changes)

### Demo Part 2: With Self-Healing (Tests Pass due to Self-Healing AI Agent)

1. Enable self-healing:
   - Set `selfHeal: true` in `browserstack.yml` file
2. Run the test once so Agent captures success context:
   - `mvn test -P sample-test` ->  **Expected: Tests PASS** 
   - Note: The Agent needs to learn from a successful test run before it can heal the test.
2. Re-run the failing test:
   - `mvn test -P sample-selfheal-test` → **Expected: Tests PASS** (AI agent automatically heals broken selectors)

### View Results

- View healed selectors and test results on the [BrowserStack Automate Dashboard](https://automate.browserstack.com/overview?tab=all). The dashboard shows which selectors broke and what the AI agent replaced them with.

---

## Additional Resources

- [BrowserStack Automate Dashboard](https://automate.browserstack.com/overview?tab=all) - View test results and healed selectors
- [Self-Healing Documentation](https://www.browserstack.com/docs/automate/selenium/self-healing?fw-lang=java) - Learn more about how self-healing works
---