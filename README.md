![results](WLS.png "This graph just screams 'sleep deprived!', doesn't it?")

# This is a repo for messing about with least squares methods in Python #

## Terminology ##
`A`, `A matrix`, `X`: the design matrix, referred to as *exogenous* in statsmodels. The explanatory variable, or *regressors*.  
`b`, `b vector`, `Y`: the outcome vector, referred to as *endogenous* in statsmodels. The response variable, or *regressand*.  

See the [docs](http://statsmodels.sourceforge.net/devel/endog_exog.html) for a complete explanation.
It should also be noted that the signatures of the [numpy.linalg.lstsq](http://docs.scipy.org/doc/numpy/reference/generated/numpy.linalg.lstsq.html) and [statsmodels.WLS](http://statsmodels.sourceforge.net/devel/generated/statsmodels.regression.linear_model.WLS.html#statsmodels.regression.linear_model.WLS) methods are reversed: numpy expects the design matrix followed by the outcome vector, while statsmodels expects the outcome vector followed by the design matrix.

Equations and matrix shapes for data used in a **weighted least squares** operation, which compares the accuracy of a similarity and affine transform of observed *x* and *y* coordinates are shown at the top of this [IPython notebook](http://nbviewer.ipython.org/urls/raw.github.com/urschrei/linalg/master/notebooks/weighted_least_squares.ipynb).

Data is contained in pickled pandas objects in the data directory.

[coordinates.pickle](data/coordinates.pickle) contains observed coordinates. This DataFrame is updated with affine and similarity residuals, and new *x* and *y* values for each transform.

It's apparent from the scatter plot that the affine transformation is the more accurate of the two, however we can compare the quality of the two transformations by obtaining the sigma zero value, which is the standard error of the *weighted residual variance* for each transform, and can be calculated by taking the square root of the `mse_resid` or `scale` attribute of the result object:  

**Standard error of the affine transform**: 0.0048  
**Standard error of the similarity transform**: 0.0254
