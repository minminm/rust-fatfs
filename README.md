Rust FAT FS
===========

[![Travis Build Status](https://travis-ci.org/rafalh/rust-fatfs.svg?branch=master)](https://travis-ci.org/rafalh/rust-fatfs)
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE.txt)
[![crates.io](http://meritbadge.herokuapp.com/fatfs)](https://crates.io/crates/fatfs)
[![Documentation](https://docs.rs/fatfs/badge.svg)](https://docs.rs/fatfs)
[![Minimum rustc version](https://img.shields.io/badge/rustc-1.24+-yellow.svg)](https://blog.rust-lang.org/2018/02/15/Rust-1.24.html)

FAT filesystem library implemented in Rust.

Features:
* read/write/create/remove file,
* enumerate directory children,
* create/remove directory,
* read/write file timestamps (updated automatically if `chrono` feature is enabled),
* FAT12, FAT16, FAT32 compatibility,
* LFN (Long File Names) extension supported,
* Basic no_std environment support.

Usage
-----

Put this in your `Cargo.toml`:

    [dependencies]
    fatfs = "0.2"

Put this in your crate root:

    extern crate fatfs;

You can start using library now:

    let img_file = File::open("fat.img")?;
    let buf_stream = fatfs::BufStream::new(img_file);
    let fs = fatfs::FileSystem::new(buf_stream, fatfs::FsOptions::new())?;
    let root_dir = fs.root_dir();
    let mut file = root_dir.create_file("hello.txt")?;
    file.write_all(b"Hello World!")?;

See more examples in `examples` subdirectory.

no_std usage
------------

Put this in your `Cargo.toml`:

    [dependencies]
    fatfs = { version = "0.2", features = ["core_io"], default-features = false }

Note: LFN support requires `alloc` and `core_io/collections` features and makes use of `alloc` crate.
You may have to provide a memory allocator implementation.

For building in `no_std` mode nightly Rust version compatible with current `core_io` crate is required.
See date string in `core_io` dependency version.

License
-------
The MIT license. See LICENSE.txt.
