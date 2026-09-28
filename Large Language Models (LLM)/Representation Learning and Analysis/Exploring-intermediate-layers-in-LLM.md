# Does Representation Matter? Exploring Intermediate Layers in Large Language Models

- **Authors**: Oscar Skean, Md Rifat Arefin, Yann LeCun, Ravid Shwartz-Ziv
- **Year / Venue**: 2024, NeurIPS Workshop on Machine Learning and Compression
- **Tags**: representation learning, interpretability, intermediate layers, Transformer, SSM, Mamba, entropy
- **Status**: Read

## 1. One-line Summary
- Intermediate layers often provide better representations than final layers, and Transformers and SSMs show substantially different layer-wise representation dynamics.

## 2. Research Question
- What makes an intermediate LLM representation "good"?
- How does representation quality change across layers, architectures, training stages, and different input conditions?

## 3. Core Idea
- Evaluate hidden representations layer-by-layer instead of focusing only on the final layer.
- Use downstream tasks together with unsupervised representation metrics.
- Compare Transformer models with Mamba / SSM architectures.
- Study how representation structure emerges during training and reacts to unusual inputs.

## 4. Method
- **Models**: Pythia, Llama3, LLM2Vec, Mamba, Mamba2.
- **Downstream evaluation**:
  - MTEB for embedding quality.
  - MMLU for entropy–performance analysis.
- **Datasets**: WikiText-103 and AI-Medical-Chatbot.
- **Metrics**:
  - **Prompt Entropy**: diversity / effective dimensionality of token representations.
  - **Curvature**: change in direction between consecutive token representations.
  - **InfoNCE**: similarity of paired augmentations relative to negatives.
  - **DiME**: dependence of correct augmentation pairs relative to random pairings.
  - **LiDAR**: clustering structure of multiple augmentations of the same prompt.
- For augmentation metrics, token embeddings are mean-pooled into one representation per prompt.

## 5. Key Results
- Intermediate layers outperform the final layer on MTEB across Pythia, Mamba, and LLM2Vec.
- Transformer models show much stronger changes in representation metrics across depth than Mamba.
- Pythia shows a pronounced entropy drop in intermediate layers, while Mamba remains relatively stable.
- In Llama3, lower intermediate-layer entropy is associated with better MMLU performance; this relationship is much weaker or absent in Mamba2.
- During Pythia training, the largest representational changes occur in intermediate layers, while early layers remain comparatively stable.
- Repeated inputs reduce intermediate-layer entropy, while random inputs increase entropy most strongly in early layers.
- Longer random prompts increase entropy, but normalized entropy grows sublinearly.
- Transformer models exhibit a bimodal entropy distribution in some intermediate layers; the paper does not identify its cause.

## 6. My Interpretation
- Intermediate layers appear to be the main region where Transformers reorganize and compress information.
- Early layers may mainly transform raw token inputs into an initial representation space, while deeper intermediate layers perform more substantial abstraction.
- Mamba processes representations more uniformly across depth, suggesting a different strategy for preserving and transforming information.
- The fact that intermediate layers also perform better on downstream embedding tasks suggests that final-layer representations are not necessarily the most generally useful.
- Compression alone should not be interpreted as "better"; its meaning depends on downstream performance and other representation metrics.

## 7. Limitations / Open Questions
- What information is actually removed during Transformer compression?
- Why do intermediate layers produce better downstream representations?
- Why is Mamba much more stable across layers?
- What causes the bimodal entropy distribution in Transformer intermediate layers?
- Are the proposed metrics measuring true semantic quality or only geometric properties correlated with it?
- Why do different invariance metrics sometimes move in different directions during training?

## 8. Connection to My Research
- Provides a framework for studying internal representations without requiring supervised probes.
- Similar metrics could be applied to agent hidden states, communication messages, or shared state representations.
- A useful extension would be to study whether information compression occurs during multi-agent communication.
- Another question is whether interacting agents develop increasingly aligned or invariant representations over multiple communication rounds.

## 9. Reproduction Notes
- [ ] Load Pythia and Mamba from Hugging Face
- [ ] Extract hidden states from every layer
- [ ] Implement matrix-based prompt entropy
- [ ] Plot entropy across model depth
- [ ] Compare Transformer vs. Mamba
- [ ] Compare normal, repetitive, and random prompts
- [ ] Test different prompt lengths
- [ ] Reproduce one augmentation-invariance metric