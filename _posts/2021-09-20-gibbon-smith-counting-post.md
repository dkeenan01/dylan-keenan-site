---
layout: post
title:  "Gibbon and Smith Counting Script"
date:   2021-09-20 18:15:00 -0400
categories: jekyll update
---
**I used a library called request to get the text in and split it by the white spaces**
```
import requests

text1 = requests.get('https://raw.githubusercontent.com/gregorycrane/DHFall2021/master/texts/declineandfall-gut.txt')
text2 = requests.get('https://raw.githubusercontent.com/gregorycrane/DHFall2021/master/texts/wealthofnations-gut.txt')

result = text1.text
result2 = text2.text

final = result.split()
final2 = result2.split()
```

**This next block creates the dictionaries, counts the words while adding them to the dictionary. Then I the dictionaries get sorted based on count(highest to lowest).**

```
counts = {}
counts2 = {}

for token in final:
  if token in counts:
    counts[token] += 1
  else:
    counts[token] = 1

for token in final2:
  if token in counts2:
    counts2[token] += 1
  else:
    counts2[token] = 1

finalcounts_1 = sorted(counts.items(), key = lambda counts: counts[1],reverse=True)
finalcounts_2 = sorted(counts2.items(), key = lambda counts2: counts2[1],reverse=True)
```

**Here is kind of a sanity check. It prints all the word in in order as long as they appear over 50 times.**

```
#will print all the words that appear over 50 times
for key, value in finalcounts_1:
  if value > 50:
    print(key, ':', value)

#will print all the words that appear over 50 times
for key, value in finalcounts_2:
  if value > 50:
    print(key, ':', value)
```

**Lastly, it checks the previous dictionaries to the one containing all the capital letters. If the first character matches, it adds it to the a new dictionary with capital letters. Then it prints.**

```
capital_letters = ["A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"]
capital_words1 = []
for word in finalcounts_1:
  if word[0][0] in capital_letters:
    capital_words1.append(word)

capital_words2 = []
for word in finalcounts_2:
  if word[0][0] in capital_letters:
    capital_words2.append(word)

print(capital_words1)
print(capital_words2)
```