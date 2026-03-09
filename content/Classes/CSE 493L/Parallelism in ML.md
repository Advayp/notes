## Data Parallel
- Scale out model, and dispatch inputs to different copies of the same model
- Doesn't speed up any one input, helps only if you have a lot of inputs

## Tensor Parallelism
- Put half of each matrix on one GPU, and the other half on the second one
- Synchronize communications to ensure matrix multiplication is complete
- If the network is fast, this increases throughput and lower latency
- weights are distributed, but this scales exponentially due to the nature of p2p communication

## Pipeline Parallelism
- Each device gets a stage of execute
- Increases throughput, higher latency
- Weights are distributed and scales linearly
