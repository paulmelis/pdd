# PDD - A more verbose `ldd`

The output of `ldd` is very useful when trying to understand dynamic library resolution. However, the `ldd` output lacks some things that would make it even better. PDD attempts to improve on this.

Example (LDD):

```
$ which cmake
/sw/arch/RHEL9/EB_production/2024/software/CMake/3.29.3-GCCcore-13.3.0/bin/cmake

$ ldd `which cmake`
    linux-vdso.so.1 (0x00007fff53dd5000)
    /sw/arch/xalt/lib64/libxalt_init.so (0x00001527ca1ae000)
    libcurl.so.4 => /sw/arch/RHEL9/EB_production/2024/software/cURL/8.7.1-GCCcore-13.3.0/lib64/libcurl.so.4 (0x00001527ca0eb000)
    libarchive.so.13 => /sw/arch/RHEL9/EB_production/2024/software/libarchive/3.7.4-GCCcore-13.3.0/lib64/libarchive.so.13 (0x00001527c9fff000)
    libz.so.1 => /sw/arch/RHEL9/EB_production/2024/software/zlib/1.3.1-GCCcore-13.3.0/lib64/libz.so.1 (0x00001527c9fdf000)
    libstdc++.so.6 => /sw/arch/RHEL9/EB_production/2024/software/GCCcore/13.3.0/lib64/libstdc++.so.6 (0x00001527c9d7d000)
    libm.so.6 => /lib64/libm.so.6 (0x00001527c9c8e000)
    libgcc_s.so.1 => /sw/arch/RHEL9/EB_production/2024/software/GCCcore/13.3.0/lib64/libgcc_s.so.1 (0x00001527c9c68000)
    libc.so.6 => /lib64/libc.so.6 (0x00001527c9a5f000)
    libidn2.so.0 => /home/paulm/.local/easybuild/RHEL9/2024/software/libidn2/2.3.7-GCCcore-13.3.0/lib/libidn2.so.0 (0x00001527c9a05000)
    libssl.so.3 => /sw/arch/RHEL9/EB_production/2024/software/OpenSSL/3/lib64/libssl.so.3 (0x00001527c995d000)
    libcrypto.so.3 => /sw/arch/RHEL9/EB_production/2024/software/OpenSSL/3/lib64/libcrypto.so.3 (0x00001527c952a000)
    libzstd.so.1 => /sw/arch/RHEL9/EB_production/2024/software/zstd/1.5.6-GCCcore-13.3.0/lib/libzstd.so.1 (0x00001527c9434000)
    libbrotlidec.so.1 => /sw/arch/RHEL9/EB_production/2024/software/Brotli/1.1.0-GCCcore-13.3.0/lib/libbrotlidec.so.1 (0x00001527c9424000)
    libacl.so.1 => /lib64/libacl.so.1 (0x00001527c9417000)
    liblzma.so.5 => /sw/arch/RHEL9/EB_production/2024/software/XZ/5.4.5-GCCcore-13.3.0/lib64/liblzma.so.5 (0x00001527c93e2000)
    libbz2.so.1 => /lib64/libbz2.so.1 (0x00001527c93cf000)
    libxml2.so.2 => /lib64/libxml2.so.2 (0x00001527c9246000)
    /lib64/ld-linux-x86-64.so.2 (0x00001527ca219000)
    libbrotlicommon.so.1 => /sw/arch/RHEL9/EB_production/2024/software/Brotli/1.1.0-GCCcore-13.3.0/lib/libbrotlicommon.so.1 (0x00001527c9221000)
    libattr.so.1 => /lib64/libattr.so.1 (0x00001527c9219000)
```

Example (PDD):

