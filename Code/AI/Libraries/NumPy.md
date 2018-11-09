# NumPy

> [Wiki](https://github.com/pytorch/pytorch)
> NumPy is a library for the Python programming language, adding support for large, multi-dimensional arrays and matrices, along with a large collection of high-level mathematical functions to operate on these arrays.

## Official

- [Web](http://www.numpy.org/)

## Tutorials
- [Quickstart tutorial](https://www.numpy.org/devdocs/user/quickstart.html)


***
## Notes 

### Concepts

- axis - the innermost is the last axis
- ndarray - a multidimensional array
    - ndarray.ndim
    - ndarray.shape
    - ndarray.size
    - ndarray.dtype
    - ndarray.itemsize
    - ndarray.data
    - [link](https://www.numpy.org/devdocs/user/quickstart.html)
  
### Tips

- array creation
    ```python
    a = np.array([1,2,3,4])
    a = np.array([(1.5,2,3),(4,5,6)])
    # initial placeholder content
    np.zeros((3,4))
    np.ones((2,2),dtype=np.int16)
    np.empty((3,3))
    np.random.random((3,3))
    # create sequences
    np.arange(10,30,5)  # start end step
    np.linspace(0,2,9) # start end total
    # reshap
    np.arange(15).
    ```
- Indexing, Slicing and Iterating
    - dots (...) represent as many colons
        - `x[1,2,...]` is equivalent to `x[1,2,:,:,:]`,
- Shape Manipulation
    -  `a.ravel()  # returns the array, flattened`
    -  `a.reshape(3,5) # returns the array with a modified shape`
    -  `a.resize(3,5) # modifies the array itself`
    -  `a.T # returns the array, transposed`
    -  `a.reshape(3,-1)` - the other dimensions are automatically calculated