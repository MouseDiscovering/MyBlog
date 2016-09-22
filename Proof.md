# Proof:K-means clustering algorithm is a special kind of Gaussian Mixed Model based on EM algorithm

## 1.K-means algorithm analysis

​	Considering the K-means clustering algorithm:
$$
(\mu_{1},...\mu_{k})^{*} =\mathop{ \text{argmin}}_{u_1,...,u_{k}}  \mathop{\text{min}}_{z_1,...z_{k}} \sum_{i =1}^{n} (\mathbf{x}_{i,k} - \mathbf{u}_{k})(\mathbf{x}_{i,k} - \mathbf{u}_{k})^T
$$
​	The steps are as below:

1. Initialize $\mathbf{\mu}_{1}, ... , \mathbf{\mu}_{k}$ to be equal to randomly selected points $x_1, ... , x_{k}$.

2. Repeat the steps below until $z_1,...,z_{n}$ stop changing.

   1. $z_{i} := \text{argmin}_{z} (\mathbf{x}_{i} - \mathbf{u}_{z})(\mathbf{x}_{i} - \mathbf{u}_{z})^T$ 

   2. $\mu_{z} := \frac{1}{N_{z}} \sum_{i:z_{i} = z}x_{i}, \quad N_{z} \text{ is the number of data belonging to } z_{i}$

      ​

## 2.A Guassian distribution whose dimensions are independent to each other 

​	In a Gaussian mixed model, EM algorithm solves the following optimization problem:
$$
\theta^{*} = \mathop{\text{argmax}} _{\theta}  \max_{z_1,...,z_n} P_{\theta}(x_1,...,x_n,z_1,...z_n)
$$
​	$\theta$ is the parameters of the Gaussian distritions, and $z$ denotes the label that the data belong to, which is called latent variable.

​	If each dimension of a Gaussian distribution is independent. For a such Gaussian distribution which has **d dimensions**, the covariance matrix has the form below.
$$
\begin{equation}
\Sigma = \left [
 	\begin{matrix}
 	1_1 &\cdots & 0  \\
 	\vdots &\ddots &\vdots \\
 	0 &\cdots & 1_{d}
 	\end{matrix}
\right]
\end{equation}
$$

​	The log likelihood function is:
$$
\begin{equation}
	\begin{aligned}
	L(\theta|X) 
	&= log\prod_{i = 1}^{n}(\frac{1}{2\pi \sigma_{k}^{2}} exp(-\frac{(\mathbf{x}_{i,k} - \mathbf{u}_{k})(\mathbf{x}_{i,k} - \mathbf{u}_{k})^T} {2 \sigma_{k}^2} ))\\
	&=- \sum_{i=1}^{n}\left( 
		log(2\pi \sigma_k)  + \frac{(\mathbf{x}_{i,k} - \mathbf{u}_{k})(\mathbf{x}_{i,k} - \mathbf{u}_{k})^T} {2 \sigma_{k}^2}
		\right)	\\
        &= - n \cdot log(2\pi) - \sum_{i=1}^{n}\frac{1}{2}(\mathbf{x}_{i,k} - \mathbf{u}_{k})(\mathbf{x}_{i,k} - \mathbf{u}_{k})^T
	\end{aligned}
\end{equation}
$$
​	The maximization of  $L(\theta | X)$ is equivalent to the minimization of $-L(\theta | X)$ . $n \cdot log(2\pi)$ is a constant so that it can be omitted. The problem is equivalent to as below.
$$
\begin{aligned}
\theta^{*} &= \mathop{\text{argmin}}L^{'}(\theta | X )  \\
&=\mathop{\text{argmin}} \sum_{i=1}^{n}  \frac{(\mathbf{x}_{i,k} - \mathbf{u}_{k})(\mathbf{x}_{i,k} - \mathbf{u}_{k})^T} {2 }
\end{aligned}
$$
​	$\theta$ here only consists of $\mu_{1},...\mu_{k}$ , for all variances are fixed to 1.

## 3.Conclusion

​	So it is proven that K-means clustering algorithm is a special Gaussian mixed model based on EM algorithm. The special mixed Gaussian distributions should have the ***identity*** covariance matrix so that the clustering problems can be equivalent.

---

- Author: Donghao
- St NO.: 031220415(SX1603137 for post graduate) 
- Data: 2016.9.14
- E-mail: dongyinhao@foxmail.com