# A Survey of Deep Learning Architectures for Algorithmic Cryptocurrency Trading

This repository is for the project A Survey of Deep Learning Architectures for Algorithmic Cryptocurrency Trading, delivered on April 22, 2022 for the University of Colorado Denver's M.S. Statistics program.

In this project, we looked at several different architectures as potential decision-making agents for an algorithmic cryptocurrency program. The algorithms can be broadly grouped into three categories: Classical Statisical Forecasting and eXtreme Gradient Boosting, Artificial Neural Networks, and Reinforcement Learning.

In the Classical Statistical and eXtreme Gradient Boosting category, we have Expoential Smoothing, Seasonal AutoRegressive Integrated Moving Average with eXogenous variables, and eXtreme Gradient Boosting. In the Aritifical Neural Networks category, we have Multi-Layer Perceptron, Convolutional Neural Network, and Long-Short Term Memory Recurrent Neural Network. In the Reinforcement Learning category, we have Deep Q-Learning (with some augmentations) and Deep Determinsitic Policy Gradient (with some augmentations). We also compare these architectures with trading on three Technical Indicators, a fully random agent, and Buy-and-Hold. This final strategy, Buy-and-Hold, wherein one enters the market and does nothing until deciding to leave, will serve as the benchmark we hope to beat.

Our data was hourly Bitcoin market data consisting of standard Open, High, Low, Close, and Volume information from July 1st of 2018 at 12:00 AM to December 31st of 2021 at 11:00 PM. We chose the last six months of this data as the testing data with the rest being training data.

Our preprocessing of the data has two parts. Part 1 was to create a data matrix of Technical Indicators, fourteen in total, on several different timeframes (where appropriate). This gave us 101 features per hour. Part 2 was applying Principal Component Analysis and reducing our matrix to the first twenty Principal Components (accounting for nearly 99% of the variance).

After running through our Classical Statistical and eXtreme Gradient Boosting and Artificial Neural Network architectures, we found that the best performance was with our Convolutional Neural Network recieving "images" of twelve hours of data. We then chose this to be the neural network used in our Reinforcement Learning models.

We augmented our Deep Q-Network with Prioritized Experience Replay and adopted both the Dueling and Double Deep Q-Network structures. This makes our full architecture a Convolutional Neural Network-Based Dueling Double Deep Q-Network with Prioritized Experience Replay. 

Our final model was a Deep Deterministic Policy Gradient, using the same Convolutional Neural Network architecture and augmented to become a Convolutional Neural Network-Based Twin Delayed Deep Deterministic Policy Gradient.

For all models except the last, the only actions the model could take were to buy or exit the market with the entirety of its portfolio.

Our results showed that the best-performing architecture after six months of trading was the Deep Q-Network model. However, it was only in the end of the period that the agent managed to surpass Buy-and-Hold, as the testing period saw large gains in Bitcoin's price near the end of 2021 which the agent could not react properly to. When adding the first two months of 2022 as testing data, as the value of Bitcoin fell, the model fared significantly better. The only algorithm to stay near, and occasionally surpass, Buy-and-Hold during the extreme price increases was the Twin Delayed Deep Deterministic Policy Gradient. This is attributed to the model's ability to invest and withdraw a continuous value of its portfolio. The downside to this was that when the price dropped in early 2022, the model also closely followed Buy-and-Hold, losing portfolio value along with Bitcoin.

Moving forward, we hope to explore other continuous-action-space models, such as Advantage Actor Critic or Proximal Policy Optimization, as well as experiment with other forms of data. In particular, we hope to develop Sentiment Analysis algorithms and combine their output with more traditional market data to see if we can do better. 
