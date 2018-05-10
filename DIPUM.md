#Chap.2 Fundamentals

$\quad\quad$Color images are formed by a combination of individual images. For example, in the RGB color system a color image consists of three individual monochrome images, referred to as the red (R), green ( G), and blue (B) primary (or component) images.

```matlab
imshow()
imtool()
imwrite()
imfinfo()
```

resolution in dpi(dot per inch)
print()

2.6 Image Types
	Gray-scale images
	Binary Images: A binary image is a logical array of Os and ls.
	

```
im2utin8
im2uint16
im2double
im2single
/mat2gray
im2bw
tofloat
```



	ndims()
	sparse()
	full()
	true()/false()
	
	ans, eps, i/j, NaN/nan, pi, realmax, realmin, computer, version, ver
	
	A function handle is a MATLAB data type that contains information used in referencing a function. 
	anonymousfunction handle, which is formed from a MATLAB expression instead of a function name. @ ( input - a rgument - list ) expression

##2.10 Code Optimization

1. Preallocation refers to initializing arrays before entering a for loop that computes the elements of the array. 
If you type tic; statements; toc in separate lines, the time measured will include the time required for you to type the second two lines.)
Function timeit can be used to obtain reliable, repeatable time measurements of function calls.
	
2. Vectorization in MATLAB refers to techniques for eliminating loops altogether, using a combination of matrix/vector operators, indexing techniques, and existing MATLAB or toolbox functions.
In older versions of MATLAB, eliminating loops by using matrix and vector operators almost always resulted in significant increases in speed. However,  recent versions of MATLAB can compile simple for loops automatically, suchas the one in s infun2, to fast machine code. As a result, many for loops that were slow in older versions of MATLAB are no longer slower than the vectorized versions. 
	
MATLAB Profiler
	
disp/input/strread

# Chap.3 Intensity Transformations and Spatial Filtering

## Intensity Transformation Functions

```matlab
g=imadjust(f ,[low_in high_in],[low_out high_out], gamma)
%  this function maps the intensity values in image f to new values in g, such that values between low_in and high_in map to values between low_out and high_out. Values below low_in and above high_in are clipped; that is, values below low_in map to low_out, and those above high_in map to high_out. 
g1 = imadjust(f,[0 1],[1 0]); % negative

Low_High = stretchlim(f)
% Sometimes, it is of interest to be able to use function imadjust "automatically," without having to be concerned about the low and high parameters discussed above. Function st retchlim is useful in that regard; its basic syntax is
```

__Concepts__

\indEach MATLAB figure window has a colormap associated with it. A colormap is simply a three-column matrix whose length is equal to the number of colors it defines. Each row of the matrix defines a particular color by specifying three values in the range zero to one. These values define the RGB components

% Input Parsing
`narginchk()` %  throws an error if the number of inputs specified in the call to the currently executing function is less than minargs or greater than maxargs. If the number of inputs is between minargs and maxargs (inclusive), narginchk does nothing.

 The `varargin` argument is a cell array that contains the function inputs, where each input is in its own cell.

 `validateattributes(A,classes,attributes)` validates that array A belongs to at least one of the specified classes (or its subclass) and has all of the specified attributes. If A does not meet the criteria, MATLAB® throws an error and displays a formatted error message. Otherwise, `validateattributes` completes without displaying any output.

`n = numel(A)` returns the number of elements, `n`, in array `A`, equivalent to `prod(size(A))`.

`tf = isa(obj,*ClassName*)` returns `true` if `obj` is an instance of the class specified by *ClassName*, and `false` otherwise. `isa` also returns true if `obj` is an instance of a class that is derived from *ClassName*.

`B = cumsum(A)` returns the cumulative sum of `A` starting at the beginning of the first array dimension in `A` whose size does not equal 1

1. Construct an input parser for variable arguments.

# Chap.8 Wavelets

Condiser an image $f(x,y)$ of size $M\times N$ and a pair of transforms: 
$$
T(u,v,\dots)=\sum_{x,y}f(x,y)g(u,v,\dots)\\
f(x,y)=\sum_{u,v,\dots}T(u,v,\dots)h_{u,v,\dots}(x,y)
$$
where $g(u,v,\dots)$ and $h_{u,v,\dots}(x,y)$ are called _forward_ and _inverse transformation kernel_. For DFT, the kernels are separable, since
$$
h_(u,v)(x,y)=g^*_{u,v}(x,y)=\dfrac{1}{\sqrt{MN}}e^{j2\pi(ux/M+vy/N)}=\dfrac{1}{\sqrt{M}}e^{j2\pi ux/M} \cdot \dfrac{1}{\sqrt{N}}e^{j2\pi ux/N}=h_u(x)h_v(y)
$$
Properties of wavelet kernels  

1.  Separability, saclability and translatability  
2. Multiresolution compatibility, satisfying the criteria of multiresolution
3. Orthogonality

## FWTs Using the Wavelet Toolbox

[Daubechies wavelet](https://en.wikipedia.org/wiki/Daubechies_wavelet)

`wfilters` receives the name of a wavelet function and returns its filters related

`waveinfo` prints a written description of wavelet family on MATLAB's Command Window.

`wavefun` receives the name of a wavelet function and the number of iterations and gives a digital approximation of an orthonormal transform's scaling and wavelet functions



`wavedec2` receives a 2-D image and computes its wavelet transform

```matlab
f=magic(4)
[c1,s1]=wavedec2(f,2,'haar')
```

