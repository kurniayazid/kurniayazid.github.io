---
title: 'Setting up a virtual environment for a Python project'
subtitle: 'The only guidance that newbie needs'
date: 2022-11-23
permalink: /posts/2022/11/settingup-python-venv
excerpt_separator: <!--more-->
toc: true
tags:
  - python
  - data-science
  - setup
  - vscode
  - virtual-environment
---
![](https://cdn-images-1.medium.com/max/1600/0*CHeZLTREb9TytmZu)

*Photo by Kelvin Han on Unsplash*

I need to write this on a post because I keep forgetting this by the time I need to create a new python project. Plus, I always get confused when figuring out to set up a Python virtual environment, so I did my research and created new blog posts to help other students in understanding the virtual environment.

<!--more-->

To begin with, we should start with the definition. What kind of animal a virtual environment, or also known as venv/virtualenv, is? Let me answer this by giving you an example.

Suppose you are working on a python project to create a python package using Pandas version 1.0 as one of the dependencies. In the next month, all of the sudden, you need to update your Pandas to version 2.0 on your PC because it provides you with the tools/functions that are more practical. However, the thing is, tools in the older version (1.0) get obsolete and are no longer used in the newer version. As a result, your python package is no longer can be used unless you update the package by employing all the Pandas tools in the newer version - in other words, you should start over your project. This is only one example among many other possibilities you would never expect and/or want to deal with.

With a Python venv, you can easily switch between Python versions and dependencies. Therefore, your package can still be used because they hold the python versions and dependencies in a sort of "virtual environment". But, bearing in mind that you're stuck with your host OS - to switch between OS you need tools called Docker (I will cover this in other posts).

One more thing is we have several types of Python virtual environment generators. Two popular ones are `pyenv` and `conda`. Then, what are the differences? and which one should I pick up?

### Python virtual environment generators: pyenv + poetry vs conda

`pyenv + poetry`
- `pyenv` is can manage multiple Python versions;
- You can set up which Python you'd like to use in your current session, globally, or on a per-project basis as well;
- All in all, `pyenv + poetry` is more lightweight, and it is best for general-purposes

`conda`
- `conda` usually comes with other data science packages when you're installing Anaconda (or Miniconda). You are probably more familiar with this when learning your very first Python course.
- It is geared towards the data science community and tends to package the most common data science dependencies along with basic python (engineers prefer the more lightweight `pyenv` rather than keeping other unnecessary data science packages)
- `conda` provides package and environment management in one tool
- Overall, I recommend you use conda if the project is heavily about data analysis

And, many more …

You can see a more detailed comparison by [Jonathan Bowman](https://dev.to/bowmanjd/python-tools-for-managing-virtual-environments-3bko).

## Setting up a Python virtualenv using pyenv + poetry

In this article, I will use `pyenv + poetry` to setup Python virtualenv. If you have already installed `pyenv` and `poetry` , you can skip number 1 and start from number 2.

### 1. Install pyenv and poetry
Actually to install both packages, you can just easily look at the documentations. But which newbie that looks at the documentation? Here I show you the easy way, particularly for mac user.
First, you can install `pyenv` using `brew`:

```bash
brew install pyenv
```

Once you finish installing `pyenv`, don't forget to submit this kind of snippet on your bash terminal:

```bash
export PATH="home/ega/.pyenv/bin$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"

# Don't worry, you do not need to copy this.
# Your terminal will provide this after you install pyenv
```

Then try to install few of python versions through pyenv , in this example, I try to install two python versions which are 3.9.1 and 3.10.6 .

```bash
pyenv install 3.9.1
pyenv install 3.10.6
```

You can check the available Python versions by inputting this command on your terminal:

```bash
pyenv versions
```
The code will generate output that looks like this:

![](https://github.com/kurniayazid/kurniayazid.github.io/blob/master/images/posts/image.png?raw=true)

From the terminal above, we can see that the available Python or pyenv versions are only two, which are `Python 3.9.1` and `Python 3.10.6` . You can specify the global Python version for your machine by implementing:

The command above will set your global python version on your machine as version 3.10.6. In other words, when you are trying to use Python on your machine, without setting up the virtualenv, you will use version 3.10.6.

While you can specify the python version for your working directory using this command:

```bash
pyenv local 3.10.6
```

You can remove the version, let it as pyenv local to check whether you have specified the pyenv local. If it returns your expected version, then you are good to go.

Then, we can install the poetry by using pip , which I prefer. The documentation suggests us to install through brew but a Python Youtube educator, [Carlos Kidman](https://www.youtube.com/watch?v=547Jr26duHQ&list=PLMs2vUk844WJGj4H-7vemH4nSWrd42b_6&index=4&ab_channel=QAatthePoint%7CCarlosKidman), recommended us to install it using `pip` to make sure we install it in the global python interpreter - yes we need to install poetry globally. Technically, like this:

```bash
pip install poetry
```

Once you finish installing poetry, don't forget to submit this snippet on your bash terminal:

```bash
export PATH=$PATH:$HOME/.poetry/bin
```

### 2. Specify pyenv local and initiate poetry in working directory

> Protip: I will recommend you use an integrated development environment (IDE) such as Virtual Studio Code (VScode) for easier and more intuitive project management.

If this your first time using `pyenv` and `poetry `, then it will be more appropriate to setup your IDE (Visual Studio Code / VScode).

Open your VScode, and don't forget to open the built-in terminal in the VScode (you can check this on your Window option). Moreover, after you install pyenv and poetry on your machine (PC or laptop), you need to specify your working directory in your terminal (if you're using macOS):

```bash
cd $Path
```

Change `$Path` with your working directory path. Furthermore, set up your local python version using `pyenv `. You can do that by executing the following command code in your terminal:

```bash
pyenv local 3.10.6
```

In this case, I will set python version 3.10.6 in my working directory. Afterward, we need to set up the `poetry`:

```bash
poetry init
```

### 3. Adding python dependencies

By executing the command above, poetry will guide you to create `pyproject.toml` for your project. Poetry will ask you several questions from the project name, to the dependencies you required for the project. No worries, you will always can edit it later.

To adding the python dependencies you can use this `poetry add` command on your terminal. For example you want to install `pandas` and `plotly`:

```bash
# Adding pandas latest version
poetry add pandas

# Adding plotly for specific version
poetry add plotly==0.1.0
```

### 4. Installing poetry dependencies

With a `pyproject.toml` file in the working directory, you can create the virtual environment using this command in the VScode terminal:

```bash
poetry install
```

The command will install all the required dependencies and virtual environment settings, and it will create `poetry.lock` file. You can check the information of your virtual environment by executing this command:

```bash
# general info
poetry env info

# env path info
poetry env info --path 

# you need to copy the path from the second command for VScode py interpreter
```

The next step is, make sure that you have installed `Python` and `Pylance` extensions on your VS code. After that, open the command pallete and try to type `Python: select interpreter` . Click enter, and paste the path that you got from the previous command.

Finally, to activate the virtual environment, run this code:

```bash
poetry shell
```

Hopefully, by following all the steps above, your python virtual environment should have already been running on your working directory. Do not forget to connect this with your GitHub repository! I will cover this later in the upcoming posts.


---

Cheers,

Ega Kurnia Yazid

I welcome feedback and constructive criticism. To discuss further you can comment on each post, or you can reach me through any social media platforms you can find on my webpage.