```
$ ./pdd `which cmake`

/sw/arch/RHEL9/EB_production/2024/software/CMake/3.29.3-GCCcore-13.3.0/bin/cmake

NEEDED entries (sorted):
    libarchive.so.13  libc.so.6  libcurl.so.4  libgcc_s.so.1  libm.so.6  libstdc++.so.6  libz.so.1  

RPATH entries:
    /sw/arch/RHEL9/EB_production/2024/software/CMake/3.29.3-GCCcore-13.3.0/lib
    /sw/arch/RHEL9/EB_production/2024/software/CMake/3.29.3-GCCcore-13.3.0/lib64
    $ORIGIN
    $ORIGIN/../lib
    $ORIGIN/../lib64
    /sw/arch/RHEL9/EB_production/2024/software/OpenSSL/3/lib64
    /sw/arch/RHEL9/EB_production/2024/software/libarchive/3.7.4-GCCcore-13.3.0/lib64
    /sw/arch/RHEL9/EB_production/2024/software/cURL/8.7.1-GCCcore-13.3.0/lib64
    /sw/arch/RHEL9/EB_production/2024/software/bzip2/1.0.8-GCCcore-13.3.0/lib64
    /sw/arch/RHEL9/EB_production/2024/software/zlib/1.3.1-GCCcore-13.3.0/lib64
    /sw/arch/RHEL9/EB_production/2024/software/ncurses/6.5-GCCcore-13.3.0/lib64
    /sw/arch/RHEL9/EB_production/2024/software/binutils/2.42-GCCcore-13.3.0/lib64
    /sw/arch/RHEL9/EB_production/2024/software/GCCcore/13.3.0/lib64
    /sw/arch/RHEL9/EB_production/2024/software/GCCcore/13.3.0/lib
    /gpfs/admin/_hpc/sw/arch/AMD-ZEN4/RHEL9/EB_production/2024/software/GCCcore/13.3.0/bin/../lib/gcc/x86_64-pc-linux-gnu/13.3.0
    /gpfs/admin/_hpc/sw/arch/AMD-ZEN4/RHEL9/EB_production/2024/software/GCCcore/13.3.0/bin/../lib/gcc
    /sw/arch/RHEL9/EB_production/2024/software/XZ/5.4.5-GCCcore-13.3.0/lib/../lib64
    /sw/arch/RHEL9/EB_production/2024/software/XZ/5.4.5-GCCcore-13.3.0/lib

Dependencies:
    libcurl.so.4 => /sw/arch/RHEL9/EB_production/2024/software/cURL/8.7.1-GCCcore-13.3.0/lib64/libcurl.so.4 [RPATH]
                    /gpfs/admin/_hpc/sw/arch/AMD-ZEN4/RHEL9/EB_production/2024/software/cURL/8.7.1-GCCcore-13.3.0/lib/libcurl.so.4.8.0 (real path)
        libidn2.so.0 => /home/paulm/.local/easybuild/RHEL9/2024/software/libidn2/2.3.7-GCCcore-13.3.0/lib/libidn2.so.0 [LD_LIBRARY_PATH]
                        /gpfs/home4/paulm/.local/easybuild/RHEL9/2024/software/libidn2/2.3.7-GCCcore-13.3.0/lib/libidn2.so.0.4.0 (real path)
            libm.so.6 => /lib64/libm.so.6 [default]
                         /usr/lib64/libm.so.6 (real path)
                libc.so.6 => /lib64/libc.so.6 [default]
                             /usr/lib64/libc.so.6 (real path)
                    ld-linux-x86-64.so.2 => /lib64/ld-linux-x86-64.so.2 [default]
                                            /usr/lib64/ld-linux-x86-64.so.2 (real path)
        libssl.so.3 => /sw/arch/RHEL9/EB_production/2024/software/OpenSSL/3/lib64/libssl.so.3 [Parent RPATH]
                       /usr/lib64/libssl.so.3.0.7 (real path)
            libcrypto.so.3 => /sw/arch/RHEL9/EB_production/2024/software/OpenSSL/3/lib64/libcrypto.so.3 [Parent RPATH]
                              /usr/lib64/libcrypto.so.3.0.7 (real path)
                libz.so.1 => /sw/arch/RHEL9/EB_production/2024/software/zlib/1.3.1-GCCcore-13.3.0/lib64/libz.so.1 [Parent RPATH]
                             /gpfs/admin/_hpc/sw/arch/AMD-ZEN4/RHEL9/EB_production/2024/software/zlib/1.3.1-GCCcore-13.3.0/lib/libz.so.1.3.1 (real path)
        libzstd.so.1 => /sw/arch/RHEL9/EB_production/2024/software/zstd/1.5.6-GCCcore-13.3.0/lib/libzstd.so.1 [LD_LIBRARY_PATH]
                        /gpfs/admin/_hpc/sw/arch/AMD-ZEN4/RHEL9/EB_production/2024/software/zstd/1.5.6-GCCcore-13.3.0/lib/libzstd.so.1.5.6 (real path)
        libbrotlidec.so.1 => /sw/arch/RHEL9/EB_production/2024/software/Brotli/1.1.0-GCCcore-13.3.0/lib/libbrotlidec.so.1 [LD_LIBRARY_PATH]
                             /gpfs/admin/_hpc/sw/arch/AMD-ZEN4/RHEL9/EB_production/2024/software/Brotli/1.1.0-GCCcore-13.3.0/lib64/libbrotlidec.so.1.1.0 (real path)
            libbrotlicommon.so.1 => /sw/arch/RHEL9/EB_production/2024/software/Brotli/1.1.0-GCCcore-13.3.0/lib/libbrotlicommon.so.1 [RPATH]
                                    /gpfs/admin/_hpc/sw/arch/AMD-ZEN4/RHEL9/EB_production/2024/software/Brotli/1.1.0-GCCcore-13.3.0/lib64/libbrotlicommon.so.1.1.0 (real path)
    libarchive.so.13 => /sw/arch/RHEL9/EB_production/2024/software/libarchive/3.7.4-GCCcore-13.3.0/lib64/libarchive.so.13 [RPATH]
                        /gpfs/admin/_hpc/sw/arch/AMD-ZEN4/RHEL9/EB_production/2024/software/libarchive/3.7.4-GCCcore-13.3.0/lib/libarchive.so.13.7.4 (real path)
        libacl.so.1 => /lib64/libacl.so.1 [default]
                       /usr/lib64/libacl.so.1.1.2301 (real path)
            libattr.so.1 => /lib64/libattr.so.1 [default]
                            /usr/lib64/libattr.so.1.1.2501 (real path)
        liblzma.so.5 => /sw/arch/RHEL9/EB_production/2024/software/XZ/5.4.5-GCCcore-13.3.0/lib/../lib64/liblzma.so.5 [Parent RPATH]
                        /gpfs/admin/_hpc/sw/arch/AMD-ZEN4/RHEL9/EB_production/2024/software/XZ/5.4.5-GCCcore-13.3.0/lib/liblzma.so.5.4.5 (real path)
        libbz2.so.1 => /lib64/libbz2.so.1 [default]
                       /usr/lib64/libbz2.so.1.0.8 (real path)
        libxml2.so.2 => /lib64/libxml2.so.2 [default]
                        /usr/lib64/libxml2.so.2.9.13 (real path)
    libstdc++.so.6 => /sw/arch/RHEL9/EB_production/2024/software/GCCcore/13.3.0/lib64/libstdc++.so.6 [RPATH]
                      /gpfs/admin/_hpc/sw/arch/AMD-ZEN4/RHEL9/EB_production/2024/software/GCCcore/13.3.0/lib64/libstdc++.so.6.0.32 (real path)
        libgcc_s.so.1 => /sw/arch/RHEL9/EB_production/2024/software/GCCcore/13.3.0/lib64/libgcc_s.so.1 [Parent RPATH]
                         /gpfs/admin/_hpc/sw/arch/AMD-ZEN4/RHEL9/EB_production/2024/software/GCCcore/13.3.0/lib64/libgcc_s.so.1 (real path)

/home/paulm/.local/easybuild/RHEL9/2024/software/libidn2/2.3.7-GCCcore-13.3.0/lib:
    libidn2.so.0  

/lib64:
    ld-linux-x86-64.so.2  libacl.so.1  libattr.so.1  libbz2.so.1  libc.so.6  libm.so.6  libxml2.so.2  

/sw/arch/RHEL9/EB_production/2024/software/Brotli/1.1.0-GCCcore-13.3.0/lib:
    libbrotlicommon.so.1  libbrotlidec.so.1  

/sw/arch/RHEL9/EB_production/2024/software/GCCcore/13.3.0/lib64:
    libgcc_s.so.1  libstdc++.so.6  

/sw/arch/RHEL9/EB_production/2024/software/OpenSSL/3/lib64:
    libcrypto.so.3  libssl.so.3  

/sw/arch/RHEL9/EB_production/2024/software/XZ/5.4.5-GCCcore-13.3.0/lib64:
    liblzma.so.5  

/sw/arch/RHEL9/EB_production/2024/software/cURL/8.7.1-GCCcore-13.3.0/lib64:
    libcurl.so.4  

/sw/arch/RHEL9/EB_production/2024/software/libarchive/3.7.4-GCCcore-13.3.0/lib64:
    libarchive.so.13  

/sw/arch/RHEL9/EB_production/2024/software/zlib/1.3.1-GCCcore-13.3.0/lib64:
    libz.so.1  

/sw/arch/RHEL9/EB_production/2024/software/zstd/1.5.6-GCCcore-13.3.0/lib:
    libzstd.so.1  

Dependencies (files):
    ld-linux-x86-64.so.2  libacl.so.1  libarchive.so.13  libattr.so.1  libbrotlicommon.so.1  libbrotlidec.so.1  libbz2.so.1  libc.so.6  
    libcrypto.so.3  libcurl.so.4  libgcc_s.so.1  libidn2.so.0  liblzma.so.5  libm.so.6  libssl.so.3  libstdc++.so.6  
    libxml2.so.2  libz.so.1  libzstd.so.1  

```

This adds the following information:

* `NEEDED` and `RPATH` entries in the file being queried
* The dependencies of the file as a tree, so you can see clearly relate the final dependencies to how they where resolved
* Symlinks used in dependency paths are resolved, with both forms shown. In the example above `ldd` resolves `libssl.so.3` to a path that is actually a symlink back to `/usr/lib64/libssl.so.3.0.7`, but this isn't immediately clear.
* The sets of resolved dependencies grouped by location. This makes it easier to spot dependencies not in the place where you expect them.

## Dependencies

* Python 3.x
* The `ldd` command (see below)

## Known issues

PDD does "manual" dependency resolution, in effect replaying the resolution steps that [`ld.so`](https://man7.org/linux/man-pages/man8/ld.so.8.html) performs when `ldd` is invoked. This resolution is somewhat complex, so currently PDD also runs `ldd` separately, and then checks the results against its own dependency resolution results. In case there is a mismatch these are marked as `>>> ldd says ... <<<` in the dependency tree and such cases should be considered a bug in PDD.

