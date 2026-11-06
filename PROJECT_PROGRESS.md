# Project Progress — Machine Learning IV

**Last verified:** 2026-11-06  
**Project root currently in use:** `C:\Users\athar\Downloads\ML_IV_Checked_Fixed`  
**Overall status:** IN PROGRESS — the dashboard and existing five-slide presentation are present, but the latest master specification has additional uncompleted requirements. Do not mark the project FINALIZED until the final copied project and ZIP pass the complete QA checklist.

## Status summary

| Area | Status | Verified state |
|---|---|---|
| Source/project inspection | COMPLETED | Inspected the project tree, notebook sections, README, CSV schemas, browser dashboard, and PowerPoint slide text/count. |
| Dataset availability | COMPLETED | The four full datasets are present under `Datasets/`; the additional selected-columns student CSV is also present and needs a use/cleanup decision. |
| Notebook modeling workflows | NEEDS VERIFICATION | Revised car-analysis cells 27–50 were executed successfully against the supplied CSV in a temporary notebook copy. Other project metrics remain from the previous verified run; the full fresh-kernel notebook and original upload flow still need verification. |
| Car model optimization | COMPLETED | Deduplicated before split; trained-only feature/model selection via five-fold CV selected log-target Lasso (CV R² 0.7822); held-out R² 0.7720 meets the 0.75 target. Historical R² 0.519 is retained as a distinct, non-comparable baseline. |
| Notebook upload/reproducibility requirements | NOT STARTED | Master specification requires robust independent upload sections, file validation, encoding handling, and a headless path fallback. The notebook currently uses Colab upload or a Tkinter picker. |
| Dashboard UI/UX redesign and car data sync | COMPLETED | One-file cyberpunk dashboard now embeds the deduplicated car data, selected Lasso metrics, five-model comparison, original baseline, actual/predicted examples, and residual points. Browser tested after refresh across all five pages and responsive widths. |
| PowerPoint | NEEDS VERIFICATION | Exactly five slides; car slide updated with selected model, CV/test metrics, target status, and historical baseline. Text and slide count verified; visual rendering is unavailable in this environment. |
| README | NEEDS VERIFICATION | Car metrics and historical-baseline explanation updated. The full setup/reproducibility sections required by the master specification still need completion. |
| GitHub Pages update | COMPLETED | Commit `b5c2f860` is pushed to `origin main`; Pages build/deploy run `42190041668` succeeded. The public directory URL now serves the updated model and metrics. |
| Requirements file | NOT STARTED | No `requirements.txt` currently exists. |
| Final project copy | NOT STARTED | No `Machine_Learning_IV_Final` directory exists. Do not replace or destructively alter the current working source tree. |
| Final ZIP | NOT STARTED | `224010_Atharv_M_Bennur_ML_IV_Final.zip` has not been created or tested. |
| Continuation documentation | COMPLETED | This progress file and the self-contained `CONTINUATION_PROMPT.md` have been created. |

## Completed tasks

- Inspected the supplied `ML_IV_Checked_Fixed.zip`. It contains the notebook, presentation, and README, but not the CSV datasets. Those three files matched the workspace copies when checked.
- Organized the active working project into `Notebook/`, `Datasets/`, and `Dashboard/` without deleting the student data. Preserved `ML_IV_Presentation.pptx`.
- Verified the four primary CSV schemas and raw dimensions:
  - `Iris.csv`: 150 rows × 6 columns.
  - `CAR DETAILS FROM CAR DEKHO.csv`: 4,340 rows × 8 columns.
  - `Mall_Customers.csv`: 200 rows × 5 columns.
  - `StudentPerformanceFactors.csv`: 6,607 rows × 20 columns, with 235 missing values.
- Executed the notebook's ML workflows in a temporary in-memory notebook using the provided CSVs. The four upload cells were replaced for that run with explicit dataset paths; notebook model/data preparation cells thereafter ran in order. This does **not** verify the unmodified notebook's interactive upload behavior.
- Created a standalone `Dashboard/index.html` with embedded data from that execution; its initial light-theme design has since been replaced by the cyberpunk redesign below.
- Reworked `Dashboard/index.html` into a premium dark cyberpunk interface with a collapsible desktop navigation rail, mobile drawer, project-information anchor, reorganized project-specific analysis layouts, responsive SVG charts, actual car residual visualization, actual metric cards, and accessible navigation labels. No prediction form was added because there is no verified prediction engine embedded in the page; the notebook's student examples remain clearly identified as examples.
- Updated `README.md` for the first dashboard delivery; it needs a fuller revision for the latest master prompt.
- Created this file and `CONTINUATION_PROMPT.md`.

