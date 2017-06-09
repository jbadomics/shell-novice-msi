---
title: "Loading Modules"
teaching: 15
exercises: 5
questions:
- "How can I run my R script with more computer resources than I have on my local machine?"
- "How can I locate and load available software modules?"
objectives:
- "Print a listing of available software modules"
- "Create files in that hierarchy using an editor or by copying and renaming existing files."
- "Display which modules are currently loaded."
- "Delete specified files and/or directories."
keypoints:
- "`module load` locates a particular software package's module file and configures your MSI user environment to use that software."
- "`module avail` prints a listing of all available modules on MSI systems."
- "`module list` prints a listing of modules currently loaded in your user environment/interactive session."
- "`module purge` will reset your session to defaults"
- "Modules must be explicitly loaded each time you launch a session on MSI."
- "For software you will use regularly, you can add `module load` statements to your user-specific Bash configuration file (`~/.bashrc`)."
- "There is no limit to the number of modules you can have loaded, but occasionally some can conflict with each other. You can unload the offending modules with `module unload`"
- "Often several versions of popular software are available. To avoid confusion and downstream problems, always call the specific version you intend to use, even if it is listed as '(default)'."
- "For more information, visit MSI's module [documentation](https://www.msi.umn.edu/support/faq/what-module)"
---

Let's take a brief detour from the shell lesson to talk about using pre-installed software on MSI systems.

Remember: computers are inherently dumb and will do exactly what you tell them, no more. This means that, while software may be available for use on MSI, we must explicitly load software packages into our environment/shell session before we can use them.

Whenever you call a command in bash, the shell will search directories included in a special environment variable called your `$PATH`. In bash, variables are prepended with dollar sign. If we wish to call a particular command, such as launching R, we can check if the R executable is in our $PATH by typing

~~~
$ which R
~~~
{: .bash}

~~~
which: no R in (/usr/local/bin:/home/sheikc/jbadalam/.local/bin:.:/bin:/usr/bin)
~~~
{: .error}

`which` is actually a program that the shell runs to scan your $PATH for the executable/program you intend to run. If that program is not in your $PATH, you will receive an error as above.

Navigate to [MSI's software listing page](https://www.msi.umn.edu/software) and type R in the search box. You should see an expanding list on the left with dozens of options. Are there really that many flavors of R?

We can search for module files much more quickly and effectively using the shell. Type

~~~
$ module avail R
~~~
{: .bash}

~~~

---------------------------------------------------- /panfs/roc/soft/modulefiles.common ----------------------------------------------------
R/2.15.1          R/3.1.3_intel_mkl R/3.2.1           R/3.2.5           R/3.3.1           R/3.3.3(default)
R/3.1.3           R/3.2.0_intel_mkl R/3.2.2           R/3.3.0           R/3.3.2           R/3.4.0
~~~
{: .output}

This looks more promising! You'll notice several available versions, a few of which are appended with additional flags. One option, `R/3.3.3`, is listed as default.

Let's load the default R module with

~~~
$ module load R
~~~
{: .bash}

~~~
 
~~~
{: .output}

It looks like nothing happened! Turns out that's not the case: you can check which module(s) you have loaded with

~~~
$ module list
~~~
{: .bash}

~~~
$ Currently Loaded Modulefiles:
  1) gmp/6.1.0_gcc6.1.0         4) isl/0.16.1_gcc6.1.0        7) bzip2/1.0.6-gnu6.1.0_PIC  10) curl/7.49.1_gcc6.1.0
  2) mpfr/3.1.4-p1_gcc6.1.0     5) gcc/6.1.0                  8) pcre/8.38_gcc6.1.0        11) R/3.3.3
  3) mpc/1.0.3_gcc6.1.0         6) zlib/1.2.8_gcc6.1.0        9) xz-utils/5.2.2_gcc6.1.0 
~~~
{: .output}

What happened here?! While only asked the shell to load R, R has several (in this case, 10) software **dependencies** in order to run properly. You need not know what they all are, and you should not unload any of them unless you know what you're doing.

A few of these dependencies are worth having loaded, and so I'll call them out by name:

*   `gcc` is the GNU compiler collection, which is required for compiling C/C++/fortran code. This is essential when installing R packages.
*   `gmp`, `mpfr`, `mpc`, and `isl` are dependences for `gcc
*   `zlib` is the library required for reading, writing, and manipulating compressed files. `bzip2` is similar to `zlib` but works with `.bz2` compressed files.
*   `pcre` stands for Perl-compatible regular expressions

It's good practice to explicitly call the version of the module you wish to load, even if it is the default. For example

~~~
$ module load R
~~~
{: .bash}

yields the same result as

~~~
$ module load R/3.3.3
~~~
{: .bash}


but the second example is more reliable. Since it's likely that a new R version will be released at some point in the future, explicitly calling the same version ensures reproducibility of your workflows across software upgrades.

> ## Which modules should I load?
>
> Generally speaking, you should only load modules for tools/software you intend to use.
> However, while widely used software (e.g. Perl and Python interpreters) come natively installed on the Linux distribution that runs on MSI systems (CentOS 6.9), these are often outdated versions and might cause problems if you need to run software that requires a more up-to-date version.
> In this case, you can simply `module load` a more recent version.
>
> Example:
>
> ~~~
> $ module purge
> $ which python && python -V
> ~~~
> {: .bash}
>
> ~~~
> /usr/bin/python
> Python 2.6.6
> ~~~
> {: .output}
> 
> ~~~
> $ module load python/2.7.9
> $ which python && python -V
> ~~~
> {: .bash}
>
> ~~~
> /soft/python/2.7.9/bin/python
> Python 2.7.9
> ~~~
> {: .output}
{: .callout}
