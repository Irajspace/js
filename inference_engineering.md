## complete inference stack
```
The diagram shows this as a foundational stack of software, building from the hardware up:

CUDA: The lowest level. This is NVIDIA's platform that allows software to communicate directly with the GPU hardware.

PyTorch: The popular machine learning framework used to build and manipulate the model's neural networks.

Inference Engines (vLLM, SGLang, TensorRT-LLM): These are highly optimized software libraries specifically designed to serve Large Language Models quickly.

Note on Kernels: The text also mentions "FlashAttention," which is a highly optimized low-level operation (a kernel) that makes processing sequences of text much faster and less memory-intensive.


```
## model performance tricks
```
Batching: Processing multiple user requests at the exact same time.

Caching: Remembering previous computations so the model doesn't have to redo work.

Quantization: Shrinking the size of the model's numbers (like going from high-res to low-res) to make it run faster using less memory.

Speculation, Parallelism, and Disaggregation: Advanced methods for predicting outputs and splitting workloads across hardware.


```
## infrastructure layer
```
Base Hardware: The physical GPUs, Storage, and Networking.
Multi-Cloud Capacity Management: Software to manage resources across different cloud providers (like AWS, GCP, or Azure).
Autoscaling: Automatically spinning up more servers when traffic spikes and turning them off when it's quiet.
Routing & Load Balancing: Directing incoming user requests to the servers that have the most capacity so no single machine gets overwhelmed.
```