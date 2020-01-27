<details>
<summary> Very Detailed Explanation </summary>﻿

#
#### (1) Temperature 
>Temperature is basically a degree of randomness in the AI's predictions.
>
>Lower temps provides smoother, more extensive dialogue (also makes the AI responses come slower). While higher temps increase the randomness of the AI (also makes the AI responses come a little faster). 
>
>For example:
>
>- In the original unmodded base game, a sex scene would be over in a single reply or two. But with a lower temperature the game would take a much smoother, more realistic pace.
>
>A temperature of 1 means "real-life" **(random)** probabilities for the next word.
>
>A temperature > 1 scales probabilities to make less-likely words more likely **(more random)**. i.e. the AI will more often use words that are unlikely in the context.
>
>A temperature < 1 will make less-likely words even less likely **(less random)**. i.e. the AI tends to use words it has seen a lot in real life training data.
>
>So a temperature of 0.4 with top_k of 20 will result in the AI considering only the top 20 words, then shifting probabilities to make the most likely (i.e. "stable") words even more likely to occur.
>
>[Example on how temperature changes the AI](https://github.com/VBPXKSMI/Open-CYOAI-Project/wiki/Example-on-how-temperature-changes-the-AI).

***

#### (2) "generate_num"
>The values "generate_num" is the number of tokens the model produces after each action.
>
>"top_p" is kinda like top_k but instead of taking one of top N samples, it removes samples with probability less than some cut off value.
>
>   * **OUTDATED**: I have not seem anyone messing with this values and I don't recommend doing so. Definetly leave top_p as it is (0.9 is the default, and is "supposed" to be the best).

***

#### (3) top_p
>Nucleus sampling (top_p_logits) in GPT-2 is bugged, it returns one less sample than it should be, unless it's only one sample or the cumulative probability at the last sample equals exactly top_p.
>
>It doesn't matter too much when the nucleus is distributed over many samples, but if, for example, the probabilities are [0.89,0.07,...] or alike (which is not uncommon) then it will cut all but the first sample so it makes the model less random and more repetitive. Also, nucleus sampling was supposed to be used instead of top_k sampling, not after it like GPT-2 folks did. What you need to get is that is better for the AI to use top_p instead of top_k, if you want to get different kind of stories. Bellow you have both more detailed info, and a way to mess with them if you are modding the game yourself (thadunge2 and CloverAnon modded versions already include them).
#
>#### What's nucleus sampling for us?
>It was meant as alternative to top_k sampling but the GPT-2 guys just put it on top of it when they learned about it. Here's a comparison of different sampling techniques from the original paper about nucleus sampling ([The Curious Case of Neural Text Degeneration](https://arxiv.org/abs/1904.09751)). It's worth a read, they talk about why neural networks devolve into repetition and stuff.
#
>#### Should we disable top_k and just use nucleus sampling then? (for the ones that try to mod the base game themselves)
>Leaving top_k with a high default value (40+) and letting players change top_p is for the best. For players that use low temperature, lowering top_p should provide better results compared to low top_k (less repetitions) but they'll have to find the sweet spot again.
#
>#### I understand top_k was the number of tokens that would be considered, whereas temperature modified the relative likelihood of each of the tokens being picked. Now that the method has changed, what exactly does top_p do?
>Considers as many tokens until their summed probabilities are >= top_p
>
    Assuming you have the following 5 tokens
    "said" - 0.4
    "looked" - 0.2
    "turned" - 0.2
    "laughed" - 0.1
    "and" - 0.05
    "whatever" - 0.05

    A top_p of 0.6 will consider "said" and "looked".
    A top_p of 0.9 will consider "said", "looked", "turned" and "laughed".
>
>Now, top_p is based on probabilities and is heavily influenced by temperature
>
    E.g. if your temperature is 0.0001, "said" will have a probability of like 0.99, so it'd be the only token considered.
>
>Conversely if your temperature is really high, all of your tokens have similar low probabilities, so top_p of 0.9 considers many more tokens.
>
>The point of top_p is that it makes no sense to always consider top_k amounts of tokens. There are contexts where only one follow-up word is extremely likely, so only that extremely likely word should be considered.
>
>**Basically, top_p is a new parameter to replace top_k. top_p varies from 0 to 1, with 1 being equal to top_k 50257 (max total number of tokens). Use small adjustments if you want to experiment.**
>
>See a comparison and more detailed info on top_k, top_p, etc., from the authors of the original paper [here](http://neuraldegen.com/).
#
>#### The top_p progreesion (compared to top_k), is of linear equivalence or more arcane?
>More arcane. top_k means taking one of top_k samples from the probability distribution, nucleus sampling is taking samples until cumulative probability is greater than or equal to top_p and then picking one of them.
#
>#### So, if you wanted to have a top_k equivalence of say about 80, what would you be aiming for in top_p? Following what you just said it would be 0.05 top_p, right?
>No, you didn't get it, it’s not that 1 top_p = 1600 top_k therefore ==> 80 top_k = 0.05 top_p.
>
>**It's NOT LINEARLY EQUIVALENT**. Actual top_p value would be around 0.925, 0.95 or 9.75. You will have to test it and find out.
#
>#### What are the recommended values that I can set to top_p then?
>Going below top_p 0.4 will probably not yield any good results. Anything over top_p 1 will be fundamentally the same as top_p 1, so never go over 1. Additionally, setting top_p to 1 will likely lead to completely incoherent sentences compared to even 0.99999 so always go bellow 1.
>
>Using top_p less than 0.7-0.8 is very dumb, using top_p less than 0.5 or greater than 0.999 is extremely dumb and if you want less randomness you should lower the temperature, and raise top_p if it repeats too much. Note that as top_p gets closer to 1, the model includes more and more samples (the difference between say 0.94 and 0.98 is more than between 0.90 and 0.94).
#
>#### Is there a good set of generation values (top_k=0, top_p=?, temp=?) which leads to good gameplay in all models?
>There is no universal solution for all models.
>
>If the AI is familiar with your context (i.e. had a lot of training data with your fetish) you want a low temperature with top_p = 0.9, if your fetish is underrepresented in the training data you want a higher temperature with top_p = 0.9 so you can at least hope for random success.    

***

#### (4) **OUTDATED**
>When the AI decides how to write, it looks at the past context and generates a list of words that would make sense given this context. Each word in this list has a probability of occurring in the current context, which it learned from the training data.
>
>It then orders this list of possible-words from most-likely to least-likely. Then, it cuts off the list after top_k entries. So if top_k is one, it will only consider the most-likely word. If top_k is 2, it will consider the two most like words. It then scales the probabilities by temperature.
>
>The AI model has various parameters you can adjust to define how it acts when generating text:
>
>Decreasing the temperature to ~0.2 and going with a top_k of 10 to 20 results in really stable results. No more falling asleep after vaguely looking at a girl, no random loud noises during sex, no sudden voices behind you.
>
>The AI pretty much stops trying to direct the story on its own and just goes with your prompts. Obviously it'll be up to you to direct the story then, but those settings are really nice if you just want the AI going along with your ERP.
</details>

***

#### **tl; dr**
>high temp - for asspulls.
>
>less temp - less random shit.
>
>top_p close to 0 = less creative AI
>
>top_p close to 1 = more random AI
>
>But just go with 0.9 (default) as top_p (because is difficult to manage), and control randomness via temperature

***

#### **Summary**
>Temp and tpo_p summary (vastly changes how the AI behaves and responds) (you have to change them at the start of each new game in the modded version):
>
>0.40 / 0.9 is for highly random games, and where most epic OCs are made. Good for easy and low effort porn. (Default of the modded AI Dungeon 2)
>
>0.15 / 0.9 is for realism (best regarded by anons). Good for detailed porn.
>
>0.07 / 0.9 is for hardcore adventure. 0.07 is hard mode because variation is limited, you gotta build up a very solid, detailed and, most importantly, clean starting prompt and input good actions or it will loop you.

***

<details>
<summary> How to tweak this values </summary>

#
The easiest way for you to change this values is to use the offline version and mess with the files **(the modded versions already allows you to modify them in game by default, so they don't require further steps if you use them)**.

There are 2 ways to achieve that: an automatic and a manual one.

#### Automatic tweak code when starting the game
>This tweak allows you to set the values when you first run the game, so you don't have to keep going back and manually edit the source code.
>
>Just replace the block of old code (on your end) with the new one [here](https://github.com/VBPXKSMI/Open-CYOAI-Project/wiki/Automatic-tweak-code-when-starting-the-game), in play.py.
>
>It should look [like this](https://i.ibb.co/vVcwY10/1576056034833-tweak-for-different-temp-and-top-k-values-in-game.png).

***

#### Manual edits
>1) Go to generator\gpt2\gpt2_generator.py and edit it in notepad++, within it there's a line like this (around line 16):
>
    def __init__(self, generate_num=60, temperature=0.4, top_k=40, top_p=0.9):
>
>2) Edit temperature and top_k to your preference. 
>
>- Temperature: higher = more random, lower = it follows prompt more closely. 
>   * Lower top_k is a hard limit of "how many fitting words should the AI consider", i.e. lowering this value also limits the AI in creativity.
>
>- Dropping temperature from 0.4 to 0.2 adds loads of stability. Dropping that to 0.1 is even slower to diverge from prompt.
>
>3) If someone wishes to fix top_p_logits, the simplest way is to open generator/gpt2/src/sample.py, find the function top_p_logits(logits, p) and change:
>
    batch, _ = logits.shape.as_list()
>
>into
>
    batch, num = logits.shape.as_list()
>
>and
>
    tf.maximum(
    (X) tf.reduce_sum(tf.cast(cumulative_probs <= p, tf.int32), axis=-1) - 1, 0
    ),
>
>into
>
    tf.minimum(tf.reduce_sum(tf.cast(cumulative_probs < p, tf.int32), axis=-1), num)
>
>- (tf.minimum here is strictly to avoid returning invalid index if p > 1 or the cumulative probability over all samples is less than 1 because of rounding error)
</details>

***

<details>
<summary> MOSTLY OUTDATED SUMMARY (as top_k is not longer in use) </summary>

#### tl;dr
>high temp - for asspulls.
>
>less temp - less random shit.
>
>top_k is keyword amount per response
>
>less keys - less random shit
>
>atm 0.15/0.20 temp and top_k 20 is considered gold standard, specially if you are tired to revert all the fucking time.

***

#### Summary
>Temp and tpo_k summary (vastly changes how the AI behaves and responds) (you have to change them at the start of each new game in the modded version):
>
>0.40 / 40 is for highly random games, and where most epic OCs are made. Good for easy and low effort porn. (Default of the unmodded AI Dungeon 2)
>
>0.40 / 80 (default of the modded AI Dungeon 2)
>
>0.15 / 20 is for realism (best regarded by anons). Good for detailed porn.
>
>0.07 / 15 is for hardcore adventure. 0.07 is hard mode because variation is limited, you gotta build up a very solid, detailed and, most importantly, clean starting prompt and input good actions or it will loop you.
</details>

***

================================================================

This shit is probably not necessary, not really sure what it does (probably a template of the finished product after tampering successfully with the top_k and temp values):

>[Properly indented play.py with the set temperature command](https://github.com/VBPXKSMI/Open-CYOAI-Project/wiki/Properly-indented-play.py-with-the-set-temperature-command).