# python-diceware
An implementation of the Diceware passphrase generation technique as a single file written in Python.

License: GPLv3

All things considered, I've found the [diceware technique](http://world.std.com/~reinhold/diceware.html) of generating strong passphrases to be the most effective for generating passphrases that are memorable and useful.  There is already [one implementation](https://github.com/ulif/diceware) that I use for this purpose, but for my use case it has a couple of drawbacks:

* It's not cross-platform; I need it on more than just my Arch Linux box.
  * I can't put a copy up someplace public and grab it when I need it.
* The passphrases it generates are a little simplistic for my tastes.  A good practice is to sprinkle numbers in the generated passphrases and this one doesn't do that.  Sure, I can do that myself (and I do, in fact) but when I'm in a hurry it's not easy to pick numbers off the top of my head.
  * Plus, I can't just copy-and-paste them into a password manager for storage.

So, I wrote my own implementation of Diceware that requires neither a fistful of d6's or a [diceware wordlist](https://www.eff.org/deeplinks/2016/07/new-wordlists-random-passphrases) open in a text editor.  My utility has the entire Diceware wordlist incorporated into it and can generate passphrases of arbitrary complexity.  It requires no external dependencies, everything needed to run it is part of the base installation of Python v2.x 

```
[drwho@windbringer python-diceware]$ ./diceware.py --help
usage: diceware.py [-h] [--words WORDS] [--caps] [--numbers]
                   [--separator SEPARATOR] [--list-separators]
                   [--random-separator]

This is a utility which generates random passphrases using the Diceware
technique (http://world.std.com/~reinhold/diceware.html).

optional arguments:
  -h, --help            show this help message and exit
  --words WORDS         Default number of words to pick. Defaults to 5.
  --caps                Whether or not to capitalize the first letter of every
                        word. Defaults to false.
  --numbers             Whether or not to scatter random numbers in between
                        words, in the same fashion. The numbers will be no
                        longer than the number of dice rolled to generate
                        passphrases so that you don't have to remember a
                        passphrase as big as a PGP key. There will never be
                        more blocks of numbers than words in the passphrase.
                        For example, 111-foo-bar-222222-baz
  --separator SEPARATOR
                        Character to separate each word with. Defaults to none
                        (the words get squished together). Note that,
                        depending on the shell you use, you may have to escape
                        the separator you pick, e.g., \*
  --list-separators     List the word separators this utility can use.
  --random-separator    Randomly pick a separator character to use. This will
                        override a separator character you supply.
```

An example of how I use diceware.py to make passphrases:

`[drwho@windbringer python-diceware]$ ./diceware.py --caps --numbers --random-separator`

Some examples of the passphrases it generates:

* Varied-29-Darkness-Ability-Aware-Alabaster-9516
  * Bits of entropy: 227.5
* Scope!75699!Supper!10835!Expulsion!94!Grouped!Flaky!33
  * Bits of entropy: 249.4
* Unshackle)Lazily)97)Implosive)Rimless)Pork)6
  * Bits of entropy: 215.4

Bits of entropy were calculated using the [password strength tester at rumkin.com](http://rumkin.com/tools/password/passchk.php).

