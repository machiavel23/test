There seems to be an error in the "print" command, it doesn't word wrap the output like the other generated texts. 

If you want to change that: 

1) Edit play.py below the code;

    "elif action == "print":"

2) And change:

    print(str(story_manager.story))

to

    console_print(str(story_manager.story))

If you want a fancier version, see [pic related](https://i.ibb.co/4ZB8VK4/1576037241369-fix-print-command.png). 

You can also enter a number to set the width you want.