## Current notebook and model metrics

Notebook: `Notebook/224010_AtharvBennur_ML_Project.ipynb`. It contains four separate dataset sections and the existing model pipelines. Current held-out metrics from the supplied data and fixed notebook split/random states:

### Iris — 150 rows

| Model | Accuracy | Weighted precision | Weighted recall | Weighted F1 |
|---|---:|---:|---:|---:|
| Logistic Regression | 0.9333 | 0.9333 | 0.9333 | 0.9333 |
| K-Nearest Neighbors (selected k=3) | 0.9333 | 0.9444 | 0.9333 | 0.9327 |

### Car price — 4,340 raw rows × 8 columns

The revised pipeline removes 763 exact duplicate rows before splitting, leaving 3,577 unique usable rows (2,861 train / 716 test; `random_state=42`). Five-fold shuffled CV (`random_state=42`) on training rows compared raw/log Linear Regression, tuned Ridge/Lasso, and tuned Extra Trees. **Lasso Regression on log selling price** was selected by highest training-CV R²; the test set was not used for model selection.

| Candidate | Training CV R² | Test MAE | Test MSE | Test RMSE | Test R² |
|---|---:|---:|---:|---:|---:|
| Raw Linear Regression | 0.6210 | 130,302.90 | 113,334,645,530.89 | 336,652.11 | 0.6482 |
| Log-target Linear Regression | 0.7660 | 96,011.17 | 69,317,640,586.85 | 263,282.44 | 0.7848 |
| Ridge Regression (log target) | 0.7729 | 94,639.64 | 68,380,857,485.17 | 261,497.34 | 0.7877 |
| **Lasso Regression (log target), selected** | **0.7822** | **95,394.85** | **73,430,608,649.04** | **270,980.83** | **0.7720** |
| Extra Trees (log target) | 0.7031 | 128,598.26 | 119,150,395,235.24 | 345,181.68 | 0.6301 |

- Selected Lasso alpha: `0.0001`. Ridge alpha: `0.1`. Extra Trees best search parameters: 140 estimators, max depth 12, max features 1.0, minimum leaf 1.
- Assignment target R² ≥ 0.75: **MET by the CV-selected model** (held-out R² 0.7720).
- Preserve the original pre-optimization result as historical: log-target Linear Regression R² `0.5189567`, MAE `160,955.1763`, MSE `146,800,118,056.3268`, RMSE `383,145.0353`. That run retained duplicates and used simpler features; it is not a like-for-like comparison.

### Mall customer segmentation — 200 rows

- K-Means with required K=5.
- Silhouette score: `0.5546572`.
- Actual cluster counts: cluster 0 = 81, cluster 1 = 39, cluster 2 = 22, cluster 3 = 35, cluster 4 = 23.
- Notebook-derived centroid names: medium income/moderate spending; high income/high spending; low income/high spending; high income/low spending; low income/low spending (cluster order 0–4 respectively).

### Student performance — 6,607 rows

| Model | MAE | MSE | RMSE | R² |
|---|---:|---:|---:|---:|
| Linear Regression (selected) | 0.4523920 | 3.2560200 | 1.8044445 | 0.7696496 |
| Random Forest Regressor | 1.0568740 | 4.4884382 | 2.1185935 | 0.6824609 |

Three notebook example estimates from the selected model: `78.65`, `60.35`, and `70.06`.

## Current dashboard status

