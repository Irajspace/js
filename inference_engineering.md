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

## model training
```
Best Practices for Evals & Fine-Tuning
1. Establishing a Baseline
Some optimization techniques risk degrading model quality, making it essential to have a strict baseline to measure against.

Standard vs. Custom Benchmarks: Standard public intelligence benchmarks (like MMLU or SWE-bench) are great for initial shortlisting, but they often become saturated or gamed.

Goodhart's Law: "When a measure becomes a target, it ceases to be a good measure." Frontier labs are incentivized to beat public world-record benchmarks, meaning you cannot rely solely on public charts. There is no substitute for directly evaluating a model against your product's actual domain.

Actionable Tips for Evals: Look at your actual data, be precise about focusing on the hardest problems your app solves, and use existing tooling rather than reinventing evaluation frameworks.


```

## what do u mean by fine-tuning
```
The Core Concept: Notice that the matrix dimensions do not change (it remains a 4x4 grid), but specific numbers inside the grid are altered (highlighted in bold green, like the 1 changing to 6, 7 changing to 3, etc.).

Key Takeaway: Fine-tuning shifts the values of a model's internal weights to specialize its knowledge while preserving its overall structural architecture.

```
## what do u mean by distillation
```


```