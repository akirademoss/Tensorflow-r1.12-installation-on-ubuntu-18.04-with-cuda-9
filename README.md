# Install Tensorflow r1.12 on Ubuntu 18.04 with cuda 9
This file contains step by step instructions to build Tensorflow r1.12 from sources with cuda v9.0 on Ubuntu 18.04.  A prerequisite is to have cuda v9.0 installed.  Instructions on doing this can be found [here](https://github.com/akirademoss/cuda-9.0-installation-on-ubuntu-18.04). 

## Summary of Steps 
```
1.) Install Bazel 0.15.2
2.) Instal NCCL 2.1.15
3.) Install Python 3.6
4.) Build and install Tensorflow r1.12 from source

```

## 1.) Install Bazel 0.15.2

#### Bazel needs a C++ compiler and unzip / zip in order to work:
```
sudo apt-get install g++ unzip zip
```

#### 1.1)  If you want to build Java code using Bazel, install a JDK:
```
# Ubuntu 18.04 (LTS) uses OpenJDK 11 by default:
sudo apt-get install openjdk-11-jdk
```

#### 1.2)  download the installer by [bazel-0.15.2-installer-linux-x86_64.sh](https://github.com/bazelbuild/bazel/releases/download/0.15.2/bazel-0.15.2-installer-linux-x86_64.sh) installer.
```
cd ~/Downloads/
chmod +x bazel-0.15.2-installer-linux-x86_64.sh
./bazel-0.15.2-installer-linux-x86_64.sh --user
```
The ```--user``` flag installs Bazel to the ```$HOME/bin``` directory on your system and sets the ```.bazelrc``` path to ```$HOME/.bazelrc```. Use the --help command to see additional installation options.

#### 1.3)  If you ran the Bazel installer with the --user flag as above, the Bazel executable is installed in your $HOME/bin directory. It’s a good idea to add this directory to your default paths, as follows: note that you will need to swap 'your-username-here' with your username.  
You need to run '''source ~/.bashrc''' anytime you use update the file for it to take effect in your terminal.  Verify the install by noting the output of bazel version
```
echo 'export PATH=/home/your-username-here/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
bazel version
```

## 2.) Install NCCL 2.1.15

#### 2.1)  If you do not already have an account with nvidia, you will need to [create an account here](https://developer.nvidia.com/nccl/nccl-download)

Download the file ```NCCL 2.1.15 O/S agnostic and CUDA 9```

#### 2.2) Go to downloads folder, extract, and copy contents to the specified directories
```
cd ~/Downloads
mkdir nccl_2.1
tar -xf nccl_2.1.15-1+cuda9.0_x86_64.txz 
cd nccl_2.1.15-1+cuda9.0_x86_64
cp -R * ~/Downloads/nccl_2.1
sudo mv ~/Downloads/nccl_2.1 /usr/local/
sudo ldconfig
```

## 3.)  Install Python 3.6

#### 3.1)  First check to see if python3.6 is already installed.  If it is, you can skip the next step.
```
python3 --version
```

#### 3.2)  Simply run the commandlines to aquire Python 3.6, pip3, and virtualenvs from the package manager
```
sudo apt-get install python3.6-dev
sudo apt install python3-pip
sudo pip3 install virtualenv virtualenvwrapper
```

#### 3.2)  Check to see if you have virtualenvwrapper setup
If the output to this command is mkvirtualenv: command not found proceed to the next step.  Otherwise skip step 3.3.
```
mkvirtualenv dl4cv
```

#### 3.3)  Setup virtualenvwrapper. To read more about using virtualenvwrappers [check out this link](https://itnext.io/virtualenv-with-virtualenvwrapper-on-ubuntu-18-04-goran-aviani-d7b712d906d5)
Also note that your-username-here must be replaced with your actual username.
```
mkdir ~/.virtualenv
echo '# virtualenvwrapper setup' >> ~/.bashrc
echo 'export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3' >> ~/.bashrc
echo 'export WORKON_HOME=$HOME/.virtualenvs' >> ~/.bashrc
echo 'export VIRTUALENVWRAPPER_VIRTUALENV=/home/your-username-here/.local/bin/virtualenv' >> ~/.bashrc
echo 'source ~/.local/bin/virtualenvwrapper.sh' >> ~/.bashrc
source ~/.bashrc
```

#### 3.4)  Create a virtual envelope to install your tensorflow to, and start working on it.  While working on this virtualenvelopewrapper python packages you install will be installed to the /home/your-username-here/.virtualenvs dir.  This is helpful when it comes to managing dependencies.
```
mkvirtualenv dl4cv
workon dl4cv
```


## 4.)  Build and install Tensorflow r1.12 from source

#### 4.1)  Create a Software directory then change into this directory. 
```
mkdir ~/Software
cd ~/Software
```

#### 4.2)  Clone the tensorflow repo, next change into tensorflow directory, then checkout r1.12, finally configure the tensorflow build
```
git clone https://github.com/tensorflow/tensorflow.git
cd tensorflow
git checkout r1.12
./configure
```

#### 4.3) The configure screen will give you several options.  
Note that the compute capability will depend on your hardware.  verify your gpu and it's compute capability [using this link](https://developer.nvidia.com/cuda-gpus)

Please specify the location of python. [Default is /usr/bin/python]: /usr/bin/python3.6

Do you wish to build TensorFlow with Apache Ignite support? [Y/n]: n

Do you wish to build TensorFlow with XLA JIT support? [Y/n]: n

Do you wish to build TensorFlow with OpenCL SYCL support? [y/N]: n

Do you wish to build TensorFlow with ROCm support? [y/N]: n

Do you wish to build TensorFlow with CUDA support? [y/N]: Y

Please specify the CUDA SDK version you want to use. [Leave empty to default to CUDA 9.0]: 9.0

Please specify the location where CUDA 10.0 toolkit is installed. Refer to Home for more details. [Default is /usr/local/cuda]: /usr/local/cuda-9.0

Please specify the cuDNN version you want to use. [Leave empty to default to cuDNN 7]: 7.3

Please specify the location where cuDNN 7 library is installed. Refer to README.md for more details. [Default is /usr/local/cuda-10.0]: /usr/local/cuda-9.0/

Do you wish to build TensorFlow with TensorRT support? [y/N]: N

Please specify the NCCL version you want to use. If NCCL 2.2 is not installed, then you can use version 1.3 that can be fetched automatically but it may have worse performance with multiple GPUs. [Default is 2.2]: 2.1

Please specify the location where NCCL 2.3.5 is installed. Refer to README.md for more details. [Default is /usr/local/cuda-10.0]: /usr/local/nccl_2.1

Please note that each additional compute capability significantly increases your build time and binary size. [Default is: 5.0] 5.0

Do you want to use clang as CUDA compiler? [y/N]: N

Please specify which gcc should be used by nvcc as the host compiler. [Default is /usr/bin/gcc-6]: /usr/bin/gcc-6

Do you wish to build TensorFlow with MPI support? [y/N]: N

Please specify optimization flags to use during compilation when bazel option "--config=opt" is specified [Default is -march=native]: -march=native

Would you like to interactively configure ./WORKSPACE for Android builds? [y/N]:N

Configuration finished


#### 4.4) The next step in the process to install tensorflow GPU version will be to build tensorflow using bazel. This process takes a fairly long time.
```
bazel build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package --config=monolithic
```