- File: `Dashboard/index.html`; it is the only HTML file in `Dashboard/`.
- Single-file HTML/CSS/JavaScript with embedded chart data; it opens from `file://` without a server or external assets.
- Redesigned to a midnight dark UI with electric cyan, violet, and restrained magenta accents; distinct overview hierarchy, KPI strip, portfolio cards, dataset registry, contextual metric comparison, findings, and separate tailored layouts for each project.
- Sidebar collapses on desktop with labels/tooltips and expands as a mobile drawer; project-information navigation scrolls to the overview registry. Print report action was verified with the browser print function intercepted.
- Car page now shows the selected Lasso model, held-out MAE/MSE/RMSE/R², five-candidate training-CV/test comparison, historical R² 0.519 context, deduplication details, real test-row prediction examples, and actual-vs-predicted/residual charts from 103 selected-model test points.
- Added model metric cards, legible confusion matrices with row/column class labels, comparison metrics, hoverable SVG `<title>` data, cluster profiles, and a car residual-vs-actual chart derived only from embedded actual/predicted test sample data.
- Browser-tested all five views at five viewport widths (25 page/viewport combinations); every project chart rendered, tables appeared, and no page-error events occurred.
- Responsive width checks at 1440, 1024, 768, 390, and 320 px found no document horizontal overflow. A transient mobile overflow during viewport transition was identified and fixed by removing the workspace margin transition at the mobile breakpoint; the complete 25-case check passed after the fix.
- Mobile drawer open/close, desktop collapse/expand, active view state, accessible navigation labels, project-information navigation, student examples, car residual points, cluster profiles, and nine cells per confusion matrix were checked. A chart hover tooltip was verified from a data point.
- Print action invoked the browser print function in the verification page. No external scripts/styles/assets are used.
- Dashboard JavaScript `node --check`, embedded JSON/shape/metric assertions, HTML parser, single-HTML-file assertion, and offline dependency checks passed after the redesign.
- All four dataset row counts and key scores were checked against the exported notebook results.
- The Iris, Mall, and Student sections retain the previously verified notebook execution. Car results were refreshed by executing the revised car section (cells 27–50) against the supplied CSV; the complete notebook's upload flow remains unverified.
- Native SVG `<title>` descriptions and the custom point tooltip were verified. A human assistive-technology audit is not performed.

## Current PowerPoint status

- File: `ML_IV_Presentation.pptx`.
- Verified by reading its Open XML package: exactly five slides.
- Car slide now includes the CV-selected log-target Lasso, CV R² 0.782, all four held-out metrics, target-met status, and historical 0.519 baseline context.
- Exactly five slides and updated text were verified. Visual rendering/overflow remains unverified because no presentation renderer is installed on PATH.

## Current folder and files modified

Current working tree:

```text
ML_IV_Checked_Fixed/
├── Notebook/224010_AtharvBennur_ML_Project.ipynb
├── Datasets/
│   ├── Iris.csv
│   ├── CAR DETAILS FROM CAR DEKHO.csv
│   ├── Mall_Customers.csv
│   ├── StudentPerformanceFactors.csv
│   └── StudentPerformanceFactors-selected-columns.csv
├── Dashboard/index.html
├── ML_IV_Presentation.pptx
└── README.md
```

The active notebook was moved into `Notebook/`; datasets were moved from lowercase `dataset` to `Datasets/`; the dashboard and README were created/updated. `ML_IV_Presentation.pptx` was preserved. The original uploaded ZIP remains at `C:\Users\athar\Downloads\ML_IV_Checked_Fixed.zip`; it is a partial source backup and does not contain the CSVs. No final project folder, requirements file, or final ZIP exists yet.

Files created/updated in the active project:

- `Dashboard/index.html` — updated with verified car results and comparison.
- `Notebook/224010_AtharvBennur_ML_Project.ipynb` — car analysis cells 26, 32–50 updated and executed in a temporary notebook copy.
- `ML_IV_Presentation.pptx` — car slide updated.
- `README.md` — car results updated; broader requirements still pending.
- `PROJECT_PROGRESS.md` — created.
- `CONTINUATION_PROMPT.md` — created.
- Dataset files — reused; no dataset contents were changed.

## Tests executed and results

- Dataset schema/quality inspection: passed.
- Revised car notebook section (cells 27–50) executed successfully in a temporary notebook copy with the supplied car CSV path; selected Lasso test metrics and target status printed as expected. The full notebook/upload workflow was not executed.
- Car training-only CV and fixed held-out metrics independently reproduced in a separate Python run; dashboard payload matches the exported comparison and 103 actual/predicted test points.
- Dashboard browser test from local `file://`: all five views rendered, project navigation worked, SVG charts appeared, comparison and prediction-example tables rendered, target callout showed the measured result, and no page errors occurred.
- Responsive dashboard check at 1440, 1024, 768, 390, and 320 CSS pixels: no horizontal page overflow (at 320, `scrollWidth` equaled viewport width); mobile drawer navigation worked.
- Dashboard JavaScript syntax check via extracted inline script and `node --check`: passed.
- Dashboard data JSON/schema assertions passed: counts, five model rows, selected and historical scores, three examples, 24 price bins, and all 27 represented model years were checked.
- PowerPoint Open XML: exactly five slides; car slide text contains CV R² 0.782, MAE, MSE, RMSE, test R² 0.772, target met, and historical baseline.
- `git diff --check`: passed before commit.
- Git: commit `b5c2f860` pushed to `origin main`.
- GitHub Pages: build and deploy run `42190041668` completed successfully. The public `/Dashboard/` URL returns HTTP 200 and embeds Lasso Regression, held-out R² 0.772049, and historical R² 0.518957. The live page was opened in the browser; its selected-model callout, metric cards, and three example rows rendered with no page errors.
- Final ZIP extraction/content verification: NOT RUN (ZIP not created).
- Visual PowerPoint rendering/overflow check: NOT RUN; no presentation renderer is installed on PATH.
- Google Colab upload verification: NOT RUN.

