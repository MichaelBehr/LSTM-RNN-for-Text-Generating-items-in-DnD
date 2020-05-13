# DnD-Item-Generator
This is a module that applies the python3 module textgenrnn RNN architecture and trains it on an expansive list of magical items from the 5th edition of Dungeons and Dragons. The D&amp;D item generator can generate new magical items based on the current list of 5th edition magical items.


textgenrnn is from https://github.com/minimaxir/textgenrnn and is a Python 3 module on top of [Keras](https://github.com/fchollet/keras)/[TensorFlow](https://www.tensorflow.org) for creating [char-rnn](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)s, with many cool features.

The training was performed using googles [Colaboratory Notebook], using the following file: https://drive.google.com/file/d/1mMKGnVxirJnqDViH7BDJxFqWrsXlPSoK/view?usp=sharing)!
Save this to your google docs if you want to try editing and running it yourself.

## Web Scraping
Data was scraped from the website: http://5e.d20srd.org/srd/magicItems/magicItemsAToZ.htm?fbclid=IwAR1QJrUpmuAGb-YHA3xvtCv5vASRvIi7UsSLA-z9AzCa5VwWgaCOZhfopHk using the Python3 modules Pandas, and Beautiful soup. Data was then gathered into a spreadsheet and made ready for cleaning. The spreadsheet is included as the file: "D&D Items.xlsx"

## Data Cleaning

## Examples

Depending on the training parameters, the generated item results can widely vary. Training the LSTM at a word level preserves much of the magical item structure, but is less flexible when creating items. In contrast training on a character level has increased flexibility but also includes a larger amount of unusuable generations (including many humorous examples!). 

Word Level Examples:

```
name : staff of the woodlands
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

Char Level Examples

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




## Maintainer/Creator

Michael Behr, michaelbehr13@gmail.com

## Credits

Andrej Karpathy for the original proposal of the char-rnn via the blog post [The Unreasonable Effectiveness of Recurrent Neural Networks](http://karpathy.github.io/2015/05/21/rnn-effectiveness/).

[Daniel Grijalva](https://github.com/Juanets) for [contributing](https://github.com/minimaxir/textgenrnn/pull/52) an interactive mode.

Max Woolf for the network architecture and basis. Max Woolf ([@minimaxir](http://minimaxir.com))

## License

MIT

Attention-layer code used from [DeepMoji](https://github.com/bfelbo/DeepMoji) (MIT Licensed)
