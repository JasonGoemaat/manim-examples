# Goemaat's MANIM Experiments

Learning python and wanted to try out some visualizations 
[like those](https://github.com/3b1b/videos/tree/master)
[3blue1brown](https://www.3blue1brown.com/) creates for
[his videos](https://www.youtube.com/3blue1brown)

## Setup

***Installed Conda***

[LINK](https://conda.io/projects/conda/en/latest/user-guide/install/index.html)

I did the regular [Windows](https://conda.io/projects/conda/en/latest/user-guide/install/windows.html)
installation of [Anaconda](https://www.anaconda.com/download/).   This is like an environment
manager for python.   It lets you setup environments with their own sets of python and
library versions, preventing errors you might have if using pip to isntall different version
of packages globally to use python.

***Conda Environment***

Conda installed a link in my start menu for 'Anaconda Powershell Prompt' which I use.   To install
manim, I setup an environment named manim and [installed](https://docs.manim.community/en/stable/installation/conda.html#)
it:

```powershell
conda create -n manim
conda activate manim
conda install -c conda-forge manim
```

***First Render***

Starting the 'Anaconda Powershell Prompt' and selecting our 'manim' environment
in conda:

```
conda activate manim
```

Creating a file 'circle.py' with one scene that renders a circle:

```py
from manim import *

class CreateCircle(Scene):
    def construct(self):
        circle = Circle()  # create a circle
        circle.set_fill(PINK, opacity=0.5)  # set the color and transparency
        self.play(Create(circle))  # show the circle on screen
```

Running manim to generate a video and play it

```powershell
manim -p circle.py -a
```

[Using opengl](https://slama.dev/manim/opengl-and-interactivity/):

1. add `manim.opengl` import to enable
2. pass `--renderer=opengl` to render to a window using opengl
3. add `self.interactive_embed()`

```py
from manim import *
from manim.opengl import *

class CreateCircle(Scene):
    def construct(self):
        circle = Circle()  # create a circle
        circle.set_fill(PINK, opacity=0.5)  # set the color and transparency
        self.play(Create(circle))  # show the circle on screen
        self.interactive_embed()
```

```powershell
manim -p circle.py -a --renderer=opengl
```

***Interactive Render***

This lets you render to a window that is left open and interact
using a console and mouse/keyboard.

Install IPython:

```
conda install -c conda-forge IPython
```

Using the opengl as base, add `self.interactive_embed()`

```py
from manim import *
from manim.opengl import *

class CreateCircle(Scene):
    def construct(self):
        circle = Circle()  # create a circle
        circle.set_fill(PINK, opacity=0.5)  # set the color and transparency
        self.play(Create(circle))  # show the circle on screen
        self.interactive_embed()
```

To render to a movie file still you can pass `--write_to_movie` which will
disable interactivity and render a video

```
manim -p --renderer=opengl --write_to_movie circle.py -a
```
