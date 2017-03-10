# Eager
An Ogre3D 1.9 and C++ project template that uses cmake to generate project files.

You can fork this repo and work on the files in the source directory.

[Click here for instructions on keeping your fork up to date with this repo.](https://help.github.com/articles/syncing-a-fork/)

## Instructions
### Building your Project

* [Linux using a Makefile or Eclipse](#gnu-make-linux)
* [Windows using Visual Studio](#windows-with-visual-studio-2015)
* [Any platform using Vagrant and a Linux Virtual Machine](#vagrant)

### Additional Libraries

In order to use the optional additional libraries below, you must make sure this repo's submodules have been cloned.
Run this command in the repo directory:

```bash
git submodule init && git submodule update --remote --merge
```

#### Libraries

* [Bullet Physics](bullet)

You can append more than one of these options to get any combination of additional libraries.

## Building Your Project
### GNU Make (Linux)

>  Check the [building OGRE from source](#building-ogre-from-source) section if anything fails here.

First, clone the repo (or fork it!):

```bash
git clone https://github.com/matthewjberger/eager
```

Then to build, use [CMake](https://cmake.org/):

```bash
cd eager
mkdir build
cd build

# To generate makefiles and build
cmake ..
make

# Alternatively, to generate an eclipse project
cmake -G "Eclipse CDT4 - Unix Makefiles" -D CMAKE_BUILD_TYPE=Debug ..
```

This will generate a makefile in the `build` directory.

You can open this folder as a project in eclipse if you generated eclipse project files, using the following instructions from the cmake wiki:

To import the created project file into Eclipse:

    1.) Import project using Menu File->Import
    2.) Select General->Existing projects into workspace:
    3.) Browse where your build tree is and select the root build tree directory. Keep "Copy projects into workspace" unchecked.
    4.) You get a fully functional eclipse project

Finally, when you compile, your project can be found in the `bin` directory.

### Windows with Visual Studio 2015

##### This requires CMake 3.8. [Click here to download CMake 3.8.](https://cmake.org/download/)

First, clone or fork this repo, and then:

1.) Install `Visual Studio 2012` express:

> [https://www.microsoft.com/en-us/download/details.aspx?id=34673](https://www.microsoft.com/en-us/download/details.aspx?id=34673)

2.) Install `Visual Studio 2015` Community:

> [https://www.visualstudio.com/vs/community/](https://www.visualstudio.com/vs/community/)

3.) Install `DirectX 9`:

> [https://www.microsoft.com/en-us/download/details.aspx?id=6812](https://www.microsoft.com/en-us/download/details.aspx?id=6812)

4.) Download the `OGRE SDK` for `Visual Studio 2012`:

> [http://sourceforge.net/projects/ogre/files/ogre/1.9/1.9/OgreSDK_vc11_v1-9-0.exe/download](http://sourceforge.net/projects/ogre/files/ogre/1.9/1.9/OgreSDK_vc11_v1-9-0.exe/download)

5.) Run the `Ogre SDK` executable to extract the `Ogre SDK` to a directory on your computer.

6.) Set an environment variable named `OGRE_HOME` to the root path of the extracted SDK folder

7.) Create a directory named `build` inside the root of your clone of this repository.

8.) Generate a `Visual Studio 2015` solution and project files:

```bash
cmake -G "Visual Studio 14 2015" -T v110 ..
```

9.) Open the solution located in the `build` folder.

* There will be a prompt asking you to 'upgrade' your project. You should hit cancel on this dialog, as we don't want to upgrade.

10.) Finally, when you run your program make sure you choose `DirectX 9` or `OpenGL` as your renderer backend.

###### Note: Consider using [Precompiled Headers](http://www.ogre3d.org/tikiwiki/Precompiled+headers), which can speed up the build time significantly.

### Vagrant

This will generate an ubuntu virtual machine with eclipse, cmake, and the Ogre3D library built from source and installed.

After loading up this virtual machine, you can follow the build instructions above for working on your project.

1.) [Install Vagrant](https://www.vagrantup.com/downloads.html)

2.) [Install Virtualbox](https://www.virtualbox.org/wiki/Downloads)

3.) Clone this repo with:

```bash
git clone https://github.com/matthewjberger/eager
cd eager
```

4.) Enter the following command:

```bash
vagrant up
```

> Username: `vagrant`

> Password: `vagrant`

The virtual machine will be downloaded and then opened in VirtualBox. You can login with the password `vagrant`. The files in this repo are in the folder `~/Code/eager` which is also shared with the host.

####Note: If there is an issue with the mouse while running a 3D program that captures the mouse, hit `ctrl+home` and then go to `input->mouse integration` and disable it. This can be re-enabled when you're finished running the program.

## Building OGRE from Source

#### Note: If you're using the ecc computers at the University of Nevada, Reno, the following steps are not required. The library has already been built from source and installed. However, if you are using NoMachine the code will compile but to run you must use the command below:
> /usr/NX/scripts/vgl/vglrun \<your project's .bin path here\>

Ogre 3D must be installed. If it isn't installed you should build it from the source with the following commands.  Mercurial is required to clone the repo.


### Ubuntu (or any Debian-Based Linux distribution)

Download the required dependencies:

``` bash
sudo apt-get install libfreetype6-dev libfreeimage-dev libzzip-dev libxrandr-dev libxaw7-dev freeglut3-dev libgl1-mesa-dev libglu1-mesa-dev libcppunit-dev libboost-thread-dev libois-dev mercurial cmake g++ gdb doxygen
```

Clone the repo and grab version 1.9:

```bash
hg clone https://bitbucket.org/sinbad/ogre
cd ogre
hg pull
hg update v1-9
```

Use cmake to generate a makefile:

```bash
mkdir build
cd build
cmake ..
```

Build OGRE:

```bash
make -j5
```

Install the library:

```bash
sudo make install
```

## Additional Libraries

### Bullet

Append the `-DINCLUDE_BULLET=ON` when you generate your project file with cmake:

```bash
# Make
cmake .. -DINCLUDE_BULLET=ON

# Eclipse
cmake -G "Eclipse CDT4 - Unix Makefiles" -D CMAKE_BUILD_TYPE=Debug .. -DINCLUDE_BULLET=ON

# Visual Studio 2015
cmake -G "Visual Studio 14 2015" -T v110 .. -DINCLUDE_BULLET=ON
```
