# Installing Adalm Pluto

This sequence of installing commands for Adalm Pluto Python API is similar to the one found in [pysdr.org](https://pysdr.org/content/pluto.html) but it has been modifyed to enabe conda environment installation and a correct api installation with pip.


## Phase 1: install essentials and create python environment

```
conda create -n pluto
conda activate pluto
mkdir ~/pluto

sudo apt-get install build-essential git libxml2-dev bison flex libcdk5-dev cmake libusb-1.0-0-dev libavahi-client-dev libavahi-common-dev libaio-dev
conda install jupyterlab numpy scipy pip matplotlib
```

## Phase 2: install libiio

```
cd ~/pluto
git clone --branch v0.23 https://github.com/analogdevicesinc/libiio.git
cd libiio
mkdir build
cd build
cmake -DPYTHON_BINDINGS=ON ..
make -j$(nproc)
sudo make install
sudo ldconfig
```

## Phase 3: install libadi9361

```
cd ~/pluto
git clone https://github.com/analogdevicesinc/libad9361-iio.git
cd libad9361-iio
mkdir build
cd build
cmake ..
make -j$(nproc)
sudo make install
```

## Phase 4: install python api


```
cd ~/pluto
git clone --branch v0.0.14 https://github.com/analogdevicesinc/pyadi-iio.git
cd pyadi-iio
conda install paramiko
pip install .
```