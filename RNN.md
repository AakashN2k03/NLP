# Recurrent Neural Networks (RNN) 🧠

A comprehensive guide to understanding Recurrent Neural Networks and their applications in sequential data processing.

## 📚 What is an RNN?

A **Recurrent Neural Network (RNN)** is a type of neural network designed to handle sequential data. Unlike traditional neural networks (like feedforward networks), RNNs remember previous inputs through internal memory (called hidden states).

👉 **This makes them powerful for tasks where context matters** — e.g., the meaning of a word in a sentence can depend on the words before it.

## 🏗️ Basic Structure of an RNN

Here's the simple architecture:

```
Input Sequence:     x₁ → x₂ → x₃ → ... → xₙ
                    ↓    ↓    ↓         ↓
Hidden States:      h₁ → h₂ → h₃ → ... → hₙ
                    ↓    ↓    ↓         ↓
Outputs:            y₁   y₂   y₃        yₙ
```

### Step-by-Step Computation

- **Input xₜ**: A word (vectorized) or a value from the sequence
- **Hidden State hₜ**: Acts as memory. It's influenced by the current input and the previous hidden state
- **Output yₜ**: Often used for prediction or further processing

## 🔂 Why is RNN Good for Sequences?

RNNs excel at sequential data because they:

- ✅ Take previous context into account
- ✅ Share weights across time steps (parameter-efficient)
- ✅ Support variable-length input sequences

## 🚀 Applications

| Domain | Task |
|--------|------|
| **NLP** | Text generation, sentiment analysis, machine translation |
| **Time-series** | Stock price prediction, weather forecasting |
| **Speech** | Voice recognition, speech synthesis |
| **Healthcare** | Patient condition prediction |

## 🧨 Problems in Vanilla RNN

Despite their usefulness, vanilla RNNs face several challenges:

1. **Vanishing Gradients**: Gradients shrink over time → hard to learn long-term dependencies
2. **Exploding Gradients**: Gradients grow exponentially → unstable learning
3. **Short-term Memory**: Works well with short sequences but fails for long ones

### 🔧 Solution
Use **LSTM** (Long Short-Term Memory) or **GRU** (Gated Recurrent Unit) → advanced RNN variants that can retain long-term memory better.

## 🔍 Example

Let's walk through a simple example with the sentence: **"I love India"**

```
Input sequence: x₁ = "I", x₂ = "love", x₃ = "India"

Initialize: h₀ = 0

Step 1: h₁ = f(Wₓ * "I" + Wₕ * h₀)
Step 2: h₂ = f(Wₓ * "love" + Wₕ * h₁)
Step 3: h₃ = f(Wₓ * "India" + Wₕ * h₂)
```

Where:
- `Wₓ` = weight matrix for input
- `Wₕ` = weight matrix for hidden state
- `f` = activation function (typically tanh or ReLU)

The output could be a next word prediction or sentiment score.

