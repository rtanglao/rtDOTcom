---
layout: post
title: "On March 3, 2021 Github action in rt-kits-api3 to get Firefox support questions broke because ruby gem ffi-1.13.1 wasn't found, fix:change Gemfile ffi version to 1.15.0"
---
* On March 3, 2021 my github action to get Firefox desktop support questions [failed](https://github.com/rtanglao/rt-kits-api3/runs/2022817162?check_suite_focus=true) because the shared library for this `ffi` Ruby gem couldn't be found!?!?
  * `LoadError: libffi.so.6: cannot open shared object file: No such file or directory - /home/runner/work/rt-kits-api3/rt-kits-api3/vendor/bundle/ruby/2.7.0/extensions/x86_64-linux/2.7.0/ffi-1.13.1/ffi_c.so`
* Still not sure why?!?
* But the fix was to change the [Gemfile.lock version](https://github.com/rtanglao/rt-kits-api3/commit/f63e754fee491ea66a04a9dfd27e4b039fac921c) of `ffi` to version `1.15.0` from `1.13.1`
* There doesn't seem to be a way to test Github actions locally that is easy. A local testing utility called `act` exists but [seems to have limitations](https://twitter.com/rtanglao/status/1371274319121182720). I don't know since I haven't tested it. I'll take Pomax's word for it :-)

