# Introduction to Jupyter Notebooks: the weird and the wonderful

Materials for British Library "hack and yack" workshop

## Aims 

Depending on your starting point you may focus only on a particular aim during this session:

- Understand what a Jupyter notebook is and why they are used 
- How to (try) running notebooks someone else has created
- Introduce some weird stuff you can do with notebooks

## Session format 

### Contents



# What is a Jupyter notebook?

If you don't know what a Jupyter notebook is or are only vaguely familiar you may want to start working through some of these resources:

- [The offical Jupyter page](https://jupyter.org/)
- [The official documentation](https://jupyter.org/documentation)
- [A Programming Historian lesson (focus on the literate computing section)](https://programminghistorian.org/en/lessons/jupyter-notebooks#literate-computing)
- What is Jupyter Notebook? [Youtube video](https://youtu.be/q_BzsPxwLOE)


## How to try running notebooks someone else has created?

Since notebook are being used increasingly to document research processes, demonstrate how to use tools and APIs, and as a way of creating training material it can often be useful to be able to run a notebook someone else has created. The difficulty of doing this ranges from easy to impossible. We'll look a little bit at some of the considerations in more detail in a moment. 

## What is a notebook?

This might seem like repetition when this is covered in the previous section but let's look at what a Jupyter notebook *really* is.

Let's take [this notebook](https://github.com/mchesterkadwell/bughunt-analysis/blob/master/notebooks/1-intro-to-strings.ipynb) as example. 
If we look at it in the GitHub web interface you'll see something like this: 

<img width="1297" alt="Screenshot 2021-05-17 at 14 50 54" src="https://user-images.githubusercontent.com/8995957/118499973-4f76ff80-b71f-11eb-874f-9556167f00f7.png">

This looks like a webpage of sorts. However this is a 'rendered' version of a notebook i.e. a version that has been transformed in some way. As an example from another setting if we look at some HTML for a heading it looks like this in its raw form:

```html
<h5>Heading 5</h5>
```

and like this when rendered:

<h5>Heading 5</h5>

If we take a look at the underlying notebook it lookls quiote diferent. We can do this in GitHub by viewing the `raw` tab at the top of the notebook. 
The notebook is now shown in its 'raw' form [here](https://raw.githubusercontent.com/mchesterkadwell/bughunt-analysis/master/notebooks/1-intro-to-strings.ipynb). The raw version of the notebook looks like this:

```json
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {
    "collapsed": true
   },
   "source": [
    "# Introdution to Jupyter Notebooks and Text Processing in Python\n",
    "This 'document' is a Jupyter notebook. It allows you to combine explanatory **text** and **code** that executes to produce results you can see on the same page.\n",
    "\n",
    "## Notebook Basics\n",
    "\n",
    "### Text cells\n",
    "\n",
    "The box this text is written in is called a *cell*. It is a *text cell* written in a very simple markup language called 'Markdown'. Here is a useful [Markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet). You can edit and then run cells to produce a result. Running this text cell produces formatted text.\n",
    "\n",
    "### Code cells\n",
    "\n",
    "The other main kind of cell is a *code cell*. The cell immediately below this one is a code cell. Running a code cell runs the code in the cell and produces a result."
   ]
  },
```

We can see when we look at the raw version of the notebook it is a json file containing version bits of information i.e. `cell_type`, `metadata`. This is importat to have in mind because it shows that on its own a notebook is basically a json file. We need to have quite a few other things in place to make it interactive. 

What do we need to have in place to run a notebook. Some considerations:

- Where is the code going to run? 
- What data is required by the notebook?
- How to get data in the environment where you are going to run your code? 
- What Python packages you will require?
- Does the code in the notebook your trying to run require particular compute resources (RAM, CPU, GPU)?

This might either seem like quite a modest list of things to consider or way to onerous to bother with. 

## Running on the cloud aka using someone else's computer 

We'll focus on running the code on someone else machine i.e using a "cloud" option. There are definitely advantages to having Jupyter/Python setup on a personal machine but the process for setting this up will vary depending on your device, whether someone else controls your device etc. 

We will focus on two main options for running notebooks in the cloud and some of the considerations for what you need to use each. 

### Binder 

[Binder](https://mybinder.org/) is one popular option for allowing people to interact with Jupyter notebooks in the cloud. 

#### What is Binder?

> The Binder Project is an open community that makes it possible to create sharable, interactive, reproducible environments. 

Binder consits of a number of different components. "BinderHub" is a tool that allows you to host a service for running notebooks in the cloud. "Mybinder" is a hosted version of this tool which is hosted with the aim of making science more reproducible. The mybinder tool can be used by anyone as a way of running notebooks without setting up any software on your own machine.'

#### Binder on easy mode 

Since Mybinder is intended to help support reproducible research it can be used to make accessing notebooks very easy. However this requires some effort on the notebook author. Often if someone has gone to this effort you will see something like this on the GitHub repository for the notebooks(s):



<img width="888" alt="Screenshot 2021-05-18 at 10 04 39" src="https://user-images.githubusercontent.com/8995957/118623851-8bae6c80-b7c0-11eb-9de2-b1f67d0a5516.png">

If we follow one of the launch on binder links Binder will begin setting up the required infrastructure required to run the notebook. For example if we go to this repository [https://github.com/mchesterkadwell/bughunt-analysis]() we will see a "Launch Binder" button. If we click on this mybinder will start creating an environment for running the notebooks in this repository. This will *usually* include the required data, python libraries etc. required for the notebook to run successfully. In this 'easy mode' we don't need to but be a bit patient whilst mybinder launches. 

#### Exercise: Binder on hard mode 

If we don't see a 'launch on binder' button the steps required to run the notebook might be a bit more involved. We'll work through an example to show what we need to check for and consider. 

We'll use a repository containing notebooks [Does Late Style Exist?](https://github.com/JonathanReeve/late-style-PCA/tree/8af8277439f0bce77d3f3ba87f5ef59018fab68f)

If we look at what's inside the repository:

<img width="858" alt="Screenshot 2021-05-18 at 12 37 32" src="https://user-images.githubusercontent.com/8995957/118647527-56fadf00-b7d9-11eb-8051-376918c376b0.png">


We can see that we have a folder for data, this is a good sign that the data is included with the repository and won't have to be sourced from somewhere else. 

We also see a bunch of notebooks, and other folders. One thing we don't see is a `requirements.txt` or `environment.yml` file. These files are used by Binder to determine which Python libraries a repository will need. Since these aren't available Binder won't know what libraries are available. Let's proceed anyway and see how we get on. 

If we go to the mybinder [website](https://mybinder.org/) you'll see an interface which allows you to paste in a URL for a repository. Paste in the link to the GitHub repository. This should start the process of setting up a binder instance for this repository. 

Once mybinder has setup you should see something like:


<img width="1158" alt="Screenshot 2021-05-18 at 13 03 35" src="https://user-images.githubusercontent.com/8995957/118647648-798cf800-b7d9-11eb-8ad3-5fbd43770161.png">


Try running through the `late-style-PCA.ipynb` notebook. 
- What problems do you run into? 
- Why do you run into these problems. 
- Do you have ideas about how to fix these issues?


#### When Binder might not be suitable

There are some occasions when Binder might not be the best choice for trying to run someone's notebook. These include:

- when you want to save your changes, although this is possible to do if you wait to long binder will shutdown and you will loose any modification's you made to the notebooks. 
- when you need more compute power; binder has fairly low resources allocated to each 'instance'. If you are running code that might require a large amount of memory then binder may struggle or crash. 
- if you require GPU: if you are running a notebook that suggests or requires a GPU then Binder is probably not a good option. 



#### Further binder resources 


### Google colab 

- enviroment notebook 
- data notebook 
-

### Demo 
TODO 

## Weird and wonderful stuff you can  do with notebooks 

https://github.com/markusschanta/awesome-jupyter

https://youtu.be/


### I don't like notebooks

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/7jiPeIFXb6U/0.jpg)](https://www.youtube.com/watch?v=7jiPeIFXb6U)


### I like notebooks

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/9Q6sLbz37gk/0.jpg)](https://www.youtube.com/watch?v=9Q6sLbz37gk)


Voila - Rendering of live Jupyter Notebooks with interactive widgets, allowing dashboarding based on Jupyter Notebooks

nbdev - Develop, package and distribute Python packages to PyPI using Jupyter as a Literate Programing environment.


