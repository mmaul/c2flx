NAME: c2flx

VERSION: .011  

AUTHOR: Mike Maul

AUTHOR_EMAIL: mike.maul@gmail.com

PKG_URL: https://github.com/mmaul/c2flx

DESCRIPTION: C binding generator

CATEGORY: dev

LIBDIR: app

-----

c2flx is generates bindings to C libraries, by using c2ffi to parse C 
header files and translates the output of c2ffi to felix source code.

## Requirements ##

* LLVM and Clang >= 3.3 

As of this writing version 3.3 must be checked out from the llvm
svn repository. See http://clang.llvm.org/get_started.html for 
getting llvm and
clang from the svn repo and building.

* c2ffi https://github.com/rpav/c2ffi 



## Quickstart Installation ##

After LLVM, Clang and c2ffi have been installed and the c2ffi executable
is in your path you can install c2flx.

    scoop get c2flx
    scoop build c2flx
if building as root or installation directory is write-able by you

    scoop install c2flx

Otherwise ( Installs what you just built as you not what root would rebuild )

     su # or sudo -s
     scoop install flx --litterbox=/home/<your username>/.felix/litterbox

## Documentation ##

Running

    c2flx <flx class> <c header file> <flx output file>

If you are lucky the generated file will be usable out of the box.
However as this is just a wrapper generator you will probably have
to write some wrapper code.

Here is what you can expect. c2flx was used to process iconv.h 

    c2flx Iconv /usr/include/iconv.h iconv.flx

iconv.flx

    class Iconv {
    const __WORDSIZE:int;
    const __USE_ISOC99:int;
    const __USE_ISOC95:int;
    const _FEATURES_H:int;
    const __USE_POSIX:int;
    const __USE_POSIX2:int;
    const __USE_POSIX199309:int;
    const _ICONV_H:int;
    const __STDC_IEC_559__:int;
    const _STDC_PREDEF_H:int;
    const __GLIBC__:int;
    const __GLIBC_MINOR__:int;
    const __STDC_NO_THREADS__:int;
    const __GNU_LIBRARY__:int;
    const __STDC_IEC_559_COMPLEX__:int;
    const __STDC_ISO_10646__:int;
    const _SVID_SOURCE:int;
    const _POSIX_C_SOURCE:int;
    const __USE_POSIX_IMPLICITLY:int;
    const _ATFILE_SOURCE:int;
    const __USE_FORTIFY_LEVEL:int;
    const __USE_ATFILE:int;
    const __USE_MISC:int;
    const _POSIX_SOURCE:int;
    const _BSD_SOURCE:int;
    const __USE_ANSI:int;
    const __USE_XOPEN2K:int;
    const __USE_POSIX199506:int;
    const __USE_SVID:int;
    const __USE_BSD:int;
    const __USE_XOPEN2K8:int;
    const _SYS_CDEFS_H:int;
    const __GLIBC_HAVE_LONG_LONG:int;

    type iconv_t = 'iconv_t'; //<--/usr/include/iconv.h:29:15 (&void)

    gen iconv_close: iconv_t->int; //<--/usr/include/iconv.h:51:12

    gen iconv: iconv_t*&&char*&size_t*&&char*&size_t->size_t; //<--/usr/include/iconv.h:42:15

    gen iconv_open: &char*&char->iconv_t; //<--/usr/include/iconv.h:37:16
    }


