Denise Rauschendorfer

9/15/2022


# __Randomly Generated Mosaic Scarf Pattern__

This repository contains a code that can be run using python to randomly generate a two-color, knitted mosaic scarf pattern.
The pattern created will automatically be written into a .txt file titled "<span style="color:blue">knit_mosaic_pattern.txt</span>". 

The pattern created from executing the following code consists of a randomly generated 4 by 2.6 inch rectangular mosaic block that repeats 135 times. A graphical representation of the repeating rectangular block will automatically be created in a .jpg file titled "<span style="color:blue">knit_mosaic_graphic_pattern.jpg</span>".

There are 24^2 (576) different pattern combinations that can be generated from this code!!

The following code was executed using Python 3.10. 

## __Creating a Written Pattern__

### __Section 1:__
In order to create a randomly generated written pattern, the modules '<span style="color:red">random</span>', '<span style="color:red">re</span>', and '<span style="color:red">np</span>' need to be imported. Additionally, the operations '<span style="color:red">pyplot</span>' and '<span style="color:red">colors</span>' in the module '<span style="color:red">matplotlib</span>' are also required. 

This section of code also includes creating the lists <span style="color:blue">final_even</span> and <span style="color:blue">final_odd</span>. These lists will later be used to save the finished rows created in <span style="color:orange">Section 5</span>, and are needed for the code in <span style="color:orange">Sections 2-5</span> to run without resulting in an error. The list <span style="color:blue">final_graphic</span> is also created and will be useful in <span style="color:orange">Section 8</span> when creating a graphic representation of the repeating rectangular block. 

```
import random
import re
import numpy as np
from matplotlib import pyplot as plt
from matplotlib import colors

final_even=[]
final_odd=[]
final_graphic=[]
```

### __Section 2:__
This section of code specifies the type of stitch needed in one row of the repeated rectangular block. Each 4 by 2.6 inch rectangular block is composed of 18 stitches (x axis) and 16 rows (y axis). In order for the pattern created to show up best on a scarf, each row of the rectangular block is broken up into 6 different sections(18 stitches/6 = 3 stitches per section). Therefore, each row of the rectangular block contains only 6 stitches of interest. To specify the type of stitch for the 6 stitches of interest, the following steps are taken:
1. A list titled <span style="color:blue">list</span> is created.
2. A for loop that repeats 6 times is created. 
3. Within the for loop, either a 0 or 1 is assigned to a variable named <span style="color:blue">n</span>. This value is then saved in list. Once this process has repeated 6 times, the for loop is broken.
4. The <span style="color:blue">list</span> populated by the for loop is then saved and added to <span style="color:blue">final_graphic</span>. The list <span style="color:blue">final_graphic</span> will be used later in <span style="color:orange">Section 8</span> to make a graphic representation of the repeating rectangular mosaic block.
5. Another list titled <span style="color:blue">odd_row1</span> is created.
6. A second for loop is created that repeats for each item within <span style="color:blue">list</span>.
7. Within this for loop, if the i<sup>th</sup> item in <span style="color:blue">list</span> equals 0, this stitch is arbitrarily determined to be "k" or a knit stitch. Similarly, if the i<sup>th</sup> item in <span style="color:blue">list</span> equals 0, it is "sl" or a slipped stitch. Once this process has repeated for all the items in <span style="color:blue">list</span>, the for loop is broken.

```
list = []
for i in range(0, 6):
    n = random.randrange(0, 2)
    list.append(n)
print(list)
final_graphic.append(list)

odd_row1 = []
for i in list:
    if i == 0:
        odd_row1.append("k")
    else:
        odd_row1.append("sl")
print(odd_row1)
```


### __Section 3:__
In this section of code, the list created in <span style="color:orange">Section 2</span> named <span style="color:blue">odd_row1</span> is simplified so that consecutive duplicates are grouped together. The number of stitches is then multiplied by 3 to represent the total number of stitches in one row of the repeated rectangular block. 

*Note: one row contains 18 stitches in 6 sections of 3 stitches*

