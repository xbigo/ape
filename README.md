# ape

## Build

For Mac & Linux
```bash
git clone https://github.com/xbigo/ape.git
cd ape
git submodule update --init
mkdir ../build
cd ../build
cmake -S ../ape -D BUILD_TESTING=1
make
make check
make install
```

For MSVC 

```bat
git clone https://github.com/xbigo/ape.git
cd ape
git submodule update --init
mkdir ..\build
cd ..\build
cmake -S ../ape -D BUILD_TESTING=1
cmake --build .
cmake --build . --target check
cmake --build . --target install
```

