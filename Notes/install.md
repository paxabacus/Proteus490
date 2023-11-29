---
geometry: margin=2cm
author:
- AB Paxtor Garcia
date: 'Change Date'
title: 'Proteus C++ Installation for Windows'
numbersections: true
---

# Dependencies

## Visual Studio Community

[Download Link](https://visualstudio.microsoft.com/vs/community/)

## CMAKE

[Download Link](https://cmake.org/download/)

__Make Sure to Allow Path__

## G++ Compiler

Follow this [GUIDE](https://www.freecodecamp.org/news/how-to-install-c-and-cpp-compiler-on-windows/)

# Repository 

## Cloning the Repo

In whatever CLI terminal you like (Git, ZSH, bash, CMD, Powershell)
  - Run the following command

    ```
    git clone https://github.com/csun-tavlab/proteus.git  
    ```

## Building the Repo

CLI Method

  ```
  cd /path/to/proteus
  ls
  mkdir build
  ls
  cd build
  cmake ..
  ```

Visual Studio Method

  If there is an error, go through Visual Studio:

  - Open Local Folder for proteus repo 
  - In _View_ in the Ribbon, open a terminal
    ```
    mkdir build
    ls
    cd build
    cmake ..
    ```

# Visual Studio

## Building Proteus' Solution

1. Open Visual Studio
2. On the solution explorer
  ![image](https://github.com/paxabacus/Proteus490/assets/64762646/452f150b-cce8-4f1e-b8e1-5d96285ec898)
3. Click the prompt to show all
4. Open "build" Folder
5. Right click on __"ALL_BUILD.vcxproj"__
   - Click __Build Project__ or equivalent
   - A __proteus.sln__ should be created
6. Double Click Proteus, so solution explorer should look like this
  ![image](https://github.com/paxabacus/Proteus490/assets/64762646/6d37bea0-7ab2-4d2b-9c14-8372c9d21e96)
7. Right click __proteus__, then set it as "Set as Startup Project"
   ![image](https://github.com/paxabacus/Proteus490/assets/64762646/4a676320-b3ee-4aa6-a789-73d8c41158db)
8. Click on Local Windows Debugger while main.cpp is open
9. A correct output should be the following
   ![image](https://github.com/paxabacus/Proteus490/assets/64762646/6b5f8c9d-dd30-4386-af07-8c4be0e6f1a5)


# Setting proteus C++ as a system environment variable

## Getting the path to proteus.exe

The path (excluding \proteus.exe) from the terminal output would be the path to proteus.exe

![image](https://github.com/paxabacus/Proteus490/assets/64762646/506dba2f-170f-4403-a987-6e9dea924c92)

My path would be

  ```
    C:\Users\abpax\Desktop\Git\proteus\build\Release
  ```

> Note: if you want to use both Swift-Proteus and C++ Proteus, then change the name of the exe in this path to be "ProteusC++" or any other name. This is so they don't clash

## Environmental Variables

   
1. Look up environment variables in the windows search
  ![image](https://github.com/paxabacus/Proteus490/assets/64762646/ab03c38e-6f73-487a-8a8a-873537690c8c)
2. Click on enviromental variables
   ![image](https://github.com/paxabacus/Proteus490/assets/64762646/da55a73b-32e0-4909-8813-77de9d716d9e)
3. Double click Path on System Variables
   ![image](https://github.com/paxabacus/Proteus490/assets/64762646/a8e3d5ad-6302-4640-9435-2c09284cd041)
4. Paste the path as a new entry
   ![image](https://github.com/paxabacus/Proteus490/assets/64762646/91ccf5b0-2d95-4993-8beb-56b9850c63c9)
5. 





