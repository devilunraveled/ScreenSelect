# ScreenSelect

**ScreenSelect** is a movie recommendation engine built upoin the concept of Naive Bayes extended by Laplace Smoothing.

The basic concept of a *Naive Bayes* is the condition that it imposes upon the data points in order to simplify the calculations and reduce the complexity of the model.


### The Basic Idea

Movie recommendation in itself can be thought of as a typical *classification* problem.
Naive Bayes assumes that the predictive feauters are independent of each other, using this important restriction, along with _Bayes theorem_, one can derive the mathematical background for the model.

### Bayes Theorem

Following is the backbone equation of [ _Bayes Theorem_ ](https://www.investopedia.com/terms/b/bayes-theorem.asp) :

$$
\begin{equation}
P(A | B) = P( B | A) \cdot \frac{P(A)}{P(B)}
\end{equation}
$$

As is clear from the equation, _Bayes Theorem_ allows us to calculate the conditional probability of an event $A$, given the condition that $B$ has occurred, given the conditional probability of $B$ given $A$, and probability of each, $A$ and $B$.

### Applying Bayes Theorem 

To apply _Bayes Theorem_, we first define two *vectors* as follows :

$$
x = (x_1, x_2,... , x_n) \\
y = (y_1, y_2,... , y_k)
$$

In this case, $x$ encodes the information regarding the possible feauters of the movie that can be used for training and analysis. Whereas $y_i$ simply represents the $i^{th}$ class among the $k$ possible ones for the output.

Therefore, the goal of the Naive Bayes is to crunch information from the data points given for the n features and based on that find a **probability distribution**, $p_{X}(i)$ that denotes the possibilty of a given vector $X$ being rightfully classified as a part of the $i^{th}$ class.


### Formulation and Naiveness

Appling (1) we have : 

$$
\begin{equation*}
P(Y = y_{i} | X = x) = P( X = x | Y = y_{i}) \cdot \frac{P(Y = y_{i})}{P(X = x)}
\end{equation*}
$$

Rewriting,

$$
\begin{equation}

P(y_{i} | x) = P( x | y_{i}) \cdot \frac{P(y_{i})}{P(x)}
\end{equation}
$$

1. Now the term on the left, also known as **posterior**, is of interest to us, since we want to determine that expression only, for all possible $i's$.
2. The term $P(x)$, called the **evidence** is not really relevant as its a constant for a particular $x$, and therefore, it can be ignrored, since we can scale the probabilities to sum to 1 anyways.
3. The term $P(y_{i})$ is a reflection of the general distribution of the known data points across the different classes, so can be calculated either from additional information or from training samples. This term is called the **prior**.
4. The term $P(x|y_i)$ is called the **likelihood** and is the most tricky to calculate in general.

Now, we introduce the Naiveness in the approach, we assume that the different features, i.e., $x_1,x_2, ...$ are independent of each other. This leads to the following simplification :

$$
\begin{equation}
P(x | y_i) = \Pi_{j=1}^{n} P( x_j | y_i)
\end{equation}
$$

Now, $P( x_j | y_i )$ can be easily calculated by simply enumerating the values of the $j^{th}$ feature already in the $i^{th}$ class.

Therefore, we have : 

$$
\begin{equation*}
P(y_i | x) \propto P(y_i) \cdot \Pi_{j=1}^{n} P(x_j | y_i)
\end{equation*}
$$

### Unknown Likelihood and Laplace Smoothing

It seems that we are in essence, done, since we have the simple proportionality relation and using the total loaw of probability we can determine the exact values as well.

But the problem arises, when a particular instance of a feature is never present in a class for the training data, this vanishes the entire posterior to 0, even if there could've been other features that heavely indicate that it belongs to that particular class.

This is where Laplace Smoothing comes in, we start calculating the features, assuming that the inital value for each of the features is 1.

This solves the Unknown Likelihood problem to some extent.


### Results

Finally. we can write down the probability distribution for the different classes.
