Denise Rauschendorfer

9/15/2022


## Randomly Generated Mosaic Scarf Pattern

This repository contains a code that can be run using python to randomly generate a two-color, knitted mosaic scarf pattern.
The pattern created will be automatically be written into a .txt file titled "knit_mosaic_pattern.txt".

The pattern created from executing the following code consists of a randomly generated 4 by 2.6 inch rectangular mosaic block that repeats 135 times.
There are 24^2 (576) different pattern combinations that can be generated from this code!!

The following code was executed using Python 3.10. 

## __Creating a Written Pattern__

### __Section 1:__
In order to create a randomly generated written pattern, the modules '<span style="color:red">random</span>' and '<span style="color:red">re</span>' need to be imported. Additionally, the operation '<span style="color:red">groupby</span>' in the module '<span style="color:red">itertools</span>' is also required. 

This section of code also includes creating the lists <span style="color:blue">final_even</span> and <span style="color:blue">final_odd</span>. These lists will later be used to save the finished rows created in <span style="color:orange">section 5</span>, and are needed for the code in <span style="color:orange">sections 2-5</span> to run without resulting in an error.

```
import random
import re
from itertools import groupby

final_even=[]
final_odd=[]
```

### __Section 2:__
This section of code specifies the type of stich needed in one row of the repeated rectangular block. Each 4 by 2.6 inch rectangular block is composed of 18 stiches(x axis) and 16 rows(y axis). In order for the pattern created to show up best on a scarf, each row of the rectangular block is broken up into 6 different sections(18 stiches/6 = 3 stiches per section). Therefore, each row of the rectanular block contains only 6 stiches of interest. To specify the type of stitch for the 6 stitches of interest, the following steps are taken:
1. A list titled <span style="color:blue">list</span> is created.
2. A for loop that repeats 6 times is created. 
3. Within the for loop, either a 0 or 1 is assigned to a variable named <span style="color:blue">n</span>. This value is then saved in list. Once this process has repeated 6 times, the for loop is broken.
4. Another list titled <span style="color:blue">odd_row1</span> is created.
5. A second for loop is created that repeats for each item within <span style="color:blue">list</span>.
6. Within this for loop, if the i<sup>th</sup> item in <span style="color:blue">list</span> equals 0, this stitch is arbitrarally determined to be "k" or a knit stitch. Similarly, if the i<sup>th</sup> item in <span style="color:blue">list</span> equals 0, it is "sl" or a slipped stitch. Once this process has repeated for all the items in <span style="color:blue">list</span>, the for loop is broken.

```
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
```


### __Section 3:__
In this section of code, the list created in <span style="color:orange">section 2</span> named <span style="color:blue">odd_row1</span> is simiplified so that consecutive duplicates are grouped together. The nuber of stiches is then multiplied by 3 to represent the total nuber of stiches in one row of the repeated rectangular block. 
*Note: one row contains 18 stiches in 6 sections/groups of 3*

To accomplish this, the following steps are taken:
1. Each consecutive duplicate of either a "k" or "sl" in the list <span style="color:blue">odd_row1</span> is numbered and grouped together into a list named <span style="color:blue">count1</span>. For example if <span style="color:blue">odd_row1</span> equaled [k,k,sl,k,sl,sl], the resulting c<span style="color:blue">count1</span> would be [2,1,1,2].
2. A list titled <span style="color:blue">count2</span> is created.
3. A for loop that repeats for each i<sup>th</sup> item in <span style="color:blue">count1</span> is created.
4. Within the for loop, each i<sup>th</sup> item is multiplied by 3 and this new value is added to the list <span style="color:blue">count2</span>. Once this process has repeated for all the items in <span style="color:blue">count1</span>, the for loop is broken. This for loop has increased each of the 6 stiches of interest by a factor of 3 to create 18 stiches per row.

```
count1 = [sum(1 for key in g) for key, g in groupby(odd_row1)]
print(count1)

count2 = []
for i in count1:
    i = i * 3
    count2.append(i)
print(count2)
```


### __Section 4:__
In this section of code, the list <span style="color:blue">count2</span> created in <span style="color:orange">sections 3</span> is combined with the list <span style="color:blue">odd_row1</span> created in <span style="color:orange">sections 2</span> to make a condensed 18 stitch row.

