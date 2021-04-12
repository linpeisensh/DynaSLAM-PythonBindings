# DynaSLAM-PythonBindings
A python wrapper for DynaSLAM, which can be found at [https://github.com/BertaBescos/DynaSLAM]
This is designed to work with the base version of DynaSLAM, with a couple of minimal API changes to access the system output.
It has been tested on ubuntu 14.04 and 16.04 and built against Python3, although it does not rely on any python3 features.

## Installation

### Prerequesities

- DynaSLAM source code
- DynaSLAM compiliation dependencies (Pangolin, Eigen, OpenCV)
- Boost, specifically its python component (python-36)
- Numpy development headers (to represent images in python, automatically converted to cv::Mat)

### Setup

#### Modifying DynaSLAM
First, we need an additional API method from ORBSLAM to extract completed trajectories.
Apply the patch file "orbslam-changes.diff" to the DynaSLAM source, which should create an additional method and add some installation instructions to the end of CMakeLists.txt.
Build orbslam as normal, and then run `make install`. This will install the DynaSLAM headers and .so to /usr/local
(if an alternative installation directory is desired, specify it to cmake using `-DCMAKE_INSTALL_PREFIX=/your/desired/location`).

#### Compilation
Return to the ORBSLAM-Python source, build and install it by running
```
mkdir build
cd build
cmake ..
make
make install
```
This will install the .so file to /usr/local/lib/python3.5/dist-packages, such that it should 
If you have changed the install location of DynaSLAM, you need to indicate where it is installed using ``-DORB_SLAM2_DIR=/your/desired/location``,
which should be the same as the install prefix above (and contain 'include' and 'lib' folders).

Verify your installation by typing
```
python3
>>> import orbslam2
```
And there should be no errors.

#### Examples

DynaSLAM's examples have been re-implemented in python in the examples folder.
Run them with the same parameters as the ORBSLAM examples, i.e.:
```
python3 orbslam_mono_kitti.py [PATH_TO_ORBSLAM]/Vocabulary/ORBvoc.txt [PATH_TO_ORBSLAM]/Examples/Monocular/KITTI00-02.yaml [PATH_TO_KITTI]/sequences/00/
```

#### Alternative Python Versions

At the moment, CMakeLists is hard-coded to use python 3.5. If you wish to use a different version, simply change the boost component used (python-35) to the desired version (say, python-27), on line 38 of CMakeLists.txt.
You will also need to change the install location on line 73 of CMakeLists.txt to your desired dist/site packages directory.

## License
This code is licensed under the BSD Simplified license, although it requires and links to DynaSLAM, which is available under the GPLv3 license

It uses pyboostcvconverter (https://github.com/Algomorph/pyboostcvconverter) by Gregory Kramida under the MIT licence (see pyboostcvconverter-LICENSE).

