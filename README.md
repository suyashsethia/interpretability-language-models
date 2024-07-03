# Interpretability 

Language models are trained to predict tokens given other tokens. More specifically, the autoregressive Language Modelling objective is given by the following distribution:

$$
P(w_{t} \mid w_{t-1}, w_{t-2} \dots w_0)
$$

The standard Transformer-based Language Model sees tokens as the lowest granularity of language. It sees tokens as entities and predicts other tokens. These models are not given the spelling of a token explicitly.

The question we ask in this assignment is, "to what extent do the representations of words from an LM encode character information?"

"What is it about the Language Modelling objective that allows a model to deduce something about the characters of a token?"


To accomplish our purposes, we will conduct probing studies.
- design a task that relies on the spelling of a word.
- check if a thin (one layer) classifier can be trained on top of LM embeddings to do this task.
- design a control to check whether the task is too easy.
  
## Q1
---
The experiment was to check if the model encodes information about the first letter of a word.the model was a multiclass model that was trained to predict the first letter of a word. The model was able to predict the first letter of a word with an accuracy of 0.59. This shows that the model is somewhat able to encode information about the first letter of a word given there were 26 classes

---
## Q2
---
the experiment was to check if the model encodes information about the letters of a word by making it impossible for the semantics to be used in the above task. We replaced the words with random letters except the fist letter of each word because we learnt in Q1 that the model is able to encode information about the first letter of a word  . and we conduct the experimnet 1 of randomly changing the words to capitalized or small and obsrve the accuracies .
The lower layers of the model performed better in the experiment compared to higher layers which shows that the model is able to encode information about the letters of a word in the lower layers of the model .

---
## Q3

The hypothesis was that certain layers of the model are used to encode certain information. The lower and middle layers of the model are used to encode letter information and the top layers are used to encode word information.
also the attention given to a certain token and letter is different across layers in a input sequence .


### experiment
- The model replaced random k letters from a word by random k letters and the task was to predict the number of letters changed .
- the k value was also randomly selcted .
- We also observed this result across different layers of the model to understand which layer is used to code what information .
-
the middle layers give a accuracy score of 0.6 whereas the starting layers are last few layers are below 0.5 and the first few layers are arounf 0.55
The middle and lower layers performed better in the experiment. This shows the letter information is concentrated in the lower layers of the model .

as observed in the graph of precision , recall , f1 and accuracy the graph takes the best values at middle layers and then take a dip 

---
 - When we analyze how the model pays attention to words in a sentence (attention maps), we see that the earlier layers focus more on the beginning words. As the model processes further (later layers), it considers both the beginning and middle parts of the sentence. The ending words seem to be less important for this specific task.
 - The attention maps show a fascinating trend: early layers focus on initial tokens, likely for spelling information. As processing deepens (later layers), attention spreads across the beginning and middle of the sequence. This suggests deeper layers grasp more complex linguistic features beyond spelling, like word structure or context. Finally, reduced attention on ending tokens in later layers might imply the model has extracted enough information for classification and doesn't need to focus heavily on the final words.

#### The model's performance and attention patterns across layers support the idea that some parts (heads) within the model pay closer attention to specific words in the input. Notably, the middle layers perform best, suggesting they're crucial for capturing both spelling and meaning. This might involve considering both individual words (local information) and the overall sentence structure (global information). Overall, the results show that the transformer model learns to link spelling patterns to correct or incorrect labels. It accomplishes this by using attention mechanisms to focus on important words at different levels of detail.
![image](https://github.com/suyashsethia/interpretability-language-models/assets/95227702/1a5643bd-7a91-427f-97fc-7a483d8a1ebf)
