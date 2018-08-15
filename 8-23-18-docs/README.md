
[Book](https://lnduy.files.wordpress.com/2013/05/comptia-linux-lx0-101-lx0-102.pdf)

<h1> CHAPTER 1 </h1>

* [Understadning Command-Line Basics](#Understadning Command-Line Basics)
* [Using Streams, Redirection, and Pipes](#Using Streams, Redirection, and Pipes)
* [Processing Text Using Filters](#Processing Text Using Filters)
* [Using Regular Expressions](#Using Regular Expressions)

<h2> Understadning Command-Line Basics</h2> <a id="Understadning Command-Line Basics"></a>
- enviornment variables = place holders for data

<h3> Shell options </h3>

- bash - GNU Bourne Again Shell(bash), default shell for unix, exam
- sh
- tcsh - Base on C shell,<font color="green">env assiging differ to Bash</font>
- csh -  Original C shell
- ksh -  Korn shell, best of bash + csh + extend 
- zsh -  Z shell, ksh+ earliersh + extend


<p><font color="red">*Two default shells:*</font>

- default ineractive shell - User enter commands
- default system shell - System runs system shell scripts

--------------------

<h3> Using a Shell</h3>

- Most linux commands are **external** - **programs** seperate from shell
- Few **internal**

----------------


### Starting a Shell ###

- *ssh* drops you to default shell
- In GUI, you can start shell emulator- **xterm, konsole**



```bash
uname
```

    Darwin



```bash
uname -a 
```

    Darwin MCIC-SEL17-D1 15.3.0 Darwin Kernel Version 15.3.0: Thu Dec 10 18:40:58 PST 2015; root:xnu-3248.30.4~1/RELEASE_X86_64 x86_64


- Os - Linux
- hostname - e6b10caa4558
- Kernel -  4.0.9-boot2docker

______________
### Using Internal and External Commands ###

   *Internal commands are called built-in commands*
   
 <h4>Internal Commands:</h4>
 
 - Change the Working Directory
```bash
cd Linux_lessons_files # changing the directory to Linux_lessons_files
cd ~ # changing the directory to $HOME
```

- Display Working Directory
```bash
pwd #print working directory
```

- Display a Line of Text
```bash
echo Hello
```

- Time an Operation
```bash
time pwd
```
    - Total execution time (aka real time)
    - User CPU time
    - System CPU time


```bash
time echo Helloooo
```

    Helloooo
    
    real	0m0.000s
    user	0m0.000s
    sys	0m0.000s


- Set Options 

> Ex:

> In bash like in any Bourne-like shell, set is the command to set options (shell configuration settings like -f, -C, -o noclobber...) and positional parameters (\$1, \$2...).

> ```bash
set FILEM="razrax"
echo "$1"
```
FILEM=razrax

    - The syntax for variable assignment in Bourne-like shells is:
  
  ```bash
  VAR=value
  ```

- Terminate the Shell
  - exit - Terminates any shell, kill imulators: xterm, Terminal
  - logout - Terminates *login shell*, when iniate text-mode login


*Check a command to determine if a command is a built-in:*
  


```bash
type pwd
```

    pwd is a shell builtin



```bash
type cd
```

    cd is a shell builtin



```bash
type -a time
```

    time is a shell keyword



```bash
type bash
```

    bash is /bin/bash



```bash
#Some of the commands are duplicated by external-commands, to check use -a
type -a cd
```

    cd is a shell builtin



```bash
type -a pwd
```

    pwd is a shell builtin
    pwd is /bin/pwd


><font color="Red"> Note:</font>
>Even external commands are installed *built-in* commands take precedence  

>Sometime *built-in* provides slightly different output than external-commands

> when type a command, shell checks its internal commands, then in *PATH* - list of directories in which commands can be found.


**You have to set the program's executable bit to execut a program**

--------------

### Performing Some Shell Command Tricks ###

- Command Completion
    - Maximum characters for the filename = 255
- history
    - Last 500 commands
    - !! show and execute the last command 
    - !20 execute the 20th command
    - history -c clear the history
    - History stored in <font color="green">**.bash_history -plain text file**</font>
    - **Retrieve a Command**: *Up* or *Down* or ctrl + P or ctrl + N
    - **Search for a Command**: *ctrl + R* - backward search, and type characters unique to command, then keep press *ctrl + R* until you find it. Forward search *ctrl + S*
    - <font color="red">TIP:</font> if your stuck while above step use *ctrl + Q*. To avoid ** stty -ixon **
    - *Ctrl + G* -Terminate
    
- Move within the line
    - *Ctrl+A* - Go to the begining of the line
    - *Ctrl+E* - Go to the end od the line
    - *>* or *Ctrl+F* - Move one character to the right
    - *<* or *Ctrl+B*  - Move one character to the left
    - *Ctrl + >* or * Esc then F* - Move word at a time to right
    - *Ctrl + <* or * Esc then B * - Move word at a time to left
    
- Delete Text
    - *Ctrl+D* - Delete chatacter / *Delete* button
    - *Ctrl+K* - Delete all the character from the curosr to the end of the line
    - *Ctrl+X and Backspace* - Delete all the characters from the curosr to the begining 
    
- Transpose text
    - *Ctrl +T* - Transpose the character before the cursor with character under the cursor
    - *Esc and T* - Transpose the two words immediatly before the cursor
    
- Change Case
    - *Esc then U* - Cusrsor to end of the word upper case
    - *Esc then L* - Cursor to end of the word to lower case
    - *Esc then C* - Letter undet the cursor to upper case, rest unaffected
    
- Invoke Editor
    - *Ctrl+X followed by Ctrl+E* - Editor 
    - Launch depends on \$FCEDIT or \$EDITOR
    
    

___
### Exploring Shell Configuration ###

- shells configured throgh the configuration files-plain test formated file
- Bash configuration file -bash shell script
- e.g: ~/.bashrc and /etc/profile

<font color="red">WARNING:</font> Careful when changing the global config files. 
    - Make a copy before change
    - Logging in using another VT and check the changes

___________
### Using Environment Variables ###
- Variables like in programes, hold data rfered to by the variables
- Differ from internal variables:
    - part of the program enviornment, such as shell
    - can modifiy this environment
- Programs rely on environment variable
    - e.g: text-based programs rely on \$TERM, hold the capabilitis of terminal program you use


```bash
echo $TERM
```

    xterm-256color


- Setting environment variable
    - E.g:

```bash
export PS1="My new Prompt"
echo $PS1

```
- <font color="red">NOTE:</font> Some variable are set automatically, via shell **shell config file**,e.g $PATH. *Program doc should say use of any env variables*
- env - Shows all the env variables
- unset - To delete a variable
    - e.g: 
    
    ```bash 
    unset $PS1 
    
    ```
    - To delete terminal prompt

_____________
### Getting Help ###

- man - Help system, summaries file, command, or other feature does
- Use _less_ pager to display
    - _Space bar_ - move a page forward
    - _Esc then V_ - move a page backward
    - _ Up arrow or Down arrow_ - line by line
    - _/_ - To search text
    - _Q_ - To excit
- To change the pager
    - e.g: To _more_
    ```bash
    man -P /bin/more uname
    ```
- e.g: If you want to know the 'export' or builtin command

```bash
man export
man builtin
```
- Search the manual pages for the keywords
```bash 
man -k "system information"
```
    - man util keyword search not implimented in old systems, to get it work, type in the terminal as _sudo_
    - 
    ```bash
    makewhatis
    ```
-Keywords can be in serveral sections, default man print lowest-numbered section
    - 
    ```bash
    man 5 passwd
    ```
    - returns info on the passwd _file format_ than the _passwd command_

<table id="box-table-a">
<tr>
    <th>Section number</th> <th>Description</th> 
</tr>
    
    <tr> <td>1 </td> <td>Executable programs and the shell commands</td> </tr>
    <tr> <td>2 </td> <td  >System calls provideed by the kernel</td> </tr>
    <tr> <td>3 </td> <td  >Library Calls provided by program libraries</td> </tr>
    <tr> <td>4 </td> <td  >Device files (usually stored in /dev</td> </tr>
    <tr> <td>5 </td> <td  >File formats</td> </tr>
    <tr> <td>6 </td> <td  >Games</td> </tr>
    <tr> <td>7 </td> <td  >Miscellaneous (macro packages, conventions, and so on</td>
    <tr> <td>8 </td> <td  >System administration commands (Programs run mostly or exlusively by root)</td> </tr>
    <tr> <td>9 </td> <td  >Kernel routines</td> </tr>
</table>

- <font color="green">info</font> - same as _man_, but use Hypertext format, can easily go section to section
- <font color="green">help</font> - pages for builtin commands

<h2> Using Streams, Redirection, and Pipes </h2> <a id="Using Streams, Redirection, and Pipes"></a>

### Exploring File Descriptors ###
- For Linux all objects are files
- Programs treat STDIN, STDOUT and, STDERR as regular files

<table id="box-table-a">
<tr>
    <th>Name</th> <th>Abbrevation</th> <th>Descriptor</th> 
</tr>
    
    <tr> <td>Standard Input </td> <td>STDIN</td> <td>0</td></tr>
    <tr> <td>Standard output </td> <td>STDOUT</td> <td>1</td></tr>
    <tr> <td>Standard Error </td> <td>STDERR</td><td  >2</td>  </tr>
</table>



### Redirecting Input and Output ###

- STDOUT to a file


```bash
echo $PATH 1> Linux_lessons_files/path.txt
cat Linux_lessons_files/path.txt
```

    /Users/saranga/anaconda/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/usr/local/mysql/bin:/Users/saranga/Documents/WORK/Software/samtools-1.2/misc:/Users/saranga/Desktop/Tomato_RNA_Align_Kallisto/Software/kallisto/build/src:/Users/saranga/Documents/WORK/Software/samtools-1.2/:/Users/saranga/Documents/WORK/Software/FastQC:/Users/saranga/Documents/WORK/Software/scythe:/Users/saranga/Documents/WORK/Software/sickle:/Users/saranga/Documents/WORK/Software/tophat-2.1.0.OSX_x86_64:/usr/texbin:/Users/saranga/Documents/WORK/Software/bedtools2/bin:/Users/saranga/cctools/bin:/Users/saranga/Documents/WORK/Software/bowtie2-2.2.6


<font color="blue">Note:</font> STDOUT or STDIN doesn't need to use its descriptir(1/0), can use the operator only (>/<). 

<table id="box-table-a">
<tr>
    <th>Redirection Operator</th><th>Descriptor</th> <th>New File</th> <th>Over Writes Exist File</th> <th>Descriptor Need</th>
</tr>
    
    <tr> <td>> </td> <td>1, STDOUT</td><td>Creates</td> <td>Yes</td> <td>No, Operator enough</td> </tr>
    <tr> <td>>> </td> <td>1, STDOUT</td><td>No</td> <td>No, Appends</td> <td>No, Operator enough</td> </tr>
    <tr> <td> 2> </td> <td>2, STDERR</td><td>Creates</td> <td>Yes</td> <td>Yes</td> </tr>
    <tr> <td> 2>> </td> <td>2, STDERR</td><td>No</td> <td>No, Appends</td> <td>Yes</td> </tr>
    <tr> <td> &> </td> <td>Both STDOUT n STDERR</td><td>Yes</td> <td>Yes</td> <td>No</td> </tr>
     <tr> <td> < </td> <td>0, STDIN<td>NA</td> <td>NA</td> <td>No</td></tr>
     <tr> <td> <\< </td> <td>0, STDIN<td>NA, Accept text on following lines as STDIN</td> <td>NA</td> <td>No</td></tr>
     <tr> <td> <> </td> <td>NA<td>NA,Accept file as input and output</td> <td>Yes</td> <td>No</td></tr>


</table>


```bash
echo "Hello From the otherside" >Linux_lessons_files/Hello.txt
```

    


```bash
cat <> Linux_lessons_files/Hello.txt
```

    Hello From the otherside


- << implements _a here document_ 


```bash
sort -k1 << EOF
1 one
3 three
2 two
EOF
```

    1 one
    2 two
    3 three


<font color="Orange">TIP: </font>STDERR or STDOUT to /de/null, device connect to nothing which is used when you want to get rid of data

________________
### Piping Data Between Programs ####

- Pipe redirects the first program's STDOUT to second's STDIN
    - grep, command used with pipe
    - tee, splits the STDIN and diplay om STDOUT
        - Use when STDOUT needs to be stored and view
        - File is over writen, to append 
        ```bash
        tee -a
        ```


```bash
echo $PATH | tee Linux_lessons_files/Pipe_tee.txt
```

    /Users/saranga/anaconda/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/mysql/bin:/Users/saranga/Desktop/Mothur_Workshop/mothur


_________________________
### Generating Command lines ###

<font color="Orange">USE CASE :</font> Search for the directories belong to certain users 
- Commands : find & xargs

```bash
xargs [options] [command[initial-arguments]]

find / -name Christne | xargs -d "\n" rm 

```
    -d "\n" when dealing with folder with spaces in their filenames, use only newline as delimeter

- Command : (`) backtick
```bash
rm `find ./ -user Christine`
```
    - Both xargs and ` work very similar but ` fails some complex situations.
    - Backtick outputs contains command is passed to the command it precedes as if it had been typed at the shell
    ![Example](images/backtick.png)
- Command : \$()

```bash
rm $(find ./ -name Christine)
```

____________________
<h2> Processing Text Using Filters </h2><a id="Processing Text Using Filters"></a>

### File-Combining Commands ###

- Command : <font color="green">_cat_ </font>_concatenate_
    - display content of short file, for larger files pagers like _less_ or _more_


```bash
cat Linux_lessons_files/cat_first.txt Linux_lessons_files/cat_second.txt | tee Linux_lessons_files/cat_final.txt
```

    Data from first file
    Data from second file


<table id="box-table-b">
<tr>
    <th>Description</th> <th>Option</th> 
</tr>
    
    <tr> <td>Display Line Ends</td> <td>-E, --show-ends (\$) </td></tr>
    <tr> <td>Number line Ends</td> <td>-n, --number, -b, --number-nonblank (number only lines that contain text)</td></tr>
    <tr> <td>Minimize Blank Lines</td> <td>-s, --squeeze-blank(group of blank line to single blank line)</td></tr>
    <tr> <td>Display Special Chatacters</td> <td>-T, --show-tabs(^I), -v,--show-nonprinting</td></tr>
</table>


```bash
cat -e Linux_lessons_files/sort_splitedab
```

    555-9871 Orwell, Samuel, FEB, ABC$
    555-7929 Jones, Theresa, MAR, dEF


```bash
cat -n Linux_lessons_files/sort_this_file.txt
```

         1	555-2397 Beckett, Barry, JAN, aBc
         2	555-5116 Carter, Gertrude, DEC, ABc
         3	555-9871 Orwell, Samuel, FEB, ABC
         4	555-7929 Jones, Theresa, MAR, dEF


```bash
cat Linux_lessons_files/cat_squeeze.txt && cat -s Linux_lessons_files/cat_squeeze.txt
```

    Line one
    
    
    Line two
    Line one
    
    Line two


- Command : <font color="green">_tac_ </font>_same as cat_
    - revers the order of the output

### Joining files by Filed with _join_ ###

- combine two files by matchig coloumn, more like database join
- Your two coloumns have to be <font color="red"> sorted</font> befor joining

<table id="box-table-b">
<tr>
    <th>Parameter</th> <th>Purpose</th> 
</tr>
    
    <tr> <td>-t _char_</td> <td>Default _tabs_, can use to set the field seperator</td></tr>
    <tr> <td>-i</td> <td>ignore case while do the field matching </td></tr>
    <tr> <td>-1 -2 </td> <td>-1 3 -2 2, Use 3rd col of first file n 2nd filed of sec'nd file </td></tr>
    <tr> <td>-o </td> <td>Output fileds </td></tr>
   
</table>


```bash
cat Linux_lessons_files/join_this_file1.txt Linux_lessons_files/join_this_file2.txt
```

    555-2397
    555-5116
    555-9871
    555-7929
    555-2397 Beckett
    555-5116 Carter
    555-9871 Orwell
    555-7929 Jones



```bash
join Linux_lessons_files/join_this_file1.txt Linux_lessons_files/join_this_file2.txt
```

    555-2397 Beckett
    555-5116 Carter
    555-9871 Orwell
    555-7929 Jones


### Merging Lines with paste ### [cbtnuggets](https://www.cbtnuggets.com/it-training/lpi-linux-lpic-1-and-comptia-linuxplus-prep/20?autostart=1)
- combine line by line seperate by tab


```bash
cat Linux_lessons_files/join_this_file1.txt Linux_lessons_files/join_this_file2.txt
```

    555-2397
    555-5116
    555-9871
    555-7929
    555-2397 Beckett
    555-5116 Carter
    555-9871 Orwell
    555-7929 Jones



```bash
paste Linux_lessons_files/join_this_file1.txt Linux_lessons_files/join_this_file2.txt
```

    555-2397	555-2397 Beckett
    555-5116	555-5116 Carter
    555-9871	555-9871 Orwell
    555-7929	555-7929 Jones


### Converting Tabs to Space with _expand_ ###
- By default, tab is every 8 characters
- t changes the number


```bash
paste Linux_lessons_files/join_this_file1.txt Linux_lessons_files/join_this_file2.txt | expand
```

    555-2397        555-2397 Beckett
    555-5116        555-5116 Carter
    555-9871        555-9871 Orwell
    555-7929        555-7929 Jones


### Display  Files in Octal with _od (Octal Dump)_ ###

- some files not in ASCII, graphical files, music files


```bash
od Linux_lessons_files/Pipe_tee.txt
```

    0000000    052457  062563  071562  071457  071141  067141  060547  060457
    0000020    060556  067543  062156  027541  064542  035156  072457  071163
    0000040    066057  061557  066141  061057  067151  027472  071565  027562
    0000060    064542  035156  061057  067151  027472  071565  027562  061163
    0000100    067151  027472  061163  067151  027472  071565  027562  067554
    0000120    060543  027554  074555  070563  027554  064542  005156        
    0000136


### Sorting Files with *sort* ###




| Parameter | Perpose |
|----------:|---------:|
| -f, --ignore-case | Ignore Case |
| -M, --month-sort | Month sort (JAN-DEC)|
| -n, --numeric-sort | sort by number |
| -r, --reverse | sorts in reverse order |
| -k, --key=filed | default, first field, --k=1 or --k=1,3,4  |


```bash
sort  Linux_lessons_files/sort_this_file.txt
```

    555-2397 Beckett, Barry, JAN, aBc
    555-5116 Carter, Gertrude, DEC, ABc
    555-7929 Jones, Theresa, MAR, dEF
    555-9871 Orwell, Samuel, FEB, ABC



```bash
sort -k 2 Linux_lessons_files/sort_this_file.txt #With k

```

    555-2397 Beckett, Barry, JAN, aBc
    555-5116 Carter, Gertrude, DEC, ABc
    555-7929 Jones, Theresa, MAR, dEF
    555-9871 Orwell, Samuel, FEB, ABC



```bash
sort -M -k 4 Linux_lessons_files/sort_this_file.txt
```

    555-2397 Beckett, Barry, JAN, aBc
    555-9871 Orwell, Samuel, FEB, ABC
    555-7929 Jones, Theresa, MAR, dEF
    555-5116 Carter, Gertrude, DEC, ABc



```bash
sort -k 5 Linux_lessons_files/sort_this_file.txt #without -f option
```

    555-9871 Orwell, Samuel, FEB, ABC
    555-5116 Carter, Gertrude, DEC, ABc
    555-2397 Beckett, Barry, JAN, aBc
    555-7929 Jones, Theresa, MAR, dEF



```bash
sort -f -k 5 Linux_lessons_files/sort_this_file.txt #with -f option
```

    555-2397 Beckett, Barry, JAN, aBc
    555-5116 Carter, Gertrude, DEC, ABc
    555-9871 Orwell, Samuel, FEB, ABC
    555-7929 Jones, Theresa, MAR, dEF


-------------------------------------------------------------------------------------------------------------------

### Breaking a File into pieces with *split*  ###

| Parameter | Perpose |
|----------:|---------:|
| -b *Size*, --bytes=*size* | split into *size* bytes files, can avoid split files half way |
| -C=*size*, --line-bytes=*size* | Split by Bytes in Line-Sized chunks|
| -l=*lines*, --lines= *lines* | Split by Number of Lines |


```bash
split -l 2 Linux_lessons_files/sort_this_file.txt Linux_lessons_files/sort_splited
```

    

This will break *sort_this_file* into two files, numbers aa and ab 


```bash
ls -ls Linux_lessons_files/*
```

    4 -rw-r--r-- 1 1000 staff  70 Jan  6 19:01 Linux_lessons_files/sort_splitedaa
    4 -rw-r--r-- 1 1000 staff  67 Jan  6 19:01 Linux_lessons_files/sort_splitedab
    4 -rw-r--r-- 1 1000 staff 137 Sep 10 18:18 Linux_lessons_files/sort_this_file.txt



```bash
head  Linux_lessons_files/sort_splitedaa
```

    555-2397 Beckett, Barry, JAN, aBc
    555-5116 Carter, Gertrude, DEC, ABc


> **NOTE:** 
> <p>*If you specify any default*

> ```bash
split Linux_lessons_files/sort_this_file.txt
```
> *file split into **1,000 line chunks**, name begins with x ( xaa,xab, and so on). If no input is specified **split uses standard input** *




```bash
ls -lh Linux_lessons_files/sort_this_file.txt;split -b 40 Linux_lessons_files/sort_this_file.txt Linux_lessons_files/sort_splited_bytes
ls -lh Linux_lessons_files/sort_splited_bytes*
```

    -rw-r--r--  1 saranga  staff    40B Jan 31 13:36 Linux_lessons_files/sort_splited_bytesaa
    -rw-r--r--  1 saranga  staff    40B Jan 31 13:36 Linux_lessons_files/sort_splited_bytesab
    -rw-r--r--  1 saranga  staff    40B Jan 31 13:36 Linux_lessons_files/sort_splited_bytesac
    -rw-r--r--  1 saranga  staff    17B Jan 31 13:36 Linux_lessons_files/sort_splited_bytesad


--------------------------------------------------------------------------------------------------------------------

### Translating Characters with *tr* ###

```bash
    tr [options] SET1 SET2

```

| Parameter | Perpose |
|----------:|---------:|
| -t, --truncate-set1 | truncate, SET1=SET2 |
| [:alnum:]| all letters and digits|
| [:upper:] | all upper case letters |
| [:lower:] | all lower case letters|
| [:digit:] | all digits |
| -, range | A-M any character between A to M|

<p>SET1 : characters you want replaced in 
<p>SET2 : characters you want them to be replaced as


```bash
tr BC bc < Linux_lessons_files/sort_this_file.txt
```

    555-2397 beckett, barry, JAN, abc
    555-5116 carter, Gertrude, DEc, Abc
    555-9871 Orwell, Samuel, FEb, Abc
    555-7929 Jones, Theresa, MAR, dEF

> **NOTE:**
> <p> * **tr** relies on standard input, i.e why (<) redirection of a input is needed*


```bash
tr BCJ bc < Linux_lessons_files/sort_this_file.txt
```

    555-2397 beckett, barry, cAN, abc
    555-5116 carter, Gertrude, DEc, Abc
    555-9871 Orwell, Samuel, FEb, Abc
    555-7929 cones, Theresa, MAR, dEF

When SET2 < SET1 *tr* substitutes the last letter of SET2 with missing letter. In this case, "c" with "J"



```bash
#run this in Ubuntu
tr -t BCJ bc < Linux_lessons_files/sort_this_file.txt
```

    555-2397 beckett, barry, JAN, abc
    555-5116 carter, Gertrude, DEc, Abc
    555-9871 Orwell, Samuel, FEb, Abc
    555-7929 Jones, Theresa, MAR, dEF


```bash
tr -d BC < Linux_lessons_files/sort_this_file.txt
```

    555-2397 eckett, arry, JAN, ac
    555-5116 arter, Gertrude, DE, Ac
    555-9871 Orwell, Samuel, FE, A
    555-7929 Jones, Theresa, MAR, dEF


```bash
tr [:lower:]  [:upper:] < Linux_lessons_files/sort_this_file.txt
```

    555-2397 BECKETT, BARRY, JAN, ABC
    555-5116 CARTER, GERTRUDE, DEC, ABC
    555-9871 ORWELL, SAMUEL, FEB, ABC
    555-7929 JONES, THERESA, MAR, DEF


```bash
type -a tr 
```

    tr is /usr/bin/tr


### Converting Spaces to Tabs with *unexpand* ###

*expand*

- Logical oppsite to *expand*
- Converts multiple *spaces* to *Tabs*

<font color="blue">Note:</font> This helps to reduce file size, make delimited file

-t/ --tabs=num Sets the tab spacing to once every *num*


```bash
unexpand Linux_lessons_files/join_this_file2.txt
```

    555-2397 Beckett
    555-5116 Carter
    555-9871 Orwell
    555-7929 Jones


### Deleting Duplicate Lines with _uniq_ ###


```bash
tee  Linux_lessons_files/sort_me.txt << EOF
the\n
one\n
to\n
the\n
one\n
two\n
the\n
to\n
EOF
```

    the\n
    one\n
    to\n
    the\n
    one\n
    two\n
    the\n
    to\n



```bash
sort Linux_lessons_files/sort_me.txt | uniq #File has to be sorted before uniq command execution
```

    one\n
    the\n
    to\n
    two\n



```bash
uniq Linux_lessons_files/sort_me.txt
```

    the\n
    one\n
    to\n
    the\n
    one\n
    two\n
    the\n
    to\n


### File-Formating Commands ###
- <font color="green">fmt,nl, pr </font> format the text in file
- fmt - reformat text file, lines are long for your display
- nl - number the lines of your files
- pr - format files to suitable for processing 



```bash
cat Linux_lessons_files/fmt.fasta
```

    >BM1Na_2 MCIC-SOLEXA_0051_FC:0::1:1:3547:1067:ATCACG
    GAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCTGTGAATTGCAGAATTTAGTGAATCATCGAAGCTTTTTGCAACAAAAACTGACCTCGGATCGGGTAGGACTACCCGCTGAACTTAA
    >BM1Na_6 MCIC-SOLEXA_0051_FC:0::1:1:7881:1167:AAGGTT
    GACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAAGAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCAAGGTTGACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAA
    >BM1Na_7 MCIC-SOLEXA_0051_FC:0::1:1:5494:1193:ATCACG
    GAAATTCGATAAGTAGTGTGAATTGCAGAATTCCGCGsdajjdkjakjdkajskdjakjdsipeq[]qklq,mvckdajdjakdjkajakdjakdjakdadjakjdakjdkajdkajkdjsAATCATCGAATCTTTGAACGCCCTCTTTCCTCA	AGGTTGACCTCGGATCAGGTGGGAAGACCCGCTGAACTTAA



```bash
fmt -w 60 Linux_lessons_files/fmt.fasta
```

    >BM1Na_2 MCIC-SOLEXA_0051_FC:0::1:1:3547:1067:ATCACG
    GAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCTGTGAATTGCAGAATTTAGTGAATCATCGAAGCTTTTTGCAACAAAAACTGACCTCGGATCGGGTAGGACTACCCGCTGAACTTAA
    >BM1Na_6 MCIC-SOLEXA_0051_FC:0::1:1:7881:1167:AAGGTT
    GACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAAGAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCAAGGTTGACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAA
    >BM1Na_7 MCIC-SOLEXA_0051_FC:0::1:1:5494:1193:ATCACG
    GAAATTCGATAAGTAGTGTGAATTGCAGAATTCCGCGsdajjdkjakjdkajskdjakjdsipeq[]qklq,mvckdajdjakdjkajakdjakdjakdadjakjdakjdkajdkajkdjsAATCATCGAATCTTTGAACGCCCTCTTTCCTCA
    AGGTTGACCTCGGATCAGGTGGGAAGACCCGCTGAACTTAA


###### Numbering Lines with _nl_ ######

<table id="box-table-b">
<tr>
    <th>Description</th> <th>Option</th> 
</tr>
    
    <tr> <td>Body Numbering Style</td> <td>-b, --body-numbering=_style option_, style:format code </td></tr>
    <tr> <td>Header and Footer Numbering Style</td> <td> -h style --header-numbering=_style_, -f _style_, --footer-numbering</td></tr>
    <tr> <td>Page Separator</td> <td>-how to find new page -d=code or --section-delimiter=code(code=character for the new page)</td></tr>
    <tr> <td>Line-Number Options for New pages</td> <td>-n _format_, --number-format=_format_: ln left justfied, rn:right justfied, no leading 0, rz, r j +0</td></tr>
</table>

<table id="box-table-b">
<tr>
    <th>Style Code</th> <th>Description</th> 
</tr>
    
    <tr> <td>t</td> <td>Default:number none empty lines </td></tr>
    <tr> <td>a</td> <td>Number all lines + empty lines</td></tr>
    <tr> <td>n</td> <td>All lines numbers to be omitted</td></tr>
    <tr> <td>-p_REGEXP_</td> <td>Number any line match to regexp</td></tr>
</table>


```bash
nl Linux_lessons_files/fmt.fasta
```

         1	>BM1Na_2 MCIC-SOLEXA_0051_FC:0::1:1:3547:1067:ATCACG
         2	GAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCTGTGAATTGCAGAATTTAGTGAATCATCGAAGCTTTTTGCAACAAAAACTGACCTCGGATCGGGTAGGACTACCCGCTGAACTTAA
         3	>BM1Na_6 MCIC-SOLEXA_0051_FC:0::1:1:7881:1167:AAGGTT
         4	GACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAAGAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCAAGGTTGACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAA
         5	>BM1Na_7 MCIC-SOLEXA_0051_FC:0::1:1:5494:1193:ATCACG
         6	GAAATTCGATAAGTAGTGTGAATTGCAGAATTCCGCGsdajjdkjakjdkajskdjakjdsipeq[]qklq,mvckdajdjakdjkajakdjakdjakdadjakjdakjdkajdkajkdjsAATCATCGAATCTTTGAACGCCCTCTTTCCTCA	AGGTTGACCTCGGATCAGGTGGGAAGACCCGCTGAACTTAA



```bash
nl -h n Linux_lessons_files/fmt.fasta
```

         1	>BM1Na_2 MCIC-SOLEXA_0051_FC:0::1:1:3547:1067:ATCACG
         2	GAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCTGTGAATTGCAGAATTTAGTGAATCATCGAAGCTTTTTGCAACAAAAACTGACCTCGGATCGGGTAGGACTACCCGCTGAACTTAA
         3	>BM1Na_6 MCIC-SOLEXA_0051_FC:0::1:1:7881:1167:AAGGTT
         4	GACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAAGAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCAAGGTTGACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAA
         5	>BM1Na_7 MCIC-SOLEXA_0051_FC:0::1:1:5494:1193:ATCACG
         6	GAAATTCGATAAGTAGTGTGAATTGCAGAATTCCGCGsdajjdkjakjdkajskdjakjdsipeq[]qklq,mvckdajdjakdjkajakdjakdjakdadjakjdakjdkajdkajkdjsAATCATCGAATCTTTGAACGCCCTCTTTCCTCA	AGGTTGACCTCGGATCAGGTGGGAAGACCCGCTGAACTTAA



```bash
nl -n ln Linux_lessons_files/fmt.fasta
```

    1     	>BM1Na_2 MCIC-SOLEXA_0051_FC:0::1:1:3547:1067:ATCACG
    2     	GAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCTGTGAATTGCAGAATTTAGTGAATCATCGAAGCTTTTTGCAACAAAAACTGACCTCGGATCGGGTAGGACTACCCGCTGAACTTAA
    3     	>BM1Na_6 MCIC-SOLEXA_0051_FC:0::1:1:7881:1167:AAGGTT
    4     	GACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAAGAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCAAGGTTGACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAA
    5     	>BM1Na_7 MCIC-SOLEXA_0051_FC:0::1:1:5494:1193:ATCACG
    6     	GAAATTCGATAAGTAGTGTGAATTGCAGAATTCCGCGsdajjdkjakjdkajskdjakjdsipeq[]qklq,mvckdajdjakdjkajakdjakdjakdadjakjdakjdkajdkajkdjsAATCATCGAATCTTTGAACGCCCTCTTTCCTCA	AGGTTGACCTCGGATCAGGTGGGAAGACCCGCTGAACTTAA



```bash
nl -n rn Linux_lessons_files/fmt.fasta
```

         1	>BM1Na_2 MCIC-SOLEXA_0051_FC:0::1:1:3547:1067:ATCACG
         2	GAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCTGTGAATTGCAGAATTTAGTGAATCATCGAAGCTTTTTGCAACAAAAACTGACCTCGGATCGGGTAGGACTACCCGCTGAACTTAA
         3	>BM1Na_6 MCIC-SOLEXA_0051_FC:0::1:1:7881:1167:AAGGTT
         4	GACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAAGAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCAAGGTTGACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAA
         5	>BM1Na_7 MCIC-SOLEXA_0051_FC:0::1:1:5494:1193:ATCACG
         6	GAAATTCGATAAGTAGTGTGAATTGCAGAATTCCGCGsdajjdkjakjdkajskdjakjdsipeq[]qklq,mvckdajdjakdjkajakdjakdjakdadjakjdakjdkajdkajkdjsAATCATCGAATCTTTGAACGCCCTCTTTCCTCA	AGGTTGACCTCGGATCAGGTGGGAAGACCCGCTGAACTTAA



```bash
nl -n rz Linux_lessons_files/fmt.fasta
```

    000001	>BM1Na_2 MCIC-SOLEXA_0051_FC:0::1:1:3547:1067:ATCACG
    000002	GAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCTGTGAATTGCAGAATTTAGTGAATCATCGAAGCTTTTTGCAACAAAAACTGACCTCGGATCGGGTAGGACTACCCGCTGAACTTAA
    000003	>BM1Na_6 MCIC-SOLEXA_0051_FC:0::1:1:7881:1167:AAGGTT
    000004	GACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAAGAAATGCGATAAGTAATGTGAATTGCAGAATTCAGTGAATCATCGAATCTTTGAACACCCCCCTTTTCTCAAGGTTGACCTCGGATCAGGTAGGAAGACCCGCTGAACTTAA
    000005	>BM1Na_7 MCIC-SOLEXA_0051_FC:0::1:1:5494:1193:ATCACG
    000006	GAAATTCGATAAGTAGTGTGAATTGCAGAATTCCGCGsdajjdkjakjdkajskdjakjdsipeq[]qklq,mvckdajdjakdjkajakdjakdjakdadjakjdakjdkajdkajkdjsAATCATCGAATCTTTGAACGCCCTCTTTCCTCA	AGGTTGACCTCGGATCAGGTGGGAAGACCCGCTGAACTTAA


### Preparing a File for Printing with _pr_ ###

Skiping

### File-Viewing Commands ###

- head, first 10 lines

|Option|Description|
|------|-----------|
|-c _num_, --bytes=_num_ | display _num_ bytes|
|-n _num_, --lines=_num_| n of lines to display|

- tail, last 10 lines

|Option|Description|
|------|-----------|
|-c _num_, --bytes=_num_ | display _num_ bytes|
|-n _num_, --lines=_num_| n of lines to display|
|-f , --follow | Track a file|
|--pid=_pid_ | tail to terminate tracking once the process ID terminate|

<font color="green">NOTE:</font> Extract line 11-15


```bash
nl -b t Linux_lessons_files/sort_me.txt| head -n 6 | tail -n 2
```

         5	one\n
         6	two\n


### Paging through Files with _less_ ###

- _less_ is more
- _less_ print file screen at a time
- **move forward screen at a time** **Space Bar**  
- **go backward**  

|Press|Followed By|
|------|-----------|
|**Esc**|**V**|

- **Search fowrward ** /"search me"

    
|Search|Followed By|
|------|-----------|
|forwared with search|n|
|Go backward|**N**|
 
- **Search backward** 

|Search backward|key|
|------|-----------|
||**?**|

- **Go to line 50**

|Press|Followed By|
|------|-----------|
|**G**|50|
 
 - Help of 
 
|Press|Followed By|
|------|-----------|
|**H**|Help of _less_|

<h3>File-Summarizing Commands</h3>
- _cut_  get part of the file and send to STDOUT
- _wc_ basic statistics of a file
<h4>Extracting Text with _cut_</h4>
- _list_ : 2, 2-4, open range -4 or 4-

|Option|Description|
|------|-----------|
|-b _list_, --bytes=_list_|list of bytes from the input file|
|-c _list_, --characters =_list_| Cuts specified list of characters from the input, _b and c same for same encoding_|
|-f _list_, --fields=_list_ | Cut the list of specified fields from the input file. _Default_  tab-delimeted field|
|-d  _char_, --delimiter=_char_ | _char_ is the character for delimit|
|-s, --only-delimited | do not print lines not containing delimiters.|


```bash
cat Linux_lessons_files/cut.txt
```

    cat command for file oriented operations.
    cp command for copy files or directories.
    ls command to list out files and directories with its attributes.


**1. Cut Characters**


```bash
cut -c 1 Linux_lessons_files/cut.txt; cut -c 2- Linux_lessons_files/cut.txt
```

    c
    c
    l
    at command for file oriented operations.
    p command for copy files or directories.
    s command to list out files and directories with its attributes.


**2. Cut bytes from the input**


```bash
cut -b 2- Linux_lessons_files/cut.txt
```

    at command for file oriented operations.
    p command for copy files or directories.
    s command to list out files and directories with its attributes.


**3. Cut Column from Delimited file**


```bash
cut -f 2 -d " " Linux_lessons_files/cut.txt
```

    command
    command
    command



```bash
cut -s -f 1 -d ":" /etc/passwd | head -n 2
```

    nobody
    root


<h4> Obtaining a Word Count with _wc_</h4>

|Option|Description|
|------|-----------|
|-l, --lines|New line characters in a doc|
|-w, --words|Words count|
|-c, --bytes|number of bytes|
|-m, --chars|Number of characters|
|-L, -max-line-length| maximum line length| 

<font color="green">NOTE:</font> For ordinary ASCII file -c and -m will give you the same output. But Multiple character encoding this will change


```bash
wc -l  Linux_lessons_files/cut.txt
```

           3 Linux_lessons_files/cut.txt


<h2>Using Regular Expressions</h2><a id="Using Regular Expressions">

<h3>Understanding Regular Expressions</h3>
- Basic Reg expression
- Extended

**Type Of Reg Expressions**
 - String - simplest regular expression.(Linux, HWaddr,"@")
 - Bracket Expressions -[] matches any <font color="red">_1 char in the bracket.</font> ex: b[aeiou]g , bag,beg,big,bug
 - Range Expression - Instead of listing every character that matches, range use start and end.a[2-4]z a2z,a3z,a4z
 - Any Single Character - ., a.z, a2z, abz, aQZ,
 - Start/End line - ^:Start $:End
 - Repetition Operators -how manytimes matching item must exist.
     -  \*  zero or more times.  Often use as  \.\* , e.g: A \.\*Lincoln 
     -  \\+ 1 or more times
     - ? Zero or 1 time
 - Multiple possible strings - \(\|\) e\.g: truck | car, will match to truck or car
 - Paraentheses 


```bash
echo "Abe Lincoln"  |  grep "A.*Lincoln" #repeat any single character (.) zero or moretimes
```

    Abe Lincoln



```bash
echo "ALincoln"  |  grep "A.\+Lincoln" #repeat any single character (.) one or moretimes.This doesnt work coz there is no characters between A and Lincoln
```

    


```bash
echo "Abe Lincoln"  |  grep "A.\+Lincoln" #repeat any single character (.) one or moretimes
```

    Abe Lincoln



```bash
grep "truck\|car" Linux_lessons_files/regex.txt
```

    this line has car
    this line has truck



```bash
grep "A.\+Lincoln" Linux_lessons_files/regex1.txt #Here ALincoln will be omitted
```

    This had Abe Lincoln


*Ex: Begining of line* *^*

The ^ matches the expression in the beginning of a line, only if it is the first character in a regular expression. ^N matches line beginning with N.


```bash
grep "^Apr" /var/log/system.log | head -n 5
```

    Apr 11 00:43:10 MacBook-Pro kernel[0]: AirParrot device perform power state change 1 -> 0
    Apr 11 00:43:10 MacBook-Pro kernel[0]: AppleThunderboltNHIType2::prePCIWake - power up complete - took 1 us
    Apr 11 00:43:10 MacBook-Pro kernel[0]: AppleThunderboltGenericHAL::earlyWake - complete - took 0 milliseconds
    Apr 11 00:43:10 MacBook-Pro kernel[0]: en0: BSSID changed to c0:3f:0e:9f:77:d6
    Apr 11 00:43:10 MacBook-Pro kernel[0]: en0: channel changed to 6


Ex 2. End of the line ( $)

Character $ matches the expression at the end of a line. The following command will help you to get all the lines which ends with the word “update”.


```bash
grep "update.$" /var/log/system.log
```

    Feb 23 01:53:04 MCIC-SEL17-D1 GoogleSoftwareUpdateAgent[90165]: 2016-02-23 01:53:04.493 GoogleSoftwareUpdateAgent[90165/0xb0219000] [lvl=2] -[KSAgentApp performSelfUpdateWithEngine:] This process may be killed if self-update is necessary. In such cases, sub-processes may still be running to complete the self-update.
    			url=https://tools.google.com/service/update2
    			</o:gupdate>
    			</gupdate>
    			url=https://tools.google.com/service/update2
    			</o:gupdate>
    			</gupdate>
    Feb 23 06:55:08 MCIC-SEL17-D1 GoogleSoftwareUpdateAgent[91137]: 2016-02-23 06:55:08.962 GoogleSoftwareUpdateAgent[91137/0xb0219000] [lvl=2] -[KSAgentApp performSelfUpdateWithEngine:] This process may be killed if self-update is necessary. In such cases, sub-processes may still be running to complete the self-update.
    			url=https://tools.google.com/service/update2
    			</o:gupdate>
    			</gupdate>
    			url=https://tools.google.com/service/update2
    			</o:gupdate>
    			</gupdate>


Ex 3. Count of empty lines ( ^$ )

Using ^ and \$ character you can find out the empty lines available in a file. “^$” specifies empty line.


```bash
grep -c "^$" /var/log/system.log
```

    0


Ex 4. Single Character (.)

The special meta-character “.” (dot) matches any character except the end of the line character. Let us take the input file which has the content as follows.


```bash
tee Linux_lessons_files/regex2.txt << EOF
1. first line
2. hi hello
3. hi zello how are you
4. cello
5. aello
6. eello
7. last line
EOF
```

    1. first line
    2. hi hello
    3. hi zello how are you
    4. cello
    5. aello
    6. eello
    7. last line



```bash
grep ".ello" Linux_lessons_files/regex2.txt
```

    2. hi hello
    3. hi zello how are you
    4. cello
    5. aello
    6. eello


In case if you want to search for a word which has only 4 character you can give grep -w “….” where single dot represents any single character.


```bash
grep -w  "...." Linux_lessons_files/regex2.txt
```

    7. last line


Ex 5. Zero or more occurrence (*)

The special character “\*” matches zero or more occurrence of the previous character. For example, the pattern ‘1*’ matches zero or more ‘1’.


```bash
grep "SecStaticCode: *." /var/log/system.log | head -n 2
```

    Apr 11 20:44:28 MacBook-Pro mdworker[591]: SecStaticCode: verification failed (trust result 5, error -2147409622)
    Apr 11 20:46:59 MacBook-Pro mdworker[590]: SecStaticCode: verification failed (trust result 5, error -2147409622)


In the above example it matches for SecStaticCode and colon symbol followed by any number of spaces/no space and “.” matches any single character.

Ex 6. One or more occurrence (\+)

The special character “\+” matches one or more occurrence of the previous character. ” \+” matches at least one or more space character.
If there is no space then it will not match. The character “+” comes under extended regular expression. So you have to escape when you want to use it with the grep command.


```bash
tee Linux_lessons_files/regex3.txt << EOF
hi hello
hi    hello how are you
hihello
EOF
```

    hi hello
    hi    hello how are you
    hihello



```bash
grep "hi \+hello" Linux_lessons_files/regex3.txt
```

    hi hello
    hi    hello how are you


In the above example, the grep pattern matches for the pattern ‘hi’, followed by one or more space character, followed by “hello”. If there is no space between hi and hello it wont match that. However, \* character matches zero or more occurrence.
“hihello” will be matched by \* as shown below.


```bash
grep "hi *hello" Linux_lessons_files/regex3.txt
```

    hi hello
    hi    hello how are you
    hihello


Ex7. Zero or one occurrence (\?)

The special character “?” matches zero or one occurrence of the previous character. “0?” matches single zero or nothing.


```bash
grep "hi \?hello" Linux_lessons_files/regex3.txt
```

    hi hello
    hihello


“hi \?hello” matches hi and hello with single space (hi hello) and no space (hihello).
**The line which has more than one space between hi and hello did not get matched in the above command.**

Ex8.Escaping the special character (\\)

If you want to search for special characters (for example: \* , dot) in the content you have to escape the special character in the regular expression.

<h3> Using sed</h3>

```bash

sed [options] -f script-file inputfile
sed [options] script-text inputfile

```

- *script-file* set of commands sed to perform
- *script-text* typically enclosed in single quote

|Command|Addresses|Meaning|
|------|-----------||
|=|0 or 1|Display the current line number |
|a\text|0 or 1|Append text to the file |
|i\text|0 or 1|Insert text into the file|
|r filename|0 or 1|Append text from filename into the file |
|c\text| Range|Replace the selected range of lines with the provided text  |
|s/regexp/replacement| Range| Replace text that matches the regular expression (regexp) with replacement |
|w filename| Range| Write the current pattern space to the specified file |
|q| 0 or 1| Immediately quit the script, but print the current pat- tern space  |
|Q| 0 or 1| Immediately quit the script  |

- *sed* commands operate on addresses *which are line numbers*

**Ex:**

```bash

sed 's/2012/2013/' cal-210.txt > cal-txt.txt
```

- This replaces first occuerance of '2012'.
- To replace all the occurences use 'g'.

**Ex:**

```bash

sed 's/2012/2013/g' cal-210.txt > cal-txt.txt
```





**Real World Scenario**

Dos to Unix

```bash
tr -d \\r < in_file.txt > unixfile.txt
```
Unix to Dos
```bash
sed 's/$/\r/' in_file.txt > unixfile.txt
```


```bash
echo "dig" | grep "d.ig"
```

    


```bash

```
