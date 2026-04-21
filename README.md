# Conky-v1.19.8-Mouse-Events-install-to-Kubuntu-v25.10-KDE-Plasma-6-Wayland
How to downgrade from conky 1.20x versions in which mouse events do not work.

Step 1) Remove existing conky
```
sudo apt purge --autoremove conky conky-all conky-std conky-cli
sudo apt autoremove --purge
sudo apt clean
```
Step 2) Confirm removal
```
which conky
```
If it returns something like /usr/bin/conky, delete it:
```
sudo rm -f /usr/bin/conky
```
Step 3) Download the source files customized by Commander Shepard of Conkyporn Reddit:

https://www.mediafire.com/file/kya05ncoaeit9ex/conky1.19.8cmdr.zip/file

STEP 4) Extract the directory conky-1.19.8 from the .zip file and move to:

/home/username/conky-1.19.8

Step 5) Install Dependencies
```
sudo apt update
sudo apt install -y \
build-essential cmake git pkg-config \
libcairo2-dev libcairo-script-interpreter2 \
liblua5.3-dev \
libx11-dev libxft-dev libxext-dev libxdamage-dev libxfixes-dev \
libxcb1-dev libxcb-util0-dev libxcb-randr0-dev \
libxcb-composite0-dev libxcb-image0-dev \
libxcb-xfixes0-dev libxcb-damage0-dev \
libimlib2-dev \
libcurl4-openssl-dev \
libxml2-dev \
libuv1-dev \
libncurses-dev \
mesa-common-dev
```

```
sudo apt install -y \
fonts-dejavu-core fonts-droid-fallback \
curl jq lm-sensors hddtemp
```

```
sudo apt install -y libxinerama-dev
```

```
sudo apt install -y libxi-dev
```

```
sudo apt install -y libxnvctrl-dev
```
STEP 5a) Create a build folder:

mkdir build

cd build

Step 6) Configure
```
cmake .. \
-DCMAKE_BUILD_TYPE=Release \
-DBUILD_X11=ON \
-DBUILD_WAYLAND=OFF \
-DBUILD_LUA_CAIRO=ON \
-DBUILD_LUA_IMLIB2=ON \
-DBUILD_IMLIB2=ON \
-DBUILD_CURL=ON \
-DBUILD_RSS=ON \
-DBUILD_WEATHER_METAR=ON \
-DBUILD_NVIDIA=ON
```
Step 7) Build
```
make -j$(nproc)
```

Step 8) Install
```
sudo make install
```

Step 9) Verify
```
conky --version
```

You should see output like:

```
conky 1.19.8_pre compiled for Linux x86_64

Compiled in features:

System config file: /etc/conky/conky.conf
Package library path: /usr/local/lib/conky


 General:
  * math
  * hddtemp
  * portmon
  * IPv6
  * Curl
  * RSS
  * support for IBM/Lenovo notebooks
  * nvidia
  * builtin default configuration
  * old configuration syntax
  * Imlib2
  * OSS mixer support
  * apcupsd
  * iostats
  * ncurses
  * Internationalization support

 Lua bindings:
  * Cairo
  * Imlib2
 X11:
  * Xdamage extension
  * Xinerama extension (virtual display)
  * Xshape extension (click through)
  * XDBE (double buffer extension)
  * Xft
  * Xinput
  * ARGB visual
  * Own window
  * Mouse events

 Music detection:
  * CMUS
  * MPD
  * MOC

 Default values:
  * Netdevice: eno1
  * Local configfile: $HOME/.conkyrc
  * Localedir: /usr/local/share/locale
  * Maximum netdevices: 256
  * Maximum text size: 16384
  * Size text buffer: 256
```

