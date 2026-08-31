# 🎯 Capstone Summary — What's What in This Repo

![Lane](https://img.shields.io/badge/Lane-Refresh%20%2F%20Content%20Opportunity%20Scoring-2F5CFF)
![Status](https://img.shields.io/badge/Status-Shipped-1E8E5A)
![Paper](https://img.shields.io/badge/Paper-Live-D98E2B)

**📄 Deployed paper:** https://summayashaikh079-stack.github.io/flyrank-ml-week1/

> Start here if you're reviewing this capstone — this file maps every
> notebook in this repo to the piece of the paper it produced.

---

## 🧭 The one-line version

Trained a Random Forest model to flag which FlyRank content pages need a
refresh, benchmarked it against a simple CTR-vs-position rule, and — the
actual finding — showed that the model's impressive **90% precision** score
was an artifact of a naive train/test split. Under an honest,
client-grouped split, it dropped to **54%**, barely above the **51%** base
rate. Shipped that honest result, plus a reason-coded action playbook, as a
deployed paper.

```
   naive split          honest split         base rate
   Precision@50         Precision@50
      0.90        ──▶       0.54       ≈        0.51
   (misleading)          (what shipped)      (guessing)
```

---

## 🗂️ How the work flows into the paper

```
w01 research question ──┐
w02 ml task framing ────┤──▶  Introduction + Methodology (framing)
                         │
w03 data contract ───────┤
w03 feature leakage ─────┤──▶  Data + Methodology (feature set)
                         │
w04 baseline score ──────┤
w04 signal audit ────────┤──▶  Methodology (baseline) + Results (confirmed)
                         │
w05 model ────────────────┤──▶  Methodology (model)
                         │
w06 validation audit ────┤──▶  Results — THE core finding
                         │      (naive vs. honest split + leakage check)
                         │
w07 action playbook ─────┤──▶  Ranked recommendations
                         │
capstone.ipynb ──────────┘──▶  End-to-end mirror + demo outline + shareable cuts
```

## 📓 Notebook-by-notebook map

| Notebook | What it did | Paper section |
|---|---|---|
| `w01_research_question.ipynb` | Framed the real decision this supports: which content pages a human editor should review first | Introduction |
| `w02_ml_task_framing.ipynb` | Defined this as a ranking/scoring task, not a classification task in isolation | Methodology — task framing |
| `w03_data_contract.ipynb` | Documented the data source, table grain, working window, and Search Console coverage gap | Data |
| `w03_feature_leakage_check.ipynb` | Checked which columns are safe features vs. which leak the label | Methodology — feature set |
| `w04_baseline_score.ipynb` | Built the position-bucket CTR-gap rule baseline | Methodology — baseline |
| `w04_signal_audit.ipynb` | Verified the baseline's underlying signal actually holds (CTR drops cleanly by position bucket) | Results — baseline confirmation |
| `w05_model.ipynb` | Trained the Random Forest classifier | Methodology — model |
| `w06_validation_audit.ipynb` | **⭐ The core finding.** Re-ran the same model under a naive split vs. an honest client-grouped split; ran the leakage check (re-adding `trend_pct`) | Results — the whole naive-vs-honest comparison |
| `w07_action_playbook.ipynb` | Built the reason-coded recommendations (R1/R2/R3) | Ranked recommendations |
| `capstone.ipynb` | End-to-end notebook mirroring the deployed paper; also holds the 5-minute demo outline and the two shareable cuts (social post + employer summary) | Whole paper, mirrored |

## 📊 Outputs referenced in the paper

- `outputs/model_report.md` — model comparison table (Random Forest vs. decision tree, logistic regression, baseline rules)
- `outputs/charts/` — feature importance and distribution charts generated during exploration

## 📌 Submission trail

- `submission/paper_url.txt` — the one-line deployed paper URL (required by the assignment)
- `docs/index.html` — the deployed paper itself, served via GitHub Pages from this repo

## 🔒 Public-safety check — confirmed

- ✅ No client names, page URLs, raw search queries, or credentials anywhere in this repo or the deployed paper
- ✅ All client/content identifiers are pseudonymous hashes used only for joining and grouping
- ✅ No claim in the paper asserts a causal effect on Google's ranking algorithm — every result is framed as observed/decision-support, never causal
