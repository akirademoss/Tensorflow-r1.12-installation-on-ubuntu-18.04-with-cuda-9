# Tensorflow r1.12 installation on Ubuntu 18.04 with cuda 9
This file contains step by step instructions to build Tensorflow r1.12 from sources with cuda v9.0 on Ubuntu 18.04.  A prerequisite is to have cuda v9.0 installed.  Instructions on doing this can be found [here](https://github.com/akirademoss/cuda-9.0-installation-on-ubuntu-18.04). 

## Summary of Steps 
```
1.) Install Bazel v0.15.2

```

## 1.) Install Bazel v0.15.2

#### Bazel needs a C++ compiler and unzip / zip in order to work:
```
sudo apt-get install g++ unzip zip
```

#### If you want to build Java code using Bazel, install a JDK:
```
# Ubuntu 16.04 (LTS) uses OpenJDK 8 by default:
sudo apt-get install openjdk-8-jdk

# Ubuntu 18.04 (LTS) uses OpenJDK 11 by default:
sudo apt-get install openjdk-11-jdk
```

#### download the installer by [bazel-0.15.2-installer-linux-x86_64.sh](https://github.com/bazelbuild/bazel/releases/download/0.15.2/bazel-0.15.2-installer-linux-x86_64.sh) installer.
```
cd ~/Downloads/
chmod +x bazel-0.15.2-installer-linux-x86_64.sh
./bazel-0.15.2-installer-linux-x86_64.sh --user
```
The ```--user``` flag installs Bazel to the ```$HOME/bin``` directory on your system and sets the ```.bazelrc``` path to ```$HOME/.bazelrc```. Use the --help command to see additional installation options.

#### If you ran the Bazel installer with the --user flag as above, the Bazel executable is installed in your $HOME/bin directory. It’s a good idea to add this directory to your default paths, as follows: note that you will need to swap 'your-username-here' with your username.  
You need to run '''source ~/.bashrc''' anytime you use update the file for it to take effect in your terminal.  Verify the install by noting the output of bazel version
```
echo 'export PATH=/home/your-username-here/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
bazel version
```

## 2.) Install Python 3.6, pip3 and virtualenvs.

#### Simply Run the commandlines and aquire these from the package manager
```
sudo apt-get install python3.6-dev
sudo apt install python3-pip
sudo pip3 install virtualenv virtualenvwrapper
```

## 3.) Build Tensorflow from Sources

#### Create a Software directory then change into this directory. 
```
mkdir ~/Software
cd ~/Software
```

#### Clone the tensorflow repo, next change into tensorflow directory, then checkout r1.12, finally configure the tensorflow build
```
git clone https://github.com/tensorflow/tensorflow.git
cd tensorflow
git checkout r1.12
./configure
```

#### 
```
```

#### 
```
```

#### 
```
```

#### 
```
```

## 4.) 

#### 
```
```

## 5.) 

#### 
```
```

#### 
```
```

#### 
![nvidia-smi](https://user-images.githubusercontent.com/8731829/50403622-ae5e0780-0765-11e9-96c3-cf649dbaeac3.png)

