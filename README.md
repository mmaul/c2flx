NAME: c2flx

VERSION: .011  

AUTHOR: Mike Maul

AUTHOR_EMAIL: mike.maul@gmail.com

PKG_URL: https://github.com/mmaul/c2flx

DESCRIPTION: C binding generator

CATEGORY: dev

LIBDIR: app

-----

c2flx generates bindings to C libraries, by using c2ffi to parse C 
header files and translates the output of c2ffi to felix source code.

## Requirements ##

* LLVM and Clang >= 3.3 

As of this writing version 3.3 must be checked out from the llvm
svn repository. See http://clang.llvm.org/get_started.html for 
getting llvm and
clang from the svn repo and building.

* c2ffi https://github.com/rpav/c2ffi 

For OSX I found it necessary to do a  '''autoreconf -i ''' to generate the configure file


## Quickstart Installation ##

After LLVM, Clang and c2ffi have been installed and the c2ffi executable
is in your path you can install c2flx.

    scoop get c2flx
    scoop build c2flx

if building as root or installation directory is write-able by you

    scoop install c2flx

Otherwise 

     su # or sudo -s
     scoop install c2flx --litterbox=/home/<your username>/.felix/litterbox

## Documentation ##

Running

    c2flx <flx class> <c header file> <flx output file>

If you are lucky the generated file will be usable out of the box.
The Cairo binding was generated with c2flx and has required no 
modifications to the generated code to run felix ports of
all the Cairo examples. There are certain things
that c2flx does not handle, one of them being C++ code. That may
change, but right now it does not. The other being function pointers
in typedef delerations. When these are encountered c2fls will give
you an opaque type with the name of the function pointer. 
Which won't help you with call backs, but you can take care of that
by declaring the proper callback signature yourself.

Also note that it is up to you to create a Felix Package Config file
If you are building your library as a scoop package you can
use the create_config procedure to create it for you.

Here is what you can expect. c2flx was used to process crack.h 

    c2flx Crack /usr/include/crack.h crack.flx

crack.flx

    //class        : Crack
    //Raw Header    : /usr/include/crack.h

    requires package "Crack";
    class Crack {
      gen FascistCheck: &char*&char->&char; //<--/usr/include/crack.h:16:20
      gen GetDefaultCracklibDict: 1->&char; //<--/usr/include/crack.h:20:20
    }



## License ##

This software is FFAU (Freee For Any Use). If you find it useful
acknowledgement is always nice. 
