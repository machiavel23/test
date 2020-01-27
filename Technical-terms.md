## Not so basic info
>#### I came here of my own volition cause I seek knowledge. So let's start, what is a model?
>So you know the files your game has in one of its folders, the one named "models"? That's the game's brain.
>
>Basically it is a trained brain for the GPT-2 based programs (in other terms, the brain of the AI of your game).<br>
>The final result of training the AI on a given dataset, is the resulting "brain" that determines its behavior once its done learning.
>
>**In "simple" terms**: when you want to train the AI's "brain" you have the Machine Learning method you're using, a set of training data used to teach it, some way to check it's results (separate data, a competing AI, or a combination of the two), the resulting model, and whatever software you stick the model in. You basically make it try and understand fuckhuge datasets until it is better, more knowledgeable, coherent, etc.

***

>#### Understood. What is this GPT-2 thing then?
>**GPT-2** is a state-of-the-art transformer-based language model, trained on a dataset of a given number of web pages. Is trained with a simple objective in mind: predict the next word, given all of the previous words within some text. 
>- A **Transformer** is a deep machine learning model used primarily for language processing, and are designed to handle ordered sequences of data, such as natural language (like in web pages).<br>
>It is typically used for:
>   * machine translation
>   * document summarization
>   * natural-language generation (the use we are most interested in)
>   * named entity recognition
>   * speech recognition
>
>The folks over at [OpenAI](https://openai.com/) were the ones that released (and developed) these GPT-2 models. There are varying grades of complexities to these models.  
>Models are (ranked from least to most complex):
>- 124M (wrongly nicknamed 117M)
>- 355M (wrongly nicknamed 345M)
>- 774M
>- 1558M (the most complex one). 
>

***

>#### Ok, now I know what a model is and that GPT-2 is the "program" used to make the ones used in the game. But can you give a little more insight?
>The quick rundown version is that you break up huge volumes of text into formatted, paragraph-sized chunks and feed it to an AI blackbox and let it go to town.
>
>What you do is feed the AI a bunch of data and it responds based off that data, that's training. The creator of AI Dungeon finetuned the largest model (1558M) with 30MB of CYOA (Choose Your Own Adventure) data.
>
>Some Anons are trying to, and succeded in, finetuning new models based of different kinds of data. But training an AI takes a shitload of computing power. One Anon said that he rented a super computer for $100 to try and render one, but it turned out to not being so good because you gotta spend a shitload of time properly formatting your input and making sure the perspective of the AI stays consistent. Which formatting 8 million paragraphs of text would take more than 1 human lifetime. So not only the size of the model matters, the data quality matters as much if not even more.
>
>There is a "How to finetune models" Wiki page planned for the future, to be able to train your own models and (more importantly) contribute to the project, also it would cointain even more detailed info about the subject. But for the time being, your best bet at going at it is using one of the many guides that are over internet, e.g. [GPT-2-simple](https://github.com/minimaxir/gpt-2-simple) is an option to get started with the smaller models and see how it goes.
>
>Still, it's recommended that for now you try to contribute in other tasks, the most related one to training the AI being the formatting of the texts that are going to be used in the training.

***

>#### Got it, what about explaining what 355M, 774M, etc. mean?
>These are the sizes of the model (i.e. the number of "parameters" you have to tune... think of it analogously to "the number of neurons in the brain"). The base model finetuned by the original author had 1558M parameters (i.e. 1558 Million, or 1.5 Billion), which is the largest one. 
>
>If you were to use smaller models instead the game would require less processing power to run (e.g. the 774M uses half as much RAM as the 1558M one), but potentially at the cost of worse responses (especially with anything at or below 355M... where it's like talking with a schizophrenic).
>
>The 124M model was just made as proof of concept, while the 355M one is not that much better than it.<br>
>355M and lower are pointless for the game, as it doesn't matter how long you train them, their attention (i.e. how much they care about and "remember" your prompts) aren't good enough to get sane responses. So the really useful ones for the game are the 774M and 1558M models, which are orders of magnitude apart from the previous and from each other models.

***

>#### What does "training" mean? What is the difference with finetuning?
>First off: 
>- Training GPT-2 =/= Finetuning GPT-2
>
>Training can mean one of two things, and the meanings sometimes get confused. 
>
>**First meaning**: 
>
>The models themselves come pretrained (that's the "P" in GPT-2) with about 40GB of general text data. **Those models are already trained**, you can't train them again or you would have to train it again on those 40GB of data from scratch (which would take you a good amount of time). When you "train" those GPT-2 models, all you are doing is **finetuning** the already pretrained models, to give it some idea of the output tone and format you want (i.e. making it more specialised, more knowleadgded about certain topics, etc.).
>
>**Second meaning**:
>
>You can "train" (**actually finetune**) an AI model, which is like a base for the AI's vocabulary, writing style, flavor, etc., by feeding it metric shittons of texts and letting it process it for a few hours/days depending on how much you give it. This is how the models the game currently uses were made.
>
>To avoid confussion, the summary is:
>
>**"Training" refers exclusively to how the GPT-2 models are already pretrained, and the data they were already trained with**.
>
>**"Finetuning" refers exclusively to how those pretrained GPT-2 models are put though the process of "re-training" them again but not ditching the data they already have and just adding to them more data, and customazing them to how you would like them to perform in game**.
>
>So when one says "I trained a 774M model on 5MB data of dragon smut" what they mean and **should have said** instead is "I **finetuned** a 774M model on 5MB data of dragon smut".
>
>There is only one exception where you could say "How would I **train the AI**?" because you are refering to the AI and not the model itself. But you definetly cannot say "How would I ~train a model~?" because you would (most certainly) be refering to the **pretrained model**, which can only be **finetuned** unless you were to train it from scratch which you certainly are not gonna do.
>
>**To make it clear**:
>- Finetuning the existing GPT-2 model requires tens of MB of data and can be done in a day or two with a beefy computer.
>- Training a new model from scratch requires tens of GB of data and supercomputer time to do in any sort of reasonable time frame.
>
>Try to **always use the correct and proper meaning of these words**, as switching back and for between them will only confuse people unnecessarily.

***

>#### What does the data the AI was trained on mean?
>The data refers to the texts that you would have to feed the GPT-2 model to fine-tune the AI with. 
>
>Although you could technically feed it whatever text you wanted and it would "work", the AI then would result in nothing more than a glorified autocomplete machine, as it would be devoid of everything that makes it feel like a game. 
>
>So in order to addapt the AI to function (and feel) like a game, those texts **need to be formated** in a certain way (**in the second person**) or else the AI will throw inconsistencies (like switching gender, not recognizing which character did what, etc).
>
>Finding and collecting, but specially, formatting and curating high quality texts takes a good amount of time. Reason why it is such a big issue and we need Anons to undertake that task themselves, unless a way of doing it automatically was found (which doesn't seem likely at the moment).
>
>A "How to format the texts to feed the AI with" Wiki page is in progress, so that you can help to format those texts and contribute something to the project. But you already can start helping by collection texts and, when that page is ready, start formatting them.
>
>The original author did "considerably well" gathering his data but he could have done way better, reason why Anons are volunteering and taking up that task themselves.

***

>#### Well, that got confusing sometimes but I finally got it. Now, how would I go about using a different model for the game?
>You only have 3 options:
>- Training one yourself.
>- Finetuning a pretrained one.
>- Or using one the already finetuned models made by Anons.
>
>The first option is practically impossible to do alone.<br>
>The second one is feasible is you know what you are doing.<br>
>And the third one is by far the easiest one.<br>
>
>Where are located the finetuned models made by Anons will be discussed in the next section alongside how and where to play the game.