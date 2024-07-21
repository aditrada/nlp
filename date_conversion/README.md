# Date Conversion

Problem: Train an Encoder–Decoder model that can convert a date string from one format to another (e.g., from "April 22, 2019" to "2019-04-22").

Hyperparameter categories:
* Dataset: train_sz, batch_sz
* Model: embed_sz, RNN_type, NN
* Cost function: binary_cross_entropy
* Optimizer: optimizer, lr

Convergence criterion = Train for 30 epoxhs. Early stopping with patience 3, using the metric val_accuracy.


| run_name | train_sz | batch_sz | embed_sz | RNN_type | NN            | optimizer | lr     | converges on epoch | max val_acc | time_per_epoch |
|----------|----------|----------|----------|----------|---------------|-----------|--------|-------|-----------------|-------|
| default  |  10,000  |    32    |   32     |  LSTM    | (L=128, D=n)  |   Nadam   | 0.001  | 12    |     1.00        |       |
|----------|----------|----------|----------|----------|---------------|-----------|--------|-------|-----------------|-------|
|   run1   | **5,000**|    32    |   32     |  LSTM    | (L=128, D=n)  |   Nadam   | 0.001  |  19   |     1.00        |       |
|   run2   | **7,500**|    32    |   32     |  LSTM    | (L=128, D=n)  |   Nadam   | 0.001  |  18   |     1.00        |       |
|   run3   |**10,000**|    32    |   32     |  LSTM    | (L=128, D=n)  |   Nadam   | 0.001  |  13   |     1.00        |       |
|   run4   |**12,500**|    32    |   32     |  LSTM    | (L=128, D=n)  |   Nadam   | 0.001  |  10   |     1.00        |       |
|   run5   |**15,000**|    32    |   32     |  LSTM    | (L=128, D=n)  |   Nadam   | 0.001  |  12   |     1.00        |  22s  |
|   run6   |**17,500**|    32    |   32     |  LSTM    | (L=128, D=n)  |   Nadam   | 0.001  |  10   |     1.00        |  26s  |
|   run7   |**20,000**|    32    |   32     |  LSTM    | (L=128, D=n)  |   Nadam   | 0.001  |  9    |     1.00        |  28s  |
|   run8   |**20,500**|    32    |   32     |  LSTM    | (L=128, D=n)  |   Nadam   | 0.001  |  7    |     1.00        |  38s  |