To accomplish this, the following steps are taken:
1. A list titled <span style="color:blue">condensed_odd_row1</span> is created.
2. An if/else statement is used to to determine what the first stitch in <span style="color:blue">odd_row1</span> is ("k" or "sl").
3. Depending on if the index 0 of <span style="color:blue">odd_row1</span> is a "k" or "sl", a corresponding for loop is executed for every item in <span style="color:blue">count2</span>.
4. within the for loop, the value in each index of <span style="color:blue">count2</span> is converted into a string with the stitch type ("k" or "sl") it corresponds to and added to the list <span style="color:blue">condensed_odd_row1</span>. For example, if <span style="color:blue">condensed_odd_row1</span> begins with a knit ("k") stitch, the value in each even index of <span style="color:blue">count2</span> will have "k" appended to it and the value in each odd index of <span style="color:blue">count2</span> will have "sl" appended to it. Once this process has repeated for all the items in <span style="color:blue">count2</span>, the for loop is broken.

```
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
```


### __Section 5:__
The 16 different rows of each rectangular block are also broken up into 4 different sections (16 rows/4 = 4 rows per section) for the pattern to be visually appealing. When knitting on straight needles, every odd row you knit will be the front of the project and every even row will be the back of the project. This means that the same type of stitch(knit, purl, etc.) on an odd row will look different on an even row. This will cause a problem for our pattern when we try to repeat a row 4 times. To correct this, we need to make a front row (odd) and back row (even). Therefore, a front and back row will be repeated twice within each 4 row section of the repeated rectangular block.  
In <span style="color:orange">sections 4</span>, an odd row was created where 18 stitches were all either knit or slipped purl wise with yarn in back. To make the corresponding even row, every __knit__ stich should be changed to a __purl__ and every stitch slipped purl wise with yarn in __back__ should be slipped purl wise with yarn in __front__. This will make the 4 row repeated section look uniform. 

To accomplish this, the following steps are taken:
1. A copied list of <span style="color:blue">condensed_odd_row1</span> is created titled <span style="color:blue">con_odd_row1</span>.
2. The list <span style="color:blue">con_odd_row1</span> is then added to the list <span style="color:blue">final_odd</span> created in <span style="color:orange">section 2</span>.
3. To begin creating the matching even row, the order of the values in <span style="color:blue">condensed_odd_row1</span> is reversed to match how the stiches on the knitting needles will be configured on an even or "backwards" rows. 
4. A list titled <span style="color:blue">con_even_row1</span> is created.
5. A for loop that repeats for each i<sup>th</sup> item in <span style="color:blue">condensed_odd_row1</span> is created.
6. Within the for loop, an if/else statement is used. Using regular expressions to search determine if the i<sup>th</sup> item in <span style="color:blue">condensed_odd_row1</span> contains either a 'k' or 'sl', the i<sup>th</sup> item is replaced with a 'p' or remains 'sl'. This new value is then added to <span style="color:blue">con_even_row1</span>. Once this process has repeated for all the items in <span style="color:blue">condensed_odd_row1</span>, the for loop is broken.
7. The list <span style="color:blue">con_even_row1</span> is then added to the list <span style="color:blue">final_even</span> created in <span style="color:orange">section 2</span>.

```
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
```


### __Section 6:__
To create the 4 different row sections that make up the repeating rectangular block, a for loop is used to repeat all the code in <span style="color:orange">sections 2-5</span> 4 times. 


### __Section 7:__
In this section, a txt file named "<span style="color:blue">knit_mosaic_pattern.txt</span>" is created and populated with directions that corrolate to the values in <span style="color:blue">final_odd</span> and <span style="color:blue">final_even</span> from <span style="color:orange">section 7</span>. 
*Note: A new "<span style="color:blue">knit_mosaic_pattern.txt</span>" file will be created/overwritten each time the code is run.*

