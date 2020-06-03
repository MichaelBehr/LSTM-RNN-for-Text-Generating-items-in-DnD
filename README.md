# DnD-Item-Generator
This is a module that applies the python3 module textgenrnn RNN architecture and trains it on an expansive list of magical items from the 5th edition of Dungeons and Dragons. The D&amp;D item generator can generate new magical items based on the current list of 5th edition magical items.


textgenrnn is from https://github.com/minimaxir/textgenrnn and is a Python 3 module on top of [Keras](https://github.com/fchollet/keras)/[TensorFlow](https://www.tensorflow.org) for creating [char-rnn](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)s, with many cool features.

Initial training was performed using googles [Colaboratory Notebook], using the following file: https://drive.google.com/file/d/1mMKGnVxirJnqDViH7BDJxFqWrsXlPSoK/view?usp=sharing)! This is thanks to Max Woolf for setting up this easy to use tutorial. Save this to your google docs if you want to try editing and running it yourself.

## Web Scraping
Data was scraped from the website: http://5e.d20srd.org/srd/magicItems/magicItemsAToZ.htm?fbclid=IwAR1QJrUpmuAGb-YHA3xvtCv5vASRvIi7UsSLA-z9AzCa5VwWgaCOZhfopHk using the Python3 modules Pandas, and Beautiful soup. Data was then gathered into a spreadsheet and made ready for the data cleaning procedure. This spreadsheet is included as the file: "D&D Items.xlsx" in the root directory.

## Data Cleaning
The spreadsheet initially contained missing descriptions, weights and values for many of the items. Going through it, I added information that was missing by cross-referencing it with official D&D 5e website https://www.dndbeyond.com/magic-items. Any missing text descriptions, I filled in with "This function is self-explanatory." This only ended up being less than 150 entries or less than 10% of the total item list. For future improvements I would suggest adding invidualized descriptions for each item to improve training data quality.

I also added labels for each item, and a space between each item in order to help provide pattern structure for the RNN to learn. The cleaned spreadsheet can be seen under "D&D Items Annotated.xlsx"

## Saving as Text File
After the excel sheet was cleaned, it was converted into a text file by use of: 
```
1. File
2. Saveas 
3. Save as tab delimited text file.
```
Once it was saved as a tab delimited file, I used the Find and replace functionality to find each tab and replace it with a newline. This created a text file where each magical item was separated from each other by 2 newlinecharacters. Once this was done, I performed further cleaning by using regex to detect errors and use Find and Replace to fix them. For example, there was multiple errors throughout where there would be no space after a period. This was detected easily through Python regex and was able to be fixed (by adding a space after the period). I did similar general detection patterns for common errors in the text file, but was required to also manually scan the file for more unique problems. Additionally, I made sure to make each property in the text have its own newline. For example, the versatile property would have its own newline.  Overall the item list should be more standardized and error free.

## Running Textgenrnn
With our newly cleaned data we can then train our LSTM RNN model on the dataset. Using the textgenrnn architecture and tutorial on google's colaboratory notebook (credit to Max Woolf), we can upload our data and follow the steps to build and train our model. The advantage of colaboratory is access to GPU acceleration for the training, greatly speeding up the time for the model completion.

If you prefer running your models on local hardware, the scripts to do so are included.

To recreate the model on your own computer, after installing textgenrnn and TensorFlow, you can create a Python script with:

```
from textgenrnn import textgenrnn
textgen = textgenrnn(weights_path='colaboratory_weights.hdf5',
                       vocab_path='colaboratory_vocab.json',
                       config_path='colaboratory_config.json')
                       
textgen.generate_samples(max_gen_length=1000)
textgen.generate_to_file('textgenrnn_texts.txt', max_gen_length=1000)
```


## Model Parameter Changes
To improve the D&D item generator performance, we employed tuning using model validation. Parameter changes are as follows:

```
1. RNN layers = 5
2. RNN bi-directional = True
3. Max_Lenght of Character Vector = 40
4. Num_epochs = 20 -> any longer and you overfit
5. Train_size = 0.8
6. Validation = True
7. Dropout = 0.5 -> helps generalize the model
```

## Actual Item Examples:

Depending on the training parameters, the generated item results can widely vary. Training the LSTM at a word level preserves much of the magical item structure, but is less flexible when creating items. In contrast training on a character level has increased flexibility but also includes a larger amount of unusuable generations (including many humorous examples!). 

