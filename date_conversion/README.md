# Date Conversion

Problem: Train an Encoder–Decoder model that can convert a date string from one format to another (e.g., from "April 22, 2019" to "2019-04-22").

Hyperparameter categories:
* Dataset: train_sz, batch_sz
* Model: embed_sz, RNN_type, NN
* Cost function: binary_cross_entropy
* Optimizer: optimizer, lr

Convergence criterion = Train for 30 epoxhs. Early stopping with patience 3, using the metric val_accuracy.


| run_name | train_sz | batch_sz | embed_sz | RNN_type | NN            | optimizer | lr     | converges on epoch | max val_acc | time_per_epoch |
|----------|----------|----------|----------|---------|---------------|-----------|--------|-------|-----------------|-------|
| default  |  10,000  |    32    |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  | 12    |     1.00        |       |
|----------|----------|----------|----------|---------|---------------|-----------|--------|-------|-----------------|-------|
|   run1   | **5,000**|    32    |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  19   |     1.00        |       |
|   run2   | **7,500**|    32    |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  18   |     1.00        |       |
| **run3** |**10,000**|    32    |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  13   |     1.00        |       |
|   run4   |**12,500**|    32    |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  10   |     1.00        |       |
|   run5   |**15,000**|    32    |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  12   |     1.00        |  22s  |
|   run6   |**17,500**|    32    |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  10   |     1.00        |  26s  |
|   run7   |**20,000**|    32    |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  9    |     1.00        |  28s  |
|   run8   |**20,500**|    32    |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  7    |     1.00        |  38s  |
|----------|----------|----------|----------|---------|---------------|-----------|--------|-------|-----------------|-------|
|   run9   |  10,000  | **16**   |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  9    |     1.00        |  18s  |
| **run10**|  10,000  | **32**   |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  11   |     1.00        |  17s  |
|   run11  |  10,000  | **64**   |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  19   |     1.00        |  12s  |
|   run12  |  10,000  | **128**  |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  30   |     1.00        |  9s   |
|   run13  |  10,000  | **256**  |   32     |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  51   |     0.99        |  7s   |
|----------|----------|----------|----------|---------|---------------|-----------|--------|-------|-----------------|-------|
|   run14  |  10,000  |   32     |   32     |**LSTM** | (L=128, D=n)  |   Nadam   | 0.001  |  13   |     1.00        |  17s  |
| **run15**|  10,000  |   32     |   32     |**GRU**  | (L=128, D=n)  |   Nadam   | 0.001  |  12   |     1.00        |  13s  |
|   run16  |  10,000  |   32     |   32 |**SimpleRNN**| (L=128, D=n)  |   Nadam   | 0.001  |  17   |     0.99        |  5s   |
|----------|----------|----------|----------|---------|---------------|-----------|--------|-------|-----------------|-------|
|   run17  |  10,000  |   32     |  **8**   |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  28   |     1.00        |  17s  |
|   run18  |  10,000  |   32     |  **16**  |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  14   |     1.00        |  17s  |
| **run14**|  10,000  |   32     |  **32**  |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  13   |     1.00        |  17s  |
|   run19  |  10,000  |   32     |  **64**  |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  11   |     1.00        |  20s  |
|   run20  |  10,000  |   32     |  **128** |  LSTM   | (L=128, D=n)  |   Nadam   | 0.001  |  10   |     1.00        |  24s  |
|----------|----------|----------|----------|---------|---------------|-----------|--------|-------|-----------------|-------|


Notes:
* **Training Dataset Size:**
    - The larger the training size, the better the generalization error.

* **Batch Size:**
    - The larger the batch size, the faster an epoch is. This makes sense, because there are a fewer steps per epoch, and more parallel computation is being done.
    - The larger tha batch size, the slower the overall training. With a larger batch size, we can compute a more accurate estimate of the gradient. Recall the gradient is the mean of the gradients over all examples in the batch. The standard error of the mean estimated from n samples is given by sigma/sqrt(n). The denominator of sqrt(n) shows that there are less than linear returns to using mode examples ot esitmate the gradient.
    The optimization algorithm converges much faster if we are allowed to rapidly compute approximate estimates of the gradient rather than slowly computing the exact gradient.

* **RNN Type:**
    - GRU taks about the same time to converge as LSTM, but is faster per epoch.
    - SimplRNN takes longer to converge w.r.t no. of epochs, but each epoch is about 3x faster than that of GRU. It, however, does not achieve 100% accuracy, stagnating at about 98% validation accuracy.

* **Embedding size:**
    - As the size of the embedding vector is increased from 8 to 32, there is a improvement in the convergence rate. This makes sense as higher dimension allows more information to be packed in the embedding vector.
    - But beyong the size of 32 there is no imporvement, suggesting that all the information needed to accurately represent the information requires only 32 numbers.
