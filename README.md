# TV Scripts Generation

This project is a part of the [Deep Learning Nanodegree](https://www.udacity.com/course/deep-learning-nanodegree--nd101) at [Udacity](https://www.udacity.com/).

-- Project Status: Completed

## Project Introduction

Building a Neural Network to generate a new, "fake" TV script using Seinfeld dataset of scripts from 9 seasons.

## Methods Used

- Data Exploration
- Data Preprocessing
- Recurrent Neural Networks

## Technologies

- Python3
- Anaconda or Miniconda
- Numpy
- PyTorch
- Jupyter Notebook

## Project Description

The purpose of this project is to generate new ,"fake" [Seinfeld](https://en.wikipedia.org/wiki/Seinfeld) TV scripts using RNNs based on patterns it recognizes in [the training data](https://www.kaggle.com/thec03u5/seinfeld-chronicles#scripts.csv). I began with exploring the dataset to get an overview with some samples. Then, applied data preprocessing by creating lookup table tozenizing punctuation, and finally implemented RNN using LSTM.
After training for 35 epochs, I could generate a new, "fake" Seinfeld TV script.

**Samples of the generated fake script**

george: what about the drake?

elaine: i don't know.

kramer: yeah.

george:(to jerry) i can't believe this!

kramer: oh! yeah!

As shown the TV script doesn't make perfect sense which is fine for the project. It should look like alternating lines of dialogue (for more details see this [documentation]](https://github.com/eng-dtarek/TV_Scripts_Generator/blob/master/dlnd_tv_script_generation.html))  

## Getting Started

1. Clone this repo (for help see this [tutorial](https://help.github.com/en/articles/cloning-a-repository)).
2. Install the above technologies
3. Create a new conda environment >> conda create --name deep-learning python=3
4. Enter the environment: (Mac/Linux) >> source activate deep-learning, (Windows) >> activate deep-learning
5. Run the following to open up the notebook server >> jupyter notebook
