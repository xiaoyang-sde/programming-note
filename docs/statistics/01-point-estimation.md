# Point Estimation

## Descriptive Statistics

The sample is a collection of results of a certain random experiment that is performed $n$ times, which is denoted as $x_1, x_2, \dots, x_n$. The empirical distribution $f$ is the distribution on $\{ x_1, x_2, \dots, x_n \}$ such that $f(x_i) = \frac{1}{n} \times$ the number of times $x_i$ appeared in the sample.

- The sample mean is $\bar{x} = \frac{1}{n} \sum_{i = 1}^{n} x_i$.
- The variance of the empirical distribution is $v = \frac{1}{n} \sum_{i = 1}^{n} (x_i - \bar{x})^2$.
- The sample variance is $s^2 = \frac{1}{n - 1} \sum_{i = 1}^{n} (x_i - \bar{x})^2$.
- The sample standard deviation is $s = \sqrt{s^2} \ge 0$, which is a measure of how dispersed the data are from the sample mean.

If $X$ is a continuous random variable, each $x_i$ might appear once. In this case, $f(x_i) = \frac{1}{n}$ is a uniform distribution, which doesn't provide a meaningful information on the pdf or distribution of $X$.

The relative frequency histogram could estimate the pmf or pdf of a continuous random variable. Given a set of continuous sample data, the data could be grouped into classes, which could be used to construct a hisstogram of the grouped data. Suppose the data is grouped into $k$ classes, then the class intervals could be denoted as $(c_0, c_1], (c_1, c_2], \dots, (c_{k - 1}, c_k]$.

- The class boundaries are the limits of the class interval.
- The class limits are the smallest and the largest possible observed values in a class.
- The class mark is the midpoint of a class.
- The class mode is the interval with the largest height, and the respective class mark is called the mode.

The empirical rule states that if the histogram of a sample data, with a sample mean of $\bar{x}$ and a sample standard deviation $s$, is bell-shaped, then for large samples, $68\%$ of the data are in the interval $(\bar{x} - s, \bar{x} + s)$, $95\%$ of the data are in the interval $(\bar{x} - 2s, \bar{x} + 2s)$, and $99.7\%$ of the data are in the interval $(\bar{x} - 3s, \bar{x} + 3s)$.

## Data Analysis

Ordered stem-and-leaf display is a data visualization method, which preserves all the exact values of data points. The ordered stem-and-leaf display helps in the data
visualization/indexing in two folds. The stems are in the first column and the leaves are stored in the second column. Stems and leaves are sorted in increasing order, and the number of data point for each stem is recorded.

Let $X$ be a sample that contains $x_1, \dots, x_n$. Consider reordering the samples from the smallest to the largest. Let $y_k$ be the $k$-th order statistic of the sample, which is the $k$-th smallest value.

For $0 < p < 1$, the sample percentiles is the $(n + 1)p$-th order statistic if $(n + 1)p$ is an integer. If $(n + 1)p$ is a proper fraction, then the $(100p)$-th percentile is the weighted average of the $r$-th and $(r + 1)$-th order statistics. $y_r + [(n + 1)p - r](y_{r+1} - y_r)$. The $100p$-th sample percentile has $np$ samples less than it and $n(1-p)$ samples greater than it. The $(100p)$-th percentile is denoted as $\tilde{\pi}_p$.

- The median is the $50$-th percentile.
- The first, second, and third quartiles are the $25$-th, $50$-th, and $75$-th percentiles.
- The deciles of the sample are the $10$-th, $20$-th, ..., and $90$-th percentiles.
- The five-number summary of a data set are the minimum, the first quartile, the median, the third quartile, and the maximum.
- The interquartile range (IQR) is the difference bewteen the third and first quartiles.

## Order Statistics

Order statistics are the observations of the random sample ordered in magnitude from the smallest to the largest. Let $X_1, X_2, \dots, X_n$ be observations of a random sample of size $n$ from a continuous distribution. The random variables $Y_1 < Y_2 < \dots < Y_n$ denote the order statistics of the sample, in which $Y_n$ is the $n$-th smallest of $X_1, X_2, \dots, X_n$.

Let $Y_1 < Y_2 < \dots < Y_n$ be the order statistics of $n$ independent observations from a distribution of the continuous type with cdf $F(x)$ and pdf $F'(x) = f(x)$, where $0 < F(x) < 1$ for $a < x < b$ and $F(a) = 0$, $F(b) = 1$. The event that the $r$-th order statistics $Y_r$ is at most $y$, $\{ Y_r \le y \}$, occurs if at least $r$ of the $n$ observations are less than or equal to $y$.

- The probability of drawing an observation that is less than or equal to $y$ is $F(y)$. To have at least $r$ successes, $G_r(y) = P(Y_r \le y) = \sum_{k = r}^{n} {n \choose k} [F(y)]^k [1 - F(y)]^{n - k}$.
- The pdf of $Y_r$ is $g_r (y) = G'_r(y) = \frac{n!}{(r - 1)!(n - r)!} [F(y)]^{r - 1} [1 - F(y)]^{n - r} f(y), a < y < b$.
- The pdf of the smallest order statistic is $g_1(y) = n[1 - F(y)]^{n - 1} f(y)$.
- The pdf of the largest order statistic is $g_n(y) = n[F(y)]^{n - 1} f(y)$.

Let $F(x) = P(X < x)$ be the cdf of $X$. If $Y_1 < Y_2 < \dots < Y_n$ are the order statistics of $n$ independent observations $X_1, X_2, \dots, X_n$, then $F(Y_1) < F(Y_2) < \dots < F(Y_n)$, because $F$ is a non-decreasing function.

Let $F(x)$ be the cdf of $X$, then the random variable $F(X)$ has a uniform distribution on the interval from $0$ to $1$, because the CDF of a continuous random variable maps the variable to a value between $0$ and $1$, with each value between $0$ and $1$ being possible. Let $W_1 = F(Y_1) < W_2 = F(Y_2) < \dots < W_n = F(Y_n)$, which is the order statistics of $n$ independent observations from $U(0, 1)$.

- The cdf of $U(0, 1)$ is $G(w) = w$
- The pdf of the $r$-th order statistic, $W_r = F(Y_r)$ is $h_r(w) = \frac{n!}{(r - 1)!(n - r)!} w^{r - 1} (1 - w)^{n - r}$.
- The mean $E(W_r) = E[F(Y_r)]$ is $E(W_r) = \int_0^1 w \frac{n!}{(r - 1)!(n - r)!} w^{r - 1} (1 - w)^{n - r} dw = \frac{r}{n + 1}$.
- The expected value of the random area between adjacent order statistics is $E[F(Y_r) - F(Y_{r - 1})] = E[F(Y_r)] - E[F(Y_{r - 1})] = \frac{1}{n + 1}$.

Therefore, the order statistics $Y_1 < Y_2 < \dots < Y_n$ partition the domain of $X$ info $n + 1$ parts, which has the area equals $\frac{1}{n + 1}$.