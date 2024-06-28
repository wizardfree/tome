---
title: "Giving a slug a new coat of slime"
date: 2023-05-08T11:48:25+01:00
description: "Rewrite of the gastropod project."
draft: false
toc: false
author: Joseph Fleet
slug: techno.november.necklace
tags:
- Python
- Development
---

The [gastropod 🐌](https://github.com/wizardfree/gastropod) script is nearly **2 years old!**

Unfortunately in this time not much has changed with the project. Originally written for usage on my [personal webzone](https://wizardinthe.cloud). As well as a test of my Pythonic writing skills. It's seen little attention since it's initial development.

However I'm pleased to annouce [gastropod 🐌](https://github.com/wizardfree/gastropod) version 2 is here! **aka** the script has been rewritten to be more efficient/clearer/overall betterer.

First, lets take a look at the original script:

```python
#!/bin/env python3

import json
import random

def load_words():
    with open('words_dict.json') as f:
        data = json.load(f)
    return data

def randomWordFromFile(wordbank):
    r = random.choice(list(wordbank.items()))
    key, value = r
    return key


if __name__ == '__main__':
    english_words = load_words()
    slug = ""
    for i in range(0, 3):
        word = (randomWordFromFile(english_words))
        slug = slug + (word + ".") if not i == 2 else slug + word

    print(slug) 
```

Not pretty...but it works. Let's break it down.

```python
import json
```

This module had to be used. Because of how the data was structured. Why I didn't restructure the data myself? I'm not sure.

```python
def load_words():
    with open('words_dict.json') as f:
        data = json.load(f)
    return data
```

The case could be made for a dictionary being used here is more memory efficient than a list. Something to test perhaps. But importing a module and then reading in a seperate file. Just adds complexity where it's not needed. [**KISS**](https://en.wikipedia.org/wiki/KISS_principle)!

```python
def randomWordFromFile(wordbank):
    r = random.choice(list(wordbank.items()))
    key, value = r
    return key
```

Convert a dictionary to a list then pluck out the required value. Galaxy brain coding here.

```python
if __name__ == '__main__':
    english_words = load_words()
    slug = ""
    for i in range(0, 3):
        word = (randomWordFromFile(english_words))
        slug = slug + (word + ".") if not i == 2 else slug + word
```

Messy and gross. Kinda like a slug.

As you can see something needs to change and change it has. Welcome [gastropod 🐌](https://github.com/wizardfree/gastropod) version 2:

```python

#!/bin/env python3

import random

gastropod_word_list = [
    'hospital', 'tradition' ... , 'consultancy']
    # Full list condensed for brevity

# randomly select 3 words from the list
selection = [random.choice(gastropod_word_list) for _ in range(3)]

# join the selected words with a period separator
result = '.'.join(selection)

# print the result
print(result)

```

Speaks for itself really. Compared to the original someone without coding experience (or the comments) could read the script and understand what it does. Now show the original script and let the same person try to decipher that. Good luck.

A major change here is the data used. Firstly, the word list has changed from the [popular_words.json](https://github.com/dwyl/english-words) file to [google-10000-english](https://github.com/first20hours/google-10000-english) word list. Specifically the version which contains no swear words.

The word list is a `txt` file with each word on a newline. This is fine but without repeating the sins of the forefathers I didn't want to import this as is.
Especially given that words less than three (3) characters just aren't that useful for this context.

To tidy this list for usage in `gastropod` the following process was used:

1. Fetch the `txt` file from the [google-10000-english](https://github.com/first20hours/google-10000-english) repository.

```bash
curl -O "https://raw.githubusercontent.com/first20hours/google-10000-english/master/google-10000-english-no-swears.txt"
```

2. Convert that file to a Python list.

```python
with open('google-10000-english-no-swears.txt', 'r') as file:
    data = file.readlines()
    result = []
    for line in data:
        result.append(line.strip())

print(result)
```

3. Remove words which are 3 characters or less

```python
gastropod_word_list = []
for s in googlenoswears:
    if len(s) > 3:
        gastropod_word_list.append(s)
```

4. Shuffle the new list (I believe the original list is sorted by most frequently used words first.)

```python
random.shuffle(gastropod_word_list)
```

The rest of the script just reads much better. The complexity has been stripped out to be replaced with (in my opinion) a much more eloquent solution.

As for the future of [gastropod 🐌](https://github.com/wizardfree/gastropod). I'm really not sure what more is needed for this little slug. For now I'm happy with how this script is working after the re-write.

-Joseph