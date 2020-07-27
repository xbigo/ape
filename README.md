# ape

## Build

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
