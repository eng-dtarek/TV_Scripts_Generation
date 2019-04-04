# TV Scripts Generation

In this project, the goal is to generate new ,"fake" [Seinfeld](https://en.wikipedia.org/wiki/Seinfeld) TV scripts using RNNs based on patterns it recognizes in the training data.

## Steps for generating TV scripts

- The Dataset
- Explore the Data
- Data Preprocessing
- Build the Neural Network
- Neural Network Training
- Generate TV Script

## The Dataset

[Seinfeld Dataset](https://www.kaggle.com/thec03u5/seinfeld-chronicles#scripts.csv), a dataset for textual analysis on arguably the best written comedy television show ever.

## Explore the Data

It's importatnt to view different parts of the data. This will give you a sense of the data you'll be working with. You can see, for example, that it is all lowercase text, and each new line of dialogue is separated by a newline character 

**Dataset Stats**
- Roughly the number of unique words: 46367
- Number of lines: 109233
- Average number of words in each line: 5.544240293684143

**The lines 0 to 10**:
jerry: do you know what this is all about? do you know, why were here? to be out, this is out...and out is one of the single most enjoyable experiences of life. people...did you ever hear people talking about we should go out? this is what theyre talking about...this whole thing, were all out now, no one is home. not one person here is home, were all out! there are people trying to find us, they dont know where we are. (on an imaginary phone) did you ring?, i cant find him. where did he go? he didnt tell me where he was going. he must have gone out. you wanna go out you get ready, you pick out the clothes, right? you take the shower, you get all ready, get the cash, get your friends, the car, the spot, the reservation...then youre standing around, what do you do? you go we gotta be getting back. once youre out, you wanna get back! you wanna go to sleep, you wanna get up, you wanna go out again tomorrow, right? where ever you are in life, its my feeling, youve gotta go. 

jerry: (pointing at georges shirt) see, to me, that button is in the worst possible spot. the second button literally makes or breaks the shirt, look at it. its too high! its in no-mans-land. you look like you live with your mother. 

george: are you through? 

jerry: you do of course try on, when you buy? 

george: yes, it was purple, i liked it, i dont actually recall considering the buttons. 

## Data Preprocessing

### Lookup Table

To create a word embedding, first the words need to transformed to ids by creating two dictionaries:

- Dictionary to go from the words to an id, we'll call vocab_to_int.
- Dictionary to go from the id to word, we'll call int_to_vocab.

### Tokenize Punctuation

We'll be splitting the script into a word array using spaces as delimiters. However, punctuations like periods and exclamation marks can create multiple ids for the same word. For example, "bye" and "bye!" would generate two different word ids.

So we need to create a dictionary that will be used to tokenize the symbols and add the delimiter (space) around it. This separates each symbols as its own word, making it easier for the neural network to predict the next word. Make sure you don't use a value that could be confused as a word; for example, instead of using the value "dash", try using something like "||dash||".

## Build the Neural Network

Starting with the preprocessed input data. We'll use TensorDataset to provide a known format to our dataset; in combination with DataLoader, it will handle batching, shuffling, and other dataset iteration functions.

Then, Implement the batch_data function to batch words data into chunks of size batch_size using the TensorDataset and DataLoader classes.

After that, LSTM is used to complete the RNN through implementing the following functions:

- __init__: The initialize function.
- init_hidden: The initialization function for an LSTM hidden state.
- forward: Forward propagation function.
- forward_back_prop: Forward and backward propagation on the neural network

## Neural Network Training

With the structure of the network complete and data ready to be fed in the neural network, it's time to train it.

### Hyperparameters

I prefer starting with simple architecture, So I choose embedding_dim = 50, hidden_dim = 25, sequence_length = 30, batch_size = 50, learning_rate = 0.01 but the loss was stuck around 4.7 for many epochs even after decreasing the learning rate to 0.001.
Then I used embedding_dim = 100, hidden_dim = 50, sequence_length = 30, batch_size = 50 the loss became better around 4.3 after 10 epochs which is not good.
After that, I changed the batch_size to be 64, sequence_length = 20, embedding_dim = 200 hidden_dim = 100 loss became much better around 4.0 after 10 epochs which is not the target.
Finally I used batch_size = 64, sequence_length = 6, sequence_length = 20, embedding_dim = 500 hidden_dim = 300 for 35 epochs.
I think that I need to do more hyperparameters tuning to get better fast results but unforunately the resources are limited

**Here's the final selected Hyperparameters**

- sequence_length = 6
- batch_size = 64
- num_epochs = 35
- learning_rate = 0.0001
- vocab_size = len(vocab_to_int)
- output_size = vocab_size
- embedding_dim = 500
- hidden_dim = 300
- n_layers = 2

## Generate TV Script

With the network trained and saved, it's the time to generate a new, "fake" Seinfeld TV script.

### Sample of the generated TV scripts

jerry: you don't think i could have been a good time.

jerry: what are you doing here?

elaine: yeah, well i don't even know how to do it.(jerry enters)

george: what?

jerry: no, i'm gonna be a little bit in the building.

jerry: i can't.

george: what about the drake?

elaine: i don't know.

kramer: yeah.

george:(to jerry) i can't believe this!

kramer: oh! yeah!

### The TV Script is Not Perfect

As shown the TV script doesn't make perfect sense which is fine for the project. It should look like alternating lines of dialogue
