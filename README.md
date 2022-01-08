<h1>Goal</h1>
The goal of this project was to experiment with the deepPavlov framework and to integrate
trippy so as to achieve greater accuracy and quicker responses from the bot. 

<h1>DeepPavlov</h1>

DeepPavlov is an open-source conversational AI library built on [TensorFlow](https://www.tensorflow.org/), [Keras](https://keras.io/)
and [PyTorch](https://pytorch.org/).

DeepPavlov is designed for
* development of production ready chat-bots and complex conversational systems,
* research in the area of NLP and, particularly, of dialog systems.

<h1>How does DeepPavlov Work?</h1>
<img src="http://docs.deeppavlov.ai/en/master/_images/dp_agnt_diag.png">
<p>* The smallest building block of the library is a Component. A Component stands for any kind of function in an NLP pipeline. It can be implemented as a neural network, a non-neural ML model, or a rule-based system.</p>
<p>* Components can be joined into a Model or a Skill. A Model solves a larger NLP task than a Component. However, in terms of implementation, Models are not different from Components. What differentiates a Skill from a Model is that the input and output of a Skill should both be strings. Therefore, Skills are usually associated with dialogue tasks.</p>


<h1>Various NLP Models </h1>
[Named Entity Recognition](http://docs.deeppavlov.ai/en/master/features/models/ner.html) | [Slot filling](http://docs.deeppavlov.ai/en/master/features/models/slot_filling.html)

[Intent/Sentence Classification](http://docs.deeppavlov.ai/en/master/features/models/classifiers.html) |  [Question Answering over Text (SQuAD)](http://docs.deeppavlov.ai/en/master/features/models/squad.html) 

[Knowledge Base Question Answering](http://docs.deeppavlov.ai/en/master/features/models/kbqa.html)

[Sentence Similarity/Ranking](http://docs.deeppavlov.ai/en/master/features/models/neural_ranking.html) | [TF-IDF Ranking](http://docs.deeppavlov.ai/en/master/features/models/tfidf_ranking.html) 

[Morphological tagging](http://docs.deeppavlov.ai/en/master/features/models/morphotagger.html) | [Syntactic parsing](http://docs.deeppavlov.ai/en/master/features/models/syntaxparser.html)

[Automatic Spelling Correction](http://docs.deeppavlov.ai/en/master/features/models/spelling_correction.html) | [ELMo training and fine-tuning](http://docs.deeppavlov.ai/en/master/apiref/models/elmo.html)

[Speech recognition and synthesis (ASR and TTS)](http://docs.deeppavlov.ai/en/master/features/models/nemo.html) based on [NVIDIA NeMo](https://nvidia.github.io/NeMo/index.html)

[Entity Linking](http://docs.deeppavlov.ai/en/master/features/models/entity_linking.html) | [Multitask BERT](http://docs.deeppavlov.ai/en/master/features/models/multitask_bert.html)

**Skills**

[Goal(Task)-oriented Bot](http://docs.deeppavlov.ai/en/master/features/skills/go_bot.html) | [Open Domain Questions Answering](http://docs.deeppavlov.ai/en/master/features/skills/odqa.html)

[Frequently Asked Questions Answering](http://docs.deeppavlov.ai/en/master/features/skills/faq.html)

<h1>TripPy(A Triple Copy Strategy for Value Independent Neural Dialog State Tracking)</h1>
<img src="https://raw.githubusercontent.com/deepmipt/DeepPavlov/f72397aa8391283475a88910e8f251a850767df8/examples/img/trippy_architecture.png">
<p>
<div>Task-oriented dialog systems rely on dialog state tracking (DST) to monitor the user's goal during the course of an interaction. Multi-domain and open-vocabulary settings complicate the task considerably and demand scalable solutions.</div>  

<div> Our model has no need to maintain a list of candidate values. Instead, all values are extracted from the dialog context on-the-fly.</div>
<div>
  A slot is filled by one of three copy mechanisms:
</div>

<div>
  (1) Span prediction may extract values directly from the user input;
</div>

<div>
  (2) a value may be copied from a system inform memory that keeps track of the system's inform operations;
</div>

<div>
  (3) a value may be copied over from a different slot that is already contained in the dialog state to resolve coreferences within and across domains
</div>

</p> 
<h1>Using the Bot(Below a bot deployed to Telegram querying the Google Maps API while chatting:)</h1>
<img src="https://raw.githubusercontent.com/deepmipt/DeepPavlov/f72397aa8391283475a88910e8f251a850767df8/examples/img/trippy_telegram.jpg">

<h1>Future</h1>
In future we hope to design a bot which tokenizes the input string not based on previous utterances but based on the current utterance.
In doing so we initially will have lesser accuracy but eventually we can achieve greater accuracy by supervised training.
Every time the bot predicts a irrelevant prediction adhere to the context we will try give the bot a negative feeedback and viceversa.
By doing so the bot keeps on learning and it's accuracy increases.
Although switching to a generative mechanism, while retaining high predictability will be a key challenge to embed conversational AI into more business settings.
