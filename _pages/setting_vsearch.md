---
layout: page
title: Getting vsearch up and running
permalink: /vsearch/
---

AmphiBac requires <a href="https://github.com/torognes/vsearch">vsearch</a> to compare your 16S rRNA gene sequences to the database. While vsearch is free of use, its is available only as a downloadable binary. Luckily for you, we have a script in AmphiBac to pull a version of vsearch for your use. CLick the link below for your operating system of choice.

<ol>
  <il>Windows>/il>
    <il>MacOS (doesn't matter what chip your Mac has)</il>
    <il>Linux (Ubuntu)</il>
    
    ## Windows
    https://github.com/torognes/vsearch/releases/download/v2.22.1/vsearch-2.22.1-win-x86_64.zip
    ## MacOS
    https://github.com/torognes/vsearch/releases/download/v2.22.1/vsearch-2.22.1-macos-universal.tar.gz
    
    MacOS requires one additional step you have to do outside R. Navigate to where your ran your 'collecting_vsearch' command. Open the folder called 'vsearch' and then open the fodler called 'bin'. Right click (ctrl+click works) on the single file and select 'open with' then select 'terminal'. This will open your terminal some stuff will pop up (see below) but you can simply close the terminal and you're good to go. 
    
    
    ## Linux 
    
    If you're using Linux, you probably don't need this becuase you're a computer wizard (respect), but here it is anyways. This tutorial has options for both X86 and Arch-based linux distros.
    
    
    X86: https://github.com/torognes/vsearch/releases/download/v2.22.1/vsearch-2.22.1-linux-x86_64-static.tar.gz
    Arch linux: https://github.com/torognes/vsearch/releases/download/v2.22.1/vsearch-2.22.1-linux-aarch64-static.tar.gz
