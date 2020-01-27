| Warning |
| :---: |
| <img width="64" src="https://user-images.githubusercontent.com/58800629/72772951-4b4ad880-3be4-11ea-9d7c-2616a7d91a7e.png"> |
| You **cannot** use tensorflow models with Clover Edition or (inversely) PyTorch models with the base game and thadunge2, as the engines aren't build around them respectively. If you try to do so, it will inmediatly throw you an error and it won't work. |
| You **have to** use the corresponding models depending on the game version you use.<br> So to use tensorflow models in Clover Edition you have to either:<br> **Grab the model** already converted to PyTorch by other Anons, like the ones [here](https://mega.nz/#F!4e5kRCIB!v7q0ItVjhhGcIqfZOZy9yA).<br> **Convert the tensorflow model to PyTorch** by using the tool designed for that [here](https://github.com/cloveranon/Clover-Edition#converting-tensorflow-model-to-pytorch). |

# How to use custom models
Steps to use different models (be them either tensorflow or PyTorch ones) other than the default vanilla one:

**WARNING**: always make backup copies before replacing files.

**Colab** 
1) Download your desired model.
2) Upload said model to your Google Drive account (this may take a good ammount of time depending on your upload speed).
2) Place your new model's folder inside \"game folder"\generator\gpt2\models\
3) Select the model you want to use when starting the game.

**Offline**
1) Download your desired model.
2) Place your new model's folder inside \"game folder"\generator\gpt2\models\
3) Select the model you want to use when starting the game.
4) **Take into account** that depending on the complexity/quality of the model in question it will take higher/lower specs to run it **offline** (a 774M model requires half of the processing power of a 1558M one, etc.), the other factor being whether it is build around tensorflow or PyTorch.

================================================================

                                         MOST IMPORTANT LINKS

================================================================

