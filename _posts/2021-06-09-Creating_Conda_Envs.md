
Here are the steps:

1.  Create environment with specific Python and package versions
2.  Activate the environment
3.  List packages in environment
4.  Install PyTorch
5.  Deactivate environment
6.  List environments

### Create Environment

Enter this command in Terminal to install Python 3.6, NumPy 1.13.3, and the newest version of SciPy.  
`conda create -n pytorch python=3.6 numpy=1.13.3 scipy`

> _Note: including a conda package without a version number installs the latest and greatest by default._

### Activate Environment

You have to activate the environment to actually use it. Do this like so:  
`source activate pytorch`

### List Packages

Now we’re inside the pytorch container (notice  _pytorch_  in parantheses?). We can see which packages are installed by typing:  
`conda list`

### Install PyTorch

Let’s install PyTorch while we’re here.  
`conda install pytorch torchvision -c pytorch`

### Deactivate Environment

We can return to the root environment by typing:  
`source deactivate`

### List Environments

We can also see which environments are installed.  
`conda info --envs`
