Zerynth Partner Library Blueprints
==================================

This repository contains blueprints for developing Zerynth Partner Libraries. A partner library is hosted on Github 
in the partner account and the partner is responsible for its maintenance. 
To create a new partner library please fork this repo, choosing a custom name for it (e.g., zerynth-partnername-libname), and follow the instructions.


Modify package.json
-------------------

The `package.json` file contains information about the partner library.

The fields requiring a change are:

- *fullname*: the library identifier. It is formatted as `lib.namespace.libname` where `namespace` it is usually related to
  the partner and `libname` is the name of the library itself. The fullname determines the import syntax of the library: 
  `from namespace.libname import module`. It is therefore not possible for namespaces and libnames to start with numbers or to
  contain special symbols (apart from underscore).
- *git_pointer*: the short url where the library repo can be found. It is formatted as `github://github-account//repo`.
  For this repo, the git_pointer would be `github://zerynth/partner-blueprint`. For a forked one, with custom name, it could be `github://partnername/zerynth-partnername-libname`.
- *title*: the title of the library. It will be shown in the Zerynth package manager.
- *description*: a longer description of the library. It will be indexed to be searched in Zerynth Studio.
- *keywords*: a list of (max) 5 keywords that will be used to index the library in Zerynth Studio.
- *version*: the current version of the library. Should match the current version of Zerynth.
- *info*: a dictionary to be filled with "chip_manufacturer", "chip_name", "name" (really short description of the library) and type (one or two words for the category of the library). Info is going to be reported in [this](https://www.zerynth.com/zerynth-libraries/) table. 


Adding source code
------------------

Python source code can be added as .py files in the main folder. For .c files it is suggested but not enforced to place 
files under a `csrc` folder. 


Preparing documentation
-----------------------

Under the `docs` folder the following files can be found:

- `docs.json`: it contains a dictionary with a list of files from which the library documentation will be extracted.
  The Zerynth documentation is built with Sphinx. For each library, all the docstrings found in the files listed in 
- `index.rst`: it contains the main page of the library documentation. It must end with `.. include:: __toc.rst` in
  order to have the automatically generated table of contents appended at the end of the main page.

To test the correctness of the documentation run `ztc project make_doc lib_folder_path --open`. The command will
compile the documentation and open it on a web browser.

Adding examples
---------------

Each library can contain examples of its usage. Examples are gathered together and shown in the Zerynth Studio example
panel. Moreover they are automatically inserted in the generated documetation. Examples are very important to jump start
the usage of the library both by experienced and unexperienced users.

Examples can be added under the `examples` folder. Various subfolders can be created, one for each example. The name of
the subfolder will be the title of the example. The subfolder can't contain spaces; if a space is needed in the title,
please use an underscore instead (naming a subfolder `Hello_World` will produce an example named `Hello World`).
Inside the subfolder, at least two files must be present:

- `main.py`: it contains the main file of the example. Additional files can be added and can be imported by main.
- `project.md`: a short description in markdown format of the example. It will be shown to Zerynth Studio users.

Directly under the `examples` folder there must be one file: `order.txt`. In such file it will be specified where the various
provided examples will be placed in the Zerynth example tree.
The format of the file is quite simple: each line can begin with a certain number of `#` or without. The lines starting 
with `#` are nodes of the example tree while the lines without `#` are the leaves and correspond to the provided examples.

An `order.txt` file like this:

```
#Namespace
    ##Example group 1
        Example_1
        Example_2
    ##Example group 2
        Example_2
        Example_3
```
will produce an example tree with a main node named `Namespace` that contains two nodes `Example group 1` and `Example group 2`,
each one containing a list of examples. Note that an example can be placed under more than one path.


Testing the library
-------------------

The library repository can be easily tested by copying it under `<home>/<zerynth>/dist/<version>/libs/official/` where `<home>` is
the home folder ( `~` in Mac and Linux, `C:\Users\your-user` in Windows), `<zerynth>` is `.zerynth2` for Mac and Linux or `zerynth2`
for Windows, `<version>` is the Zerynth version you are testing for.

Opening Zerynth Studio and clicking the Example view you should see the library examples with code ready to be cloned and tested.



