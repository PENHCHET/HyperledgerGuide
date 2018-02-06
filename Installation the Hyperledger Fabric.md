# ការដំឡើង Hyperledger Fabric V1.0 ពី Source Code នៅលើ Ubuntu 16.04 LTS

នៅក្នុងរបៀបដំឡើងនេះដែរ យើងនឹងបង្ហាញពីរបៀបដំឡើង Hyperledger Fabric V1.0 ពី Source Code។ ហើយនៅក្នុងការដំឡើងនោះផងដែរ យើងបានបែងចែកចេញជាពីរជំហ៊ានធំៗ
ដែលជំហ៊ានទីមួយ នឹងនិយាយអំពីការដំឡើងនូវ Packages មួយចំនួនដែលយើងនឹងត្រូវប្រើប្រាស់នៅក្នុងការដំឡើង Hyperledger Fabric និង ជំហ៊ានបន្ទាប់ខ្ញុំនឹងបង្ហាញពីរបៀបដំឡើង Hyperledger Fabric តែម្តង។

## និយាយពីការដំឡើងនូវ Packages 

យើងត្រូវការដំឡើងដូចខាងក្រោម ចំនួន៧ ដែលចាំបាច់សម្រាប់ Hyperledger Fabric:
1. Go Language: https://golang.org/ 
1. GNU libtool: Dynamic Linking Loader (libltdl-dev): 
https://packages.debian.org/sid/libltdl-dev 
1. Docker: https://www.docker.com/ 
1. Docker Compose: https://docs.docker.com/compose/
1. Pip: https://pypi.python.org/pypi/pip 
1. Git: https://git-scm.com/ 
1. Curl: https://curl.haxx.se/

ធ្វើការប្រើប្រាស់នូវ Commands ខាងក្រោមទាំងអស់តាមរយះ Terminal 

### ១. Go Language:
យើងត្រូវធ្វើការដោនឡូត និង ធ្វើការពន្លាវា ចំពោះ Hyperledger Fabric Go Language Version ទាបបំផុតដែលអាចប្រើប្រាស់បានគឺ Version 1.7
```
$ wget https://dl.google.com/go/go1.9.3.linux-amd64.tar.gz

$ tar -xvf go1.9.3.linux-amd64.tar.gz
```

បន្ទាប់មកយើងធ្វើការកំណត់នូវ Environment Variables មួយចំនួន
```
$ mkdir $HOME/gopath

$ export GOPATH=$HOME/gopath

$ export GOROOT=$HOME/go

$ export PATH=$PATH:$GOROOT/bin
```

### ២. GNU libtool: libltdbl-dev
ដំឡើងនូវ libltdl-dev ដោយប្រើប្រាស់នូវ apt-get
```
$ sudo apt-get install libltdl-dev
```

### ៣. ដំឡើង Docker
```
$ echo 'Removing docker docker-engine docker.io...'
$ sudo apt-get remove docker docker-engine docker.io
$ echo 'Updating...'
$ sudo apt-get update
$ sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo apt-key fingerprint 0EBFCD88
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
$ echo 'Updating...'
$ sudo apt-get update
$ sudo apt-get install -y docker-ce
$ sudo apt-get install -y libltdl3-dev
$ sudo apt-get install -y build-essential
$ sudo usermod -aG docker $(whoami)
```

### ៤. ដំឡើង Docker Compose
```
$ sudo curl -o /usr/local/bin/docker-compose -L "https://github.com/docker/compose/releases/download/1.11.2/docker-compose-$(uname -s)-$(uname -m)"
$ sudo chmod +x /usr/local/bin/docker-compose
```

### ៥. ដំឡើង Pip
```
$ sudo apt-get install python-pip 
```

### ៦. ដំឡើង Git
```
$ sudo apt-get install -y git

# ពិនិត្យមើល git version
$ git --version
```

### ៧. ដំឡើង Curl
```
$ sudo apt-get install -y curl

# ពិនិត្យមើល curl version
$ curl --version
```

## ជំហ៊ានចុងក្រោយនិយាយពីការដំឡើង Hyperledger Fabric 

```
$ mkdir -p $GOPATH/src/github.com/hyperledger/
$ cd $GOPATH/src/github.com/hyperledger/ 

# Clone the fabric 
$ git clone https://github.com/hyperledger/fabric.git

$ cd fabric

# Reset commit level to fabric v1.0.2
$ git reset --hard 5fb31ddd24d6441b0d499b9bb211632800044512

# Compile and install fabric
$ make

# Verification by running end to end test
$ cd examples/e2e_cli && ./network_setup.sh up
```

### ប្រសិនបើយើងឃើញនៅព៏ត៌មានដូចខាងក្រោម នោះមានន័យថាការដំឡើងរបស់លោកអ្នកបានជោគជ័យហើយ សូមអរគុណ
===================== All GOOD, End-2-End execution completed =====================

```
 _____   _   _   ____            _____   ____    _____
| ____| | \ | | |  _ \          | ____| |___ \  | ____|
|  _|   |  \| | | | | |  _____  |  _|     __) | |  _|
| |___  | |\  | | |_| | |_____| | |___   / __/  | |___
|_____| |_| \_| |____/          |_____| |_____| |_____|
```

### ជាចុងក្រោយយើងអាចធ្វើការ បន្ថែមនូវ Environment របស់ Hyperledger Fabric Execuables ដែលមានទីតាំងនៅក្នុង $GOPATH/src/github.com/hyperledger/fabric/build/bin

```
$ export PATH:$PATH:$GOPATH:/src/github.com/hyperledger/fabric/build/bin
```

ឬក៏អ្នកទាំងអស់គ្នាអាចកំណត់វានៅក្នុង ~/.bashrc វានឹងល្អនៅពេលដែល Server របស់យើង Restart វានឹងអាចប្រើប្រាស់វាដដែល ប្រសិនយើងប្រើប្រាស់តែ export នៅក្នុង Terminal យើងធម្មតាវានឹងលែងស្គាល់

```
$ vim ~/.bashrc

# ដាក់វានៅបន្ទាប់ក្រោមគេបង្អស់ នៅក្នុង ~/.bashrc

export PATH:$PATH:$GOPATH:/src/github.com/hyperledger/fabric/build/bin
```
