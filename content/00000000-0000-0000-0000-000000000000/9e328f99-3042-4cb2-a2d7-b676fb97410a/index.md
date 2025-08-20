---
layout: textbook
title: "Mapping the Mind of LLMs: Interpreting and Manipulating Neural Features - Dissecting transformer blocks: embeddings, self-attention, and feed-forward networks"
date: 2025-08-20T16:54:50.231699
study_plan_url: "https://lumorikllc.github.io/learn/content/00000000-0000-0000-0000-000000000000/eb870ab4-00f8-4ac2-afdd-eaf709166c03/"
chapters: 9
author: "00000000-0000-0000-0000-000000000000"
description: "AI-generated textbook by Lumorik"
---

## Chapter: Dissecting Transformer Blocks: Embeddings, Self‐Attention, and Feed‐Forward Networks

---

## 1. Chapter Overview  
**Hook:**  
Transformer blocks lie at the heart of every large language model, enabling them to process tokens in parallel while capturing long‐range dependencies. Understanding embeddings, attention, and feed‐forward layers is key to interpreting how these models represent and transform language.

**Learning Goals:**  
By the end of this chapter, learners should be able to:  
- Describe the roles of token and positional embeddings in representing input sequences.  
- Derive and compute the scaled dot‐product attention mechanism, including Query, Key, and Value transformations.  
- Explain how feed‐forward networks, residual connections, and layer normalization contribute to stable training and expressive power.

---

## 2. Key Concepts & Definitions  

**Token Embedding**  
A learned vector representation mapping discrete tokens to continuous space.

**Positional Embedding**  
A fixed or learned vector encoding each token’s position in the sequence.

**Query (Q)**  
A linear projection of embeddings used to compute attention scores.

**Key (K)**  
A linear projection serving as the index against which queries attend.

**Value (V)**  
A linear projection whose weighted sum yields the attention output.

**Scaled Dot‐Product Attention**  
An operation computing attention weights as softmax($QK^\top/\sqrt{d_k}$) and applying them to $V$.

**Multi‐Head Attention**  
Parallel attention heads that attend jointly, then concatenate and project results.

**Feed‐Forward Network (FFN)**  
A two‐layer position‐wise MLP applied to each token embedding independently.

**Residual Connection**  
An additive shortcut $x + \mathrm{Sublayer}(x)$ facilitating gradient flow.

**Layer Normalization**  
Normalization that stabilizes activations by scaling each token’s features to zero mean and unit variance.

These concepts interlock within each transformer block: embeddings initialize token representations, self‐attention (via Q, K, V) reweights them, the FFN applies nonlinear transformations, and residual plus normalization layers ensure stable deep stacking.

---

## 3. Main Exposition  

### 3.1 Embeddings: Tokens and Positions  
Every input token $t_i$ (e.g., a word piece) maps to a **token embedding** vector $e_i\in\mathbb{R}^{d_{\text{model}}}$. Because transformers lack recurrence, they require **positional embeddings** $p_i\in\mathbb{R}^{d_{\text{model}}}$ to encode order. The input to layer 1 is  
$$
x_i = e_i + p_i.
$$  
Common choices for $p_i$ include sinusoidal functions or learned parameters.  

### 3.2 Scaled Dot‐Product Attention  
Given input matrix $X\in\mathbb{R}^{n\times d_{\text{model}}}$ for $n$ tokens, we compute:  
$$
Q = XW^Q,\quad K = XW^K,\quad V = XW^V,
$$  
where $W^Q,W^K,W^V\in\mathbb{R}^{d_{\text{model}}\times d_k}$. Attention is  
$$
\mathrm{Attention}(Q,K,V)=\mathrm{softmax}\!\Bigl(\tfrac{QK^\top}{\sqrt{d_k}}\Bigr)V.
$$  
The factor $1/\sqrt{d_k}$ prevents large dot‐products that saturate softmax.  

#### Multi‐Head Extension  
Split $Q,K,V$ into $h$ heads of dimension $d_k=d_{\text{model}}/h$:  
$$
\mathrm{head}_i = \mathrm{Attention}(QW_i^Q,KW_i^K,VW_i^V),\quad
\mathrm{MultiHead}(Q,K,V)=\mathrm{Concat}(\mathrm{head}_1,\dots,\mathrm{head}_h)W^O.
$$  

### 3.3 Feed‐Forward Networks  
After attention, each token embedding $z_i$ passes through a position‐wise FFN:  
$$
\mathrm{FFN}(z_i) = \max(0,\,z_iW_1 + b_1)W_2 + b_2,
$$  
where $W_1\in\mathbb{R}^{d_{\text{model}}\times d_{\text{ff}}}$ and $W_2\in\mathbb{R}^{d_{\text{ff}}\times d_{\text{model}}}$. Many models use GELU instead of ReLU for smoother activations.

### 3.4 Residual Connections & Layer Normalization  
Each sublayer (attention or FFN) is wrapped as  
$$
y = \mathrm{LayerNorm}\bigl(x + \mathrm{Sublayer}(x)\bigr),
$$  
stabilizing gradients and enabling deep stacking. Some variants apply LayerNorm before the sublayer (pre‐norm) for faster convergence.

---

## 4. Applications & Real‐World Context  

**Scenario 1: Machine Translation**  
In translation, self‐attention lets each target token attend to all source tokens via cross‐attention. Positional embeddings ensure words like “not” and “only” maintain correct order, preventing misinterpretation of phrases (“not only…but also”). Multi‐head attention captures syntax in one head (e.g., verb‐object relations) and semantics in another (e.g., pronoun antecedents), yielding more accurate translations across distant dependencies.

