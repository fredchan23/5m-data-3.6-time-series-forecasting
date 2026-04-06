# 3.6 Time-Series Data and Forecasting

## Lesson Overview

![infographic](assets/infographic-3.6.png)

## Dependencies

Refer to the following markdown file for the respective sections of the class:

- [Self Studies](./studies.md)
- [Lesson](./lesson.md)
- [Assignment](./assignment.md)
- [Quiz](./quiz.md)
- [Reference](./reference.md)

## Lesson Objectives

Learners will understand:

- Time-series data
- Time-series visualization and analysis
- Forecasting of time-series data

Learners will be able to:

- Plot various time-series charts
- Perform time-series decomposition
- Perform time-series forecasting

## Lesson Plan

| Duration | What                    | How or Why                                                  |
| -------- | ----------------------- | ----------------------------------------------------------- |
| - 5mins  | Start zoom session      | So that learners can join early and start class on time.    |
| 20 mins  | Activity                | Recap on self-study and prework materials.                  |
| 40 mins  | Code-along              | Part 1: Introduction to Time-Series Data and Visualization. |
|          | **1 HR MARK**           |
| 30 mins  | Code-along              | Part 2: Time-Series Decomposition.                          |
| 10 mins  | Break                   |                                                             |
| 20 mins  | Code-along              | Part 3: Forecasting Evaluation and Metrics.                 |
|          | **2 HR MARK**           |
| 50 mins  | Code-along              | Part 4: Forecasting Models- Naive, ARIMA, ETS.              |
| 10 mins  | Briefing / Q&A          | Brief on references, assignment, quiz and Q&A.              |
|          | **END CLASS 3 HR MARK** |

## Notebook Compatibility Fixes (2026-04-06)

The following fixes were applied to `notebooks/time_series_forecasting_lesson.ipynb` to resolve breaking changes introduced by newer library versions.

### Quick Fix — run these commands in your terminal to update the `ml` kernel

```bash
conda activate ml

pip install "seaborn>=0.13"
pip install "statsmodels>=0.14.2"
pip install "sktime>=0.40.1"
pip uninstall -y skbase
pip install "scikit-base>=0.13.1,<0.14.0"
```

Fix 1 (pandas `datetime64`) is a code change already applied in the notebook — no install needed.

### Fix Summary

| # | Package | Error | Resolution |
|---|---------|-------|------------|
| 1 | pandas 3.0 | `ValueError: Supported units are 's', 'ms', 'us', 'ns'` — `PeriodIndex.astype('datetime64')` no longer accepts bare unit | Code change: `astype('datetime64')` → `to_timestamp()` |
| 2 | seaborn 0.12 | `OptionError: No such keys(s): 'mode.use_inf_as_na'` — removed pandas option used internally | Upgrade to seaborn 0.13+ |
| 3 | statsmodels 0.14.0 | `TypeError: deprecate_kwarg() missing 1 required positional argument` — decorator broke on newer numpy | Upgrade to statsmodels 0.14.2+ |
| 4 | sktime 0.25.0 | `TypeError: _check_reg_targets() missing 1 required positional argument: 'multioutput'` — sklearn 1.8 changed internal signature | Upgrade to sktime 0.40.1+ |
| 5 | scikit-base / skbase | `ImportError: cannot import name '_check_estimator_deps'` — two PyPI packages share the `skbase` namespace; wrong one was active | Remove `skbase`, upgrade `scikit-base` to 0.13.1 |
