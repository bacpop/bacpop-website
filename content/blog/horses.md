---
title: "Multiple horses for multiple courses"
description: "Reliably interfacing programming languages -- thoughts three years on"
date: 2023-12-12T09:00:00+01:00
type: "post"
author: "John Lees"
featured_image: '/images/horses.png'
---
This post is about a talk I gave in February 2020 at [RSLondonSouthEast](https://rslondon.ac.uk/rslondonse-2020/),
a local conference for research software engineers. First an overview of the talk, then an update
after following my own advice for the past few years.

# Multiple horses for multiple courses

## Choosing a language

When deciding which programming language to use for a project, a useful principle
is 'horses for courses' i.e. pick the one that is best suited for the task. How
might you decide which one this is?

- A compiled language? Typically fast to run, but slower to develop.
- An interpreted language? Fast to develop, but slower to run.
- Use the standard language in the field? Usually there's lots of packages available
and also examples. But what if you hate the language?
- Use your favourite language? Development is usually faster and more fun, and you
spend less time on trivial tasks. Sometimes this develops into a semi-religious fervor,
the upshot being that you don't notice the language's disadvantages.

## Choosing two languages

But why compromise? How about using multiple horses for multiple courses? By using
a number of different programming languages for the same project you can:
- Use the dream package. Found some good quality C code that's used everywhere, but haven't written
any C in years? Let's call it from python. Or want to use PyTorch from some C++ code, we can do that too.
- Control over memory and multithreading where you need it. Use a compiled language
just for the pieces that need them.
- Use the language you enjoy coding in the most.

## Actually doing it

You can use a wrapper for the foreign function interface (FFI).
I like [pybind11](https://pybind11.readthedocs.io/en/stable/basics.html) which
lets you interface C++ and python code, [for example](https://github.com/bacpop/unitig-caller):

```cpp
int py_call_strings(std::vector<std::string> assembly_list,
                    std::vector<std::string> assembly_names,
                    std::vector<std::string> query_list,
                    std::string output_file, bool write_idx,
                    size_t num_threads) {
  // Check input

  // Set number of threads
  if (num_threads < 1) {
    num_threads = 1;
  }

  // Convert python objs to C++
  // Here done automatically with pybind11/stl.h

  // call pure C++ function
  call_strings(assembly_list, assembly_names, query_list, output_file,
               write_idx, num_threads);

  // return success
  return 1;
}

PYBIND11_MODULE(unitig_query, m) {
  m.doc() = "Finds presence/absence of substrings";

  m.def("call", &py_call_strings, "Print presence absence to file",
        py::arg("assembly_files"), py::arg("assembly_names"),
        py::arg("queries"), py::arg("output_file"), py::arg("write_idx") = 1,
        py::arg("threads") = 1);

  m.attr("version") = VERSION_INFO;
}
```
Is C++ code which wraps a pure C++ function `call_strings()`. This can then be called
from python:
```python
import unitig_query
unitig_query.call(fasta_in,
                    names_in,
                    unitigs,
                    options.out + ".pyseer",
                    not options.no_save_idx,
                    options.threads)
```
and the python code can deal with the CLI, make an API with flask, do some machine learning
or any of the other things it is good at.

Examples are the best way to learn:
https://github.com/tdegeus/pybind11_examples
(Interface numpy/eigen for a non-copying data transfer).
See also the newer [nanobind](https://github.com/wjakob/nanobind).

### Getting it to compile

This is the painful part, especially distributing your application to other people.

Feel free to use my [CMake files](https://github.com/bacpop/PopPUNK/blob/master/CMakeLists.txt),
[Makefiles](https://github.com/bacpop/pp-sketchlib/blob/master/src/Makefile) and [conda recipes](https://github.com/conda-forge/pp-sketchlib-feedstock/blob/main/recipe/meta.yaml) -- once you've got them going
once is easy to reuse them!

## Other languages

- C++/R can be interfaced with [cpp11](https://cran.r-project.org/web/packages/cpp11/vignettes/cpp11.html).
- Python/R can be interfaced with [reticulate](https://rstudio.github.io/reticulate/) or [rpy2](https://rpy2.github.io/).

More examples on Wikipedia: https://en.wikipedia.org/wiki/Foreign_function_interface

## If all else fails, write to file

Use formats such as HDF5: these have a common interface for multiple languages and are
written to be efficient – so you don’t have to be!

Or swallow your pride and write a csv for use between modules.

I would argue this can be a better choice than forcing a single language for the whole project.

# Perspectives on my own advice

I pretty much did stick to this advice for three years of my most intensive software
development. PopPUNK, pp-sketchlib and mandrake are all python/C++/CUDA combos which use pybind11.
Software I helped supervise (ggcaller, ska2 and unitig-caller) also followed this design
principle. A package I collaborated on (dust) was an R/C++/CUDA mix.

I do think this saved me time writing tedious C++ code (though maybe ChatGPT/copilot etc
fill more of that gap now). It was a little harder for
students to learn, but not much harder than C++ alone.

The build system has been a little painful to set up, but again not much worse than C++. I'm
glad I didn't have to set it up for the R/cpp11 interface as this was definitely
a lot more tricky. I've come to really hate the python dependency system -- at least
a few times a year a package will break because some fundamental dependency has changed its API.

Something I underestimated was the difficulty of debugging code written this way,
especially for students to learn.

I have far fewer qualms now about having a python script
or two in a repository that can be run manually or via a pipeline manager. Sacrificing the
beauty/interface of fully integrated languages or a single-language implementation
is often worth it for research software.

I'm [switching to rust](https://www.johnlees.me/posts/rust-two/) for a lot of what I do now (e.g. [ska.rust](https://github.com/bacpop/ska.rust)). No language is perfect, but it's hitting most of what I typically want to do
with python and C++. I expect in future to use rust and CUDA together. Perhaps more importantly, the build system is great and I think will work well for research software maintainers.

## Final thoughts

In summary, I still firmly believe that you don't have to be restricted by a single language, but
I more see interfacing multiple languages as a useful skill to have, rather than
something necessary.

Do it in whatever way is easiest and most fun to you, but
also minimises the maintainance burden.

