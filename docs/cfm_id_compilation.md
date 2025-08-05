# Install CMake and GCC

```bash
sudo apt update
sudo apt install cmake gcc g++ -y
```

# Install Boost Library

Install old boost library version (1.60.0)

1 - Download an old boost library from [BOOST](https://archives.boost.io/release/1.71.0/source/index.html)

2 - 

```bash

```

# Install specific RDKIT (insource location)

```bash
wget https://github.com/rdkit/rdkit/archive/Release_2017_09_3.tar.gz;
tar -zxvf Release_2017_09_3.tar.gz
cd ./rdkit-Release_2017_09_3
mkdir build
cd build
cmake .. -DRDK_PGSQL_STATIC=OFF -DRDK_BUILD_PYTHON_WRAPPERS=OFF -DRDK_BUILD_CPP_TESTS=OFF -DRDK_BUILD_DESCRIPTORS3D=OFF -DRDK_INSTALL_STATIC_LIBS=OFF-DRDK_INSTALL_INTREE=ON -DRDK_BUILD_INCHI_SUPPORT=ON -DRDK_OPTIMIZE_NATIVE=ON -DCMAKE_CXX_STANDARD=14 -DCMAKE_BUILD_TYPE=Release
sudo make install -j8
```

