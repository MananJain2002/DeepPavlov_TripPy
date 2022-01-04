# DeepPavlov_TripPy
<h1>Goal</h1>

The goal of this project was to improve the architecture of Goal-Oriented Chatbots in the DeepPavlov framework for AI smart assistants. To do so, we decided to implement a new model inspired by the latest State of the Art in Goal-Oriented bots, especially TripPy.
I have taken the code from [here](https://github.com/deepmipt/DeepPavlov/tree/f72397aa8391283475a88910e8f251a850767df8) and was looking if there were any sort of bugs or in any way I can imporve it.

<h1>DeepPavlov</h1>

DeepPavlov is an open source framework for chatbots and virtual assistants development. It is built on [TensorFlow](https://www.tensorflow.org/), [Keras](https://keras.io/)
and [PyTorch](https://pytorch.org/). It has comprehensive and flexible tools that let developers and NLP researchers create production ready conversational skills and complex multi-skill conversational assistants.

DeepPavlov is designed for
* development of production ready chat-bots and complex conversational systems,
* research in the area of NLP and, particularly, of dialog systems.

<h1>How does DeepPavlov Work?</h1>
<img src="http://docs.deeppavlov.ai/en/master/_images/dp_agnt_diag.png">
<p>* The smallest building block of the library is a Component. A Component stands for any kind of function in an NLP pipeline. It can be implemented as a neural network, a non-neural ML model, or a rule-based system.</p>
<p>* Components can be joined into a Model or a Skill. A Model solves a larger NLP task than a Component. However, in terms of implementation, Models are not different from Components. What differentiates a Skill from a Model is that the input and output of a Skill should both be strings. Therefore, Skills are usually associated with dialogue tasks.</p>

You can find more about the at https://deeppavlov.ai/

<h1>Various NLP Models </h1>

[Named Entity Recognition](http://docs.deeppavlov.ai/en/master/features/models/ner.html) | [Slot filling](http://docs.deeppavlov.ai/en/master/features/models/slot_filling.html)

[Intent/Sentence Classification](http://docs.deeppavlov.ai/en/master/features/models/classifiers.html) |  [Question Answering over Text (SQuAD)](http://docs.deeppavlov.ai/en/master/features/models/squad.html) 

[Knowledge Base Question Answering](http://docs.deeppavlov.ai/en/master/features/models/kbqa.html)

[Sentence Similarity/Ranking](http://docs.deeppavlov.ai/en/master/features/models/neural_ranking.html) | [TF-IDF Ranking](http://docs.deeppavlov.ai/en/master/features/models/tfidf_ranking.html) 

[Morphological tagging](http://docs.deeppavlov.ai/en/master/features/models/morphotagger.html) | [Syntactic parsing](http://docs.deeppavlov.ai/en/master/features/models/syntaxparser.html)

[Automatic Spelling Correction](http://docs.deeppavlov.ai/en/master/features/models/spelling_correction.html) | [ELMo training and fine-tuning](http://docs.deeppavlov.ai/en/master/apiref/models/elmo.html)

[Speech recognition and synthesis (ASR and TTS)](http://docs.deeppavlov.ai/en/master/features/models/nemo.html) based on [NVIDIA NeMo](https://nvidia.github.io/NeMo/index.html)

[Entity Linking](http://docs.deeppavlov.ai/en/master/features/models/entity_linking.html) | [Multitask BERT](http://docs.deeppavlov.ai/en/master/features/models/multitask_bert.html)

*Skills*

[Goal(Task)-oriented Bot](http://docs.deeppavlov.ai/en/master/features/skills/go_bot.html) | [Open Domain Questions Answering](http://docs.deeppavlov.ai/en/master/features/skills/odqa.html)

[Frequently Asked Questions Answering](http://docs.deeppavlov.ai/en/master/features/skills/faq.html)

<h1>TripPy(A Triple Copy Strategy for Value Independent Neural Dialog State Tracking)</h1>
<img src="https://raw.githubusercontent.com/deepmipt/DeepPavlov/f72397aa8391283475a88910e8f251a850767df8/examples/img/trippy_architecture.png">
<p>The above sketch is the full architecture that has been implemented. The process starts with a user uttering some text “Utterance”. This is then fed together with the dialogues history (empty at the beginning) and some definitions (Slot names refers to variables the model aims to fill, such as “Time”, “Foodtype”). These inputs are fed into a TripPy-like pipeline. In the “Input preprocessing” the inputs are tokenized and prepared for the BERT model. This is where the core of the model sits and the entire dialogue is fed through a multi-layer transformer model. The hidden states of the transformer are then used via multiple heads to produce different predictions. A “Hydranet” as folks at Tesla might call it.

One part of the predictions serves the purpose of action prediction. From a pre-defined list of possible actions the model predicts which it wants to take. An action may be as simple as “Goodbye”.

The other part serves the filling of the dialogue state. This is where the model keeps track of its knowledge about the users desires. If the user said “I want Japanese food”, the model may save something like “food: japanese” with an associated probability in its dialogue state tracker.

Together these two parts are used to produce a system response. The model allows the user to provide an SQLite database or an external API-Call mechanism, as shown in this tutorial. If such is provided and the predicted action is one that needs to retrieve data, a call to the database/api will be made. (E.g. an action like “Restaurant XYZ serves Japanese food.” - The model needs to retrieve a restaurant name that serves japanese food) The response is generated via a rule-based mechanism in the Natural Language Generation component and sent back to the user.

The architecture can also be used without any slot names if all the data can be defined in the actions of the model. For example, a bot that recommends people whether to play outside or stay inside based on how they feel may just need two actions (e.g. “Go play outside!” and “Stay inside!”) which it predicts based on user inputs, such as “It’s dark outside and I feel tired”. To train such a bot, one needs a dataset with ideally at least 5 dialogues for each of the bots actions. See for example the RASA tutorial.

To train a bot with slots and an api call, one needs a more advanced dataset with labels of the slots in the input. See the advanced tutorial for creating such a dataset.</p>

<h1>Using the Bot(Below a bot deployed to Telegram querying the Google Maps API while chatting:)</h1>
<img src="https://raw.githubusercontent.com/deepmipt/DeepPavlov/f72397aa8391283475a88910e8f251a850767df8/examples/img/trippy_telegram.jpg">

<h1>Future</h1>
I think the most promising improvement would be to swap the copy mechanism for a generative mechanism. The current implementation copies its slot values (what the user wants) from its own previous text or the users text. This prevents it from catching the slot value “French food “ from very convoluted sentences, like “I want to eat the food from the country with the Eiffel Tower”. However, you can’t just drop-in a purely generative model like GPT-3 due to its unpredictability - The probabilities for it giving the exact answers you want are too unlikely. A certain amount of unpredictability is acceptable, just as you cannot be sure a customer service representative won’t start insulting you, but it needs to be orders of magnitude better than GPT-3.

Switching to a generative mechanism, while retaining high predictability will be a key challenge to embed conversational AI into more business settings.
