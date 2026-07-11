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
1. Visual Breakdown of Figure 1.3
[ Large "Teacher" Matrix ]      --->      [ Small "Student" Matrix ]
      1   9   2   3                             7   1   8
      5   0   7   6                             4   5   3
      8   3   4   2                             9   2   6
      2   6   0   9
What the Diagram Shows: On the left is a large 4x4 matrix representing a massive "Teacher" model. An arrow points to the right to a significantly smaller 3x3 matrix representing a compact "Student" model.

The Core Concept: Unlike fine-tuning (where matrix size stays the same), distillation shrinks the physical structure of the model. It trains a smaller model to emulate the actual probability distributions (both good and bad behaviors) of the larger teacher model, preserving broad intelligence in a much more efficient package.

```
## comparison
![alt text](image-57.png)
```

Perceived TPS: The observed streaming speed for a single user after the first token is generated (a latency metric).

Total TPS: The combined total number of tokens generated every second across the entire inference service for all active users (a throughput metric).

Inter-Token Latency (ITL): The exact millisecond gap between individual consecutive tokens. For example, an ITL of 10 milliseconds equates directly to 100 tokens per second per user.

To ensure a reliably fast user experience, inference engineers measure latency using percentiles rather than averages. The table breaks down exactly what these mean:

P50 (Median latency): 1 in every 2 requests is slower.

P90 (90th percentile latency): 1 in every 10 requests is slower.

P95 (95th percentile latency): 1 in every 20 requests is slower.

P99 (99th percentile latency): 1 in every 100 requests is slower.
```
## chapter-2 models
```
Two Main Transformer Styles:

Autoregressive token generation: Starts from a sequence and predicts the next most likely token (e.g., LLMs).

Iterative denoising: Starts with random noise and refines it step-by-step toward a clean output via diffusion (e.g., image generation).

The basic unit of a neural network is a node (neuron), which takes an input, multiplies it by weights, adds a bias, and outputs a result. In deep networks like the ones powering LLMs, these nodes are grouped into dozens or hundreds of sequential layers.
anatomy of neural network

Figure 2.1 visually charts the structural taxonomy of a multi-layer neural network:

Input Layer: The initial layer that accepts and processes raw incoming data.

Hidden Layers: The vast core network layers between the input and output where data is iteratively transformed into intermediate representations called "hidden states".

Output Layer: The final layer that renders the network’s final prediction.

Depending on their intended task, these networks combine two main component systems:

Encoders: Convert inputs (like text/images) into high-dimensional numerical vectors containing semantic meaning.

Decoders: Process those internal numerical representations to generate new text or images. Modern LLMs are predominantly decoder-only architectures.
```
## how they do
```
absolute most essential operation inside a neural network is matrix multiplication (matmul).
y=wx+b
Where the output vector $y$ is computed by taking the input vector $x$, multiplying it through the weights matrix $W$ (which is learned during training), and adding the bias vector $b$.

```
## the linear collapse problem
```
The Linear Collapse Problem
If you pass data sequentially through two separate linear layers (y = xW_1 + b_1 followed by z = yW_2 + b_2), the mathematical matrices simply multiply together and collapse the entire chain down into a single equivalent operation ($z = xW_3 + b_3$).


To prevent deep networks from mathematically collapsing, engineers use non-linear activation functions to artificially break up linearity between layers. This allows hidden layers to capture complex semantic meanings and properly support backpropagation.

The text calls out several highly performant activation functions vital to inference, such as ReLU (Rectified Linear Unit), SiLU, Swish, and SwiGLU

The Formula: 
Relu(x)max(0,x);
How it works: Look at the chart. If the mathematical input x is negative (less than 0.0), the output flatlines perfectly at exactly 0.0. If the input is positive, the output matches the input linearly. As covered earlier, this simple switch is what introduces the vital non-linearity that keeps multi-layer neural networks from collapsing into a single layer.

```