- pytorch: an open-source machine learning library based on the Torch library.
    - known for its:
        - python-first approach
        - dynamic computation graphs
        - strong GPU acceleration
        - extensive ecosystem

- tensor: the fundamental data structure in PyTorch
    - essentially, a multi-dimentional array.
    - can represent:
        - a scalar (0-dimensional tensor)
        - a vector (1-dimensional tensor)
        - a matrix (2-dimentional tensor)
        - higher-dimensional arrays (3D, 4D, etc.)

- why tensors?
    - numerical computation: efficient for mathematical operations
    - GPU acceleration: pytorch tensors can be easily moved to a gpu for massive parallel computation, which is critical for deep learning.
    - automatic differentiation: tensors are the foundation for PyTorch's autograd system, which automatically calculates gradients (derivaties) - essential for training neural networks via backpropagation

creating and manipulating tensors
- creating tensors
    - from python lists or numpy arrays: torch.tensor()
    - tensors of specific shapes with default values: torch.zeros(), torch.ones(), torch.rand(), torch.randn()
    - torch.arange(), torch.linspace()
- tensor attributes
    - tensor.shape or tensor.size(): the dimensions of the tensor.
    - tensor.dtype: the data type of the elements
    - tensor.device: the device where the tensor is stored
- tensor operations:
    - arithmetic: element-wise add, sub, multi, div
    - matrix operations: matrix multi (@ operator or torch.matmul())
    - indexing and slicing: similar to numpy arrays
    - reshaping: tensor.view(), tensor.reshape()
    - concatenation/stacking: torch.cat(), torch.stack()
    - many other mathematical functions available in the torch module.

torch.autograd 
- automatic differentiation: the engine behind training neural networks in pytorch
- when you create a tesnor with requires_grad=True, pytorch tracks all operatiosn performed on it.
- when you have a scalar output and call .backward() on it, pytorch automatically computes the gradients of that output with respect to all tensors that had requries_grad=True and contributed to it.
- these gradients are stored in .grad attribute of the respective tensors.

mini project:
1. activate your machine learning virtual env
2. install pytorch
3. create a python script
4. run the script
5. observe the output
