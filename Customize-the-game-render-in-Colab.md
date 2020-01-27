<a id="table-of-contents" />

<hr><details><summary><strong>Table of contents</strong></summary><hr>

+ [First things first](#first-things-first)
+ [Importing fonts](#importing-fonts)
+ [Font size, weight, and line height](#font-size-weight-and-line-height)
+ [Inputbox borders and width](#inputbox-borders-and-width)
+ [Playing with colors](#playing-with-colors)
</details>

<hr><a id="first-things-first" /><details><summary><strong>First things first</strong></summary><hr>

There are a few things to know before trying to customize the game render in Colab. Read this **CAREFULLY** if you don't want to be called a retard when you'll come whining because you screwed up something explained here. Honestly, most of all the customization is quite easy, most of the lines speak for themselves, and after one or two try, you should be able to fully master it.

1. You **must** do the changes **BEFORE** running the cell, not **WHILE** it's running.

2. If you wish to keep your changes, you **WILL HAVE TO** "save a copy in Drive". Otherwise, you'll lost your changes as soon as you refresh the page. And of course, you then run the game from your copy that has the changes.

3. The customization code is clearly compartimented between `# --- OUTPUT CUSTOMIZATION ---` and `# --- END OF CUSTOMIZATION ---`. If you touch anything outside of this block, without knowing what your doing, and come crying "muh broken halp", you will be mocked. And you know how "gentle" we are.

4. To activate a value, you need to remove the `//` at the beginning of the line value. To deactivate it, simply add `//` again at the line beginning. If the colors of the whole block changes, it means you commented or deleted something in `html {`, `body {`, `#output-area .stdin-widget {`, `pre {` or a `}`. In that case, don't drooling retard panic, and simply ctrl+z until it goes back to normal.

5. Finally, the code has inline comments to quickref you. They are between `/*` and `*/`, like this: `/* This is an inline comment */`. Those are supposed to always be green, and those are **NOT** supposed to be uncommented. They sometimes contains a link that you can ctrl+click to open it in a new tab.

[Back to TOC](#table-of-contents)
</details>

<hr><a id="importing-fonts" /><details><summary><strong>Importing fonts</strong></summary><hr>

>```css
>@import url('https://fonts.googleapis.com/css?family=Courgette&display=swap');
>@import url('https://fonts.googleapis.com/css?family=Cute+Font&display=swap');
>````
>````css
>--font-render: 'Courgette', cursive;
>--font-inputbox: 'Cute Font', cursive;
>````
>`//    font-family: var(--font-inputbox);`
>
>`//    font-family: var(--font-render);`

The first thing you will notice, is that there are 2 imports. Actually, you can only use one, if you wish to use the same font in the game render and the inputbox. But if you want to use 2 different fonts, then you'll obviously need 2 imports. Let's begin by importing a font. To do so, go [there](https://fonts.google.com/). You will arrive on something like this:

<details><summary>Website screenshot</summary><img src="https://i.ibb.co/s5LZQb0/googlefonts.jpg" /></details>

Choose a font on this (almost) infinite page, by clicking the <img src="https://i.ibb.co/J3VkZ8c/plus.jpg" alt="red +" /> on the top right corner of its tile. It will make it selected and will pop a bar at the bottom right of the screen:

<details><summary>Bar screenshot</summary><img src="https://i.ibb.co/ZzFSb4n/bar.jpg" /></details>

Now, expand the bar by clicking on it, and go in its "**CUSTOMIZE**" tab:

<details><summary>Expanded bar screenshot</summary><img src="https://i.ibb.co/3fWxjBQ/customizefont.jpg" /></details>

Make sure you select **at least** the `regular 400` (can also be just regular, or even normal, or even just the font name) and the `Latin` support. It's the mandatory default. You are free to also select the additional weights you might want to use. Now that you have selected the options you wish, go back to the "**EMBED**" tab, and go in `@import` sub-section. in the first grey cell, select and copy all that is between the `<style>` and `</style>` tags, like this:

<details><summary>@import code screenshot</summary><img src="https://i.ibb.co/NYpS5S5/importhighlight.jpg" /></details>

Then paste it in the cell to **REPLACE** one of the already existing `@import`:

`@import url('https://fonts.googleapis.com/css?family=Courgette&display=swap');`

becomes:

`@import url('https://fonts.googleapis.com/css?family=Gelasio:400,500,600,700&display=swap');`

The last thing you need to do to finalize your import is to set the variables to fit the new font. On Google font, look the second grey cell:

`font-family: 'Gelasio', serif;`

Select and copy `'Gelasio', serif;` and paste it in the cell like this:

`--font-render: 'Courgette', cursive;` becomes `--font-render: 'Gelasio', serif;` to change the game render font and

`--font-inputbox: 'Cute Font', cursive;` becomes `--font-inputbox: 'Gelasio', serif;` to change the inputbox font.

That's it, you have finished to import your font. To import a second font, deselect the first one on google fonts, then select another one and copy-paste again on the second `@import` line.

You can now activate your newly imported font by uncommenting the related line:

For the game render:

`//    font-family: var(--font-render);` becomes `    font-family: var(--font-render);`

And for the inputbox:

`//    font-family: var(--font-inputbox);` becomes `    font-family: var(--font-inputbox);`

You can run the cell to see your new font(s) in action!

[Back to TOC](#table-of-contents)
</details>

<hr><a id="font-size-weight-and-line-height" /><details><summary><strong>Font size, weight, and line height</strong></summary><hr>

>```css
>//    font-size: 14px;
>//    font-weight: 400;
>//    line-height: 1.24;
>```

So, the previous part was a bit tedious, but rest assured it's the only one, the rest of the customization is pretty easy. Let's start with the most obvious, `font-size: 14px`. Of course, you need to remove `//` first to activate it, and same goes for all the other values.

Just change the value `14` to the desired font size you want. You'll have to run the cell to see what it look like though. Here are a few font size to help you start:

<img src="https://i.ibb.co/QXtxgPR/fontsize.jpg" alt="fontsize" border="0" />

Ok, `font-size` is over, time to take a look at `font-weight.` OMG!! It's exactly the same principle, how lucky! there's one difference though, the increment. Actually, `font-weight` goes from 100 to 900 by increments of 100, meaning you can't set it to 368. It'll be 300 or 400. So it has only 9 possible values. The default font goes only to the "**bold**" state, but if you import a font containing different weight as seen in the previous part, you can achieve a "boldness" that suits your tastes!!

The last one is `line-height`. As the name suggest, it defines the height of a line (no shit sherlock...), but the interesting thing is that by changing the lines height, you change the **vertical space** between lines! I haven't tested it much, but there's two pics of it in action. Feel free to experiment! As usual, activate by removing `//`.

<details><summary>Default 1.24</summary><img src="https://i.ibb.co/cb4nwMV/lineheightdefault.jpg" /></details><details><summary>Set to 2.0</summary><img src="https://i.ibb.co/wdwPY3X/lineheight2-0.jpg" /></details>

I love pictures, it's so easy to express something with them. Anyway, we're done for that section. The next one will be a bit long, but not difficult at all. See you there anon!!

[Back to TOC](#table-of-contents)
</details>

<hr><a id="inputbox-borders-and-width" /><details><summary><strong>Inputbox borders and width</strong></summary><hr>

>```css
>    width: 90%;
>//    border: 3px ridge hsl(0, 100%, 100%);
>//    border-radius: 5px 20px 20px 5px;
>```

Now we're going to talk about the inputbox borders customization. First thing, we will avoid talking about `hsl()` for now, since it concerns colors and that has a dedicated section [here](#playing-with-colors). Now, let's examine what the `border:` parameter has. We notice a `3px` and a `ridge`. As always, activate by removing `//` at the beginning of the line.

The `3px` is simply the thickness of the border. It grows quite fast with each increment of 1 though, you'll probably don't want to go 10 by 10.

The `ridge` is actually the style of the border. There are a couple you can use to suit your tastes as depicted below. You can see them better by directly checking the source link provided. Just change `ridge` to whatever you like.

<details><summary>Borders styles</summary><img src="https://i.ibb.co/4SytxZz/borderstype.jpg" /><br><a href="https://codepen.io/geoffgraham/pen/gxvKbQ" target="_blank">Source</a></details>

The next value is `border-radius`, and its name is a bit misleading. It actually manages the **curvation** of the inputbox's **corners**. The values are in order **_TOP LEFT_**, **_TOP RIGHT_**, **_BOTTOM RIGHT_**, **_BOTTOM LEFT_**:

```
1---------2
|         |
4---------3
```

You can check [this page](https://css-tricks.com/almanac/properties/b/border-radius/) for a quick rundown on how it works, it also has a tool to test your desired values! How handy!

The default values given in the cell, `5px 20px 20px 5px;` gives a D-shape to the inputbox. If you set one of the corners to be `0px`, that corner won't curve at all.

That's all for the inputbox border customization for now. The last thing we didn't checked yet, `hsl()`, will be explained in the last part of this helper, so keep reading a bit.

[Back to TOC](#table-of-contents)
</details>

<hr><a id="playing-with-colors" /><details><summary><strong>Playing with colors</strong><hr></summary>

```css
//    background: hsl(0, 100%, 0%);
//    color: hsl(0, 100%, 100%);
//    border: 3px ridge hsl(0, 100%, 100%);
```
This last helper will explain you the basics of the color customization within the Colab. It's quite simple, and a simple tool will help you to get what you want. The colors use the hsl function, which is for _HUE_, _SATURATION_, and _LUMINOSITY_. The advantage of this formula is the ability to have a really precise control over the color you wish. Open [this tool](https://image-color.com/color-picker.html) in a new tab (screenshots come from there) and let's define each value.

hsl(**_0_**, 100%, 100%); The first value goes from 0 to 360, by increments of 1. It's the base color.
<details><summary>Top 0, bottom 360</summary><img src="https://i.ibb.co/V2TYtrn/spectrum.jpg" /></details>

hsl(0, **_100%_**, 100%); The saturation. The more you go near 0, the more faint is the color.
<details><summary>Top 100%, bottom 0%</summary><img src="https://i.ibb.co/Ks12J3Q/realsaturation.jpg" /></details>

hsl(0, 100%, **_100%_**); The luminosity. It control the darkness of the color.
<details><summary>Top 100%, bottom 0%</summary><img src="https://i.ibb.co/tm2jYzh/saturation.jpg" /></details>

With that, you should understand how to select the exact tint you want to color anything in the game (backgrounds, inputbox borders and texts). Choose your color with the selector on the right, define it precisely with the main picker, and copy-paste the resulting values!

<details><summary>These values</summary><img src="https://i.ibb.co/bHHmsXt/thiscode.jpg" /></details>

This concludes the colab customization helper. If you still have a problem, you can open an issue [here](https://github.com/VBPXKSMI/Open-CYOAI-Project/issues/new/choose) or ask in the thread.

[Back to TOC](#table-of-contents)
</details>