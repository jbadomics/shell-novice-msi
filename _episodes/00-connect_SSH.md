---
title: "Connecting to MSI via SSH"
teaching: 5
exercises: 0
questions:
- "How do I conduct my computing tasks on MSI?"
objectives:
- "Explain how the shell relates to the keyboard, the screen, the operating system, and users' programs."
- "Explain when and why command-line interfaces should be used instead of graphical interfaces."
keypoints:
- "The Minnesota Supercomputing Institute is a service that provides computational services and support to the University of Minnesota research community."
- "MSI's compute nodes come in several flavors to suit your data analysis needs."
- "Secure shell (SSH) establishes communication between your computer and an MSI compute node, such that commands you type are executed on the MSI node"
---
### Background
MSI's supercomputers physically reside in the basement of Walter Library on the U of M campus. In nearly all situations, anyone affiliated with the University of Minnesota can use MSI computing resources free of charge*. 

Currently MSI operates three types of computing **clusters** for different tasks depending on required resources:

*   Lab (for routine or low-resource analyses, file manipulation; interactive sessions)
*   Itasca
*   Mesabi

Each cluster contains dozens--or even hundreds--of individual supercomputers, called **nodes**.  Think of one single node as a standalone desktop computer that comes with a defined number of processors and memory.  This lesson will utilize lab nodes, which are ideal for performing interactive computing tasks.

### Before we begin
*   **Windows users:** if you have not done so already, complete steps 1-8 from [these instructions](https://www.msi.umn.edu/support/faq/how-do-i-configure-putty-connect-msi-unix-systems) to install and configure PuTTY **YOU CAN SKIP THE OPTIONAL STEPS**
*   **Mac users:** launch a Terminal window by navigating to Applications --> Utilities --> Terminal.

### Launching an interactive MSI session
Most of the time, you will use a command line interface (CLI; topic of this lesson) to communicate with MSI nodes.  This communication is established via a secure shell (SSH) connection which we will set up now.

*  **Windows users:** With PuTTY configured, complete steps 9-11 from [these instructions](https://www.msi.umn.edu/support/faq/how-do-i-configure-putty-connect-msi-unix-systems). When prompted, enter your X.500 and password.
*  **Mac/Linux users:** In Terminal, type

~~~
$ ssh username@login.msi.umn.edu
~~~
{: .bash}
    
where `username` is your X.500. Enter your password when prompted.

> ## Why can't I see my password?!
>
> When connecting to a remove computer via SSH, the cursor will not move, blink, or show hidden characters when you type your password.
> Don't worry, your password is still being entered properly!
> Simply type Enter/Return and if you mistyped your password you will be re-prompted for it.
{: .callout}

\* Running jobs on Itasca or Mesabi will consume Service Units (SU's) from your principal investigator's annual SU allocation. More info can be found [here](https://www.msi.umn.edu/content/su-allocations).
