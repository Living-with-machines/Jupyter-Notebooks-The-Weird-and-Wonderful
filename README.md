# Introduction to Jupyter Notebooks: the weird and the wonderful

[![DOI](https://zenodo.org/badge/368131278.svg)](https://zenodo.org/badge/latestdoi/368131278)

Materials for a British Library, Digital Scholarship "hack and yack" workshop. 

## Aims 

Depending on your starting point, you may focus only on a particular aim during this session:

- Understand what a Jupyter notebook is and why they are used 
- How to (try) running notebooks someone else has created
- Introduce some weird/wonderful stuff you can do with notebooks

## Session format 

Choose your own adventure! Depending on how familiar you are with the topic, you can choose to go through the material independently. This page roughly starts with the basics and finishes with some more experimental approaches to using notebooks. 

Alternatively, you can join a slightly more guided journey through some of the below material. 

# What is a Jupyter notebook?

If you don't know what a Jupyter notebook is or are only vaguely familiar you may want to start working through some of these resources:

- [The official Jupyter page](https://jupyter.org/)
- [The official documentation](https://jupyter.org/documentation)
- [A Programming Historian lesson](https://programminghistorian.org/en/lessons/jupyter-notebooks#literate-computing) (focus on the literate computing section)
- What is Jupyter Notebook? [Youtube video](https://youtu.be/q_BzsPxwLOE)


## How to try running notebooks someone else has created?

Since notebooks are being used increasingly to document research processes, demonstrate how to use tools and APIs, and create training material, it can often be helpful to run a notebook someone else has made. The difficulty of doing this ranges from easy to impossible. We'll look a little bit at some of the considerations in more detail in a moment. 

## What is a notebook?

This might seem like repetition when covered in the previous section but let's look at what a Jupyter notebook *really* is.

Let's take [this notebook](https://github.com/mchesterkadwell/bughunt-analysis/blob/master/notebooks/1-intro-to-strings.ipynb) as example. 
If we look at it in the GitHub web interface you'll see something like this: 

<img width="1297" alt="Screenshot 2021-05-17 at 14 50 54" src="https://user-images.githubusercontent.com/8995957/118499973-4f76ff80-b71f-11eb-874f-9556167f00f7.png">

This looks like a webpage of sorts. However, this is a 'rendered' version of a notebook, i.e. a version that has been transformed somehow. Using an example from another setting might illustrate this. If we look at some HTML for a heading, it looks like this in its raw form:

```html
<h5>Heading 5</h5>
```

and like this when rendered:

<h5>Heading 5</h5>

If we take a look at the underlying notebook, it looks quite different. We can do this in GitHub by viewing the `raw` tab at the top of the notebook. 
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

When we look at the raw version of the notebook, we can see a JSON file containing version bits of information, i.e. `cell_type`, `metadata`. This is important to have in mind because it shows that on its own, a notebook is basically a JSON file. We need to have quite a few other things in place to make it interactive and execute to code inside the notebook. 

What do we need to have in place to run a notebook? Some considerations:

- Where is the code going to run? We need some computer/system to run the Python code in the notebooks
- What data is required by the notebook?
- How to get data in the environment where you are going to run your code? 
- What Python packages you will require?
- Does the code in the notebook you are trying to run require particular compute resources (RAM, CPU, GPU)?

This might either seem like quite a modest list of things to consider or way too demanding to bother with. 

## Running on the cloud, aka using someone else's computer 

We'll focus on running the code on someone else machine, i.e. using a "cloud" option. There are definitely advantages to having Jupyter/Python set up on a personal machine. Still, the process for setting this up will vary depending on your device, whether someone else controls your device etc. 

We will focus on two main options for running notebooks in the cloud and some considerations for what you need to use each. 

### Binder 

[Binder](https://mybinder.org/) is one popular option for allowing people to interact with Jupyter notebooks in the cloud. 

#### What is Binder?

> The Binder Project is an open community that makes it possible to create sharable, interactive, reproducible environments. 

Binder consits of a number of different components. "BinderHub" is a tool that allows you to host a service for running notebooks in the cloud. "Mybinder" is a hosted version of this tool which is hosted to make science more reproducible. The mybinder tool can be used by anyone as a way of running notebooks without setting up any software on your own machine.'

#### Binder on easy mode 

Since Mybinder is intended to help support reproducible research, it can be used to make accessing notebooks very easy. However, this requires some effort on the notebook author. Often if someone has gone to this effort, you will see something like this on the GitHub repository for the notebooks(s):

<img width="888" alt="Screenshot 2021-05-18 at 10 04 39" src="https://user-images.githubusercontent.com/8995957/118623851-8bae6c80-b7c0-11eb-9de2-b1f67d0a5516.png">

If we follow one of the "launch on binder" links, Binder will begin setting up the required infrastructure required to run the notebook. For example, if we go to this repository [https://github.com/mchesterkadwell/bughunt-analysis]() we will see a "Launch Binder" button. If we click on this mybinder will start creating an environment for running the notebooks in this repository. This will *usually* include the required data, python libraries etc., needed for the notebook to run successfully. In this 'easy mode,' we don't need to do anything but be a bit patient whilst mybinder launches. 

#### Exercise: Binder on hard mode 

If we don't see a 'launch on binder' button, the steps required to run the notebook might be a bit more involved. We'll work through an example to show what we need to check for and consider. 

We'll use a repository containing notebooks [Does Late Style Exist?](https://github.com/JonathanReeve/late-style-PCA/tree/8af8277439f0bce77d3f3ba87f5ef59018fab68f)

If we look at what's inside the repository:

<img width="858" alt="Screenshot 2021-05-18 at 12 37 32" src="https://user-images.githubusercontent.com/8995957/118647527-56fadf00-b7d9-11eb-8051-376918c376b0.png">


We can see that we have a folder for data. This is a good sign that the data is included with the repository and won't have to be sourced elsewhere. 

We also see a bunch of notebooks and other folders. One thing we don't see is a `requirements.txt` or `environment.yml` file. These files are used by Binder to determine which Python libraries a repository will need. Since these aren't available, Binder won't know what libraries are available. Let's proceed anyway and see how we get on. 

If we go to the mybinder [website](https://mybinder.org/) you'll see an interface that allows you to paste in a URL for a repository. Paste in the link to the GitHub repository. This should start the process of setting up a binder instance for this repository. 

Once mybinder has setup you should see something like:


<img width="1158" alt="Screenshot 2021-05-18 at 13 03 35" src="https://user-images.githubusercontent.com/8995957/118647648-798cf800-b7d9-11eb-8ad3-5fbd43770161.png">


Try running through the `late-style-PCA.ipynb` notebook:
- What problems do you run into? 
- Why do you run into these problems. 
- Do you have ideas about how to fix these issues?


#### When Binder might not be suitable

There are some occasions when Binder might not be the best choice for trying to run someone's notebook. These include:

- when you want to save your changes, although this is possible to do, if you wait too long binder will shut down, and you will lose any modification's you made to the notebooks. 
- when you need more compute power, binder has relatively low resources allocated to each 'instance'. If you are running code that might require a large amount of memory, binder may struggle or crash. 
If you require GPU, if you are running a notebook that suggests or requires a GPU, Binder is probably not a good option. 


#### Further Binder exercises

Using [documentation](https://mybinder.readthedocs.io/en/latest/introduction.html) from binder either follow their example or try replicating it on another GitHub repository containing Jupyter notebooks. 

Some possible sources for notebooks include:
- https://github.com/quinnanya/dh-jupyter
- https://github.com/search?l=Jupyter+Notebook&q=notebook&t 

If you are feeling particularly ambitious you can fork a GitHub repository and make the required changes to get it running in binder.

### Google colab 

An alternative option to Binder is Google Colab. This is also a hosted notebook service but has a few differences from Binder:

- Colab is focused on running single notebooks more than copying all the requirements from a GitHub repository
- Colab offers free GPUs which is really helpful/essential if you are running a notebook that uses deep-learning based approaches to machine learning
- Getting the environment setup and data into colab is quite different
- Colab notebooks can be saved, but the notebook 'state' will reset after colab times out (maximum time is ~12 hours, but this requires interacting i.e. the notebook won't sit idle for 12 hours). 
- you need a Google account to use Colab. 

#### Colab on easy mode 

Colab is also increasingly being used as a way of making notebooks accessible for others to work with. This means that alongside a 'run on binder' option you will sometimes see a "open in colab" option. When you see this *often* the authors of the notebook will have tried to set up the notebook in a way which doesn't require additional work for you to get it to run. Some examples of this:

- https://github.com/BL-Labs/Jupyter-notebooks-projects-using-BL-Sources
- https://github.com/Living-with-machines/Computer-Vision-for-the-Humanities-workshop


#### Colab on hard mode

You may want to run a notebook on Colab which hasn't specifically been setup for Colab. There are a few main things you will need to get a notebook working in Colab:

- setup the environment: often notebooks will rely on Python packages that aren't included in the Colab environment. You will need to make sure these are installed in Colab
- setup data: if the notebook your working with requires external data you will often need to setup some way of getting this data into Colab. 

#### Exercise:

For each of these topics a notebook has been prepared that discusses how to tackle these topics. These hopefully give some sense of what to look out for and how to get a notebook running. 

- [environment notebook](https://colab.research.google.com/drive/1dGe37rIgQaiiqCpPETpk7wnjvL2scW7D?usp=sharing)
- [data notebook](https://colab.research.google.com/drive/1U6SAx0fsdsxixVBPYakL5E_WIixgvD4t?usp=sharing)

You will need a Google account to run these notebooks. 

## Are notebooks bad?

There is a bit of a debate about when/whether notebooks are a good idea. These two 'opposing' views are pretty well expressed in these two talks. It may be helpful to be aware of these debates and some of the arguments but forward if you plan to work with notebooks further. There may be occasions when some 'explains' to you that notebooks are terrible and you should stop using them and instead use their preferred coding environment/text editor/font etc 😜. 

### I don't like notebooks

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/7jiPeIFXb6U/0.jpg)](https://www.youtube.com/watch?v=7jiPeIFXb6U)

### I like notebooks

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/9Q6sLbz37gk/0.jpg)](https://www.youtube.com/watch?v=9Q6sLbz37gk)


## Weird and wonderful stuff you can  do with notebooks 

Supposing all of the above is old news to you and you are already confident in using binder/colab/running notebooks locally. In that case, this section introduces some weird and wonderful things we can do using notebooks you could explore. 

For a fuller list of things you can do in notebooks, there is a nice list of ["awesome jupyter"](https://github.com/markusschanta/awesome-jupyter) that you might also want to look at. In the below list, I've picked out some personal highlights with a short summary of what they are and why they might be helpful in a GLAM setting. 

For some specific GLAM examples of notebook see: [https://glam-workbench.net/more-glam-notebooks/]()

### Create a Python library using notebooks

[`nbdev`](https://nbdev.fast.ai/):  Develop, package and distribute Python packages to PyPI using Jupyter as a Literate Programming environment.

The `nbdev` tool allows you to develop python libraries/packages inside Jupyter Notebooks. These packages can then be uploaded onto `PyPI` or installed from a GitHub repository. 

There are some features that are worth highlighting:

- Documentation is generated from the Jupyter notebooks; this allows you to write documentation alongside code and provide examples. Since the documentation is itself generated from a notebook, people can run the code from the documentation. 
- Tests can be written inside notebooks. Tests are used in software development to ensure that the code has the behaviour you want/expect.
- A lot of the 'boilerplate' work that has to be done to create Python packages is automated using `nbdev`.

#### Why this could be useful in a library setting?

Increasingly people who aren't software engineers are creating code in GLAM settings. This code could be used for quite specific tasks or might be one-time 'throw away' scripts. However, there will also be situations when code is written that could be useful in the future for yourself or others. Creating a Python package that can easily be installed by other people isn't always entirely straightforward. This is where `nbdev` helps make this process easier. Many people find it more comfortable developing and experimenting with code in a notebook because you can inspect the outputs at various points and make small changes cell by cell. `nbdev` helps allows you to do this experimentation inside the same environment as the 'finished' code.

Testing software is something that is often skipped on projects because it's seen as too much effort. Because `nbdev` makes writing tests quite simple, it's easier to add at least some basic tests to your code. 

A final reason this approach might be particularly lovely in a GLAM setting is the ease of documenting the libraries and showing the development of the code. This allows the possibility of including some 'pedagogy' or teaching inside the library. People cannot only use the library/code directly but also see how the library approached problems. 

Some examples of `nbdev` in action:

- [`fastai`](https://docs.fast.ai/): The original use of `nbdev` was to create version 2 of the `fastai` deep learning library. It shows nbdev in usage for a relatively large project. 
- [`jupyterplot`](https://lvwerra.github.io/jupyterplot/) is a nice example of a focused and relatively small library being built in nbdev
- From the Living with Machines project, a small library [`gh_orgstats`](https://github.com/Living-with-machines/gh_orgstats) for helping gather some GitHub usage data for reporting to our funder. 
- A [blog post](https://medium.com/overstoryai/how-nbdev-helps-us-structure-our-data-science-workflow-in-jupyter-notebooks-9cf6081b051f) discussing the usage of fastai. 

### Build interactivity into notebooks and create dashboards

Although notebooks are already 'interactive', we sometimes may want to create something that either allows for interactivity dependent on people knowing how to change code. For example, we might want to add a button that allows someone to upload an image or document into a notebook rather than already know how to load the image and reference it in the code. We may also want to create a little interactive "GUI" like interfaces for working with data in a notebook. For example, we might add a dropdown interface for going through a directory of images:

<img width="418" alt="Screenshot 2021-05-19 at 14 45 59" src="https://user-images.githubusercontent.com/8995957/118823576-fc34b680-b8b0-11eb-91df-ce329cf9f7b4.png">


There are a growing number of tools for adding this kind of interactivity to notebooks, from small 'widgets' to add sliders or dropdowns to notebooks to tools that are intended to build full dashboards from Jupyter notebooks. 

#### Why this could be useful in a library setting?

Creating new ways of interacting and working with collections is becoming more critical as more collections are available digitally. Although notebooks offer one way of making access to collections easier, it still assumes some basic coding knowledge. Adding some 'widgets' to add interactivity to these notebooks could open up these notebooks as 'interfaces' to a broader audience. 

Building full dashboards or tools for interacting with collections is a major undertaking. There is often no resource available to build 'proper' interfaces to a collection, but a more modest approach could use dashboards created out of Jupyter notebooks. Whilst these might not replace a fully-featured interface developed as a bespoke solution, they also won't require the same resources to create. An example of a dashboard created using one of these tools gives a sense of the kind of things that can be developed:

<img width="1361" alt="Screenshot 2021-05-19 at 14 59 16" src="https://user-images.githubusercontent.com/8995957/118825686-ce507180-b8b2-11eb-9817-e5ff853f80b8.png">

[Source](https://nyc-taxi.pyviz.demo.anaconda.com/dashboard)

#### Tools for adding interactivyt 

Some tools for adding interactivity include:

- [ipywidgets](https://ipywidgets.readthedocs.io/en/latest/): offers various widgets for notebooks
- [Voilà](https://voila.readthedocs.io/en/stable/using.html): a tool for creating apps from notebooks
- [Panel](https://panel.holoviz.org/): a set of tools focused on helping create dashboards or interactive components
- [Gradio](https://www.gradio.app/): Generate an easy-to-use UI for your ML model, function, or API with only a few lines of code. Integrate directly into your Python notebook, or share a link with anyone.

#### Examples

- A notebook that includes some interactive elements with a focus on computer vision [https://github.com/Living-with-machines/maps-at-scale-using-computer-vision-and-jupyter-notebooks]()
- An example of a notebook that has been turned into a web application using voila: [https://mybinder.org/v2/gh/fastai/bear_voila/master?urlpath=%2Fvoila%2Frender%2Fbear_classifier.ipynb]()


#### Things to explore 

If you want to get stuck into this topis these getting started pages, and examples will give you a sense of what is possible: 

- https://www.gradio.app/getting_started 
- https://panel.holoviz.org/getting_started/index.html
- https://awesome-panel.org/ 

### Create and publish books, slides, and blogs from notebooks 

The final awesome things we'll cover are various ways of "publishing" a notebook. Obviously, we may just publish a notebook "as is" but a growing number of tools allow for transforming notebooks into other formats. 

#### Why this could be useful in a library setting?

An obvious use case is for publishing tutorials and other teaching materials in a more 'polished' format. However, there are also exciting opportunities to utilise the code inside notebooks whilst presenting the final product in a way that 'hides' the code. This offers exciting opportunities for things like:

- automatically updating blog posts 
- collections guides for digital material which are underpinned by code working with those collections but are displayed as pretty HTML 
- slides can be built directly from notebooks.

Some tools for doing this type of transformation or publishing

- [`nbconvert`](https://nbconvert.readthedocs.io/en/latest/): a Swiss army knife for converting notebooks to other formats
- [`Jupyter book`](jupyterbook.org/): Jupyter Book is an open-source project for building beautiful, publication-quality books and documents from computational material. 
- [`fastpages`](https://github.com/fastai/fastpages): fastpages uses GitHub Actions to simplify the process of creating Jekyll blog posts on GitHub Pages from a variety of input formats.
- [`rise`](https://github.com/damianavila/RISE): RISE allows you to instantly turn your Jupyter Notebooks into a slideshow. No out-of-band conversion is needed, switch from jupyter notebook to a live reveal.js-based slideshow in a single keystroke, and back.


#### Examples:

- [V&A Data Explorations](http://developers.vam.ac.uk/notebooks/data-explorations/intro.html) an example of a Jupyterbook for aiding collection exploration
- [Introduction to Cultural Analytics & Python](https://melaniewalsh.github.io/Intro-Cultural-Analytics/welcome.html) an example of using a Jupyter Book for course materials
- [https://covid19dashboards.com/]() an example of fastpages being used to create dashboards that automatically updates
- [github.com/living-with-machines/github_stats_report]() an example showing `nbconvert` being used as a way of producing a report as an HTML page from a notebook. 


