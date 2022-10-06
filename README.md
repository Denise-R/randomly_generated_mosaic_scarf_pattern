Denise Rauschendorfer
9/15/2022


## Randomly Generated Mosaic Scarf Pattern

This repository contains a code that can be run using python to randomly generate a two-color, knitted mosaic scarf pattern.
The pattern created will be automatically be written into a .txt file titled "knit_mosaic_pattern.txt".

The following code was executed using Python 3.10. 

## __Creating a Written Pattern__




'''
import random
import re
from itertools import groupby

final_even=[]
final_odd=[]
for k in range(4):
    list = []
    for i in range(0, 6):
        n = random.randrange(0, 2)
        list.append(n)
    print(list)

    
    odd_row1 = []
    for i in list:
        if i == 0:
            odd_row1.append("k")
        else:
            odd_row1.append("sl")
    print(odd_row1)

    count1 = [sum(1 for key in g) for key, g in groupby(odd_row1)]
    print(count1)

    count2 = []
    for i in count1:
        i = i * 3
        count2.append(i)
    print(count2)

    condensed_odd_row1 = []
    if odd_row1[0] == 'k':
        print("k is first")
        for i in range(0, len(count2)):
            if i % 2 == 0:
                condensed_odd_row1.append(str(count2[i]) + "k")
            else:
                condensed_odd_row1.append(str(count2[i]) + "sl")
    else:
        print("sl is first")
        for i in range(0, len(count2)):
            if i % 2 == 0:
                condensed_odd_row1.append(str(count2[i]) + "sl")
            else:
                condensed_odd_row1.append(str(count2[i]) + "k")

    con_odd_row1 = condensed_odd_row1.copy()
    print(con_odd_row1)
    final_odd.append(con_odd_row1)
    condensed_odd_row1.reverse()
    con_even_row1 = []
    for i in condensed_odd_row1:
        if re.search("k$", i):
            con_even_row1.append(i.replace('k', 'p'))
        else:
            con_even_row1.append(i.replace('sl', 'sl'))
    print(con_even_row1)
    final_even.append(con_even_row1)
'''
