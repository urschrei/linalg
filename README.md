# This is a repo for messing about with least squares methods in Python #

See here for motivation: http://stats.stackexchange.com/questions/66538/using-pandas-and-statsmodels-for-ordinary-least-squares

## Terminology ##
`A`, `A matrix`, `X`: the design matrix, referred to as *exogenous* in statsmodels. The explanatory variable, or *regressors*.  
`b`, `b vector`, `Y`: the outcome vector, referred to as *endogenous* in statsmodels. The response variable, or *regressand*.  

See the [docs](http://statsmodels.sourceforge.net/devel/endog_exog.html) for a complete explanation.
It should also be noted that the signatures of the [numpy.linalg.lstsq](http://docs.scipy.org/doc/numpy/reference/generated/numpy.linalg.lstsq.html) and [statsmodels.WLS](http://statsmodels.sourceforge.net/devel/generated/statsmodels.regression.linear_model.WLS.html#statsmodels.regression.linear_model.WLS) methods are reversed: numpy expects the design matrix followed by the outcome vector, while statsmodels expects the outcome vector followed by the design matrix.

The similarity transform is given by the following two equations:

![similarity](http://latex.codecogs.com/png.latex?f_i%28a%2C%20b%2C%20%5CDelta%7Bx%7D%29%20%3D%20ax_i-by_i&plus;%5CDelta%7Bx%7D%5C%5C%20f_i%28a%2C%20b%2C%20%5CDelta%7By%7D%29%20%3D%20bx_i&plus;ay_i&plus;%5CDelta%7By%7D "Similarity Transform")

The affine transform is given by the following two equations:

![affine](http://latex.codecogs.com/png.latex?f_i%28a_0%2Ca_1%2Ca_2%29%20%3D%20a_0&plus;a_1x_i&plus;a_2y_i%5C%5C%20f_i%28b_0%2Cb_1%2Cb_2%29%20%3D%20b_0&plus;b_1x_i&plus;b_2y_i "Affine Transform")

Data is contained in pickled pandas objects in the data directory.

[coordinates.pickle](data/coordinates.pickle) contains observed coordinates. This DataFrame is updated with affine and similarity residuals, and new `x` and `y` values for each. These are then plotted:

![results](results.png "This graph just screams 'sleep deprived!', doesn't it?")

It's apparent from the scatter plot that the affine transformation is the more accurate of the two, however we can compare the quality of the two transformations by obtaining the sigma zero value, which is the standard error of the *weighted residual variance* for each transform, and can be calculated by taking the square root of the `mse_resid` or `scale` attribute of the result object:  
**Standard error of the affine transform**: 0.0048  
**Standard error of the similarity transform**: 0.0254

You can see the IPython notebook used for all calculations [here](http://nbviewer.ipython.org/urls/raw.github.com/urschrei/linalg/master/statsmodels.ipynb).