### Original Format:
![Staff of Woodlands](https://github.com/MichaelBehr/LSTM-RNN-for-Text-Generating-items-in-DnD/blob/master/Pictures/woodlands.PNG)
![Staff of Withering](https://github.com/MichaelBehr/LSTM-RNN-for-Text-Generating-items-in-DnD/blob/master/Pictures/staffwithering.PNG)


### Text Reformatted:

```
Name: Staff of the Woodlands
Rarity: rare
Type: staff simple weapon melee weapon
Attunement: Yes by a druid
Weight: 4 lb.
Value: 
Description: This staff can be wielded as a magic quarterstaff that grants a +2 bonus to attack and damage rolls made with it. While holding it you have a +2 bonus to spell attack rolls. The staff has 10 charges for the following properties. It regains 1d6 + 4 expended charges daily at dawn. If you expend the last charge roll a d20. On a 1, the staff loses its properties and becomes a nonmagical quarterstaff.
Spells: You can use an action to expend 1 or more of the staff's charges to cast one of the following spells from it using your spell save DC: animal friendship (1 charge) awaken (5 charges) barkskin (2 charges) locate animals or plants (2 charges) speak with animals (1 charge) speak with plants (3 charges) or wall of thorns (6 charges). You can also use an action to cast the pass without trace spell from the staff without using any charges. 
Tree Form: You can use an action to plant one end of the staff in fertile earth and expend 1 charge to transform the staff into a healthy tree. The tree is 60 feet tall and has a 5-foot-diameter trunk and its branches at the top spread out in a 20-foot radius. The tree appears ordinary but radiates a faint aura of transmutation magic if targeted by detect magic. While touching the tree and using another action to speak its command word you return the staff to its normal form. Any creature in the tree falls when it reverts to a staff 
Versatile: This weapon can be used with one or two hands. A damage value in parentheses appears with the property—the damage when the weapon is used with two hands to make a melee attack.
```

```
Name: Staff of Withering
Rarity: rare
Type: staff simple weapon melee weapon
Attunement: Yes by a cleric druid or warlock
Weight: 4 lb.
Value: 
Description: This staff has 3 charges and regains 1d3 expended charges daily at dawn. The staff can be wielded as a magic quarterstaff. On a hit it deals damage as a normal quarterstaff and you can expend 1 charge to deal an extra 2d10 necrotic damage to the target. In addition the target must succeed on a DC 15 Constitution saving throw or have disadvantage for 1 hour on any ability check or saving throw that uses Strength or Constitution 
Versatile: This weapon can be used with one or two hands. A damage value in parentheses appears with the property—the damage when the weapon is used with two hands to make a melee attack.
```

## Generated Items Examples:

Depending on the training parameters, the generated item results can widely vary. Training the LSTM at a word level preserves much of the magical item structure, but is less flexible when creating items. In contrast training on a character level has increased flexibility but also includes a larger amount of unusuable generations (including many humorous examples!). In both cases, the results must be filtered through. Eventually, I will implement a scoring metric for the results in order to better select answers.

### Word Level Examples:

```
name : staff of birdcalls
rarity : rare
type : staff simple weapon melee weapon
attunement : yes by a druid sorcerer warlock or wizard
weight : 4 lb .
value :
description : this staff has 10 charges . while holding it you can use an action to expend 1 of its charges and create orchestral music on a creature . once used this property can't be used again until the next dawn. The wearer has disadvantage on stealth ( dexterity ) checks.

name : mind lash
rarity : rare
type : melee weapon
attunement : yes by a mind flayer
weight : 3 lb .
value :
description : this longsword has a flanged head and it functions as a magic mace that grants a + 3 bonus to attack and damage rolls made with this sword . in addition while you hold the sword you can use your reaction to make one melee attack with it against any creature in your reach that deals damage to you . you have advantage on the attack roll and any damage dealt with this special attack ignores any damage immunity or resistance the target has
versatile : this weapon can be used with one or two hands . a damage value in parentheses appears with the propertythe damage when the weapon is used with two hands to make a melee attack .
```

### Char Level Examples:

```
Nessurplecal Three
Rarity: none
Type: treasure
Attunement: No
Weight: 
Value: 100 gp
Description: A translucent ruby with electrum ability. The flames last until you use a bonus action to speak the command word again while touching it. When the creature becomes a figurine again its property can't b.

name: Sword of Wounditing Wfthen
Rarity: rare
Type: wondrous item
Attunement: No
Weight: 
Value: 
Description: This bullseye lantern common and poisoned. The poisoned condition for 1 hour.
```

## Future Steps
```
1. Increase the item list as new items are released with new material.
2. Improve dataset quality and structure: Organizing it differently may yield performance increases.
3. Train multiple models on different item rarities. More complex magical items skew the training model and perhaps should be separated for increased quality of text generation.
4. Implement a validation metric for the generated text.
```

## Maintainer/Creator

Michael Behr, michaelbehr13@gmail.com

## Credits

Andrej Karpathy for the original proposal of the char-rnn via the blog post [The Unreasonable Effectiveness of Recurrent Neural Networks](http://karpathy.github.io/2015/05/21/rnn-effectiveness/).

[Daniel Grijalva](https://github.com/Juanets) for [contributing](https://github.com/minimaxir/textgenrnn/pull/52) an interactive mode.

Max Woolf for textgenrnn providing the network architecture and entire model basis: https://github.com/minimaxir/textgenrnn. Max Woolf ([@minimaxir](http://minimaxir.com))

## License

MIT

Attention-layer code used from [DeepMoji](https://github.com/bfelbo/DeepMoji) (MIT Licensed)
