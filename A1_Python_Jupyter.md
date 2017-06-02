## Generate download link
from IPython.display import FileLink
%cd xxx
FileLink('data/'+filename)


## How to auto reload extrnal modules
```
# for auto-reloading external modules
# see http://stackoverflow.com/questions/1907993/autoreload-of-modules-in-ipython
%load_ext autoreload
%autoreload 2
```

## Control Matplot
```
%matplotlib inline
plt.rcParams['figure.figsize'] = (10.0, 8.0) # set default size of plots
plt.rcParams['image.interpolation'] = 'nearest'
plt.rcParams['image.cmap'] = 'gray'
```

Other option (using [seaborn](https://seaborn.pydata.org/))
```
import seaborn as sns
sns.set_context("paper")
```

