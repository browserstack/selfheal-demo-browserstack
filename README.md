# BrowserStack Self-Healing AI Agent Demo

## What is BrowserStack Self-Healing AI Agent?

BrowserStack’s Self-Healing AI Agent diagnoses automation failures such as broken selectors due to DOM shifts and automatically recovers tests without masking genuine product bugs. When the application’s DOM shifts (for example, a button ID changes from #submit to #submit-btn), traditional tests fail with NoSuchElementException errors.

The Self-Healing Agent dynamically identifies these selector failures, uses contextual signals from past successful run to find the correct element in real time, and allows the test to continue, thereby, reducing manual maintenance and improving build stability.

## Introduction

This repository demonstrates BrowserStack's Self-Healing AI Agent for web and native apps.
- For Web demo, checkout branch `testng-automate` and follow the readme
- For Native App Demo, checkout branch `testng-appium-app` and follow the readme
