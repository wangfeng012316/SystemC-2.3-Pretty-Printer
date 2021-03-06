## Installing Pretty-Printer:
Currently you installed only a version of SystemC. With this shared libraries you are not able to see the value/s stored within an object. The interesting part will come now. I provide a git directory which contains multiple folders with example applications, the python Pretty-Printer and the python printers test interface. Furthermore, we install some dependencies for Python3.

```sh
cd ~
git clone https://github.com/AHeimberger/SystemC-2.3-Pretty-Printer.git
mv SystemC-2.3-Pretty-Printer systemc23-pretty-printer
sudo apt-get install python3 python3-pip
python3 -m pip install numpy
gedit .gdbinit
```

In the next step we have to modify the .gdbinit file in the home directory. This file is loaded by GDB at the start of the debug session. It depends upon your Linux version whether this file already exists or not. If this file exists to print data types of the <a href="https://sourceware.org/gdb/wiki/STLSupport">standard template library</a>, ensure  this file imports also OS, creates a variable to your home directory and registers the Pretty-Printer for SystemC.

```python
python
import sys, os

home = os.path.expanduser("~")

sys.path.insert(0, home + '/systemc23-pretty-printer/systemc23/')
from systemc23printers import register_systemc23_printers
register_systemc23_printers (None)

end
```

Next, we start GDB in the terminal and check if all Pretty-Printers were loaded correctly.

```sh
gdb
info pretty-printer
#    .*
#    bound
#    SystemC23
#    sc_bit
#    sc_bv_base
#    sc_fix
#    sc_fixed
#    sc_lv
#    sc_logic
#    sc_ufix
#    sc_ufixed
```
