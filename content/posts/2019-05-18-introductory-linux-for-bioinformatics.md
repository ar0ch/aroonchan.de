---
layout: blog
title: Introductory Linux for Bioinformatics
date: 2019-05-19T00:07:31.150Z
thumbnail: /static/img/uploads/tux.png
---
# Bioinformatics ♥ Linux

Much of bioinformatics happens on the **command line**, a text-based system for interacting with files, running commands and writing programs.  The command line can feel scary foe newcomers, you are likely used to the Window-Icon-Pointer-Mouse (**WIMP**) interface of most operating systems (like Windows or MacOS).  In WIMP, you use a _mouse_ to move a _pointer_ around the screen, clicking on and interacting with _windows_ and _icons_ as your work.  These graphics on the screen are often called **Graphical User Interfaces** (**GUIs**).  GUIs are convenient and even required for some of the tasks I do day to day in bioinformatics, such as editing figures in Illustrator or creating presentations in PowerPoint, but quickly get in the way of doing larger analyses.  

Take for example the below list of steps to take pre-processed **next generation sequencing reads** from an Illumina sequencer and turn them into a **genome assembly** (concepts I'll talk about in later posts) using the open-source bioinformatics GUI, [UGENE](http://ugene.net/).   

1. Tools → DNA assembly → Assemble genomes
2. Select SPAdes from the "Assembly method" drop down
3. Select "Paired-end" from the "Library" type drop down
4. Under "Left reads" click "Add"
5. Navigate to folder containing reads
6. Select Left reads (R1 usually)
7. Under "Right reads" click "Add"
8. Navigate to folder containing reads
9. Select right reads (R2 usuallly)
10. _Repeat 4-8 for every sample_
11. Set "Dataset type" to the appropriate type
12. Choose your run mode (Probably "Error correction and Assembly")
13. Select your k-mer sizes ("auto" is probably fine)
14. Click "Start"

For one sample this is not too bad, but what about for tens or hundreds of samples?  Bioinformatics datasets are increasingly being made up of hundreds to thousands of samples.  Clicking through a GUI for this is not scalable.  Instead we might use the below **Bash** oneliner, don't worry about what those two words mean or that the below is incomprehensible to you at the moment.  

```bash
for i in reads/*_R1*.fastq.gz; do spades.pi --careful -1 $i -2 ${i/_R1_/_R2_} -o output/$(basename $i | cut -f1 -d_) -t 6; done
```

The Bash oneliner (really a for-loop written on one line) can process all of the paired reads without user intervention.  



Those of you on MaxOS, just open your Terminal.app from Spotlight (found in /Applications/Utilities/Terminal.app).  For those of you on Windows (hopefully, Windows 10), please install the [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10), which provides a pretty good Linux environment straight in Windows running [Ubuntu](https://www.ubuntu.com/).  

![Install Ubuntu on Windows subsystem for linux](/static/img/uploads/wsl.png "Install Ubunto on WSL")
