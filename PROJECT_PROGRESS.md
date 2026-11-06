# Project Progress — Machine Learning IV

**Last verified:** 2026-11-06  
**Project root currently in use:** `C:\Users\athar\Downloads\ML_IV_Checked_Fixed`  
**Overall status:** IN PROGRESS — the dashboard and existing five-slide presentation are present, but the latest master specification has additional uncompleted requirements. Do not mark the project FINALIZED until the final copied project and ZIP pass the complete QA checklist.

## Status summary

| Area | Status | Verified state |
|---|---|---|
| Source/project inspection | COMPLETED | Inspected the project tree, notebook sections, README, CSV schemas, browser dashboard, and PowerPoint slide text/count. |
| Dataset availability | COMPLETED | The four full datasets are present under `Datasets/`; the additional selected-columns student CSV is also present and needs a use/cleanup decision. |
| Notebook modeling workflows | NEEDS VERIFICATION | Notebook modeling cells were executed successfully in a temporary in-memory copy, with the four upload cells replaced by explicit paths to the supplied datasets. The original notebook's upload cells were not fully tested in Colab or headless VS Code. |
| Notebook upload/reproducibility requirements | NOT STARTED | Master specification requires robust independent upload sections, file validation, encoding handling, and a headless path fallback. The notebook currently uses Colab upload or a Tkinter picker. |
| Dashboard UI/UX redesign | COMPLETED | Rebuilt the standalone dashboard as a dark premium cyberpunk analytics workspace, preserving verified embedded results and one-file/offline operation. Browser tested at desktop and responsive widths. |
| PowerPoint | NEEDS VERIFICATION | Existing deck has exactly five slides and its text includes the measured metrics. It still needs full visual/overflow review and updates to cover all latest slide requirements, including car RMSE and residual analysis. |
| README | NEEDS VERIFICATION | README was updated for the first dashboard deliverable, but it does not yet satisfy the full latest guide requirements (installation, requirements, per-environment notebook use, reproducibility, etc.). |
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

### Car price — 4,340 rows

Notebook selected **Log-target Linear Regression** using training-only cross-validation. Held-out test metrics:

- MAE: `160,955.1763`
- MSE: `146,800,118,056.3268`
- RMSE: `383,145.0353` (derived as `sqrt(MSE)`)
- R²: `0.5189567`
- Assignment target R² ≥ 0.75: **NOT MET**. Do not manipulate or obscure this result.
- Raw-target Linear Regression test metrics: MAE `210,859.8603`, MSE `170,955,646,620.6259`, R² `0.4398024`; RMSE is `sqrt(MSE)`.

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
- Added model metric cards, legible confusion matrices with row/column class labels, comparison metrics, hoverable SVG `<title>` data, cluster profiles, and a car residual-vs-actual chart derived only from embedded actual/predicted test sample data.
- Browser-tested all five views at five viewport widths (25 page/viewport combinations); every project chart rendered, tables appeared, and no page-error events occurred.
- Responsive width checks at 1440, 1024, 768, 390, and 320 px found no document horizontal overflow. A transient mobile overflow during viewport transition was identified and fixed by removing the workspace margin transition at the mobile breakpoint; the complete 25-case check passed after the fix.
- Mobile drawer open/close, desktop collapse/expand, active view state, accessible navigation labels, project-information navigation, student examples, car residual points, cluster profiles, and nine cells per confusion matrix were checked. A chart hover tooltip was verified from a data point.
- Print action invoked the browser print function in the verification page. No external scripts/styles/assets are used.
- Dashboard JavaScript `node --check`, embedded JSON/shape/metric assertions, HTML parser, single-HTML-file assertion, and offline dependency checks passed after the redesign.
- All four dataset row counts and key scores were checked against the exported notebook results.
- The dashboard is based on the previously verified notebook execution; it should be refreshed if notebook evaluation or preprocessing is changed in future work.
- Native SVG `<title>` descriptions and the custom point tooltip were verified. A human assistive-technology audit is not performed.

## Current PowerPoint status

- File: `ML_IV_Presentation.pptx`.
- Verified by reading its Open XML package: exactly five slides.
- Text includes all four projects and most current measured results, including the car R² target failure, Mall silhouette and cluster counts, and both student model comparisons.
- Needs a visual review for overflow/readability and a content update to include the car RMSE and residual-analysis findings required by the latest specification. Recheck all values against the final notebook after any model change.

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

