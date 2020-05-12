# DnD-Item-Generator
Module using the python3 module textgenrnn architecture, the D&amp;D item generator can generate new magical items based on the current list of 5th edition magical items.


textgenrnn is from https://github.com/minimaxir/textgenrnn and is a Python 3 module on top of [Keras](https://github.com/fchollet/keras)/[TensorFlow](https://www.tensorflow.org) for creating [char-rnn](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)s, with many cool features.

The training was performed using googles [Colaboratory Notebook], using the following file: https://drive.google.com/file/d/1mMKGnVxirJnqDViH7BDJxFqWrsXlPSoK/view?usp=sharing)!
Save this to your google docs if you want to try editing and running it yourself.

## Examples

```python
from textgenrnn import textgenrnn

textgen = textgenrnn()
textgen.generate()
```

```text
[Spoiler] Anyone else find this post and their person that was a little more than I really like the Star Wars in the fire or health and posting a personal house of the 2016 Letter for the game in a report of my backyard.
```

The included model can easily be trained on new texts, and can generate appropriate text *even after a single pass of the input data*.

```python
textgen.train_from_file('hacker_news_2000.txt', num_epochs=1)
textgen.generate()
```

```text
Project State Project Firefox
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
