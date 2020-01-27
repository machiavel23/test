Do you want to play on the most up to date (official) version of the game, change the temp and top_k values, and play on your own fork?
Just follow this steps:

1) Go [here](https://github.com/AIDungeon/AIDungeon/blob/master/AIDungeon_2.ipynb).

2) Fork it.

3) Then you just have to add this to the second cell:
>
    from IPython.display import Javascript
    display(Javascript('''google.colab.output.setIframeHeight(0, true, {maxHeight: 5000})'''))
    #make sure you change it again
    !sed -i "s/temperature=0.4/temperature=0.15/" /content/AIDungeon/generator/gpt2/gpt2_generator.py
    !sed -i "s/top_k=40/top_k=20/" /content/AIDungeon/generator/gpt2/gpt2_generator.py
    !python play.py

4) Play.