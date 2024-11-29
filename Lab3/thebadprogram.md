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
<!-- Here, since file permission
Race Condition -->
## Threats
### Issues

# Exploitation

# Mitigation
**Description:** As program does not validate the output file path before writing to it, an attacker could create a symbolic link to a sensitive file (e.g., /etc/shadow) and exploit the timing of the file operations.
**Impact:**
This vulnerability could allow an attacker to overwrite sensitive files, leading to unauthorized access or privilege escalation. To prevent race conditions in your application, we thought about the following strategies:

**Input Validation:**
Validate user inputs to ensure that the output file path does not point to sensitive files. Disallow paths that lead to system files or directories.

```c
   if (strstr(out, "/etc/") != NULL) {
       fprintf(stderr, "Output file cannot be a system file.\n");
       return -1;
   }
```
What we are doing is that we check if the output file path contains `/etc/`, we pring an error message and free any allocated memory before returing an error. 
**Check for Symlinks:**
Before writing to a file, we can check if the target is a symlink and resolve it to its actual target. If it points to a sensitive file, deny the operation.

```c 
   struct stat statbuf;
   if (lstat(out, &statbuf) == 0 && S_ISLNK(statbuf.st_mode)) {
       fprintf(stderr, "Output file cannot be a symlink.\n");
       return -1;
   }
```
Here we added `lstat` to check if the output file is a `symbolic link`. If it is, we print an error message and return an error without proceeding with the copy operation.

These modifications help us to mitigate the risk of `race conditions` and unauthorized access to sensitive data. 

# Conclusion



