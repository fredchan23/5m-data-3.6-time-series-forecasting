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

### 1. `PeriodIndex.astype('datetime64')` removed (pandas 3.0)

**Error:** `ValueError: Supported units are 's', 'ms', 'us', 'ns'`

**Fix:** Replaced `data.index.astype('datetime64')` with `data.index.to_timestamp()`. Bare `datetime64` without a unit is no longer accepted in pandas 3.0; `to_timestamp()` is the correct conversion for a `PeriodIndex`.

### 2. `mode.use_inf_as_na` pandas option removed (seaborn 0.12 + pandas 3.0)

**Error:** `OptionError: No such keys(s): 'mode.use_inf_as_na'`

**Fix:** Upgraded seaborn from 0.12.2 → 0.13.2. Seaborn 0.12 internally called `pd.option_context('mode.use_inf_as_na', True)`, which was removed in pandas 3.0. Seaborn 0.13 no longer uses this option.

### 3. `deprecate_kwarg()` signature change (statsmodels 0.14.0)

**Error:** `TypeError: deprecate_kwarg() missing 1 required positional argument: 'new_arg_name'`

**Fix:** Upgraded statsmodels from 0.14.0 → 0.14.6. The internal `deprecate_kwarg` decorator in statsmodels 0.14.0 was incompatible with the installed numpy version, causing an import failure for `statsmodels.tsa.stattools`.

### 4. `_check_reg_targets()` signature change (sktime 0.25.0 + sklearn 1.8.0)

**Error:** `TypeError: _check_reg_targets() missing 1 required positional argument: 'multioutput'`

**Fix:** Upgraded sktime from 0.25.0 → 0.40.1. sklearn 1.8.0 added `sample_weight` as a new required positional argument to the internal `_check_reg_targets()` function (between `y_pred` and `multioutput`), breaking sktime's `mean_absolute_percentage_error`. The upgrade also resolved the dependency by pulling in sklearn 1.7.2 and pandas 2.3.3.

### 5. `_check_estimator_deps` not found in `skbase` (sktime 0.40.1 + scikit-base conflict)

**Error:** `ImportError: cannot import name '_check_estimator_deps' from 'skbase.utils.dependencies'`

**Fix:** Removed the conflicting `skbase` PyPI package and upgraded `scikit-base` from 0.6.2 → 0.13.1. Both `skbase` (a separate, unrelated PyPI package) and `scikit-base` (sktime's actual dependency) install into the same `skbase` Python namespace. The `skbase` package clobbered `scikit-base`, and neither version had `_check_estimator_deps`, which was added in `scikit-base 0.7+`. sktime 0.40.1 requires `scikit-base>=0.6.1,<0.14.0`.
