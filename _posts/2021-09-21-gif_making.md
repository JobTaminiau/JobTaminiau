---
title: "Script for making GIFs"
date: 2021-09-21T20:42:30-04:00
categories:
  - Scripts
tags:
  - python_code
  - animations
---
There are times when I want to visualize a series of images as an animation. To do this, there are four basic steps involved.
1. Create the images of interest. This can be done in a for loop or with separate code per image.
2. Place the location name of each image in a list.
3. Append the images together.
4. Save the appended images as a GIF.

Step 1 is specific to the project.

Step 2 is as follows:
```python
  # step 2: 
  # this will save the figure as a high-res png in the output path. you can also save as svg if you prefer.
  filepath = os.path.join(output_path + filename)
  chart = ax1.get_figure()
  chart.savefig(filepath, dpi=100)
  list_of_plots.append(filepath)
```

Step 3 is as follows:

```python
from PIL import Image, ImageDraw

# Append all images together
images = []
for plot in list_of_plots:
    im = Image.open(plot)
    images.append(im)
```

Step 4 is provided below:

```python
# Save all images as a GIF
images[0].save('animation/KIER_campus.gif',
               save_all=True, append_images=images[1:], optimize=False, duration=800, loop=0)
```
