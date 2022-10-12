# scikit-learn Debugging Python 3.11

This are instructions for debugging for Linux

```bash
git clone https://github.com/thomasjpfan/scikit-learn-debugging-python3.11
git submodule init
git submodule update

# Build Python v3.11.0rc2
pushd cpython
./configure
# If you want to debug symbols
# ./configure --with-pydebug
make -j8
popd

# Create venv
./cpython/python -m venv .venv
source .venv/bin/activate

python -m pip install numpy scipy Cython pytest

cd scikit-learn
python setup.py develop

# Run pytest
pytest sklearn -v

# Run pytest with gdb
gdb --args python -m pytest sklearn -v
```
