# Learning Linear Models for XOR-PUF (ML Assignment 1)
Developed a linear model for a XOR-PUF (Physical Unclonable Function) system. Here the XOR-PUF consists of three PUFs, each with eight multiplexers, and takes an 8-bit challenge as input. All the three PUFs are connected in parallel. The goal is to create a new feature vector from the challenge and use a linear model to predict the PUF's response. The assignment requires implementing three methods: get_renamed_labels() for label mapping, get_features() for feature transformation, and solver() for training the linear model using gradient descent. The linear model is capable of predicting the XOR-PUF response very accurately. 

---
##### What is PUF and XOR-PUF?
A Physical Unclonable Function (PUF) is a hardware security feature that exploits the inherent variations in physical properties of electronic devices to provide unique and unclonable identities. PUFs play a crucial role in enhancing the security of electrical devices, making them resistant to cloning, tampering, and unauthorized access.
![4 bit PUF](https://github.com/saqeeb360/Learning-Linear-Models-for-XOR-PUF/blob/main/images/4bit-PUF.png?raw=true)

XOR-PUF (Exclusive OR-Physical Unclonable Function) is a type of Physical Unclonable Function that combines multiple PUFs (Physical Unclonable Functions) in parallel using the XOR operation. It is designed to enhance the security and uniqueness of PUF-based systems.
![4 bit XOR-PUF](https://github.com/saqeeb360/Learning-Linear-Models-for-XOR-PUF/blob/main/images/4bit-XorPUF.png?raw=true)

##### How does this work!
The given assignment presents a problem related to XOR-PUFs (Physically Unclonable Functions). Here one XOR-PUF is given which has 3 parallel Arbiter PUF connected using XOR. Each arbiter PUF consists of a chain of multiplexers with different delays. The challenge bit is fed into each PUF, and the response is determined by comparing the arrival times of signals at the finish line.

We create new feature vector from an 8-bit challenge, solving (the mathmetical equations mentioned in answer pdf) we get 729 dimension feature vector. 
As W = 8 demension and bias is 1 dimension for one arbiter PUF
Combining 3 arbiter PUF using XOR -> (8+1)^3 => 729 dimension feature vector.
![generating features](https://github.com/saqeeb360/Learning-Linear-Models-for-XOR-PUF/blob/main/images/features.png?raw=true)

We convert the 8 bit train data into 729 feature vector.

For the label there exists a way to map the binary digits 0,1 to sign -1, +1 as say m: {0, 1} -> {-1, +1} and another way f: {-1, +1} -> {0, 1} to map signs to bits (not that m and f need not be inverses of each other) so that for any set of binary digits (b1, b2, . . . , bn) for any n € N we have:
![generating labels](https://github.com/saqeeb360/Learning-Linear-Models-for-XOR-PUF/blob/main/images/labels.png?raw=true)

Then we train a linear model using gradient descent. To train our model we use learning rate (eta = 0.12) and lambda parameter (lambda_para = 0.0001) and initialize our weight metrics W with zeros as this gives the best accuracy to our model. Further
with each iteration our learning rate will decrease by vt where t is the iteration number. So that our model will converge easily.
We learned these hyperparameters by randomly using different values for each parameter it is more like random search hyperparameter tuning.
We assign different values for eta and lambda_para in search space with random values and predict using the model foreach setting of hyperparameter. Our metric to find our hyperparameter. So we find on what setting of hyperparameter our model performs best and give high accuracy or produces minimum classification error.
We get the convergence graph as follows:
![Convergence Curve](https://github.com/saqeeb360/Learning-Linear-Models-for-XOR-PUF/blob/main/images/Convergence-Curve.png?raw=true)


# Results
| timeout | avg_hinge/num_trials | avg_error/num_trials | avg_time_reported/num_trials | avg_time_wrapper/num_trials |
|---------|----------------------|----------------------|------------------------------|-----------------------------|
| 0.2     | 0.015347             | 0.005060             | 0.200038                     | 0.201032                    |
| 0.5     | 0.000000             | 0.000000             | 0.500037                     | 0.501668                    |
| 1.0     | 0.000000             | 0.000000             | 1.000033                     | 1.002543                    |
| 2.0     | 0.000000             | 0.000000             | 2.000019                     | 2.004446                    |
| 5.0     | 0.000000             | 0.000000             | 5.000018                     | 5.010145                    |