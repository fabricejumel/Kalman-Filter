# Kalman Filter Examples

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png) Here give you some exmaples to demonstrate how to use Kalman filter in projects.

### 1. Kalman filter in 1D space
Assume you got signal from a sensor, to measure the distance, temperature or volume, there exist noise in sensor, how to correct and predict the read value ?

#### Example : 
We assume the real signal sequence is a sigmoid function, from 0 to 100, we got measurement from sensor presented as `z`, and the measurement noise variance is `R`, while we got predicted state and variance as `x` and `P`, and the process noise variance is `Q`, the state predicted by transition matrix `F` in each time step. The predicted state and variance mapping to measurement space `H` matrix.

#### Measurement 
Simulated signal `z` by sigmoid function mix with measurement noise `R`.

```
z = 1/(1+e^(-t)) + R
```
#### Prediction 
State `x` and variance `P` mix with process noise `Q`, transition matrix `F` is `1` in this exmaple.

```
x' = F * x
P' = F * P + Q
```
#### Correct and Update
Mix measurement and prediction mean and variance by multiply of two gaussian distribution, we got best estimated in current time (K is Kalman gain, calculate it to generate mix gaussian distribution).

```
K = P / (P - R)
x = x' + K * (z - H * x')
P = (1 - K) * P
```

#### Simulation results
![](Images/Kalman1d.png)