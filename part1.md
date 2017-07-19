
# 指数分布族

$$
\begin{align}
p(y|n) = h(y) \cdot g(\eta) \cdot exp\{ \eta^T T(y) \}
\end{align}
$$
其中$\eta$是分布的自然参数，$\mu(y)$是充分统计量，通常$\mu(y)=y$，当参数h、g、T都固定时，就是关于$\mu(y)$的函数族

下面分别介绍伯努利分布和高斯分布，分别把它们表示成指数分布族的形式

## 伯努利分布
伯努利分布是对0、1问题进行建模，对于一个伯努利分布$Bernoulli(\psi), y \in \lbrace 0,1\rbrace$， 有$p(y=1|\psi) = \psi, p(y=0|\psi) = 1-\psi$，
$$
\begin{align}
P(y|\psi) & = \psi^y(1-\psi)^{1-y}= exp(\log \psi^y(1-\psi)^{1-y}) \\
& = exp(y\log \psi + (1-y)\log (1-\psi)) \\
& = exp(y\log \frac{\psi}{1-\psi} + \log(1-\psi))\\
& = (1-\psi)exp(y\log \frac{\psi}{1-\psi})
\end{align}
$$
对应到指数分布族:

$$
h(y) = 1\\
\eta = \log \frac{\psi}{1-\psi} \Rightarrow \psi = \frac{e^\eta}{e^\eta + 1}=\frac{1}{1+e^{-\eta}} \\
g(\eta) = 1-\psi = \frac{1}{e^\eta+1}\\
T(y) = y
$$

可以看出，$\psi$的形式就是sigmoid函数的形式，这是因为logistic模型对问题的前置概率估计其实就是伯努利分布

## 高斯分布
下面对高斯分布进行推到

$$
\begin{align}
N(\mu,1) & = \frac{1}{\sqrt{2\pi}}exp\left( -\frac{1}{2} (y-\mu)^2\right) = \frac{1}{\sqrt{2\pi}}exp\left( -\frac{1}{2}y^2-\frac{1}{2}\mu^2+\mu y \right) \\
& = \frac{1}{\sqrt{2\pi}} exp(-\frac{1}{2}y^2)exp(-\frac{1}{2}\mu^2)exp(\mu y)
\end{align}
$$
对应到指数分布族:

$$
h(y) = \frac{1}{\sqrt{2\pi}} exp(-\frac{1}{2}y^2)\\
\eta = \mu \\
g(\eta) = exp(-\frac{1}{2}\mu^2)\\
T(y) = y
$$

## 广义线性模型

仔细观察伯努利分布和高斯分布的指数分布族形式中的$\eta$变量。可以发现，在伯努利的指数分布族形式中，伯努利分布的参数$\phi$是关于$\eta$的一个logistic函数（下面会介绍logistic回归的推导）。此外，在高斯分布的指数分布族表示形式中，η与正态分布的参数μ相等，下面会根据它推导出普通最小二乘法（Ordinary Least Squares）。通过这两个例子，我们大致可以得到一个结论，η以不同的映射函数与其它概率分布函数中的参数发生联系，从而得到不同的模型，广义线性模型正是将指数分布族中的所有成员（每个成员正好有一个这样的联系）都作为线性模型的扩展，通过各种非线性的连接函数将线性函数映射到其他空间，从而大大扩大了线性模型可解决的问题。
