---
title: "Connecting to MSI via SSH"
teaching: 15
exercises: 0
questions:
- "How do I conduct my computing tasks on MSI?"
objectives:
- "Explain how the shell relates to the keyboard, the screen, the operating system, and users' programs."
- "Explain when and why command-line interfaces should be used instead of graphical interfaces."
keypoints:
- "The Minnesota Supercomputing Institute is a service that provides computational services and support to the University of Minnesota research community."
- "MSI's compute nodes come in several flavors to suit your data analysis needs."
- "Secure shell (SSH) establishes communication between your computer and an MSI compute node, such that commands you type are executed on the MSI node, not on your local machine."
---
### Background
Most of MSI's supercomputers physically reside in the basement of Walter Library on the U of M campus. In nearly all situations, anyone affiliated with the University of Minnesota can use MSI computing resources free of charge*. 

Currently MSI operates three types of computing **clusters** for different tasks depending on required resources:

*   Lab (for routine or low-resource analyses such as viewing data and file manipulation; ideal for most interactive sessions)
*   Itasca
*   Mesabi

Each cluster contains dozens--or even hundreds--of individual supercomputers, called **nodes**.  Think of one single node as being analogous to a standalone desktop computer that comes with a defined number of processors and memory.  This lesson will utilize lab nodes, which are ideal for performing interactive computing tasks.

### Before we begin
*   **Windows users:** if you have not done so already, complete steps 1-8 from [these instructions](https://www.msi.umn.edu/support/faq/how-do-i-configure-putty-connect-msi-unix-systems) to install and configure PuTTY. **YOU CAN SKIP THE OPTIONAL STEPS**
*   **Mac users:** launch a Terminal window by navigating to Applications --> Utilities --> Terminal.

### Launching an interactive MSI session
Most of the time, you will use a command line interface (CLI; topic of this lesson) to communicate with MSI nodes.  This communication is established via a secure shell (SSH) connection which we will set up here.

To establish an interactive SSH connection to an MSI lab node, complete the following three steps:

1.  Connect to MSI via SSH

    *  **Windows users:** With PuTTY configured, complete steps 9-11 from [these instructions](https://www.msi.umn.edu/support/faq/how-do-i-configure-putty-connect-msi-unix-systems). When prompted, enter your X.500 and password.
    *  **Mac/Linux users:** In Terminal, type
    
    ~~~
    $ ssh username@login.msi.umn.edu
    ~~~
    {: .bash}
    
    where `username` is your X.500. Enter your password when prompted. Type `yes` if prompted to add an RSA fingerprint.

    > ## Why can't I see my password?!
    >
    > When connecting to a remove computer via SSH, the cursor will not move, blink, or show hidden characters when you type your password.
    > Don't worry, your password is still being entered properly!
    > Simply type Enter/Return and if you mistyped your password you will be re-prompted for it.
    {: .callout}

    If you have logged in properly, you should see a welcome message, followed by a command prompt that looks similar to this:
    
    ~~~
    jbadalam@login02 [~] % 
    ~~~
    {: .output}

    For novice shell users, the command prompt may look intimidating, but there's quite a bit of useful information embedded there. Let's break it down:

    *   `jbadalam` is my username
    *   I am currently connected to a **login node**, whose purpose is exactly what it sounds like. Think of a login node as a staging or holding area that allows you to access other MSI nodes.
    *   The tilde (`~`) in square brackets shows that I am in my home directory, which will be covered later in this lesson.
    *   The % sign separates the command prompt from commands you will type. Sometimes this will be a dollar sign ($). In either case, this sign tells you that you are logged in as a normal user. 

    > ## Going forward
    >
    > **NOTE:** From this point forward, all commands and instructions in this lesson apply to all learners regardless of their local machine's underlying operating system (Mac, Windows, or Linux).
    {: .callout}

2.  **Connect to the lab cluster**

    Within your existing SSH connection to the login node, type
    ~~~
    % ssh lab
    ~~~
    {: .bash}

    ~~~
    jbadalam@labqi046 [~] %
    ~~~
    {: .output}

    Note how the node to which I am now connected has changed - in this case to `labqi046`.

3.  **Launch a 4-hour interactive session**

    MSI uses PBS/Torque to automatically schedule and queue jobs according to several factors including user priority and available compute resources/nodes. Generally speaking, a **job** is a set of instructions (i.e. commands) that you wish to run, and these instructions can either be specified in advance (non-interactively, via a PBS script) or on-the-fly (interactively). Interactive sessions are especially useful when
    *   you don't know the exact set of commands you wish to run
    *   you want to explore your data and experiment with different tools
    *   you do not need more compute resources than are available on a lab node

    To launch your interactive session, type

    ~~~
    % qsub -I -q lab -l nodes=1:ppn=16;mem=4gb,walltime=4:00:00
    ~~~
    {: .bash}

    ~~~
    qsub: waiting for job 530694.nokomis0015.msi.umn.edu to start
    qsub: job 530694.nokomis0015.msi.umn.edu ready

    jbadalam@labc02 [~] % 
    ~~~
    {: .output}

    This command establishes an interactive session with the `-I` argument (capital 'eye'), and the `-l` argument (lowercase 'el') is used to request the physical computer resources you need. For this lesson, we need only 1 node with 4 GB of memory for a total of 4 hours (specified as HH:MM::SS). For other, more intensive jobs, you may need to request additional resources and/or walltime. Alternatively (beyond the scope of this lesson), you can select other job **queues** which provide additional flexibilty.

    Don't worry! We will spend much more time on command line arguments further along in the shell lesson.

    > ## How much time should I request?
    >
    > Estimating how much compute time you need will come with experience and practice. By default, your session will last 2 hours.
    > It is best to request more time than you think you need; any unused time will be freed up for other users when you log out.
    {: .callout}

\* Running jobs on Itasca or Mesabi will consume Service Units (SU's) from your principal investigator's annual SU allocation. More info can be found [here](https://www.msi.umn.edu/content/su-allocations).


