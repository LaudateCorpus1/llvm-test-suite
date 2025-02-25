# NIST Fortran 77 Test Suite
# http://www.fortran-2000.com/ArnaudRecipes/fcvs21_f95.html
#
# Reference results generated with gfortran -v:
# Using built-in specs.
# COLLECT_GCC=gfortran
# COLLECT_LTO_WRAPPER=/usr/lib/gcc/x86_64-linux-gnu/7/lto-wrapper
# OFFLOAD_TARGET_NAMES=nvptx-none
# OFFLOAD_TARGET_DEFAULT=1
# Target: x86_64-linux-gnu
# Configured with: ../src/configure -v --with-pkgversion='Ubuntu 7.5.0-3ubuntu1~18.04' --with-bugurl=file:///usr/share/doc/gcc-7/README.Bugs --enable-languages=c,ada,c++,go,brig,d,fortran,objc,obj-c++ --prefix=/usr --with-gcc-major-version-only --program-suffix=-7 --program-prefix=x86_64-linux-gnu- --enable-shared --enable-linker-build-id --libexecdir=/usr/lib --without-included-gettext --enable-threads=posix --libdir=/usr/lib --enable-nls --enable-bootstrap --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --with-default-libstdcxx-abi=new --enable-gnu-unique-object --disable-vtable-verify --enable-libmpx --enable-plugin --enable-default-pie --with-system-zlib --with-target-system-zlib --enable-objc-gc=auto --enable-multiarch --disable-werror --with-arch-32=i686 --with-abi=m64 --with-multilib-list=m32,m64,mx32 --enable-multilib --with-tune=generic --enable-offload-targets=nvptx-none --without-cuda-driver --enable-checking=release --build=x86_64-linux-gnu --host=x86_64-linux-gnu --target=x86_64-linux-gnu
# Thread model: posix
# gcc version 7.5.0 (Ubuntu 7.5.0-3ubuntu1~18.04)
#
# See additional comments in `driver_run` script should reference
# results ever need to be updated.
#
# Following test have been intentionally ommitted due to feature
# deletion in Fortran 95 standard:
# F95: 103, 111, 252, 253, 255, 257, 259, 260, 719
#
# We omit these tests because they never pass with any recent
# compiler:
# 001, 406, 923
# 
# Tests make use of arithmetic IF which is now a deleted feature
# in Fortran 2008
# 
# Note that the NIST license allows redistribution but requires
# explicit acknowledgement of what has been changed. Please
# amend README file if you modify the tests.

# clean-up fort.* files otherwise one of the tests will fail
llvm_test_prepare(rm -f %S/fort.*)

# Test 509 requires this flag in more recent versions of GCC
check_fortran_compiler_flag("-std=legacy" SUPPORTS_LEGACY)
if (SUPPORTS_LEGACY)
  add_compile_options(-std=legacy)
endif ()

set(FP_TOLERANCE 1.0e-11) # set by the most sensitive numerical test
llvm_singlesource()

file(COPY lit.local.cfg DESTINATION "${CMAKE_CURRENT_BINARY_DIR}")
