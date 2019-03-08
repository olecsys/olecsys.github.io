Team Viewer ID: 380 028 999 XEaCBht

teamviewer info
sudo teamviewer passwd [password]

ffmpeg -f video4linux2 -i /dev/video0 -vframes 6 test%3d.jpeg
ffmpeg -f video4linux2 -i /dev/video1 -vframes 6 test%3d.jpeg

magick convert rose.jpg rose.png
mogrify -format png *.jpg

http://magicsmoke.co.za/?p=375
https://www.pyimagesearch.com/2017/10/09/optimizing-opencv-on-the-raspberry-pi/

CROSSCOMPILE
=====================
wget http://download.qt.io/official_releases/qt/5.9/5.9.2/single/qt-everywhere-opensource-src-5.9.2.tar.xz
chmod +x qt-everywhere-opensource-src-5.9.2.tar.xz

mkdir ./QT
tar xvfJ ./qt-everywhere-opensource-src-5.9.2.tar.xz -C ./QT

wget https://downloads.raspberrypi.org/raspbian_latest

# wget https://downloads.raspberrypi.org/raspbian_lite_latest
unzip raspbian_lite_latest -d raspbian

mkdir ./rasp-pi-rootfs

fdisk -l raspbian/file.img

take img2 and take Start and Sector size(logical/physical)
then:

sudo mount raspbian/file.img -o loop,offset=$(( Sector size * Start block for img2)) ./rasp-pi-rootfs

# sudo mount raspbian/*.img -o loop,offset=$((512 * 94208)) ./rasp-pi-rootfs


arm-rpi-4.9.3-linux-gnueabihf из https://github.com/raspberrypi/tools.git нельзя использовать из-за  https://github.com/raspberrypi/tools/issues/50

-------------------------------------------------------- Качаем linaro т.к. не компилируется qt проект с зависимостью от avcodec из raspbian stretch ---------------------------------------------------------------------

$ wget https://releases.linaro.org/components/toolchain/binaries/latest-5/arm-linux-gnueabihf/gcc-linaro-5.4.1-2017.05-x86_64_arm-linux-gnueabihf.tar.xz -O gcc-linaro.tar.xz
$ mkdir ./tools
$ tar xvfJ ./gcc-linaro.tar.xz -C ./tools

-------------------------------------------------------------------------------------------------------------------------или---------------------------------------------------------------------------------------------------------------------------------------------------------------------

$ git clone https://github.com/raspberrypi/tools.git

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Compile order after qtbase compiling
qtimageformats, qtsvg, qtjsbackend, qtscript, qtxmlpatterns, qtdeclarative, qtsensors, qt3d, qtgraphicaleffects, qtjsondb, qtlocation, qtdocgallery


cd ./tools

wget https://raw.githubusercontent.com/riscv/riscv-poky/master/scripts/sysroot-relativelinks.py
chmod +x ./sysroot-relativelinks.py

sudo ./sysroot-relativelinks.py ../rasp-pi-rootfs


#./configure -skip wayland -skip webkit -skip script -qt-xcb -no-pch -no-use-gold-linker -nomake tests -nomake examples -reduce-exports -release -opengl es2 -device linux-rasp-pi3-g++ -device-option CROSS_COMPILE=$BASEPATH/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin/arm-linux-gnueabihf- -sysroot $BASEPATH/sysroot -opensource -confirm-license -make libs -prefix $BASEPATH/qt5pi -extprefix $BASEPATH/qt5pi -hostprefix $BASEPATH/qt5 -v


#./configure -opengl es2 -device linux-rasp-pi-g++ -device-option CROSS_COMPILE=~/opt/gcc-4.7-linaro-rpi-gnueabihf/bin/arm-linux-gnueabihf- -sysroot /mnt/rasp-pi-rootfs -opensource -confirm-license -optimized-qmake -reduce-exports -release -make libs -prefix /usr/local/qt5pi -hostprefix /usr/local/qt5pi


#./configure -opengl es2 -device linux-rasp-pi-g++ -device-option CROSS_COMPILE=/home/olecsys/RaspberriPy/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin/arm-linux-gnueabihf- -sysroot /home/olecsys/RaspberriPy/rasp-pi-rootfs -opensource -confirm-license -optimized-qmake -reduce-exports -release -make libs -prefix /usr/local/QT5Pi -hostprefix /usr/local/QT5Pi -no-compile-examples -nomake examples -nomake tests


if x64 then:
$ sudo apt install ia32-libs
if x64  multiarch then:
$ sudo apt install lib32z1 lib32ncurses5

change -lEGL to -lbrcmEGL and -lGLESv2 to -lbrcmGLESv2 in QT/qtbase/mkspecs/devices/linux-rasp-pi3-g++/qmake.conf

-------------------------------------------------------------------------Если linaro, то --------------------------------------------------------------------------------------

Если QT 5.9.2, то убираем -skip webkit

