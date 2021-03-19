# Example 1


```python
import numpy as np
from math import *
import matplotlib.pyplot as plt
```

$$f(x) = \sin(kx)$$ 
where $$k = \frac{2\pi}{\lambda}$$


```python
# Initial Parameters
xmax = 10.0
nx = 200
dx = xmax/(nx-1)
x = np.linspace(0,xmax,nx)

# Initialising the sine function
l = 20*dx
k = 2*pi/l
f = np.sin(k*x)

```


```python
plt.plot(x,f)
plt.title('sin function')
plt.xlabel('x,m')
plt.ylabel('amplitude')
plt.xlim(0,xmax)
plt.grid()
plt.show()
```


    
![png](output_4_0.png)
    


The analytical derivative of $$f(x)$$ is
$$f'(x) = k\cos(kx)$$

The central finite difference derivative will be 
$$f'(x) = \frac{f(x+dx-f(x-dx)}{2dx}$$


```python
# The derivative
nder=np.zeros(nx)
ader = np.zeros(nx)

# numerical derivative
for i in range(1,nx-1):
    nder[i]=(f[i+1]-f[i-1])/(2*dx)
    
# analytical derivative
ader = k*np.cos(k*x)

#excluding boundaries
ader[0]=0
ader[nx-1]=0

# Error (rms)
rms = np.sqrt(np.mean(nder-ader)**2)

# Plots
plt.plot(x,nder,label="Numerical Derivative, 2 points", marker="*",color="blue")
plt.plot(x,ader,label="Analytical Derivative", marker="_",color="black")
plt.plot(x,nder-ader,label="Difference",lw=4,ls=":")
plt.title("First Derivative, Err (rms) = %.6f "%(rms))
plt.xlabel('x,m')
plt.ylabel('Amplitude')
plt.legend(loc='upper left')
plt.grid()
plt.show()
```


    
![png](output_6_0.png)
    



```python
plt.plot(x,nder,label="Numerical Derivative, 2 points", marker="*",color="blue")
plt.title("First Derivative, Err (rms) = %.6f , $n_\lambda$ = %.2f"%(rms, l/dx))
plt.xlabel('x,m')
plt.ylabel('Amplitude')
plt.xlim((xmax/2-1, xmax/2+1))
plt.legend(loc='upper right')
plt.grid()
plt.show()
```


    
![png](output_7_0.png)
    



```python
# Init Vectors for looping n

nmin = 3
nmax = 17

# To save the derivatives
nder=np.zeros(n)
ader = np.zeros(n)

# Spatial Domain (1D)
xmax = 10.0

# vector containing each integer between nmin and nmax
na = np.zeros(nmax-nmin+1)

# Vector to save errr values for each corresponding value of n
err = np.zeros(nmax-nmin+1)

# We want to set values of n to each indical location in na. let the array index be j
j = -1 # so that we can set j=j+1 within the loop

#outer loop for values of n in vector na
for n in range(nmin,nmax): #n is the associated integer value 
    j = j+1 # j is the indical position
    na[j] = n # we hereby assign the value n from the loop to the vector element at j in na
    dx = xmax/(n-1)
    x = np.linspace(0,xmax,n)
    l = n*dx
    k = 2*pi/l
    f = np.sin(k*x)
    # analytical derivative
    ader = k*np.cos(k*x)

    #excluding boundaries
    ader[0]=0
    ader[n-1]=0
    
    # numerical derivative
    for i in range(1,n-1):
        nder[i]=(f[i+1]-f[i-1])/(2*dx)
        


    # Error (rms) at x = xmax/2
    i0 = np.int(n/2)
    err[j] = 100*(nder[i0]-ader[i0])**2/ader[i0]**2
    
# print(na)
# print(err)
# print(nder)
# print(ader)

plt.plot(na,err)
plt.xlabel("n")
plt.ylabel("RMS Error %")
plt.title("Error as a function of $n_\lambda$, the Number of Grid Points per $\lambda$")
plt.ylim((0,40))
plt.grid()
plt.show()
```


    
![png](output_8_0.png)
    



```python

```
