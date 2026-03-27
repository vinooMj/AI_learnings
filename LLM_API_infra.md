
​LLM API Infrastructure: The Journey of a Prompt (~400ms)
​1. Entry & Security (API Gateway)
​Process: TLS Termination → Authentication (API Key) → Rate Limiting.
​Key Details: This is where 429 Too Many Requests errors occur based on TPM (Tokens Per Minute) and RPM (Requests Per Minute) limits.
​Latency: ~5ms
​2. Traffic Management (Load Balancer)
​Process: Routing the request to specific GPU Clusters (A, B, or C).
​Algorithms: Geographic routing, Least-connections, and continuous health checks.
​Latency: ~2ms (This step is why latency varies between identical calls).
​3. Preparation (Tokenization)
​Process: Raw Text → Tokenizer → Token IDs.
​Technical Note: Uses BPE, SentencePiece, or WordPiece. Each token is roughly 4 characters.
​Business Logic: Token Count = Your Cost.
​Latency: ~3ms
​4. Optimization (Model Router)
​Function: The "Hidden Layer" that directs traffic based on request type:
​Large Model: Sent to multi-GPU Heavy Inference Clusters.
​Small Model: Sent to single-GPU Optimized Clusters.
​Embedding: Sent to dedicated embedding clusters.
​5. The Core: Inference Engine
​This is "where the magic happens," divided into two distinct execution phases:
​A. Prefill Phase
​Processes all input tokens in parallel to generate the KV (Key-Value) Cache.
​Impact: Long prompts result in higher TTFT (Time to First Token).
​B. Decode Phase (Autoregressive)
​Generates the response one token at a time.
​The Loop: KV Cache + Previous Token → Attention Layer → FFN → Softmax → Sample Next Token.
​Streaming: This loop is the reason streaming exists; each token is sent as it is generated.
​C. Technical Specs & Hardware
​Attention Detail: Uses Query/Key/Value vectors. Modern models use GQA/MQA and Flash Attention for memory efficiency.
​Hardware Layer: Powered by A100/H100/H200 clusters. Models are often split across GPUs using Tensor Parallelism.
​Latency: ~300-800ms (Total inference time).
​6. Cleanup (Post-Processing)
​Process: Generated Tokens → Detokenization → Safety Classifier (Content Moderation) → Format Response (JSON).
​Latency: ~5ms
​7. Final Delivery (Response & Billing)
​Billing Logic: Total Cost = (Input Tokens × Rate) + (Output Tokens × Rate).
​Note: Output tokens are usually 3x–5x more expensive than input tokens.
​Logging: Latency, token counts, and safety flags are sent to observability dashboards.
​
