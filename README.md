# Temporal Regularized Matrix Factorization

Project was inspired by the paper:

Yu, H. F., Rao, N., & Dhillon, I. S. (2016). Temporal regularized matrix factorization for high-dimensional time series prediction. In Advances in neural information processing systems (pp. 847-855).

Which can be found there: http://www.cs.utexas.edu/~rofuyu/papers/tr-mf-nips.pdf


## 1. Problem description

We have N timeseries of length T which are presented by matrix Y. We want to factorize it <a href="https://www.codecogs.com/eqnedit.php?latex=$Y&space;=&space;F\times&space;X$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$Y&space;=&space;F\times&space;X$" title="$Y = F\times X$" /></a>.

To solve this problem we will minimize:

<a href="https://www.codecogs.com/eqnedit.php?latex=$$\min\limits_{F,X}\sum\limits_{(i,t)\in\Omega}\left(Y_{it}-f_i^Tx_t\right)^2&plus;\lambda_fR_f(F)&plus;\lambda_xR_x(X).$$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$$\min\limits_{F,X}\sum\limits_{(i,t)\in\Omega}\left(Y_{it}-f_i^Tx_t\right)^2&plus;\lambda_fR_f(F)&plus;\lambda_xR_x(X).$$" title="$$\min\limits_{F,X}\sum\limits_{(i,t)\in\Omega}\left(Y_{it}-f_i^Tx_t\right)^2+\lambda_fR_f(F)+\lambda_xR_x(X).$$" /></a>

By doing that we will find latent embedding vectors for timeseries and latent temporal embeddings for timepoints.
One can further use this embeddings to forecast new data or to impute missings.

## 2. Package description
Package consists of:
- trmf : time series modelling
- synthetic_data : data generation for experiments

additionaly:
- Metrics : metrics for experiments and validation
- Forecast : simple models for testing experiments
- RollingCV : rolling cross-validation implementation

## 3. Experiments

In experiments_[something].ipynb you can find some experiments on the package:

1) experiments_synthetic.ipynb: testing trmf model against other simple model on synthetic data

** Lags = {1} **

|| h=1 | h=5 | h=10 | h=20 |
|------|------|------|------|
| Naive | **0.105**/**0.138** | **0.151**/**0.2** | **0.175**/**0.23** | 0.38/**0.477** |
| Mean | 1.0/1.136 | 1.0/1.114 | 1.0/1.094 | 1.0/1.079 |
| AutoRegression | 0.107/0.142 | 0.16/0.215 | 0.2/0.275 | 0.42/0.536 |
| TRMF | 0.172/0.218 | 0.155/0.227 | 0.197/0.261 | **0.368**/0.48 |

** Lags = {1,7} **

|| h=1 | h=5 | h=10 | h=20 |
|------|------|------|------|
| Naive | 0.82/0.956 | 1.072/1.292 | 0.893/1.119 | 1.051/1.303 |
| Mean | 1.0/1.176 | 1.0/1.219 | 1.0/1.236 | 1.0/1.259 |
| AutoRegression | **0.503**/**0.581** | **0.496**/**0.599** | 0.572/0.717 | **0.86/1.107** |
| TRMF | 0.515/0.612 | 0.498/0.603 | **0.565/0.704** | 0.87/1.117 |

** Lags = {1,7,14,28} **

| h=1 | h=5 | h=10 | h=20 |
|------|------|------|------|
| Naive | 1.012/1.191 | 0.97/1.18 | 0.968/1.202 | 0.917/1.162 |
| Mean | 1.0/1.164 | 1.0/1.218 | 1.0/1.206 | 1.0/1.197 |
| AutoRegression | **0.618**/0.733 | **0.506**/**0.648** | **0.567**/**0.715** | 0.619/0.755 |
| TRMF | 0.633/**0.662** | 0.544/0.676 | 0.578/0.726 | **0.582**/**0.72** |

2) experiments_electricity.ipynb: testing trmf model against other simple model on electricity data


3) experiments_crypto.ipynb: testing trmf model against other simple model on crypto-currency data


4) experiments_missings.ipynb: testing trmf model against other simple model on missing data imputation

| missings | 5% | 10% | 25% |
|------|------|------|
| Naive | 0.367/0.574 | 0.373/0.584 | 0.391/0.613 |
| Mean | 129.506/150.367 | 108.291/125.712 | 89.242/103.586 |
| TRMF | **0.359/0.516** | **0.36/0.519** | **0.361/0.52** |

More details in notebooks.

## 4. Conclusion

1) TRMF model needs additional regularization on matrix W (sum of the row elements must be close to one). Otherwise, predictions for long periods will be unstable;

2) Every timeseries is better to be normalized before using TRMF;

3) TRMF is good on data imputation;

4) TRMF is good when data has missings.

## 5. Plan

1) Article analysis // done
2) Synthetic Data Generator // done
3) Basic realization of trmf with gradient descent // done
4) Documentation and help functions // done
5) Experiments on synthetic data (vs other models) // done
6) Rolling CV functionality // done
7) Experiments on electricity data (vs other models) // done
8) CryptoCurrency forecasting (vs other models) // done
9) Missing data handling // done
10) Missing data imputation experiments (vs other models) // done