```
filename = "knit_mosaic_pattern.txt"
with open(filename, 'w') as f:
    f.write('Knit Mosaic Scarf Pattern\n\n')
    f.write("This pattern was inspired by my friend Phia Wilson who designs and makes scarves for fun.\n\n")
    f.write("This pattern consists of a randomly generated 4 by 2.6 inch rectangular mosaic block that repeats 135 times.\n"
            "There are 24^2 (576) different pattern combinations that can be generated from this code!!.\n\n")
    f.write("Materials\n"
            "\t-255 yards worsted yarn (4) for the main color\n"
            "\t-255 yards worsted yarn (4) for the contrast color\n"
            "\t-US 8 (5mm) needles\n"
            "\t-Stitch markers\n"
            "\t-Tapestry needle\n\n")
    f.write("Abbreviations\n"
            "\t-CC: Contrast Color\n"
            "\t-CO: Cast on\n"
            "\t-k: Knit\n"
            "\t-MC: Main Color\n"
            "\t-p: purl\n"
            "\t-pm: Place Marker\n"
            "\t-pwise: Purlwise\n"
            "\t-wyib: With Yarn in Back\n"
            "\t-wyif: With Yarn in Front\n\n")
    f.write("Size\n"
            "\tCreates a 72 by 20 inch rectangular scarf once washed and blocked.\n\n")
    f.write("Gauge\n"
            "\t18 stitches by 24 rows = 4 inch square\n\n")
    f.write("Instructions\n"
            "\tCasting On\n"
            "\t\tUsing US 8 needles, CO 90 stitches in MC.\n"
            "\tRepeating Pattern\n"
            "\t\tRow 1 (MC): "+str(final_odd[0])+" pm and repeat to end of row.\n"
            "\t\t\t\t* For all odd rows, slip yarn pwise wyib * \n"
            "\t\tRow 2 (MC): "+str(final_even[0])+" Repeat.\n"
            "\t\t\t\t* For all even rows, slip yarn pwise wyif * \n"
            "\t\tRows 3-4: Repeat rows 1-2.\n"
            "\t\tRow 5 (CC): "+str(final_odd[1])+" Repeat.\n"
            "\t\tRow 6 (CC): "+str(final_even[1])+" Repeat.\n"
            "\t\tRows 7-8: Repeat rows 5-6, 2 times\n"
            "\t\tRow 9 (MC): "+str(final_odd[2])+" Repeat.\n"
            "\t\tRow 10 (MC): "+str(final_even[2])+" Repeat.\n"
            "\t\tRows 11-12: Repeat rows 9-10, 2 times\n"
            "\t\tRow 13 (CC): "+str(final_odd[3])+" Repeat.\n"
            "\t\tRow 14 (CC): "+str(final_even[3])+" Repeat.\n"
            "\t\tRows 15-16: Repeat rows 13-14, 2 times\n"
            "\t\tRows 17-432: Repeat rows 1-16, 27 times\n"
            "\tBinding Off\n"
            "\t\tStep 1: Knit 2 stitches"
            "\t\tStep 2: Move those 2 stitches back to the other needle.\n"
            "\t\tStep 3: Knit the 2 stitches together\n"
            "\t\tStep 4: Knit 1 stitch\n"
            "\t\tStep 5: Repeat steps 2-4 until there is only one stitch left.\n"
            "\t\tStep 6: Cut your yarn leaving a ~5 inch tail and pull it through the last stitch.\n"
            "\t\t\t\tThis will create a knot and prevent your scarf from unraveling.\n"
            "\t\tStep 7: Using the tapestry needle work in all any ends.\n"
            "\t\tStep 8: Wash and block you scarf :)\n"
            "\tAdding Fringe (optional)\n"
            "\t\tStep 1: Cut 4, 8 inch strands of yarn\n"
            "\t\tStep 2: Holding the 4 strands together, use the crochet hook to pull the center of each\n"
            "\t\t\t\tstrand through a stitch along the bottom/top of the scarf. This will create a loop.\n"
            "\t\tStep 3: Pull the fridge ends through the loop, and tighten\n"
            "\t\tStep 4: Trim fringe ends to desired length\n"
            "\t\tStep 5: Repeat steps 1-4 to add additional fringe wherever desired\n\n")
    f.write("Coded by: Denise Rauschendorfer (2022)\n")
f.close()
```

