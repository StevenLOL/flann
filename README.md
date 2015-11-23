FLANN - Fast Library for Approximate Nearest Neighbors
======================================================

FLANN is a library for performing fast approximate nearest neighbor searches in high dimensional spaces. It contains a collection of algorithms we found to work best for nearest neighbor search and a system for automatically choosing the best algorithm and optimum parameters depending on the dataset.
FLANN is written in C++ and contains bindings for the following languages: C, MATLAB, Python, and Ruby.


Documentation
-------------

Check FLANN web page [here](http://www.cs.ubc.ca/research/flann).

Documentation on how to use the library can be found in the doc/manual.pdf file included in the release archives.

More information and experimental results can be found in the following paper:

  * Marius Muja and David G. Lowe, "Fast Approximate Nearest Neighbors with Automatic Algorithm Configuration", in International Conference on Computer Vision Theory and Applications (VISAPP'09), 2009 [(PDF)](http://people.cs.ubc.ca/~mariusm/uploads/FLANN/flann_visapp09.pdf) [(BibTex)](http://people.cs.ubc.ca/~mariusm/index.php/FLANN/BibTex)


Getting FLANN
-------------

The latest version of FLANN can be downloaded from here:

 *  Version 1.8.4 (15 January 2013)
    [flann-1.8.4-src.zip](http://people.cs.ubc.ca/~mariusm/uploads/FLANN/flann-1.8.4-src.zip) (Source code)  
    [User manual](http://people.cs.ubc.ca/~mariusm/uploads/FLANN/flann_manual-1.8.4.pdf)  
    [Changelog](https://github.com/mariusmuja/flann/blob/master/ChangeLog)  

If you want to try out the latest changes or contribute to FLANN, then it's recommended that you checkout the git source repository: `git clone git://github.com/mariusmuja/flann.git`

If you just want to browse the repository, you can do so by going [here](https://github.com/mariusmuja/flann).


Conditions of use
-----------------

FLANN is distributed under the terms of the [BSD License](https://github.com/mariusmuja/flann/blob/master/COPYING).

Bug reporting
-------------

Please report bugs or feature requests using [github's issue tracker](http://github.com/mariusmuja/flann/issues).






#How to install?
To say you have ubuntu, then:

~~~
sudo apt-get install python-dev cmake gcc openssh-server git
wget https://github.com/pypa/pip/raw/master/contrib/get-pip.py
sudo python ./get-pip.py
sudo pip install numpy scipy
git clone https://github.com/mariusmuja/flann.git
~~~

Go the folder flann
~~~
mkdir build
cd build
cmake ..
make all
sudo make install
~~~


To test, create a python file, eg yourPython.py with following content:

~~~

#coding=utf-8
from pyflann import *
from numpy import *
from numpy.random import *

dataset = rand(10000, 400)
testset = rand(1000, 400)
flann = FLANN()
#建索引，自动调参数,　会运行很多词建立很多索引，目的是找到最佳参数
params = flann.build_index(dataset, algorithm="autotuned", target_precision=0.9, log_level = "info");
#打印最佳参数，以后就可以用最佳参数，直接建立一个索引
print params
#保存索引，以后就可以直接load index
flann.save_index('./temp.index.bin')
#测试建立的索引，找出最近的５五个
result, dists = flann.nn_index(testset,5, checks=params["checks"]);
#打印检索结果，包含每个测试向量的　5 个临近向量的　index ，就是在dataset 里面的序列号
print result
#打印出　测试向量到　5个临近向量的距离
print dists

~~~

Then python ./yourPython.py

Done!
