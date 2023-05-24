# Simple Fourier Filter
## Simple FFT based library for noise reduction
All methods are based on my [Bachelor's thesis](https://urn.fi/URN:NBN:fi-fe2022050332349) where I go into more detail.
### Installing

```
pip install simplefourierfilter
```

### So easy to use :)
```python
from simplefourierfilter import fourierFilter
import numpy as np

# Data generation
N = 100
e = np.random.normal(size=N)
t = np.linspace(0,1,N)
f = 2*np.sin(10*t)
X = f+e

# Simple filter
X_f = fourierFilter(X)
```
![image](https://github.com/PauliAnt/SimpleFourierFilter/assets/63787410/06b6d8d5-c9ec-4ff2-bab2-e3d4ab1c0d3c)

## Documentation :D
```python
fourierFilter(X,ratio,method,nopadding,zeropadding,plotting)
````

### Parameters
`X` : numpy array  
Time sequence with equal spacing

### Optional parameters
`ratio`: float (default 0.2)  
Number between 0 and 1 defining how much stuff needs to go.  
  
`method`: string (default "threshold")  
Defining method used for noise reduction.  
"threshold" uses amplitude thresholding.  
"lowpass" uses simple low pass filter.  
"dist" uses Cauchy distribution scaling method.    
  
`nopadding`: boolean (default False)  
Function uses padding by default. Disable if preferrable.  

`zeropadding`: boolean (default False)  
Function uses first and last value with padding. Use zero padding if preferrable.  

`plotting`: string (default "data")  
Plotting mode. "data" plots original and filtered data. "frequency" plots normalised frequency spectrum and filtering conditions. "both" plots both in the same subplot. "none" disables plotting  
  
## Advanced examples
### Trigonometric function with no padding
```python
from simplefourierfilter import fourierFilter
import numpy as np

# Data generation
N = 100
e = np.random.normal(size=N)
t = np.linspace(0,2*np.pi,N)
f = np.sin(2*t)
X = f+e

# Simple filter
X_f = fourierFilter(X,ratio=0.4,method="threshold",plotting="both",nopadding=True)
```
![image](https://github.com/PauliAnt/SimpleFourierFilter/assets/63787410/1104150f-5aa5-4248-a504-606de7fbd7ad)

### Smooth function featuring default padding and Cauchy distribution scaling
```python
from simplefourierfilter import fourierFilter
import numpy as np 
# Data generation
N = 100
e = 0.1*np.random.normal(size=N)
t = np.linspace(0,3,N)
f = -0.5*np.power(t-2,2)+2.5*np.power(t+1,-2)
X = f+e

# Simple filter
X_f = fourierFilter(X,ratio=0.05,method="dist",plotting="both")
```
![image](https://github.com/PauliAnt/SimpleFourierFilter/assets/63787410/9991f4d3-8281-4ab5-a7c0-6faa41092353)

