# install build requirements
sudo apt-get install python-dev python-setuptools swig -y

# download my fork of the wiringpy-python build that contains submodile to wiringOP library
git clone --recursive https://github.com/DaniyalGeek/wiringop-python.git

# build C and install both Wiring Pi C library and Python
cd wiringop-python
cd WiringPi/
sudo ./build
cd ..
export CFLAGS="-lwiringPi -lwiringPiDev"
swig2.0 -python wiringpi.i
sudo python setup.py install

# enable gpio kernel module
sudo sed -i 's/\#gpio_sunxi/gpio_sunxi/g' /etc/modules
sudo modprobe gpio_sunxi