## Known issues and limitations

1. The car target is met by the CV-selected model (test R² 0.7720); the historical pre-optimization 0.519 score is preserved and is not directly comparable.
2. The original notebook's non-Colab upload code uses Tkinter; the robust headless path fallback, full upload validation, encoding recovery, and Colab upload behavior remain unverified.
3. Notebook execution outputs were not saved to the source notebook; the updated car section was executed in a temporary copy with only its upload cell pointed to the provided CSV.
4. The full fresh-kernel notebook and all four upload sections have not yet been executed after the changes.
5. Student raw data has 235 missing values; the existing workflow imputes predictor gaps inside a training-fitted pipeline and drops rows with a missing target.
6. `StudentPerformanceFactors-selected-columns.csv` is extra to the requested clean package. Determine whether it is referenced before packaging; preserve the source copy.
7. There is no `requirements.txt`, final `Machine_Learning_IV_Final` directory, or final ZIP yet.
8. The code and dashboard deployment are complete for this change. A later progress-documentation commit still needs to be pushed after this status update.

## Exact next steps

1. Audit and improve the notebook upload helper: four independent upload sections, Colab support, GUI when available, explicit headless path fallback, and useful extension/content/column/multi-file/encoding validation.
2. Execute the complete notebook from a fresh kernel against all four included datasets without source-cell edits, and document any environment-specific UI test gaps.
3. Complete README setup/reproducibility coverage and add a minimal, accurate `requirements.txt`.
4. Create a separate `Machine_Learning_IV_Final` folder and `224010_Atharv_M_Bennur_ML_IV_Final.zip`; preserve the source folder/archive and package only required datasets plus required project files.
5. Review PowerPoint layout with a renderer if one becomes available; otherwise retain the current text/bounds checks and record the limitation.
6. Extract-test the final ZIP, run all final checks, then update both continuation files. Keep overall status IN PROGRESS until every requirement is verified.

## Technical decisions to preserve

- Use the full `StudentPerformanceFactors.csv` for notebook/dashboard results, not the selected-columns variant.
- Keep each notebook dataset upload independent; do not require all four files at notebook start.
- Preprocessing must be fitted within training pipelines; preserve fixed seeds/splits and training-only CV for model selection.
- Preserve test-set independence; do not tune against test results or fabricate metrics.
- Dashboard must remain one self-contained `Dashboard/index.html`, open directly, and use only values from the final notebook run.
- Current dashboard UI/UX redesign uses a dark cyberpunk system with restrained cyan/violet/magenta, page-specific hierarchies, accessible named navigation, collapsed tooltips, and mobile drawer; do not revert to the former light theme.
- Presentation must be exactly five slides.
- Work in a new final folder and preserve the existing working project/source archive.

## Commands for continuing verification (Windows PowerShell)

Run the notebook with Jupyter in a fresh environment (after installing the requirements):

```powershell
python -m pip install -r requirements.txt
jupyter notebook .\Notebook\224010_AtharvBennur_ML_Project.ipynb
```

Check dashboard JavaScript syntax without creating temporary files:

```powershell
@'
const fs = require('fs');
const html = fs.readFileSync('Dashboard/index.html', 'utf8');
const script = html.match(/<script>\s*([\s\S]*?)<\/script>/)[1];
new Function(script);
console.log('Dashboard JavaScript syntax OK');
'@ | node
```

Inspect the final ZIP:

```powershell
tar -tf .\224010_Atharv_M_Bennur_ML_IV_Final.zip
```

Use the VS Code browser/test tools for actual navigation, chart rendering, responsive behavior, and console errors. Do not claim a browser or Colab test that was not run.
