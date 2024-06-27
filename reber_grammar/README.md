# Reber Grammars Hyperparameter Study

Convergence criterion = Early stopping, monitoring validation accuracy, with patience=3

Hyperparameters under test:
* Training size: obviously, more data, means faster convergence. But it also means more time to generate the data. 15,000 is a nice sweetspot.


| run_name | train_sz | embed_sz | batch_sz | RNN_type | NN            | optimizer | lr     | converges on epoch | max val_acc |
|----------|----------|----------|----------|----------|-------------  |-----------|--------|-------|-----------------|
|**run1**  |**15,000**|    5     | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 12    |     1.00        |
|   run2   |**20,000**|    5     | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 9     |     1.00        |
|   run3   |**10,000**|    5     | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 15    |     1.00        |
|   run4   |**11,000**|    5     | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 13    |     1.00        |
|   run5   |**12,000**|    5     | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 13    |     1.00        |
|   run6   |**13,000**|    5     | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 13    |     1.00        |
|   run7   |**14,000**|    5     | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 10    |     1.00        |
|   run8   |**5,000** |    5     | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 24    |     1.00        |
|   run9   |**7,000** |    5     | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 21    |     1.00        |
|   run10  |**9,000** |    5     | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 18    |     1.00        |
|   run11  |**30,000**|    5     | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 8     |     1.00        |
|   run12  |**50,000**|    5     | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 6     |     1.00        |
|----------|----------|----------|----------|----------|---------------|-----------|--------|-------|-----------------|
|  run13   |  15,000  |   **1**  | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 17    |     0.97        |
|  run14   |  15,000  |   **3**  | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 12    |     1.00        |
|  run1    |  15,000  |   **5**  | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 12    |     1.00        |
|  run15   |  15,000  |   **7**  | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 12    |     1.00        |
|  run16   |  15,000  |  **10**  | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 11    |     1.00        |
|  run17   |  15,000  |  **10**  | 32       |  GRU     | (R=32, D=1)   | SGD       | 0.02   | 12    |     1.00        |
|----------|----------|----------|----------|----------|---------------|-----------|--------|-------|-----------------|
|  run18   |  15,000  |     5    | 32       |  GRU     |**(R=8, D=1)** | SGD       | 0.02   | 28    |     0.9605      |
|  run19   |  15,000  |     5    | 32       |  GRU     |**(R=16, D=1)**| SGD       | 0.02   | 17    |     0.9740      |
|  run20   |  15,000  |     5    | 32       |  GRU     |**(R=24, D=1)**| SGD       | 0.02   | 14    |     1.00        |
|**run20b**|  15,000  |     5    | 32       |  GRU     |**(R=24, D=1)**| SGD       | 0.02   | 10    |     1.00        |
|  run1    |  15,000  |     5    | 32       |  GRU     |**(R=32, D=1)**| SGD       | 0.02   | 12    |     1.00        |
|  run21   |  15,000  |     5    | 32       |  GRU     |**(R=40, D=1)**| SGD       | 0.02   | 12    |     1.00        |
|  run21b  |  15,000  |     5    | 32       |  GRU     |**(R=40, D=1)**| SGD       | 0.02   | 10    |     1.00        |
|----------|----------|----------|----------|----------|---------------|-----------|--------|-------|-----------------|
|  run20   |  15,000  |     5    | 32       |**GRU**   |**(R=24, D=1)**| SGD       | 0.02   | 14    |     1.00        |
|  run22   |  15,000  |     5    | 32       |**LSTM**  |  (R=24, D=1)  | SGD       | 0.02   | 18    |     0.9940      |
|  run23   |  15,000  |     5    | 32       |**RNN**   |  (R=24, D=1)  | SGD       | 0.02   | N/A   |     0.7250      |
|  run24   |  15,000  |     5    | 32       |**RNN**   |  (R=32, D=1)  | SGD       | 0.02   | N/A   |     0.7250      |
|  run25   |  15,000  |     5    | 32       |**RNN**   |  (R=32, R=32, D=1)  | SGD | 0.02   | N/A   |     0.6930      |


Notes:
* SimpleRNN is much slower to train than LSTM, and performs much worse.( 23s/epoch for 2layer SRNN, 15s/epoch for 1layer RNNN  vs 3s/epoch for 1 layer GRU/LSTM)
* With SimpleRNN, performance improves at the very intially, and then falls sharply, and stagnates.
