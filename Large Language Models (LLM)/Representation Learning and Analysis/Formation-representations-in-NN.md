# Formation of Representations in Neural Networks

- **Authors**: Liu Ziyin, Isaac Chuang, Tomer Galanti, Tomaso Poggio
- **Year / Venue**: 2025, ICLR
- **Tags**: representation learning, interpretability, alignment, neural geometry, CRH, PAH
- **Status**: Read

## 1. One-line Summary
- Proposes that neural representations emerge through alignment between representation, gradient, and weight geometries, leading to compact task-relevant representations.

## 2. Research Question
- How do structured and compact representations emerge during neural network training?
- Is there a general relationship between hidden representations, gradients, and learned weights?

## 3. Core Idea
- Describe representations, gradients, and weights through their geometric structure.
- **Canonical Representation Hypothesis (CRH)**: these geometries approximately align during training.
- Alignment causes the network to focus on task-relevant directions and suppress irrelevant ones.
- When exact proportional alignment breaks, the geometries may instead follow power-law relationships (**Polynomial Alignment Hypothesis, PAH**).
- The paper connects this alignment to the balance between gradient noise and regularization.

## 4. Method
- For a hidden representation \(h\), define representation geometry using its second moment:

\[
H = \mathbb{E}[hh^T]
\]

- For neuron gradients \(g\):

\[
G = \mathbb{E}[gg^T]
\]

- For a layer with weight matrix \(W\), analyze weight geometry through:

\[
W^TW \quad \text{and} \quad WW^T
\]

- **CRH** predicts approximate proportional alignment:

\[
H \propto G \propto Z
\]

- The paper considers both the input and output sides of a layer, producing six alignment relations between:
  - Representation ↔ Gradient
  - Representation ↔ Weight
  - Gradient ↔ Weight
- **PAH** generalizes exact alignment into power-law relationships between their eigenspectra.

## 5. Key Results
- Representation, gradient, and weight geometries become increasingly aligned during training.
- Stronger alignment is associated with more compact / lower-rank representations.
- Exact proportionality is an idealized regime; real networks can show systematic deviations from it.
- These deviations often follow reciprocal power-law relationships described by PAH.
- Alignment strength varies across layers and training conditions rather than being universally exact.
- The framework connects previously observed phenomena such as Neural Collapse and the Neural Feature Ansatz.

## 6. My Interpretation
- Training gradually makes three things agree:
  - **what the representation encodes**
  - **what the loss is sensitive to**
  - **what the weights emphasize**
- Task-irrelevant directions become less important, producing a more compact representation.
- CRH should not be interpreted as saying \(H\), \(G\), and \(W\) are exactly proportional in every real network.
- Instead, it describes an approximate canonical geometry that networks may move toward during training.
- The deviation from perfect alignment may itself contain useful information about different representational regimes.

## 7. Limitations / Open Questions
- How universal is CRH across modern large-scale architectures?
- Why do some layers align much more strongly than others?
- What determines the power-law exponent when CRH breaks?
- Does geometric alignment necessarily imply better or more interpretable representations?
- What semantic information corresponds to the dominant aligned directions?
- Can the same framework explain representation formation in LLMs and multi-agent systems?

## 8. Connection to My Research
- Provides a possible explanation for **why structured / compressed representations emerge**, complementing work that only measures compression.
- Instead of analyzing hidden states alone, representation interpretability could jointly examine:
  - hidden-state geometry,
  - gradient geometry,
  - and weight geometry.
- Similar alignment ideas could potentially be applied to agent communication or shared states.
- Possible question: do communicating agents gradually develop aligned representational subspaces?
- Possible question: can changes in alignment reveal when agents begin encoding the same concepts?

## 9. Reproduction Notes
- [ ] Load a small pretrained model
- [ ] Extract hidden representations from several layers
- [ ] Compute \(H = \mathbb{E}[hh^T]\)
- [ ] Extract gradients and compute \(G = \mathbb{E}[gg^T]\)
- [ ] Compute weight Gram matrices \(W^TW\) / \(WW^T\)
- [ ] Compare eigenspaces and eigenvalue spectra
- [ ] Measure alignment across layers
- [ ] Compare checkpoints during training
- [ ] Test whether deviations follow a power law