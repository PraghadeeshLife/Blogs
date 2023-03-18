Understanding Singular Value Decomposition

Singular Value Decomposition is a mathematical technique that helps us in decomposing a matrix into smaller components and extract important features from it. In simple terms, a matrix is factorized into three matrices
1. U matrix
2. Sigma matrix
3. V matrix
This involves identifying Eigen Vectors and Eigen Values that help identify the important features of the matrix.

Given an m x n matrix A, SVD decomposes it into three matrices: U, Σ, and V.

A = UΣV^T

Where U is an m x m matrix, Σ is an m x n diagonal matrix, and V^T is an n x n matrix.


But Why SVD?
SVD is often used in many applications related to Science, Mathematics and Engineering. Some of them are
1. Dimensionality Reduction - The SVD algorithm is used in reducing the dimensionality of the dataset to a smaller dimension, by extracting the important features corresponding to the important singular values and the singular vectors that holds most of the information.
2. Data compression: SVD can be used to compress data by keeping only the most important singular values and corresponding singular vectors.
These application also find their used cases in Machine Learning

In this blog, let's understand Singular Value Decomposition by compressing an image

SVD for Image Compression
Let's take a look at how we can use SVD for image compression. Suppose we have an image with dimensions m x n. We can represent this image as a matrix A, where each element A_ij represents the intensity of the pixel at position (i, j).

To compress the image, we perform SVD on the matrix A. We then keep only the k most significant singular values and set the rest to zero. This gives us a new matrix Σ' that has the same dimensions as Σ, except that the last (m+n-k) diagonal elements are zero.

The U matrix contains information about the image's horizontal features, while the V matrix contains information about the image's vertical features. The Σ matrix contains information about the strength of these features.

By keeping only the top few values of Σ, we can effectively discard the weaker features of the image while retaining the stronger features. This allows us to compress the image without losing important details.

We can then reconstruct the compressed image by computing the product UΣ'V^T. The resulting image will have a reduced size and retain most of the essential features of the original image.


```
%matplotlib inline
import matplotlib.pyplot as plt
import numpy as np
import time

from PIL import Image, ImageFile
ImageFile.LOAD_TRUNCATED_IMAGES = True


img = Image.open('prag.jpg')
imggray = img.convert('LA')
plt.figure(figsize=(9, 16))
plt.imshow(imggray);
```

![image](https://user-images.githubusercontent.com/102030901/226106100-d2e54a20-a31b-4980-9215-0d22e283a531.png)

```
imgmat = np.array(list(imggray.getdata(band=0)), float)

imgmat.shape = (imggray.size[1], imggray.size[0])
imgmat = np.matrix(imgmat)
U, sigma, V = np.linalg.svd(imgmat)

This performs the Singular Value Decomposition (SVD) on the image matrix using the linalg.svd() function from NumPy's linear algebra module. The result is three matrices: U, which contains the left singular vectors; sigma, which contains the singular values; and V, which contains the right singular vectors.

rank = 25
reconstimg = np.matrix(U[:, :rank]) * np.diag(sigma[:rank]) * np.matrix(V[:rank, :])
plt.figure(figsize=(9,16))
plt.imshow(reconstimg, cmap='gray')

rank = 50
reconstimg = np.matrix(U[:, :rank]) * np.diag(sigma[:rank]) * np.matrix(V[:rank, :])
plt.figure(figsize=(9,16))
plt.imshow(reconstimg, cmap='gray')

rank = 100
reconstimg = np.matrix(U[:, :rank]) * np.diag(sigma[:rank]) * np.matrix(V[:rank, :])
plt.figure(figsize=(9,16))
plt.imshow(reconstimg, cmap='gray')

rank = 200
reconstimg = np.matrix(U[:, :rank]) * np.diag(sigma[:rank]) * np.matrix(V[:rank, :])
plt.figure(figsize=(9,16))
plt.imshow(reconstimg, cmap='gray')
