---
layout: page
title: Getting vsearch up and running
permalink: /vsearch/
---

AmphiBac requires <a href="https://github.com/torognes/vsearch">vsearch</a> to compare your 16S rRNA gene sequences to the database (don't forget to cite their hard work if you publish...like seriously, look at their source code and appreciate them). While vsearch is free of use, its is available only as a downloadable binary. Luckily for you, we have a script in AmphiBac to pull a version of vsearch for your use. Click the link below for your operating system of choice.

<ol>
  <li>Windows</li>
    <li>MacOS (doesn't matter what chip your Mac has)</li>
    <li>Linux (Ubuntu)</li>
    </ol>  
    
 ## Windows
 
 You're in R...that's like half the battle already. First let's run the 'getwd' command.
 ```
 getwd()
 ```
 This will spit out where R is currently working ony our computer. You want to make note of this because for us to call vsearch in subsequent functions, you want to make sure you're in the right folder. With that let's run the command "COMMAND".

```
download.file("https://github.com/torognes/vsearch/releases/download/v2.22.1/vsearch-2.22.1-win-x86_64.zip", "./vsearch")
unzip("/.vsearch")
 ```
 
 Ths command uses base R functions to download the a version of vsearch (2.22.1), unzips the file to your current workign directory (the location from the 'getwd' command you jsut ran), deletes extra files, and moves the vsearch binary to your current directory. With that, you're all set, nothing else is needed. 
 

    
 ## MacOS
    https://github.com/torognes/vsearch/releases/download/v2.22.1/vsearch-2.22.1-macos-universal.tar.gz
    
    MacOS requires one additional step you have to do outside R. Navigate to where your ran your 'collecting_vsearch' command. Rind the file called 'vsearch'. Right click (ctrl+click works) on the single file and select 'open with' then select 'terminal'. This will open your terminal some stuff will pop up (see below) but you can simply close the terminal and you're good to go. 
    
    
  ## Linux 
    
    If you're using Linux, you probably don't need this becuase you're a computer wizard (respect), but here it is anyways. This tutorial has options for both X86 and Arch-based linux distros.
    
    
    X86: https://github.com/torognes/vsearch/releases/download/v2.22.1/vsearch-2.22.1-linux-x86_64-static.tar.gz
    Arch linux: https://github.com/torognes/vsearch/releases/download/v2.22.1/vsearch-2.22.1-linux-aarch64-static.tar.gz
