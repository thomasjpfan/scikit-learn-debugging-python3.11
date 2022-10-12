# scikit-learn Debugging Python 3.11 on Linux

This are instructions for debugging for Linux.

```bash
git clone https://github.com/thomasjpfan/scikit-learn-debugging-python3.11
git submodule update --init

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

# Install dependencies
python -m pip install numpy scipy Cython pytest

# Install scikit-learn with debug symbols
cd scikit-learn
export SKLEARN_BUILD_PARALLEL=8
CFLAGS="-Og -g" python setup.py develop

# Run pytest
pytest sklearn -v

# Run pytest with gdb
gdb --args python -m pytest sklearn -v
```

With debug symbols on, I get [this backtrace](https://gist.github.com/thomasjpfan/192b2e9439512a21e710fca0a90f4f76).