- `Dashboard/index.html` — created.
- `README.md` — updated; further work required.
- `PROJECT_PROGRESS.md` — created.
- `CONTINUATION_PROMPT.md` — created.
- `Notebook/224010_AtharvBennur_ML_Project.ipynb` and dataset files — moved/reused, not otherwise modified during dashboard creation.

## Tests executed and results

- Dataset schema/quality inspection: passed.
- Notebook model workflow execution in a temporary in-memory copy with explicit dataset paths: passed. This is not a full test of the notebook's original upload cells, Colab, or headless path fallback.
- Dashboard browser test from local `file://`: passed; all five views rendered; all charts and tables were present; no page errors occurred.
- Dashboard responsive behavior: 25 page/viewport combinations at 1440, 1024, 768, 390 and 320 px passed without horizontal overflow.
- Dashboard actions verified: collapsed rail, mobile drawer, project-information jump, chart tooltip, and print action.
- Dashboard JavaScript `node --check`: passed.
- HTML parser and embedded dashboard JSON/metric assertions: passed.
- PowerPoint Open XML slide count and text extraction: exactly five slides, passed.
- Final ZIP extraction/content verification: NOT RUN (ZIP not created).
- Visual PowerPoint rendering/overflow check: NOT RUN.
- Google Colab upload verification: NOT RUN.

## Known issues and limitations

1. The latest master prompt adds requirements beyond the original dashboard request. Notebook upload improvements, full README, requirements, final project copy, PowerPoint visual/content review, and package/ZIP remain outstanding.
2. The current notebook's non-Colab upload code uses Tkinter; it lacks the requested guaranteed headless fallback, extension/required-column validation at file selection, and tested encoding recovery.
3. Notebook cells were not saved with execution outputs; the successful execution was performed in a temporary copy with dataset loader cells changed only for that run.
4. The car price target R² of 0.75 remains unmet. Report honestly and investigate only with leakage-free validation; do not promise improvement.
5. Student raw data has 235 missing values; current workflow imputes missing predictors inside a training-fitted pipeline and drops rows with missing target.
6. `StudentPerformanceFactors-selected-columns.csv` is extra to the requested clean package. Determine whether it is used/referenced before deciding to retain it in the final ZIP; never delete the only copy without checking.
7. There is no `requirements.txt`, final `Machine_Learning_IV_Final` directory, or final ZIP yet.

## Exact next steps

1. Read `CONTINUATION_PROMPT.md`, recheck this progress file, and inspect current files/diffs before changing anything.
2. Make a separate `Machine_Learning_IV_Final` copy while preserving the current working folder and original source ZIP. Do not overwrite or destructively clean the source.
3. Audit and improve the notebook upload helper: four independent dataset upload sections; Colab upload support; local GUI when available; dependable path fallback; no silent in-project auto-load; extension, non-empty file, required-column, multi-upload, and encoding validation with useful errors.
4. Execute the final notebook from a fresh kernel against all four included datasets without editing cells to inject paths. Save a clean reproducible notebook and record actual results. Test browser/GUI/Colab behavior only where the environment permits and state gaps clearly.
5. Reassess the car model using training-only validation and the untouched test split. Add requested residual analysis. Retain the current honest result if a sound improvement does not meet 0.75.
6. If final notebook metrics change, refresh embedded dashboard data and rerun all five-view, chart, navigation, responsive, offline, and browser error checks. The current cyberpunk redesign and car residual visualization are implemented.
7. Update the PowerPoint to exactly five slides with all required metrics (including car MAE/MSE/RMSE/R²), cluster insights, student model comparison, and concise conclusions. Render/inspect slide bounds if a rendering tool is available.
8. Add a minimal, accurate `requirements.txt`; complete README with Windows setup, VS Code/Colab instructions, datasets, reproducibility, real metrics, and limitations.
9. Keep only the four required datasets in the final package unless the extra selected-columns CSV is proven necessary. Build final folder exactly as specified, add both continuation files, create `224010_Atharv_M_Bennur_ML_IV_Final.zip`, and inspect/extract-test it.
10. Run final notebook, dashboard, PowerPoint, structure, and ZIP checks. Update this progress file after each major stage and mark FINALIZED only after all mandatory requirements are verified.

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
