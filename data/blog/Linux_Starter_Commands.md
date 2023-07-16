---
title: Linux Starter Commands
date: '2021-03-13'
tags: ['competative programming', 'dynamic programming', 'algorithms']
draft: false
summary: Basic Linux Commands and Techniques
images: []
layout: PostLayout
canonicalUrl:
---

# Linux Starter Commands

## **Fun Commands**

```
# Display arch symbol.
archey3

# task manager
top

# show your hardware info
hwinfo

# Let a cow say your fortune
fortune | cowsay

# Show matrix
cmatrix
```

## **Batch Script**

@echo off: to disable output to console

Define function in cmd file

```
:treeProcess
rem Do whatever you want here over the files of this subdir, for example:
set package[0]=content_api
set package[1]=retail_api
set package[2]=retail_db
set package[3]=shared_repository
set package[4]=student_repository

call :treeProcess
```

Call functions in cmd file

```
:: To call function without parameters 
CALL :function_name 
:: To call function with parameters
CALL :function_name param1, param2,...,paramN
:: To call function with return values
CALL :function_name return_value1,return_value2,..,return_valueN
```

Loops in batch file

```
Syntax: FOR %%var_name IN list DO example_code

FOR /L %%A IN (1,1,200) DO (
  ECHO %%A
)

/L signifies that for loop is used for iterating through a range of values

Or

set "i=0"
:SymLoop
if defined package[%i%] (
    call echo %%package[%i%]%%   
    set /a "i+=1"
    GOTO :SymLoop   
)
```

Conditional Operators

```
EQU Tests the equality between two objects
NEQ Tests the difference between two objects
LSS Checks to see if the left object is less than the right operand
LEQ Checks to see if the left object is less than or equal to the right operand
GTR Checks to see if the left object is greater than the right operand
GEQ Checks to see if the left object is greater than or equal to the right operand
```

## **Bash Script and Linux Tips**

```
for (( initializer; condition; step ))
do
  shell_COMMANDS
done
```

Command substitution

We can execute commands and store output of a command using command substitution

```
echo $(date)

Difference between
remoteOrigin=$(git remote -v)

--> git remote -v is executes the command where the program is run from irrespective of all cd commands used before the program

and

git remote -v

--> executes command and accounts the directory changes that happend
```

Command exit status

```
cmd="git remote -v"
# execute the command
$cmd
# check the output status
status=$?
# echo only if status is 0

```

###

### Show all Github Repos link

```
#!/bin/bash

## TODO: take filename as input
for file in ~/Applications/Repos/*

do
	cmd="git remote -v"
	output=$(cd "$file" && $cmd)
	# get command exit status
	status=$?
	[ $status -eq 0 ]  && echo "$output"
done

## save this script as lsr.sh, give appropirate permissions and run
## lsr >> repolist.txt
```

### **Setting up Environment Variables**

```
resource: https://unix.stackexchange.com/questions/26047/how-to-correctly-add-a-path-to-path

vi .profile

export MAVEN_HOME="path/to/maven/"

PATH=$PATH:$MAVEN_HOME/bin
```

## **Linux commands usage**

### Setting up Bash Aliases

```
touch ~/.bash_aliases
nano ~/.bash_aliases
alias go_home="path/to/home"
source ~/.bash_aliases
```

### ssh keygen

```
ssh-keygen -t rsa -b 4096 -C "krishna@vostro"
```

### Remove a package along with its dependencies using pacman

```
sudo pacman -Rcns mysql-workbench
```

## **Creating a desktop entry for your application**

```
cd ~/.local/share/applicaions

touch myapp.desktop

gedit myapp.desktop

# paste the below content and modify accordingly

[Desktop Entry]

# The type as listed above
Type=Application

# The version of the desktop entry specification to which this file complies
Version=1.0

# The name of the application
Name=Intellij

# A comment which can/will be used as a tooltip
Comment=Idea for java

# The path to the folder in which the executable is run
Path=/run/media/krishna/HOME_PART/Applications/idea/idea-IU-213.6777.52/bin/

# The executable of the application, possibly with arguments.
Exec=idea.sh

# The name of the icon that will be used to display this entry
Icon=idea

# Describes whether this application needs to be run in a terminal or not
Terminal=false

# Describes the categories in which this entry should be shown
Categories=Education;Languages;Java;
```

## **Display all files and their sizes using "du"**

```
# show normal files only

du -sh * | sort -n

# show hidden files only

du -sh .[^.]* | sort -n

# show all files and their sizes

du -ah -d 1 | sort -n
```

## **Mount a Partition on bootup**

```
lsblk
sudo mkdir /media
sudo chown $USER /media
mkdir /media/HOME_PART
sudo mount /dev/sdaXY /media/HOME_PART/

su -

cat /etc/fstab

echo "UUID=$(lsblk -no UUID /dev/sda2) /media/HOME_PART $(lsblk -no FSTYPE /dev/sda2) defaults,noatime 0 2" >> /etc/fstab

cat /etc/fstab
mount -a

```

###

## **Find command**

find is used to search a directory for files. If no initial location is specified, "." is used

There are 5 main options

- \-H
- \-L
- \-P
- \-D
- \-O

\-HLP options control treatment of symbolic links.

These should come before filenames in find command

\-H \-L : Follow symbolic links

\-P:  Never follow symbolic links

\-D: debugopts

```
find [options] [-Olevel] [start-point...] [expression]
```

```
find ./ -name AuthController.java -depth

# find a file with extension .db

find . -name *.db
```

## **awk & grep basics**

Every awk command/rule specifies a pattern to search and an action to perform when the search is successful

```
pattern { action }
pattern { action }
```

### **Regex search in awk**

```
awk '/regex pattern/ {action}' file_name.txt
```

Print 2 column in CSV

```
awk '{print $2}' enterprise-survey.csv
```

Find a word in file

```
awk '/word_to_search/ {print $1 $2}' file_name.csv
```

### **Search a word that fully or partially matches  using grep**

```
grep "service" lib/*
```

### **Search a word that exactly matches**

```
grep -w 'exact_string' lib/*
```

**ZIP a folder**

```
zip -r <output_folder>.zip <folder_to_zip>/*
```
