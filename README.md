# DLTP-IIITH-Assigment-2

Subject: CS7.601 Deep Learining: Theory and Practice

Prof: Naresh Manwani

Instructions:

1. Please submit your code for Q1 and Q2 in Jupyter Notebooks. Analysis should be included in the notebook itself using markdown cells. Note that unlike assignment 1, the analysis and reasoning of the results obtained will carry a significant weightage in the marks distribution.
2. Only the following libraries are allowed:** **
   * Numpy
   * Pandas
   * Matplotlib
   * Pytorch (version ≥ 2.0)
   * Tensorflow (version ≥ 2.0) (Only allowed for assignment 2, assignments 3 and 4 will be pytorch only)
   * tqdm
   * scikit-learn

# Q1) RNN For Auto-Regressive Models

In this exercise, you are asked to generate an Auto-Regressive model and then create an RNN that predicts it. Generate samples of an Auto-Regressive model of the form** **

X(t) = a1X(t − 1) + a2X(t − 2) + a3X(t − 3) + U(t)** **

where,

x = value of time series at time "t"

U(t) ∼ Uniform(0,0.1), 

a1 = 0.6,

a2 = −0.5,

a3 = −0.2. 

Generate 2000 training and 2000 test examples using this model. Now train an RNN that predicts the sequence. Apply the training algorithm on new samples and calculate the averaged cost square error cost function.

Questions:

1. Investigate RNN with 1,2 and 3 hidden layers. Describe the architecture used for the network.
2. Plot the epoch-MSE curve during training.
3. Report MSE (mean square error), MAE (mean absolute error) and R2 (R-square) on the test data.

# Q2) *Learning Long Term Dependencies [7 Marks]*

There are p + 1 input symbols denoted a1,a2,...,ap−1,ap = x, ap+1 = y.

ai is represented by p + 1 dimensional vector whose ith component is 1 and all other are 0.

A net with p + 1 input units and p + 1 output units sequentially observes input symbol sequences, one at a time, trying to predict the next symbols. Error signals occur at every single time steps.

To emphasize the long term lag problem, we use a training set consisting of only two sets of sequences:

{(x,ai1,ai2,...,aip−1,x) | 1 ≤ i1 ≤ i2 ≤ ... ≤ ip−1 ≤ p − 1}

and

{(y,ai1,ai2,...,aip−1,y) | 1 ≤ i1 ≤ i2 ≤ ... ≤ ip−1 ≤ p−1}.

In this experiment take p = 100.

The only totally predictable targets, however, are x and y, which occur at sequence ends.

Training sequences are chosen randomly from the two sets with probability 0.5.

Compare how RNN and LSTM perform for this prediction problem and Report the following.

1. Describe the architecture used for LSTM and for RNN. Also mention the activation functions, optimizer and other parameters you choose. Experiment around with multiple architectures and report your observations.
2. Plot the number of input sequences passed through the network versus training error (for both LSTM and RNN).
3. Once the training stops, generate 3000 sequences for test set.
4. **Report the average number of wrong predictions on the test set in 10 different trials (for both LSTM and RNN). **

   Example:

   Consider p = 5. Suppose the set of random integers (i1, i2, i3, i4) are {1, 1, 3, 4} respectively.**  Then, the sequence {(x, i1, i2, i3, i4, x)} will have matrix representation as: **

0 1 1 0 0 0

0 0 0 0 0 0

0 0 0 1 0 0

0 0 0 0 1 0

1 0 0 0 0 1

0 0 0 0 0 0

Explanation:

Here are some clarifications to the second question:

* \( a_i \) is a 1-hot vector of dimension p+1 with it's \( i^{\text{th}} \) element set to 1.
* x = \( a_p \) and y = \( a_{p+1} \)
* There are two types of sequences in the training dataset as mentioned in the pdf, sequences which start with x and end with x and sequences which start with y and end with y.
* The input to the model will be a p+1 dimensional vector at every timestep and you have to predict the next symbol in the sequence. There are p total timesteps. The input to the sequence at the first timestep will be x/y.
* The loss is to be calculate only for the last timestep.

Example explanation:

* We have considered p=5. This means x = \( a_p \) = (0, 0, 0, 0, 1, 0) and y = \( a_{p+1} \) =(0, 0, 0, 0, 0, 1).
* We first have to choose randomly between the sequences of type (x, \( i_1 \), \( i_2 \), \( i_3 \), \( i_4 \), x) and (y, \( i_1 \), \( i_2 \), \( i_3 \), \( i_4 \), y). We have chosen the first type, (x, \( i_1 \), \( i_2 \), \( i_3 \), \( i_4 \), x).
* We then randomly generate \( i_1 \), \( i_2 \), \( i_3 \), \( i_4 \) following the constraints mentioned in the problem, which turn out to be 1, 1, 3, 4.
* In the first timestep, we provide x as the input to the network, and it is supposed to predict \( i_1 \).
* In the second timestep, we provide \( i_1 \) as the input and it is supposed to predict \( i_2 \).
* In the third timestep, we provide \( i_2 \) as the input and it is supposed to predict \( i_3 \).
* In the fourth timestep, we provide (\( i_3 \) as the input and it is supposed to predict \( i_4 \).
* In the fifth and the final timestep, we provide \( i_4 \) as the input and it is supposed to predict x.

If the final prediction is correct, the sequence is considered to be correctly classified.
