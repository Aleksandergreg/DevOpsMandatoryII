# Software Quality

## Background  
Our team initially adopted **SonarQube**, but the free tier felt too limited for our needs.  
After researching alternatives, we switched to **DeepSource**, whose free tier covered everything we required.

---

## DeepSource Findings  

| Category | Count |
|----------|-------|
| Issues   | **8** |
| Bug risks| **4** |
| Anti‑patterns | **4** |

### Bug Risks

| Bug Risk | Status |
|----------|--------|
| Risk of race condition in non‑atomic file operations | **Fixed** |

> **Description (DeepSource)**  
> *“Non‑atomic file operations can cause problems that are difficult to reproduce, especially in cases of frequent file operations in parallel …  
> For example, creating a directory if there is none, has the following problems:  
> • An exception occurs when the directory didn’t exist at the time of `exist?`, but someone else created it before `mkdir` was executed.”*

**Resolution** ‑ We removed the unnecessary existence‑check (`exist?`) and perform the file operation atomically, as DeepSource recommended.

### Anti‑Patterns

| Anti‑pattern | Status |
|--------------|--------|
| Using `refute` instead of `assert_not` in Minitest | **Ignored (for now)** |

* DeepSource noted that `assert_not` is the true antonym of `assert`, improving readability and maintainability.  
* We tried:
  1. **Simple replacement** (`refute` → `assert_not`) – tests failed.  
  2. **Switching gems** (from **minitest** to **rack‑test**) – still failed.  
* Because this is purely stylistic and not a performance issue, we chose to **suppress** the warning for now.

---

## Dockerfile Analysis  

*DeepSource* reports **no issues** in our Dockerfiles.  
That aligns with expectations—­we had previously linted them heavily with **Hadolint** and **CodeRabbit** before introducing DeepSource’s Docker analysis.

---

## CodeRabbit Integration  

* **Trigger:** Runs on every pull‑request to `main` or `dev`.  
* **Benefits:**  
  * Performs a thorough review of code, workflows, and Dockerfiles.  
  * Generates automatic **sequence diagrams** for new or changed code, giving reviewers a quick visual overview.  
  * Helps both the author and reviewers confirm the changes behave as intended.

---

## Lessons Learned & Future Recommendations  

1. **Enable quality‑gates on Day 1.**  
   *Configuring DeepSource, CodeRabbit, etc. at project start prevents technical debt from snowballing.*

2. **Fix issues immediately, when context is fresh.**  
   *Delays make refactors riskier as more components grow dependent on the problem code.*

3. **Use multiple complementary tools.**  
   *Static analysers, linters, and diagram generators each catch different classes of issues.*

---

