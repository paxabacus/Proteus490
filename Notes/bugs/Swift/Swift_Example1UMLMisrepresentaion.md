# Report Background

Name of bug finder: AB Paxtor Garcia

Date of Bug Discovery: 11/28/2023

Environment Configuration (i.e. Operating System, Terminal, and etc.):
  - Operating System: Windows 10
  - Ran in terminal (powershell and x86_64 Native Terminal)


# Bug Details

Proteus Version: SWIFT


Error Type (i.e. hangs, parsing error, output error, and etc.):
  - Output Error: In our presention for Elliot, it was noted that the PlantUML markup was incorrect for "1.proteus" in the example folder


Deliverables (i.e. images and others):

  - PlantUML Markup
      ```
      @startuml

      Title Man
      [*] --> Awake
           state Awake {
      
      Awake --> Asleep : CLOCK
             }
           state Asleep {
      
      Asleep --> Awake : CLOCK
             }
      
      @enduml
      ```
      
  - HSM Diagram generated from the plant uml
    
    ![image](https://github.com/paxabacus/Proteus490/assets/64762646/ed148fe3-5c04-4c87-85c9-aea92de19c9e)




# Steps to recreate the bug

## Code being used

  ```
  event CLOCK{int};
  
  actor Man {
      statemachine {
          initial Awake;
  
          int wake_count = 0;
  
          state Awake {
              on CLOCK{hour} {
                  goif (hour == 22) Asleep {}
              }
          }
  
          state Asleep {
              on CLOCK{hour} {
                  goif (hour == 7) Awake {
                      wake_count = wake_count + 1;
                  }
              }
          }
      }
  }
  ```


## How code was compiled

In terminal (x86-64 Native and Powershell)

  ```
  proteus.exe build 1.proteus
  ```



# Other misc. information

## The proposed correct HSM

Elliot said that the correct transitions should be after the states not nested

 ```
@startuml

Title Man
[*] --> Awake
     state Awake {

       }
Awake --> Asleep : CLOCK
     state Asleep {


       }
Asleep --> Awake : CLOCK

@enduml
```

![image](https://github.com/paxabacus/Proteus490/assets/64762646/5b3816da-16f0-4f4f-8d28-49785df2be60)