To accomplish this, the following steps are taken:
1. A list titled <span style="color:blue">count1</span> is created.
2. The variable <span style="color:blue">n</span> is also created and set to equal 1.
3. The value 'NULL' is then added to the end of <span style="color:blue">odd_row1</span>.
4. A for loop that will iterate through the indices 0-5 of <span style="color:blue">odd_row1</span> is created. This for loop will be used to count each consecutive duplicate of either a "k" or "sl" in the list <span style="color:blue">odd_row1</span>. The grouped number of duplicates are then added to the list <span style="color:blue">count1</span>. For example if <span style="color:blue">odd_row1</span> equaled ['k','sl','k','sl','k','k'], the resulting <span style="color:blue">count1</span> would be [1,1,1,1,2].
5. Within the for loop, an if/else statement is used to make a running count of consecutive duplicates.
6. Next, the 'NULL' value added to <span style="color:blue">odd_row1</span> is removed.
7. A list titled <span style="color:blue">count2</span> is created.
8. A for loop that repeats for each i<sup>th</sup> item in <span style="color:blue">count1</span> is created.
9. Within the for loop, each i<sup>th</sup> item is multiplied by 3 and this new value is added to the list <span style="color:blue">count2</span>. Once this process has repeated for all the items in <span style="color:blue">count1</span>, the for loop is broken. This for loop has increased each of the 6 stitches of interest by a factor of 3 to create 18 stitches per row.

```
count1 = []
n = 1
odd_row1.append('NULL')
for i in range(0, 6):
    if odd_row1[i] == odd_row1[i + 1]:
        n += 1
    else:
        count1.append(n)
        n = 1
print(count1)
odd_row1.remove('NULL')

count2 = []
for i in count1:
    i = i * 3
    count2.append(i)
print(count2)
```


### __Section 4:__
In this section of code, the list <span style="color:blue">count2</span> created in <span style="color:orange">Sections 3</span> is combined with the list <span style="color:blue">odd_row1</span> created in <span style="color:orange">Sections 2</span> to make a condensed 18 stitch row.

To accomplish this, the following steps are taken:
1. A list titled <span style="color:blue">condensed_odd_row1</span> is created.
2. An if/else statement is used to determine what the first stitch in <span style="color:blue">odd_row1</span> is ("k" or "sl").
3. Depending on if the index 0 of <span style="color:blue">odd_row1</span> is a "k" or "sl", a corresponding for loop is executed for every item in <span style="color:blue">count2</span>.
4. Within the for loop, the value in each index of <span style="color:blue">count2</span> is converted into a string with the stitch type ("k" or "sl") it corresponds to and added to the list <span style="color:blue">condensed_odd_row1</span>. For example, if <span style="color:blue">condensed_odd_row1</span> begins with a knit ("k") stitch, the value in each even index of <span style="color:blue">count2</span> will have "k" appended to it and the value in each odd index of <span style="color:blue">count2</span> will have "sl" appended to it. Once this process has repeated for all the items in <span style="color:blue">count2</span>, the for loop is broken.

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
The 16 different rows of each rectangular block are also broken up into 4 different sections (16 rows/4 = 4 rows per section) for the pattern to be visually appealing. When knitting on straight needles, every odd row you knit will be the front of the project and every even row will be the back of the project. This means that the same type of stitch (knit, purl, etc.) on an odd row will look different on an even row. This will cause a problem for our pattern when we try to repeat a row 4 times. To correct this, we need to make a front row (odd) and back row (even). Therefore, a front and back row will be repeated twice within each 4 row section of the repeated rectangular block.  
In <span style="color:orange">Section 4</span>, an odd row was created where 18 stitches were all either knit or slipped purl wise with yarn in back. To make the corresponding even row, every __knit__ stitch should be changed to a __purl__ and every stitch slipped purl wise with yarn in __back__ should be slipped purl wise with yarn in __front__. This will make the 4 row repeated section look uniform. 

*Note: Changes in where the yarn is held (front/back) for slipped stitches will be noted only in the .txt file*

