# NFTGenerator: BitBirds NFT Generator

*******************************************************************************************

Author: Ali Toori, Full-Stack Python Developer, Bot-Builder.

Founder: https://boteaz.com

YouTube: https://youtube.com/@AliToori

Telegram: https://t.me/@AliToori
*******************************************************************************************

# Usage
Install the required packages by running the following command.
    
    pip install -r requirements.txt

Run the following command in terminal opened at the main folder.
    
    python BitBirdGenerator.py

# BitBirds generation script
# Intro
This is like grassroots and stuff. 

Specifically I'm asking you in good faith not to directly knock off the BitBirds project, or otherwise screw me over for sharing this. Do not use this for anything hateful or discriminatory.

There is a YouTube video walkthrough to complement this ReadMe [...Link...](https://youtu.be/vTxjLLHncMo).

# Setting the expectations
If you're new to programming you may struggle to set up the dependencies. If you're persistent, you can do it! I believe in you. 

Often in technology, setting up a pre-requisite like PIP (a python asset installation tool) isn't something the developer thinks about in a given project because it has been on their computer for months or years. 

Even having set up a number of dependencies just a few weeks ago for this project, I don't remember exactly how I worked through the various error messages. When you try to run the script, if it fails there will often be some useful nugget of information buried in the cryptic response blob. As a rule for life - Google is your friend, and others have probably encountered your exact error message. When asking questions on discord, stackoverflow, or wherever, say very specifically (1) what you've tried (2) what you expect as the result and (3) what issue/error you're encountering. That'll get a lot more useful feedback than just shouting HALP.

# Dependencies
The dependenices were all installed with the terminal/command line. There is documentation abound about terminal generally, and these tools specifically, but unfortunately I did not save copies of the web pages I used. From memory the things I needed to setup were:

- Python 3 (default on my mac was python 2.7)

- PIP - a command-line installation mechanism for python assets. 

IIRC I needed to use some special command with python 3 to use pip as an installation mechanism for the items below- perhaps `pip3 install ...` rather than `pip install ...`?

- Pillow - python library to generate images - installed via terminal/command-line with PIP

- NumPy - python library to work with arrays - installed via terminal/command-line with PIP

- I don't *think* I had to install the 'random' library (included in the script) to use the number-randomization feature, but might have.

If you encounter specific setup items I haven't mentioned here let me know, and I'll add them.

# How this script works
The YouTube video [video](https://youtu.be/vTxjLLHncMo) complements this overview. 

We are iterating through a 'loop' once for each bird. The loop starts with a 'seed number' that is used to deterministically generate pseudo-random numbers. I say 'deterministically' and 'pseudo-random' because from the same seed number the 'random' output will always be the same. It's not truly random in a security or mathematical sense. I used the most recent ETH block at the time as my seed number - 11981207.

There is then a 'chain' of additional random numbers generated that are used to define all of the various traits of the birds. Many of the attributes generate a random number between 1-1000 and use that for some sort of logical statement (e.g. to decide beak color). 

Interestingly, the way I've used this random-number chain seems to have resulted in some specific behavior and combinations that I can't yet personally explain. For example the way the bird type selection random number and beak color selection random number chain from one another seems to have resulted in no red-beaked woodpeckers. I also noticed that all of the four cockatoos generated seemed to have the exact same blue crest. Because I wanted more variety than that, in the minted NFTs I ran another batch of cockatoos and replaced the second, third, and fourth cockatoos in the original sequence with others that provided more variety. I made no other changes to the randomly generated set of birds, and if you run the script yourself (without changing the seed) you should see identical matches for each number. If you spot a pattern in why the random numbers behave in this way, I would love to discuss on twitter or discord.

- Head color and throat color are a random 1-255 number generated into each of the three RGB values in a color.
- Eye color looks at a random number between 1-1000 and if it's 47 or less, will give the bird crazy eyes. Crazy eyes always have the same pupil color (154, 0, 0) and then generate a random color for the 'white of the eye,' in the same way the head and throat color are generated.
- Beak color is determined by an evaluation of another 1-1000 'random' number. Grey is most common, gold is also common, red is rare, and black is very rare.

The bird images are 24x24 arrays of variables, representing every pixel in the final image. I've used variables with two letters for each type of pixel (e.g. outline `ol`, head color `hd`, beak color `bk`), so as to keep the 'matrix' of pixel variables easy to see and work with. If you zoom way out on the code you may even be able to see a rough picture of the birds in the code, just from the slight differences in the variables.

The script uses another 1-1000 'random' number to decide which of the bird type templates to use. Basic bird is most common, at about 75% probability. Jay has a 15% probability, woodpecker has 6%, eagle has 3.5%, and cockatoo has half a percent probability.

From there, you're just about home free. The final bit of the loop re-sizes the generated bird from 24x24 pixels up to 480x480 pixels. It generates the image file path (dynamically, wherever you have the folder using the `os` library), and saves the image into the included folder `bird_images`.

Then it goes right back to the top of the loop, and does it again for the next bird, until the number of defined loops is completed. 


