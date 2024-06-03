 **Pearson correlation coefficient** (**PCC**)(https://en.wikipedia.org/wiki/Pearson_correlation_coefficient) is a [correlation coefficient](https://en.wikipedia.org/wiki/Correlation_coefficient "Correlation coefficient") that measures [linear](https://en.wikipedia.org/wiki/Linear "Linear") correlation between two sets of data.
 $$
 \rho_{X,Y} = \frac{\mathrm{cov}(X, Y)}{\sigma_X \sigma_Y} = \frac{\mathbb{E}[XY] - \mathbb{E}[X]\mathbb{E}[Y]}{\sqrt{\mathbb{E}[X^2] - (\mathbb{E}[X])^2}\sqrt{\mathbb{E}[Y^2] - (\mathbb{E}[Y])^2}}
$$
## sample Pearson correlation coefficient
$$
r_{x,y} = \frac{\sum_{i = 1}^n (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i = 1}^n (x_i - \bar{x})^2}\sqrt{\sum_{i = 1}^n (y_i - \bar{y})^2}} = \frac{1}{n - 1}\sum_{i = i}^n \left(\frac{x_i - \bar{x}}{s_x}\right)\left(\frac{y_i - \bar{y}}{s_y}\right)
$$
where $s_x = \sqrt{\frac{1}{n}\sum_{i = 1}^n (x_i - \bar{x})^2}$
$$
\Sigma = \begin{bmatrix}
	\sigma_x^2 
\end{bmatrix}
$$