To accomplish this, the following steps are taken:
1. A copied list of <span style="color:blue">condensed_odd_row1</span> is created titled <span style="color:blue">con_odd_row1</span>.
2. The list <span style="color:blue">con_odd_row1</span> is then added to the list <span style="color:blue">final_odd</span> created in <span style="color:orange">Section 2</span>.
3. To begin creating the matching even row, the order of the values in <span style="color:blue">condensed_odd_row1</span> is reversed to match how the stitches on the knitting needles will be configured on an even or "backwards" rows. 
4. A list titled <span style="color:blue">con_even_row1</span> is created.
5. A for loop that repeats for each i<sup>th</sup> item in <span style="color:blue">condensed_odd_row1</span> is created.
6. Within the for loop, an if/else statement is used. Using regular expressions to determine if the i<sup>th</sup> item in <span style="color:blue">condensed_odd_row1</span> contains either a 'k' or 'sl', the i<sup>th</sup> item is replaced with a 'p' or remains 'sl'. This new value is then added to <span style="color:blue">con_even_row1</span>. Once this process has repeated for all the items in <span style="color:blue">condensed_odd_row1</span>, the for loop is broken.
7. The list <span style="color:blue">con_even_row1</span> is then added to the list <span style="color:blue">final_even</span> created in <span style="color:orange">Section 1</span>.

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
To create the 4 different row sections that make up the repeating rectangular block, a for loop is used to repeat all the code in <span style="color:orange">Sections 2-5</span>, 4 times. 


### __Section 7:__
In this section, a txt file named "<span style="color:blue">knit_mosaic_pattern.txt</span>" is created and populated with directions that correlate to the values in <span style="color:blue">final_odd</span> and <span style="color:blue">final_even</span> from <span style="color:orange">Section 7</span>. 

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


## __Creating a Graphic Pattern__

### __Section 8:__
In this section, a graphic representation of the repeating rectangular block is created and saved as a jpg file titled "<span style="color:blue">knit_mosaic_graphic_pattern.jpg</span>".

To accomplish this, the following steps are taken:
1. The list <span style="color:blue">final_graphic</span> that contains the 4 different odd row sections of the repeating rectangular block, is reversed. This step is necessary because the scarf is made from bottom to top. *Note: Because correlating odd and even rows look the same from the front and back, only the odd rows are needed to visualize the front of the scarf.*
3. A two-toned, black and white color map named <span style="color:blue">cmap</span> is created. All values of 1 (knit) will be represented by white squares and all the values of 0 (slip) will be represented by black squares.
4. Within the color map, <span style="color:blue">cmap</span>, subplots are created to be able to add gridlines.
5. Black grid lines along the x and y axis are then added to easily visualize each unique stitch (6 unique stitches per row).
6. The location of the x and y gridlines are then specified. 
7. The x and y axis labels are removed from the graphic.
8. The title, <span style="color:blue">Repeating Rectangular Block</span>, is added to the graphic.
9. Using the data from <span style="color:blue">final_graphic</span>, the color map is plotted as an image.
10. The color map image is then saved as a jpg file titled "<span style="color:blue">knit_mosaic_graphic_pattern.jpg</span>".

```
final_graphic.reverse()

cmap = colors.ListedColormap(['white', 'black'])

fig, ax = plt.subplots()
ax.grid(color='black', linewidth=2)
ax.set_xticks(np.arange(-0.5, 6, 1))
ax.set_yticks(np.arange(-0.5, 4, 1))
ax.set_xticklabels([])
ax.set_yticklabels([])
plt.title("Repeating Rectangular Block", fontsize=20, color="black")

plt.imshow(final_graphic, cmap=cmap)
plt.savefig("knit_mosaic_graphic_pattern.jpg")
```


## __Appendix__

### __Compiled Copy of Raw Code:__
```
import random
import re
import numpy as np
from matplotlib import pyplot as plt
from matplotlib import colors

final_even=[]
final_odd=[]
final_graphic=[]
for k in range(4):
    list = []
    for i in range(0, 6):
        n = random.randrange(0, 2)
        list.append(n)
    print(list)
    final_graphic.append(list)

    odd_row1 = []
    for i in list:
        if i == 0:
            odd_row1.append("k")
        else:
            odd_row1.append("sl")
    print(odd_row1)

    count1 = []
    n = 1
    odd_row1.append('NULL')
    for i in range(0, 6):
        if odd_row1[i] == odd_row1[i + 1]:
            n += 1
        else:
            count1.append(n)
            n = 1
    print(count1)
    odd_row1.remove('NULL')

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


print(final_graphic)
final_graphic.reverse()
print(final_graphic)

cmap = colors.ListedColormap(['white', 'black'])

fig, ax = plt.subplots()

ax.grid(color='black', linewidth=2)
ax.set_xticks(np.arange(-0.5, 6, 1))
ax.set_yticks(np.arange(-0.5, 4, 1))
ax.set_xticklabels([])
ax.set_yticklabels([])
plt.title("Repeating Rectangular Block", fontsize=20, color="black")

plt.imshow(final_graphic, cmap=cmap)
plt.savefig("knit_mosaic_graphic_pattern.jpg")
```


