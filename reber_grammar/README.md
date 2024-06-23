# Reber Grammars Hyperparameter Study

Convergence criterion = Early stopping, monitoring validation accuracy, with patience=3

Hyperparameters under test:
* Training size: obviously, more data, means faster convergence. But it also means more time to generate the data. 15,000 is a nice sweetspot.


| run_name | train_sz | embed_sz | batch_sz | RNN_type | NN          | optimizer | lr     | converges on epoch |
|----------|----------|----------|----------|----------|-------------|-----------|--------|-------|
|**run1**  |**15,000**| 5        | 32       |  GRU     | (R=32, D=1) | SGD       | 0.02   | 12    |
|   run2   |**20,000**| 5        | 32       |  GRU     | (R=32, D=1) | SGD       | 0.02   | 9     |
|   run3   |**10,000**| 5        | 32       |  GRU     | (R=32, D=1) | SGD       | 0.02   | 15    |
|   run4   |**11,000**| 5        | 32       |  GRU     | (R=32, D=1) | SGD       | 0.02   | 13    |
|   run5   |**12,000**| 5        | 32       |  GRU     | (R=32, D=1) | SGD       | 0.02   | 13    |
|   run6   |**13,000**| 5        | 32       |  GRU     | (R=32, D=1) | SGD       | 0.02   | 13    |
|   run7   |**14,000**| 5        | 32       |  GRU     | (R=32, D=1) | SGD       | 0.02   | 10    |
|   run8   |**5,000** | 5        | 32       |  GRU     | (R=32, D=1) | SGD       | 0.02   | 24    |
|   run9   |**7,000** | 5        | 32       |  GRU     | (R=32, D=1) | SGD       | 0.02   | 21    |
|   run10  |**9,000** | 5        | 32       |  GRU     | (R=32, D=1) | SGD       | 0.02   | 18    |
|   run11  |**30,000**| 5        | 32       |  GRU     | (R=32, D=1) | SGD       | 0.02   | 8     |
|   run12  |**50,000**| 5        | 32       |  GRU     | (R=32, D=1) | SGD       | 0.02   | 6     |