**Scenario 2: Text Summarization**  
Summarization demands identifying key phrases in long documents. Self‐attention assigns higher weights to salient sentences (“In conclusion…,” statistics), effectively spotlighting summary‐worthy content. The FFN then refines these representations into concise abstract sentences. Residual connections and normalization guarantee that even after many layers, the model retains core document meaning.

**Scenario 3: Sentiment Analysis**  
To gauge sentiment, attention can focus on opinion words (e.g., “terrible,” “fantastic”). One head may specialize in negation scope (recognizing “not good” flips polarity), while another weights intensifiers (“very,” “extremely”). Positional embeddings help the model understand that “not” preceding “good” reverses sentiment, a task challenging for RNNs over long spans.

---

## 5. Common Misconceptions & Pitfalls  

1. **“Self‐attention is just averaging embeddings.”**  
   Correction: It’s a weighted sum whose weights depend dynamically on $QK^\top$, capturing context‐sensitive interactions.

2. **“More attention heads always yield better results.”**  
   Correction: Beyond a certain point, added heads overlap in function and increase compute without gains.

3. **“Positional embeddings only matter at shallow layers.”**  
   Correction: Positional signals are reused at every layer; removing them collapses sequence structure entirely.

4. **“Feed‐forward layers mix tokens across positions.”**  
   Correction: FFNs apply position‐wise, acting independently on each token’s features.

---

## 6. Worked Example Problem  

**Problem:**  
Consider a 2‐token sequence with embeddings $x_1 = [1,0]$, $x_2 = [0,1]$ in $\mathbb{R}^2$. Let $W^Q=W^K=W^V=I_{2\times2}$ and $d_k=2$. Use single‐head attention, ReLU‐FFN with $d_{\text{ff}}=2$, where $W_1=I$, $b_1=0$, $W_2=I$, $b_2=0$. LayerNorm is identity. Compute:  
1. Attention scores and weights.  
2. Attention output vectors.  
3. FFN outputs after residual connections.  

**Solution:**  
1. *Compute Q, K, V:*  
   Q = K = V = [ [1,0]; [0,1] ].  

2. *Dot‐products:*  
   $QK^\top = \begin{bmatrix}1&0\\0&1\end{bmatrix}$, so each row has one 1 on the diagonal and 0 off‐diagonal.  

3. *Scale & softmax:*  
   Scale by $1/\sqrt{2}\approx0.707$:  
   $$S = \frac{QK^\top}{\sqrt2} = \begin{bmatrix}0.707&0\\0&0.707\end{bmatrix}.$$  
   Softmax row‐wise gives weights $\alpha_{11}=1,\alpha_{12}=0$ and $\alpha_{21}=0,\alpha_{22}=1$.  

4. *Attention outputs:*  
   $O = \alpha V = X$ (unchanged): $o_1=[1,0],\,o_2=[0,1]$.  

5. *Residual + FFN:*  
   Input to FFN is $z_i = x_i + o_i = 2x_i$. ReLU gives $2x_i$. FFN second layer returns $2x_i$. Adding residual: $y_i = 2x_i + o_i = 3x_i$.  

**Commentary:**  
Each step shows how attention preserves or modifies embeddings; residuals amplify signals, while FFN applies nonlinear scaling.

---

## 7. Practice Exercises  

Q1. Define **token embedding** and **positional embedding**, explaining why both are necessary.  
Q2. Why divide $QK^\top$ by $\sqrt{d_k}$ before softmax?  
Q3. In multi‐head attention, what is the purpose of the output projection $W^O$?  
Q4. Describe how the feed‐forward network differs from the attention sublayer.  
Q5. Explain the role of residual connections in preventing vanishing gradients.

---

## 8. Summary & Further Reading  

**Key Takeaways:**  
- Transformers represent tokens via **token** + **positional embeddings** for order information.  
- **Scaled dot‐product attention** computes context‐dependent weights using $Q,K,V$ and softmax.  
- **Multi‐head attention** enables multiple relational patterns in parallel.  
- **Feed‐forward networks** apply position‐wise nonlinear transformations.  
- **Residual connections** and **layer normalization** stabilize deep transformer stacks.

**Annotated Bibliography:**  
- Vaswani et al. (2017), “Attention Is All You Need.” The seminal paper introducing the transformer architecture and self‐attention.  
- Alammar, J. (2018), “The Illustrated Transformer.” A visual guide explaining transformer internals with interactive diagrams.  
- Devlin et al. (2019), “BERT: Pre-training of Deep Bidirectional Transformers.” Demonstrates transformer pre-training on masked language modeling.  
- Dai et al. (2019), “Transformer-XL: Attentive Language Models Beyond a Fixed‐Length Context.” Introduces recurrence in attention for longer contexts.  

---

## 9. Solutions  

**Q1.** Token embeddings map discrete tokens to vectors; positional embeddings encode token order. Both ensure the model knows “what” each token is and “where” it appears.  

**Q2.** Scaling by $\sqrt{d_k}$ prevents large dot‐product magnitudes that push softmax into very small gradients.  

**Q3.** $W^O$ projects the concatenated heads back to $d_{\text{model}}$, enabling integration of multiple attention patterns.  

**Q4.** The FFN applies the same two‐layer MLP independently at each position, whereas attention mixes information across tokens.  

**Q5.** Residual connections add the input back to the sublayer output, maintaining gradient flow and preventing vanishing gradients in deep networks.