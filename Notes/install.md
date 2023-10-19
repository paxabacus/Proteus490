
# How to install Proteus
> Shoutout to Sam for figuring it out



## Download Visual Studio Community
> Not VS code (we are trying to make that one work too)


## Download CMAKE

[Download Link](https://cmake.org/download/)

__Make Sure to Allow Path__



## Clone that repo
> the proteus repo obv

In whatever CLI terminal you like (Git, ZSH, bash, CMD, Powershell)
  - Run the following command

    ```
    git clone https://github.com/csun-tavlab/proteus.git  
    ```

## Do the repo commands from proteus repo

CLI Pro's

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

## Visual Studio Community Config

### Building Proteus

1. Open Visual Studio
2. Open a local folder, choose the "build" folder from proteus
3. On the file view (right side of Visual Studio), do the following
    - Rigt click ALL_BUILD.vcxproj
    - Click _BUILD Project_ or equivalent
    - Wait 10 decades for proteus to get ready
4. There should be a "proteus.sln" created 

### Using proteus

1. Open click "proteus.sln"
2. Expand the proteus sub folder
    - Right click "main.cpp"
    - Set "main.cpp" as the startup project
    ![image](https://github.com/paxabacus/Proteus490/assets/64762646/f865ecc4-6b25-451b-91a6-ce67caac1279)



4. Just hit that Local Windows Debugger whilst main.cpp is open
5. A terminal should open with the following lines
  
   ```
      
      The Proteus language compiler
      Usage:
        proteus [OPTION...] INPUT [OUTPUT]
      
        -h, --help          Print this message
            --logfile arg   Output compilation messages to this file instead of
                            stderr
            --loglevel arg  Set the log level (accepts: error, warning, info,
                            debug) (default: info)
        -d, --debug         Same as --loglevel=debug
            --noprefix      Don't emit prefixes in generated code
            --trace         Add trace messages to generated code
        -i, --input arg     Input file
        -o, --output arg    Output file
      
      C:\Users\abpax\Desktop\Git\proteus\build\Release\proteus.exe (process 6656) exited with code 0.
      To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.
      Press any key to close this window . . .   
   ```

    
  

  
