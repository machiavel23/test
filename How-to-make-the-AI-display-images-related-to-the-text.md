================================================================

**Only functional way of doing this at this moment**

================================================================

>#### Image displaying features
>Should be easy to implement in your version of the game.
>
>https://github.com/MegAnon-code/image_splat

***

>#### How to use it
>**"\image_gen"** toggles generation on / off
>
>**"\image_samples"** sets the batch size for how many images you want the game to select from for a given noun phrase
>
>**"\image_flavour"** lets you describe the type of image you want e.g. 'art' (default) or 'photo' , 'anime' 'porn' or whatever else you can think of.
>
>**"\image_format"** choose between some common image formats. If you choose 'gif' the game will display animated gifs (This was a bitch to get working using pyglet).
>
>Combine these and you should get what you want, for the most part.
>
>But lets face it, **"\image_format gif + \image_flavour porn"** is basically all people are interested in.
>
>**Clarification**: typing "\image_samples" and then "5" won't give you 5 separate images per phrase, it'll just give you one, but picked at random from a sample of 5.
>
>There are works on getting the noun phrases to pick up things like 'The Scary Dragon sprays fire' and convert it into what would normally have to be detected from "scary dragon fire spray", so watch the GitHub.

***

>#### How it works 
>Detects noun phrases 'Scary dragon', 'Powerful wizard' etc, in your actions (ideally this would happen for AI responses too, but it's rarely descriptive enough for the NLP model to detect a 'noun phrase', so probably not), and scrapes related images off the internet, and displays them.
>
>The game literally reads your most recent action, and then if there's anything particularly well described in it, it pops up a window displaying some art of that thing (it literally Google Image searches 'art of [that thing]'). It downloads whatever image it finds first into a tempfile, displays it, and then deletes the file.
>
>**By default it scrapes from google**, although it's easy enough to tinker with the code to get it to scrape from wherever (just look at the documentation for google_images_download, you can literally change one parameter to get it to scrape from a particular website instead.)
>
>There's no content filter on it, so even without changing the website you're scraping, you can just change image_flavour to whatever genre of image you're looking for. You could even do something like 'elf r34' as the flavour, if you wanted.
>
>Sites like "https://yandex.com/images" could work better. This can be done changing the url.
>
>There seems to be only one issue so far (something about permissions not being granted and not being able to reach a resource) that happens once in a blue moon. It doesn't crash the game, you can just press enter and the '>' will come up as normal.
>
>Just be aware that if this happens, the scraped images might not have been properly deleted from the 'contextimages' folder that gets created. It might be worthwhile to add a line into your "play.py" file that wipes everything from this folder, and deletes it, just in case. (Else if you're generating smut images, you might very very slowly end up accumulating smut on your drive. As said, this seemed to happen only once in like 5 hour of playtesting it).

================================================================

**Ideas** to make the game use images according to displayed text

================================================================

>AI detects certain keywords in the text (i.e. goblin)
>
>Scours a booru for lewd goblin pictures under 500KB
>
>Runs them through https://manytools.org/hacker-tools/convert-images-to-ascii-art/
>
>Automatically use the functions “color” and “invert”
>
>Delivers them in the text

***

>The ASCII images would need to be 72 letters per row otherwise it will start a new line and the picture will look noting like it’s supposed to, but the low numbers of letters per image means there is less details that will be render out (this could potentially be fixed with good zooming on face/body but that’s another layer of complications).

***

>Another comment:
>
>Unless all the pictures are using greyscale only and have monochrome background the script will only output and nonsense diarrhea of text. I think it would be simpler to do what “Infinite Story” did and have a list of premade drawings, so everything is made in same style and format, but that would require at least hundreds of drawing at minimum with all kind of combinations.

***

>Other sites that might work:
>
>https://aiartists.org/ai-generated-art-tools
>
>https://github.com/jamesli1618/Obj-GAN (Too slow to load, worse than “manytools.org”)
>
>http://www.webestools.com/ascii-art-image-generator-converter-img2ascii-code-free-ascii-art-generator-image2ascii.html

***

>There are a number of tools to convert images to a text format. It really depends what your terminal supports. w3m-img does full resolution photos. Pic related (https://i.ibb.co/6gftZv5/1577845985568.png) is chafa which I used to make the clover logo and it does full color but blocky pixels that work on older terminals. And really shitty terminals can't be relied on to render color at all. At the very least you can get a lot more resolution if you allow some unicode characters.

================================================================

**Further ideas**

================================================================

>#### About the images... how about some old school folders/characters/monsters/goblin1, goblin2, golbin3.
>So that people can add their own pictures sets.
>
>Want a Warcraft setting? Add Tauren1, Tauren2, Tauren3 and so on. You can build virtually anything. Perhaps a clearer mind can come up with a better idea.
>
>This could be done either with a already loaded to the game custom set of images, or with specific sites/words that the script would use while searching.
>
>But this idea could only be implemented if you played a specific setting and you ALSO played with low temperatures, to ensure the AI doesn't go nuts with the randomness.
>
>Otherwise you could start a Morrowind setting, the images would load as the setting fits the searchable words, but then the AI could throw you into a scifi tier setting and the script wouldn't work anymore now for the most part, as the words that would appear probably wouldn't cointain the original setting common ones.
>
>That's why a general script would have to be made too (like the one done above).
>
>Having an option to disable pictures would be a lifechanger for a lot of people, as it wouldn't be pleasant if the AI would search for the word "scat" if it appeared on screen.
>
>This makes a tag system the only viable alternative if we want to avoid that kind of situations. Maybe have the tags separated between "Porn/Fetish related" and "Generic" categories, that the user could choose from a menu.
>
>Obviously, a function to toggle "enable pics/disable pics" should be put in place, as some people just enjoy text and prefer to imagine the whole thing.