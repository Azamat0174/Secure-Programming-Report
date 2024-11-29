---
title: Time Your Programs
subtitle:
author: 
  - Shiva Prasad Gyawali
  - Shirinshoev Azamat
date: 28 November 2024
geometry: top=1.5cm,left=2cm,right=2cm,bottom=2cm
license: CC0 1.0
numbersections: true
highlightstyle: pygments
header-includes:
    - \usepackage{package_deps/comment}
    - \usepackage{multicol}
    - \usepackage{lmodern}
    - \newcommand{\hideFromPandoc}[1]{#1}
    - \hideFromPandoc{
        \let\Begin\begin
        \let\End\end
      }
colorlinks: true
lang: en-GB
---


# Introduction


# Analysis
In this section, we first build our program to get its executable binary and observe it's behaviour by executing with different inputs. We will also explore if there are any threats or issues we can find potential to be exploited.

## Program Behaviour 
### Source Code Analysis
Our Directory hierarchy for project_v0 is:
```bash
project_v0
├── CMakeLists.txt
└── sources
    ├── functions
    │   ├── functions.c
    │   ├── functions.h
    │   └── hidden_functions
    │       ├── hidden_functions.c
    │       └── hidden_functions.h
    └── main.c
```
Program execution flow is as shown in the following diagram:
![Program Flowchart](./images/flowchart.png)

### Program Internal working
In the `secure_copy_file()` function, it is working as below:

![Secure copy function](./images/secure_copy.png)

Time of Check, Time of Use:
Here, since file permission
Race Condition
## Threats
### Issues

# Exploitation

# Mitigation



# Conclusion



