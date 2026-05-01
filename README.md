# hw3_starter

# CS520 Spring 2026 - Homework 3

## Overview and Goal
In this assignment, you will work with an existing implementation of an Expense Tracker application. This application applies the MVC architecture pattern.
Rather than building brand-new user features, your task is to understand, analyze, and restructure the system using sound software engineering principles.

Treat this as a realistic on-boarding task: you are joining a team with shipped software, and your responsibility is to improve understandability, modularity, extensibility readiness, and testability while preserving current behavior. 

## Getting Started
1. Clone the repository: `git clone https://github.com/CS520-Spring2026/hw3_starter`
2. Read this `README.md` file.
3. Build, test, and run the application using the commands below.
4. Explore source code in `src/` and tests in `test/`.

We'll use the ant build tool (`https://ant.apache.org/manual/installlist.html`) to build and run the application.

## Optional Working Files
You may draft your answers in local markdown files (for example under `docs/`) while working, but these files are optional and are not required for grading.
All written graded content must appear in `HW3_answers.pdf`.

## Build and Run

The Expense Tracker application has the following structure:
- `bin/`: Contains the generated class files
- `jdoc/`: Contains the generated javadoc folders/files
- `lib/`: Contains the third party software jar files
- `src/`: Contains the Java folders and source files
- `test/`: Contains the JUnit test suite source files
- `build.xml`: Is the ant build tool input file
- `build/`: Contains the ant build tool output files
- `coverage_report/`: Contains the test coverage report

The build requirements are:
- JDK 21+: Generate API doc (javadoc), compile (javac), run (java)
- Ant 1.10.15+: Build and run the application and test suite(s)

From the root directory (containing the build.xml file):

1. Build app: `ant compile`

<!-- 2. Run the app: `java -cp bin ExpenseTrackerApp` -->
2. Run the app:
   - On Windows: `java -cp "bin;lib\xchart-3.8.8.jar;lib\tinylog-api-2.7.0.jar;lib\tinylog-impl-2.7.0.jar" ExpenseTrackerApp`
   - On Linux/macOS: `java -cp "bin:lib/xchart-3.8.8.jar:lib/tinylog-api-2.7.0.jar:lib/tinylog-impl-2.7.0.jar" ExpenseTrackerApp`

3. Build and run tests: `ant test` (See the build/TEST-*.txt files for more details.)

4. Generate the test coverage report: `ant coverage.report` (See `coverage_report/index.html` for more details.)

5. Generate Javadoc: `ant document`

6. Perform linting `ant lint`

7. Clean generated artifacts (e.g., class files, javadoc files): `ant clean`

# Architecture

The Expense Tracker application applies the MVC architecture pattern as follows:
* model package: Contains the data model represented as a list of transactions
* view package: Contains the visualizations of the model and supports user interactions
* controller package: Contains the application logic to process the user interactions

# Features

* **Add Transaction:**
  Enter a valid amount and category, then click **Add Transaction**.
  The valid transaction appears in the list, and the total cost updates automatically.

* **Delete Transaction:**
  Select a valid transaction from the list.
  In the 'Edit' menu, select the 'Delete' menu item.
  The valid transaction disappears from the list, and the total cost updates automatically.

* **Save the Transaction List:**
  In the 'File' menu, select the 'Save As...' menu item
  In the Save dialog, first select a valid output file and then click the 'Save' button

* **Open a Transaction List:**
  In the 'File' menu, select the "Open File..." menu item
  In the Open dialog, first select a valid input file and then click the 'Open' button

* **Analyze:**
  First select the 'Analysis' tab.
  In that tab, select the analysis time window (e.g., 'Last week')
  In the tab, click the 'Analyze' button
  If there are transactions in that time window, displays the analysis results. If not, displays an error message.

# Accessibility

The application includes the following screen reader (e.g. VoiceOver on macOS) support:

* **App Description on Launch:**
  When the application first opens, focus is automatically moved to a description label at the top of the window. The screen reader will read out a description of the app and how to navigate it, so users know what the app does and where to go before interacting with any input fields.

* **Analyze Error Announcement:**
  If the user clicks the 'Analyze' button without any transaction data available for the selected time window, the error message is displayed on screen and focus is automatically moved to it. The screen reader will read the error message aloud, instead of staying on the Analyze button.

# Logging

The application uses the [tinylog](https://www.tinylog.org/) library to log events at runtime with timestamps, log level, and the method that triggered the event.

The following events are logged:

* **App startup**: logged at `INFO` level when the application launches.
* **Add Transaction**: logged at `INFO` when a transaction is successfully added, including the amount and category. Logged at `WARN` if the amount cannot be parsed as a number, or if the amount or category is invalid.
* **Delete Transaction**: logged at `INFO` when a transaction is successfully deleted, including the row number. Logged at `WARN` if no valid transaction was selected.
* **Open File**: logged at `INFO` when a file is chosen, how many existing transactions were cleared beforehand (`DEBUG`), and how many transactions were imported. Logged at `ERROR` if the file cannot be read.
* **Save File**: logged at `INFO` when a file is chosen for saving. Logged at `ERROR` if the save fails.
* **Analyze**: logged at `INFO` when the Analyze button is clicked, including the selected time window (e.g. Last Week, Last Year, All). Logged at `WARN` if there are no transactions available to analyze in that time window.