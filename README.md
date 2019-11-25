# Tensorflow-r1.12-installation-on-ubuntu-18.04-with-cuda-9
# Cuda 9.0 installation on Ubuntu 18.04 LTS 
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

echo '' >> ~/.bashrc

#### 
```
```

## 3.) 

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

