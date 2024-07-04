Compile cc-tool on Apple Silicon (M1/M2/M3)

to erase/read/write flash memory of TI CC2530


#### Prepare 
```
brew install autoconf automake libusb boost pkgconfig libtool ##install needed tools to compile the tool :-D
git clone https://github.com/dashesy/cc-tool.git
cd cc-tool\
```





#### Build
```
CC=/usr/bin/clang \
CXX=/usr/bin/clang++ \
CPPFLAGS=-I/usr/local/include \
LDFLAGS=-I/usr/local/include \
 ./bootstrap

CC=/usr/bin/clang \
CXX=/usr/bin/clang++ \
CPPFLAGS=-I/usr/local/include \
CXXFLAGS="-std=c++0x -arch x86_64" \
LDFLAGS="-I/usr/local/include -lboost_system" \
LIBUSB_CFLAGS=-I/usr/local/include/libusb-1.0 \
LIBUSB_LIBS="-L/usr/local/lib -lusb-1.0" \
 ./configure

make clean ; make
```

#### Use
```
./cc-tool -e -w file.hex 
```

Original post https://gist.github.com/kidpixo/ef1a26ae953e3939a4eebe1b6fd2f07c
  
