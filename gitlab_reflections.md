# GitLab Flow & How We Used It

## Reference  
We based our process on the GitLab Flow guidelines documented in the repo:  
<https://github.com/DevOpsDynamite/DynaSearch/blob/main/docs/choosing_git_branching_strategy.md>

---

## What Went Wrong at First

| Misstep | Impact |
|---------|--------|
| **Protected both `main` _and_ `dev`** | - **Double reviews:** every feature branch needed approval *twice* (`feature → dev` ➜ `dev → main`).<br>- **Longer lead time:** deployments slowed significantly.<br>- **Unclear ownership:** who should open the second PR (`dev → main`)? |

The extra bureaucracy **added no real value** and **hurt developer experience**.

---

## Course‑Correction

1. **Re‑read the GitLab Flow docs.**  
2. Realised that **only `main`** should be protected.  
3. Updated branch‑protection rules accordingly.

### Results
* **Single review path** (`feature → dev → auto‑merge to main` once dev is stable).  
* **Faster deployments** and fewer procedural questions.

---

## Personal Takeaways (Aleksander)

| Aspect | Reflection |
|--------|------------|
| **Git proficiency** | Comfortable with Git **before** the course (3 prior semesters of group work), but previously relied on **IntelliJ GUI**. |
| **CLI skills** | Now prefer working via **terminal**; the course pushed me to adopt CLI workflows. |
| **Merge conflicts** | Few *real* conflicts (low concurrent work load). Practiced conflict resolution in **solo exercises** to upskill. |
| **Vim discovery** | Using **Vim** inside merge tools was a *game‑changer*—although for heavy conflicts, a visual merge tool or fixing directly on GitHub can still be faster. |

---

## Lessons Learned

* **Read the docs carefully**—small misinterpretations (e.g., branch protection) can snowball into big productivity issues.  
* **Keep reviews lightweight**—protect only what truly needs guarding.  
* **Invest in the CLI early**—it pays off in speed and flexibility.  
* **Simulate tricky scenarios** (like merge conflicts) in a safe sandbox to build confidence before they matter in production.