./configure -skip wayland -skip webengine -skip multimedia -skip webview -skip script -no-compile-examples -no-directfb -no-linuxfb -no-kms -qt-xcb -no-pch -no-use-gold-linker -nomake tests -nomake examples -release -opengl es2 -device linux-rasp-pi3-g++ -device-option CROSS_COMPILE=/home/olecsys/RaspberriPy/tools/gcc-linaro-5.4.1-2017.05-x86_64_arm-linux-gnueabihf/bin/arm-linux-gnueabihf- -sysroot /home/olecsys/RaspberriPy/rasp-pi-rootfs -opensource -confirm-license -optimized-qmake -reduce-exports -release -make libs -prefix /usr/local/QT5Pi -hostprefix /usr/local/QT5Pi -v

------------------------------------------------------ или https://github.com/raspberrypi/tools.git -------------------------------------------------------

./configure -skip wayland -skip webkit -skip script -qt-xcb -no-pch -no-use-gold-linker -nomake tests -nomake examples -release -opengl es2 -device linux-rasp-pi3-g++ -device-option CROSS_COMPILE=/home/olecsys/RaspberriPy/tools/arm-bcm2708/arm-rpi-4.9.3-linux-gnueabihf/bin/arm-linux-gnueabihf- -sysroot /home/olecsys/RaspberriPy/rasp-pi-rootfs -opensource -confirm-license -optimized-qmake -reduce-exports -release -make libs -prefix /usr/local/QT5Pi -hostprefix /usr/local/QT5Pi

./configure -skip wayland -skip webkit -skip script -qt-xcb -no-pch -no-use-gold-linker -nomake tests -nomake examples -release -opengl es2 -device linux-rasp-pi3-g++ -device-option CROSS_COMPILE=/home/olecsys/RaspberriPy/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin/arm-linux-gnueabihf- -sysroot /home/olecsys/RaspberriPy/rasp-pi-rootfs -opensource -confirm-license -optimized-qmake -reduce-exports -release -make libs -prefix /usr/local/QT5Pi -hostprefix /usr/local/QT5Pi

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
make -j 4
make install

=====================

DOCKER
=====================

mkdir -p ./rasp-pi-rootfs/lib ./rasp-pi-rootfs/usr/include ./rasp-pi-rootfs/usr/lib ./rasp-pi-rootfs/opt/vc ./rasp-pi-rootfs/usr/bin ./rasp-pi-rootfs/usr/share

sudo mount raspbian/*.img -o loop,offset=$((512 * 94208)) ./TMP

cp -r TMP/lib/* rasp-pi-rootfs/lib/ ; cp -r TMP/usr/lib/* rasp-pi-rootfs/usr/lib/ ; cp -r TMP/usr/include/* rasp-pi-rootfs/usr/include/ ; cp -r TMP/opt/vc/* rasp-pi-rootfs/opt/vc/

cd Docker
docker build -t boorpi .
docker run --name rpi_qt boorpi
cd ..

docker cp <containerId>:lib/. ./rasp-pi-rootfs/lib
docker cp <containerId>:usr/include/. ./rasp-pi-rootfs/usr/include
docker cp <containerId>:usr/lib/. ./rasp-pi-rootfs/usr/lib
docker cp <containerId>:opt/vc/. ./rasp-pi-rootfs/opt/vc
# docker cp rpi_qt:lib/. ./rasp-pi-rootfs/lib ; docker cp rpi_qt:opt/vc/. ./rasp-pi-rootfs/opt/vc ;  docker cp rpi_qt:usr/share/. /home/olecsys/RaspberriPy/rasp-pi-rootfs/usr/share ; docker cp rpi_qt:usr/bin/. /home/olecsys/RaspberriPy/rasp-pi-rootfs/usr/bin ; docker cp rpi_qt:usr/lib/. ./rasp-pi-rootfs/usr/lib ; docker cp rpi_qt:usr/include/. ./rasp-pi-rootfs/usr/include

cd tools
sudo ./sysroot-relativelinks.py ../rasp-pi-rootfs
cd ..

=====================


------------------------------------------------------ Компиляция -------------------------------------------------------
$ cd ~/RaspberriPy
$ sudo mount raspbian/2017-09-07-raspbian-stretch.img -o loop,offset=$((512 * 94208)) ./rasp-pi-rootfs
$ cd ~/upwork/AaronHarnden/qcustommultimedia
$ /usr/local/QT5Pi/bin/qmake
$ make

$ cd ~/upwork/AaronHarnden/qvideoapp
$ /usr/local/QT5Pi/bin/qmake
$ make
-------------------------------------------------------------------------------------------------------------------------

Если возникает ошибка линковщика по поводу turbojpeg и fPIC, возможное решение:
------------------------------------------------------------------------------------------------------------------------------------------------------
ln -s /usr/lib/x86_64-linux-gnu/libturbojpeg.so.0.1.0 /usr/lib/x86_64-linux-gnu/libturbojpeg.so
------------------------------------------------------------------------------------------------------------------------------------------------------

На RPI 3 
qml-module-qtquick-controls2

harfbuzz cups/cups.h


Пример `dockerfile` для `raspbian stretch`:
```dockerfile
FROM resin/rpi-raspbian:stretch
RUN echo "deb-src http://archive.raspbian.org/raspbian stretch main contrib non-free rpi firmware" >> /etc/apt/sources.list
RUN apt-get update && apt-get install -y \
  libraspberrypi-bin
```