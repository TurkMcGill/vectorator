# vectorator
*Quick disclaimers... I'm new to the Vector SDK, new to Python, new to github. If I'm doing something wrong, or if you see problems in my code, please let me know! Also, Vectorator is likely buggy and I haven't finished fine-tuning the timings -- though you can tweak these as much as you like by downloading and editing the dialogue.csv file. Instructions below.*

I wanted to add more actions/reactions to Vector, but without Anki's tools this would be extremely difficult and time-consuming. Much easier, is making Vector talk! So that is the origins of my new program. (Vector + orator = Vectorator). I have written hundreds of lines of random dialogue, and edited nearly a thousand joke and "fact of the day" files. In addition, every morning Vector will tell you the news and your local weather! (You have to enter your city and region names in the config.py file.)

I went through and documented a lot of my code this morning, but I'll provide some additional instructions below:

### Editing Vector's "dialogue"
When the program runs it downloads a file called dialogue.csv from my website. If you copy this file to the same folder as the program, Vectorator will use it instead of the downloaded version. The file is here: http://cuttergames.com/vector/dialogue.csv

The first column (NAME), contains event/trigger names. 

The second column (LINES), is how many random lines of dialogue there are for that name. You can add as many lines as you like, and you can leave lines blank, but make sure this number is correct.

The third and fourth columns (INT_LOW and INT_HIGH) are the number of seconds Vector will wait before responding to that event/trigger again. The program picks the value at random, between the low and high values.

The fifth column (NORMAL) is Vector's mood. If I continue to work on the program I'd like to add moods like: playful, angry, sad, afraid, etc. Those new moods will appear in the following columns.

**Words in Curly Braces:**

You will notice that some lines of dialogue have words enclosed in curly braces. If my program detects the word "{name}" then it will check to see if Vector has recently seen a named human and use it in place of "{name}". If he has NOT seen anyone in the last few seconds, then I replace "{name}" with a null string. This seems to work pretty well. The robot will either say, "Hey John, here is an interesting fact." Or he will say, "Hey , here is an interesting fact." They both sound good.

The other words in curly brackets: "{good}", "{weird}", "{interesting}" and "{scary}" get randomly replaced with synonyms in order to add some more randomness. You can ONLY use: good, weird, interesting, and scary. I haven't tested it much but you should be able to use more than one in a line of dialogue, though be aware that if you use "{scary}" twice it will pick the same word both times.

IMPORTANT NOTE: My program picks lines of dialogue with biased random numbers. The first few lines will get repeated a LOT, while other lines won't get said nearly as often. If there are 10 lines of dialogue, the odds of Vector saying #10 is less than 1%. So if you write your own dialogue for Vector, be sure to put the generic lines in the beginning.

### Add Your Own Jokes! ###
Like the dialogue.csv file, my program downloads "jokes.txt" from my website, but you can have a local copy and Vectorator will use that instead. The file is here: http://cuttergames.com/vector/jokes.txt 

Be aware that I have added a lot of commas and purposely mispelled some words, in an effort to make Vector more understandable. (I also slow down his speech a little bit.) One example is that Vector can't pronounce "Cozmo" -- so I have to spell it "Kawzmo".

### Change the Random Facts or Add New Ones ###
You can also download the facts.txt file I use and make changes to it. It's available here: http://cuttergames.com/vector/facts.txt

I have edited this file, too, but I have not heard Vector try to say everything, so there could still be some mispronunciations or words that are hard to understand.

### Editing the config file
You will need to enter your city and state/region to get weather forecasts. The API I'm using doesn't seem to be especially great, but perhaps the accuracy is somewhat location dependent.

For the temperature, enter either "farenheit" or "celsius". With the former you will also get wind speeds in miles-per-hour, while the latter will give kilometers-per-hour results. (I hope this works, I just realized that I only tested "farenheit".)

The chattiness setting (1 to 10) affects the INT_LOW and INT_HIGH values above. If INT_LOW is 1000 and chattiness is "5" then INT_LOW remains 1000. But if chattiness is at "6" then INT_LOW changes to 800. 

Be aware that any changes to chattiness might not be noticed right away, because I am saving time stamps every time Vector says anything. In other words, once Vector tells a joke he saves a timestamp that won't allow him to tell another joke until, say, 4:45. So changing Chattiness won't have any impact. You can get around this by deleting the timestamps.csv file. If my code doesn't find this file it creates a new one with fresh times.
