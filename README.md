# Safe Link - Threat Detection Desktop App

**Course:** Concurrency Programming - Mini-project 2026-2027
**Instructor:** Dr. Boudjellal Nada
**University:** Abdelhamid Mehri - Constantine 2
**Faculty / Department:** Faculty of NTIC - Department of Software Technologies and Information Systems


## 1. Team Information
 1 | BENKOLLI Majdouline Safia  | G1 | URL analyzer.
 2 | OUDINA Sirine              | G1 | GUI.
 3 | BENMAGHSOULA Mohammed Samy | G1 |  Models + concurrency manager.
 4 | BENMEHDI Aymen Bahaaeddine | G2 | Message + CSV.


## 2. Project Overview

Safe Link is a desktop application that evaluates suspicious **URLs** and **text messages** (e-mail / SMS) and reports a risk level for each entry. Users can add items one by one or load a **CSV batch file**, start the analysis, and follow the progress and the result of every entry in real time.

A core rule of the project: "an item that cannot be verified is never reported as safe". Any failure (empty input, malformed URL, invalid row, internal error) produces the status **Not verified**.

  
## 3. Technical Choices

  *Language: Java 17
  *GUI framework: JavaFX 21 (javafx-controls 21.0.5) with a custom CSS theme
  *Build tool: Maven (javafx-maven-plugin 0.0.8)
  *Testing: JUnit 5 (5.10.2)
  *Concurrency: java.util.concurrent (ExecutorService fixed thread pool, atomic variables)
  *Architecture: model, service, concurrency, ui packages; the backend has no dependency on JavaFX

## 4. Detection option selected

**Option A - Rule-Based Detection** (local Java rules, no external API, works offline).

- **URL rules** (`UrlAnalyzer`): HTTP instead of HTTPS, IP address as hostname, `@` in the URL, punycode domains, suspicious keywords (login, verify, secure..), suspicious TLDs (.tk, .xyz...), URL shorteners, too many subdomains, misleading brand names in subdomains (e.g. `paypal.com.secure-login.tk`), many hyphens, very long URLs, non-standard ports.
- **Message rules** (`MessageAnalyzer`): urgency wording, account-blocking threats, credential requests, banking/payment requests, prize/refund promises, "click here" wording. Links found inside a message are also analyzed by `UrlAnalyzer`.
- **Scoring:** points are accumulated (0-100) and mapped to a level:

 Score & Risk level 
* 0 - 24 ---> Low 
* 25 - 49 ---> Medium 
* 50 - 100 ---> High 
* analysis impossible ---> **Not verified** 

## 5. Requirements

- **JDK 17** or newer
- **Maven 3.8+**


## 6. Build and Run

 - Run the application
mvn javafx:run

 - Run without the artificial delay
mvn javafx:run -Dthreat.delay=0

 - Run the unit tests
mvn test

**From VS Code, run the `Launcher` class (not `App`) to avoid the *"JavaFX runtime components are missing"* error.**

---

## 7. How to Use

1. Choose the input type: **URL** or **Message**.
2. Type or paste the content and click **Add** (or click **Example** to insert a sample).
3. Or click **Browse CSV...** to load a batch file.
4. Click **Analyze all** and watch the per-item status and the global progress bar.
5. Read the risk level (Low / Medium / High / Not verified) and the reasons for each entry; the summary counters update at the end.
6. Click **Clear** to start over.

## 8. Tests

JUnit 5 unit tests cover the model, URL and message analyzers, CSV parsing, the detection service and the concurrent `AnalysisManager` (**41 tests, 0 failures**).

```bash
mvn test
```


##  AI Usage Disclosure

Artificial intelligence (Claude & ChatGPT) was used in this project at an estimated **49%** of the overall work.

AI assistance was used for:
-  restructuring the project architecture and merging the four parts into one;
-  Fixing the architecture problem by separating the user interface from the backend logic (model, service, concurrency and ui packages).
- Finding and correcting errors in the code so that the project compiles and runs.
- Understanding the project: reading the project statement and the Sprint N01 requirements, and clarifying what each one expects.
- Breaking the project down into smaller parts (user interface, detection rules, CSV loading, concurrency, tests) to organize the work.
- Reviewing the code and checking that the project meets every Sprint 1 requirement.
-Comments in all the code are generated automatically with VSC.

  **Thank you Dr.NADA for your project, where "Not Verified" is never "Safe"... and where Sprint 1 made us a bit safer as developers!**