### __Example of the 'knit_mosaic_pattern.txt':__
```
Knit Mosaic Scarf Pattern

This pattern was inspired by my friend Phia Wilson who designs and makes scarves for fun.

This pattern consists of a randomly generated 4 by 2.6 inch rectangular mosaic block that repeats 135 times.
There are 24^2 (576) different pattern combinations that can be generated from this code!!.

Materials
	-255 yards worsted yarn (4) for the main color
	-255 yards worsted yarn (4) for the contrast color
	-US 8 (5mm) needles
	-Stitch markers
	-Tapestry needle

Abbreviations
	-CC: Contrast Color
	-CO: Cast on
	-k: Knit
	-MC: Main Color
	-p: purl
	-pm: Place Marker
	-pwise: Purlwise
	-wyib: With Yarn in Back
	-wyif: With Yarn in Front

Size
	Creates a 72 by 20 inch rectangular scarf once washed and blocked.

Gauge
	18 stitches by 24 rows = 4 inch square

Instructions
	Casting On
		Using US 8 needles, CO 90 stitches in MC.
	Repeating Pattern
		Row 1 (MC): ['3k', '3sl', '3k', '3sl', '6k'] pm and repeat to end of row.
				* For all odd rows, slip yarn pwise wyib * 
		Row 2 (MC): ['6p', '3sl', '3p', '3sl', '3p'] Repeat.
				* For all even rows, slip yarn pwise wyif * 
		Rows 3-4: Repeat rows 1-2.
		Row 5 (CC): ['6k', '3sl', '3k', '6sl'] Repeat.
		Row 6 (CC): ['6sl', '3p', '3sl', '6p'] Repeat.
		Rows 7-8: Repeat rows 5-6, 2 times
		Row 9 (MC): ['3sl', '3k', '3sl', '6k', '3sl'] Repeat.
		Row 10 (MC): ['3sl', '6p', '3sl', '3p', '3sl'] Repeat.
		Rows 11-12: Repeat rows 9-10, 2 times
		Row 13 (CC): ['3sl', '9k', '3sl', '3k'] Repeat.
		Row 14 (CC): ['3p', '3sl', '9p', '3sl'] Repeat.
		Rows 15-16: Repeat rows 13-14, 2 times
		Rows 17-432: Repeat rows 1-16, 27 times
	Binding Off
		Step 1: Knit 2 stitches		Step 2: Move those 2 stitches back to the other needle.
		Step 3: Knit the 2 stitches together
		Step 4: Knit 1 stitch
		Step 5: Repeat steps 2-4 until there is only one stitch left.
		Step 6: Cut your yarn leaving a ~5 inch tail and pull it through the last stitch.
				This will create a knot and prevent your scarf from unraveling.
		Step 7: Using the tapestry needle work in all any ends.
		Step 8: Wash and block you scarf :)
	Adding Fringe (optional)
		Step 1: Cut 4, 8 inch strands of yarn
		Step 2: Holding the 4 strands together, use the crochet hook to pull the center of each
				strand through a stitch along the bottom/top of the scarf. This will create a loop.
		Step 3: Pull the fridge ends through the loop, and tighten
		Step 4: Trim fringe ends to desired length
		Step 5: Repeat steps 1-4 to add additional fringe wherever desired

Coded by: Denise Rauschendorfer (2022)
```


### __Example of 'knit_mosaic_graphic_pattern.jpg':__
![knit_mosaic_graphic_pattern](https://user-images.githubusercontent.com/95630229/194775952-089835af-288b-4cd2-9aad-889227119df5.jpg)
