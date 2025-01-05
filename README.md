# Mini Torch Implementation

This repository contains a lightweight implementation of key functionalities found in PyTorch, designed to help developers understand the underlying principles of deep learning frameworks. The project focuses on recreating core features like tensor operations, automatic differentiation, and basic neural network modules.

---

## Features

- **Tensor Operations**: Efficient handling of multi-dimensional arrays with broadcasting support.
- **Automatic Differentiation**: Gradient computation for backpropagation using a computation graph.
- **Neural Network Layers**: Basic modules like Linear, ReLU, and Loss functions.
- **Optimization**: Simple gradient-based optimizers such as SGD.
- **Extensibility**: Easy-to-read code for educational purposes and custom extensions.

---

## Installation

Clone this repository to your local machine:

```bash
git clone https://github.com/your-username/mini-torch.git
cd mini-torch
```

### Dependencies

Ensure you have Python 3.7+ installed. Install required libraries:

```bash
pip install numpy
```

---

## Usage

### Creating and Operating on Tensors

```python
from minitorch.tensor import Tensor

# Create a tensor
x = Tensor([[1, 2], [3, 4]], requires_grad=True)
y = Tensor([[2, 0], [1, 3]])

# Perform operations
z = x + y
print(z.data)  # Output: [[3 2] [4 7]]

# Backpropagation
z.sum().backward()
print(x.grad)  # Output: Gradient w.r.t x
```

### Building a Neural Network

```python
from minitorch.nn import Linear, ReLU
from minitorch.optim import SGD

# Define a simple model
class SimpleNN:
    def __init__(self):
        self.fc1 = Linear(2, 4)
        self.relu = ReLU()
        self.fc2 = Linear(4, 1)

    def forward(self, x):
        x = self.fc1(x)
        x = self.relu(x)
        x = self.fc2(x)
        return x

# Instantiate the model
model = SimpleNN()

# Define an optimizer
optimizer = SGD([model.fc1.weights, model.fc1.bias, model.fc2.weights, model.fc2.bias], lr=0.01)

# Example training loop
for epoch in range(100):
    optimizer.zero_grad()
    x = Tensor([[1.0, 2.0], [3.0, 4.0]])  # Input data
    y = Tensor([[1.0], [0.0]])            # Target
    y_pred = model.forward(x)
    loss = ((y_pred - y)**2).mean()
    loss.backward()
    optimizer.step()
    print(f"Epoch {epoch}, Loss: {loss.data}")
```

---

## Project Structure

```plaintext
mini-torch/
│
├── minitorch/
│   ├── tensor.py        # Tensor implementation with automatic differentiation
│   ├── nn.py            # Neural network layers and activation functions
│   ├── optim.py         # Gradient-based optimizers
│   └── utils.py         # Utility functions
│
├── tests/               # Unit tests for core functionality
├── examples/            # Example scripts for common use cases
└── README.md            # Project documentation
```

---

## Contributing

We welcome contributions! If you have ideas for features or improvements, feel free to:

1. Fork this repository.
2. Create a new branch:
   ```bash
   git checkout -b feature-name
   ```
3. Commit your changes:
   ```bash
   git commit -m "Add feature description"
   ```
4. Push to your branch:
   ```bash
   git push origin feature-name
   ```
5. Open a pull request.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

This project was inspired by the simplicity and modularity of PyTorch. It is intended for educational purposes and as a starting point for building custom frameworks.

---