> [Trained models made by Anons](https://mega.nz/#F!51ED1CSA!YbifAmboqSLCrr3Y78axqw).

> [Contact link to upload models to the Mega](https://mega.nz/C!NhMmlYoC).

> [Vanilla GPT-2 models + 2 CYOA data](https://mega.nz/#F!U8QA0KCC!CY3GCnavOfNz18clY1lBgA) (the original and the lewd one posted by an Anon) and the base game AI Dungeon model_v5 you get from the torrent just as a back up.

> [Some of the models made by Anons that were converted to PyTorch](https://mega.nz/#F!4e5kRCIB!v7q0ItVjhhGcIqfZOZy9yA).

> [CloverAnon datasets page](https://github.com/cloveranon/Clover-Edition/blob/master/DATASETS.md).



================================================================

                                           SECUNDARY LINKS

================================================================

Possible sites / things to fine-tune the AI with:

Porn related:

> [Here](https://mega.nz/#!Y6ozAQQb!MjTI68j3kChkOkNDtEDOqDWnBOAcTCYkws4SjbPeoVQ) is 280 MB (~60M words) of erotic fanfiction that can be fed as training/fine-tuning data; cleaned, formatted and tagged to the best of my abilities.

> Models trained on HTTYD, Spyro Fanfics, some weird smut with dragons, some beast stuff and Overlord:
[Dragon model v1.0](https://mega.nz/#!4N10nSiA!4mLFFn2thmNIqtGPOCcXHHOauM12blCb32cIaO67jok)
Reccomendations:
Set timeout to 240 or 380.
Do not use word slit. It'll hang for a long ass time and break. Just trust me.
That model wasn't trained that long with 1558M, so it'll either shit out gold or will give you cancer. Have fun and don't forget to make backups of your original models. It was trained on 250 steps with batch size of 4 only.
[Dragon model v2.0](https://mega.nz/#!UV82wShY!ABqkN71e-ClQP7ivKGLJ9OiPtqH4CkFeQYPVuV_ytOs)
It might work better for some. But might work worse for some. I know my older one was better for sure at doing what I want.

> [5MB of curated and formatted smut CYOA](https://www.mediafire.com/file/9ggqahtg1srgw4l/New_CYOA.txt/file), a mix of fantasy and modern with many different fetishes. Taken from CYOA sex stories. Lots of non-sexual events, battles, fights, magic, world building, and other nonsense mixed in with sexual fun. 90% fantasy and 10% modern. Might make a good addition to someone's smut training file.

================================================================

Other sites / non porn related things:

> [Almost 500MB of (nearly entirely) properly formatted CYOA data](https://mega.nz/#!G8AQkITS!V3UbE6Fju-ByZ6ShGqV-0o1BgUHfUdWvP7H3_d5PKKw), including a fair amount of lewd stuff (taken from http://editthis.info/create_your_own_story/, all the stories from the site into a .txt) (this data is unusable due to bad formatting).

> Example of a formated text an Anon made (not proofreaded): https://pastebin.com/tFh0jhpX

> [Grimoires in the /x/ occult magic general](https://mega.nz/#F!gwNBRAzS!mkAUO0OBTbZ8gXVQkRXsqQ).


================================================================

        IDEAS, SITES, NON-DIRECT DOWNLOAD LINKS AND OTHER RANDOM THINGS COMPLETELY UNSORTED

================================================================

Possible sites / things to fine-tune the AI with:

Porn related:

> Back when I was into text adventures I remember there were groups for "Adult Interactive Fiction" (AIF), I wonder if the text from these games can be extracted and fed into the algorithm: http://www.ifwiki.org/index.php/Category:Porn/Erotica

> https://www.literotica.com

> http://textfiles.com/sex/EROTICA/

> asstr.org

> https://mcstories.com/

> https://editthis.info/create_your_own_story/All_Adult_Stories

> Flexible Survival

> Grey Archive

> Marjorie's Bedtime Stories

> http://old.bearchive.com/~addventure/game1/

> Miranda scenes from Fall of Eden

================================================================

Other sites / non porn related things:

> Look into "Elliquiy". Kind of a pain in the ass to get into, requires an application. Once in, there are many years worth of pretty hardcore forum-based roleplaying and collaborative writing. Much of it very dirty and a lot of it based in a variety of fandoms. The catch is that it's all in forum posts and not properly archived. But if I could pick one source to train the AI on, it would be Elliquiy just for the sheer amount of stuff it has.

> I found this Reddit post of someone who apparently archived 400GB of fanfic.net stories: https://www.reddit.com/r/FanFiction/comments/3jlene/i_archived_nearly_every_story_on_ffnet/
Training on this would make the AI an expert at popular fictional universes. I imagine most of it is pretty low quality though. Got to weed out the shit. Half of it is literally shit that best thrown in the trash.

> https://archiveofourown.org/

> Logs from /vg/station SS13 server

> [A web archive of the BIONICLE legend](http://wallofhistory.com/), compiled and presented in an easy-to-read format,

> Easy literature database to scrape: gutenberg.org

> Lord of the Mysteries

> There is a good CYOA series called "Endless Quest".

> [Site which collects every piece of Elder Scrolls lore](https://www.imperial-library.info/).

> Pathfinder books.

> About "gamerules" being incorporated into the training data, this site could be useful: http://textfiles.com/rpg/

>  [A novelization of Planescape: Torment](http://discogenie.dyndns.org/planescape/) (written in first person, unfortunately).

>  [Some forums where you could find archived session replays](https://forum.rpg.net/index.php?forums/roleplaying-actual-play.68/).

> I think both Anais Nin and Bataille both wrote second person stories,

    > Idea (assuming the stories are of high quality):
    (1)  Decompile all stories made by Anons into training data (could use Regex to find common misspellings and fix them)
    (2)  Retrain models on Anons stories
    (3)  ????
    (4)  PROFIT
>
    > List of 2nd-person narrative books/stories that could be formatted:
    (1)  Juno Diaz, "Miss Lola"
    (2)  Lorrie Moore, Self-Help
    (3)  David Foster Wallace, Forever Overhead
    (4)  Eduoard Leve, Suicide
    (5)  Ron Butlin, The Sound of My Voice
    (6)  Andy Weir, The Egg
    (7)  Mohsin Hamid, How to Get Filthy Rich in Rising Asia (could potentially work)
    (8)  If on a winter's night a traveler (story with lots of 4th wall breaking)

> Tails Gets Trolled

> Slablands

> Pessoa's "Book of Disquiet"

    > Works from:
    (1)  Nabokov
    (2)  Michael Moorcock
    (3)  Stanislaw Lem
    (4)  Roger Zelazny
    (5)  Robert E. Howard
    (6)  Piers Anthony's The Incarnations of Immortality series

> For scraping Reddit: the r/subsimulatorgpt2 guys did just that and there's also a big archive of millions of reddit posts I think they used for training that can be downloaded as a ".zip".