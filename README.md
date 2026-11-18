# QRT Asset Allocation Performance Forecasting

This solution predicts the sign of next-day returns for approximately 278 asset allocations using 20 days of returns, signed volume, and turnover. The challenge metric is accuracy.

## Data

The data is not included in this repository. After registering, download it from [Challenge Data](https://challengedata.ens.fr/challenges/167) and place the files in `data/`.

## Key finding

Consecutive TS dates share 19 of their 20 return days: the median best-match shifted correlation is 0.9935, and 2,100 of 2,522 dates have a correlation above 0.95. Random-date K-fold therefore leaks information. I rebuilt the timeline by chaining dates on that correlation and used 8 contiguous chronological blocks for cross-validation.

## Results

Out-of-fold accuracy:

| Stage | Model | OOF Acc |
|---|---|---|
| Benchmark | LightGBM MSE | 52.22% |
| Phase 2 | Huber + Binary + GROUP | 52.32% |
| Phase 3 | 111 engineered features, chrono CV | 52.49% |
| Phase 3.5 | 131 features + group z-scores | 52.51% |
| Phase 4 | Regularised trees, 55/45 Binary/Huber blend | 52.62% |

## How to run

1. Install dependencies: `pip install -r requirements.txt`
2. Put the challenge data in `data/`.
3. Run `qrt_solution.ipynb` from top to bottom.

## Credits

Challenge and data by Qube Research & Technologies via Challenge Data (ENS).
