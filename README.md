Command Line
=================


#### Showing the date

`$ date` => `Sun  9 Aug 2015 13:53:19 BST`


#### Listing files

`$ ls`

```
Applications  Documents Library   Music   Public
Desktop   Downloads Movies    Pictures  myFile
```

`$ ls -A` will list everything including invisible files

`$ ls -lA` will list everything including invisible files in long format (displays user permissions); shorthand for `$ ls -l -A`, combining multiple switches (or parameters) in one command (`-l` = *long format*; `-A` = *all files*)


#### Print working directory

`$ pwd` => `/Users/andygout/desktop`


#### Changing directory

`$ cd ..` => change to parents directory
`$ cd .` => change to current directory (i.e. do no change position)
`$ cd documents/projects/command-line` => change to most inner directory given by path
`$ cd ~` => change to home directory


#### Creating and destroying files

`$ touch newfile.rb` => creates this file in current directory

`$ rm newfile.rb` => removes this file (N.B. difficult to recover)


#### Creating and destroying directories

`$ mkdir newdirectory` => creates this directory in current directory

`$ rmdir newdirectory` => removes this directory (providing empty)

`$ rmdir -r newdirectory` => removes this directory and all files within it (`-r` switch = tells remove command to recursively remove all files within the directory as well as the directory itself)


#### Additional rm parameters

`$ rm -i` => `-i` switch = *interactive*; will prompt you to confirm that you want to delete each file (useful for when you have lot of files but only want to delete a few)

`$ rm -f` => `-f` switch = *force*; will remove any file even if 'write protected'


#### Copying files

`$ cp newfile filecopy` => two parameters required: file to be copied and name of the resultant duplicate


#### Moving files

`$ mv newfile ../newfile` => two parameters: file to be moved (and its location) and location to where file will be moved (in this case the parent directory); if second parameter has different name then file will be renamed:

`$ mv newfile filecopy` => will essentially rename the file


#### Viewing and writing files

`$ cat file1` => will display file's text; `cat` = *concatenate*

`$ cat > file1` => allows you to type text into a file but will delete all pre-existing text; end by hitting return then Ctrl-C

`$ cat file1 file2 > combined` => combines text of two files into new third file

`$ less longtext.txt` => displays a file with lots of text, allowing you to scroll up and down with keyboard to view entire document; quit by typing `q`

`$ head -3 longtext.txt` => displays first three lines only (with no parameter it will default to first ten lines, i.e. `head longtext.txt`)

`$ tail -3 longtext.text` => displays last three lines only

`$ tail -f log.text` => switch that allows you to watch last 10 messags of log (i.e. `tail -f /private/var/log/system.log`); Ctrl-C to stop tailing


#### Getting help

`$ man ls` => provides manual for *list* function


#### Pipes and redirection

KEYBOARD -> 1.stdin -> PROGRAMME -> 2.stdout -> DISPLAY

`$ cat combined.txt | less` => passes the output stream (what would normally be printed on the screen) of the command to left of pipe to the input stream of the command on the right; so here passing output of the file `combined.txt` into the `less` command

`$ ls -lA | less` => allows you (with thousands of files) to move up and down the resultant list as if the output were a normal file

`$ cat combined.txt > newcombined.txt` => writes the output stream of the command on the left to the file on the right


#### Advanced searches: ls

`$ ls *.txt` => list files in current directory that have a `.txt` suffix only

`$ ls new*.txt` => list files with text suffix that has filename starting with 'new'

`$ ls *` => list all files

`$ ls *n*` => list all files that include an 'n' (with characters on either side)


#### Advanced searches: find

`$ find . -name "*.txt" -print` => another way to list specific files, and will also search all subdirectories rather than just current one

`$ cd ~`, then `find . -name "*.txt" -print` => will print every text file in home directory

`$ cd ~`; then `find . -name *.mp3 -print > myMusic.text` => creates a text document that lists every mp3 file in Music directory


#### Advanced searches: grep

`$ grep binary *.txt` => takes two parameters: first is search term (i.e. 'binary'; actually a regex); second is which files to search the content of for this term

`$ find ~ -name "*.txt" -print | grep README` => prints all text files in home directory that have 'readme' in their name: first command will find all matching files but instead of printing will redirect to grep which will only print those filenames that include 'readme'

`$ find ~ -name "*" -print | grep "\d+"` => looks for all files that have numbers in the filename


#### Counting lines, words and characters

`$ wc longtext.txt` => `8     492    3003 longtext.txt`; `wc` = *word count*: line, word and character count for given file

`$ wc -l longtext.txt` => `8 longtext.txt` (lines only)

`$ wc -w longtext.txt` => `492 longtext.txt` (words only)

`$ wc -c longtext.txt` => `3003 longtext.txt` (characters only)

`$ find ~ -name "*.txt" -print | grep README | wc -l` => finds all text files; grep selects those that have 'readme' in their filename; `wc -l` will count how many lines were given to it by grep


#### Permissions

`$ whoami` => `andygout`

Every file on a unix-based system has three classes of permissions:

**User** - determines permisions that owner of the file has; every file has a user (no more than one) as an owner

**Group** - determines permissions that owner of the file has; any user can belong to one or more groups of users (but doesn't have to).

**Others** - all users that fall into neither of above two groups

Every class has three permissions:

**Read** - allows a file to be read; or if a directory allows list of files to be read (reading the included files will depend on their individual read permission settings as permission are not inherited)

**Write** - allows you to write to a file; or if a directory allows files to be created, deleted and renamed

**Execute** - allows you to execute a file; such permission may be required to run a programme

`$ ls l` => displays directory contents in *long* format, with permissions on right in this format: `drwxr-xr-x`

First letter [d]: type of file (`d` = directory; `-` = file)

Next three characters [rwx]: read, write and execute permissions of 'user' class

Next three characters [r-x]: read, write and execute permissions of 'group' class

Next three characters [r-x]: read, write and execute permissions of 'other' class


#### Changing permissions

`$ chmod u+w readme.txt` => *change mode*; `u` = user (`g` = group; `o` = others; `a` = all); `+` = adding permission (`-` = removing permission); `w` = write (`r` = read; `x` = execute)

`$ chmod a-rx readme.txt` => removes read and execute permissions from all users


#### Shebang

Shebang is the instruction for your computer that tells what program to use to execute your script. It is a combination of a hash and an exclamation mark followed by the path to the interpreter, placed on the very first line of the file

`$ cat hello.rb`; then `puts "Hello, world!"`

To tell file where your current version of Ruby is located, add a shebang to first line of file to tell command line to use this ruby interpreter to execute the file:

`#!/Users/andygout/.rvm/rubies/ruby-2.0.0-p0/bin/ruby`

`$ ./hello.rb` => `Hello, world!`

Amend shebang path to work on other computers:

`#!/usr/bin/env ruby`


#### Superuser mode

Name of the superuser is 'root'; use only as necessary as **can cause significant damage to the system**

`$ sudo rm inaccessiblefile` => *superuser do*; asks for your password and command will then execute with superuser priveleges (despite you not having priveleges to do so)

[Can be used to make sandwiches](http://xkcd.com/149/)


#### Environment / Environment variables

`$ env` => lists current environment variables

`$ echo $HOME` => `/Users/andygout` (displays a specified environment variable)

`$ export SECRET_KEY=12345abcde` => can then be acquired in Ruby code using `secret_key = ENV['SECRET_KEY']`

`$ export SEASON=winter` => creates new environment variable called SEASON

`$ echo $SEASON` => `winter`; reads back value of specified environment variable

*However*, in a new terminal window the environment variable will no longer exist; they must be saved to `.bash_profile`, one of the files executed automatically on load:

`echo "export SEASON=winter" >> ~/.bash_profile`


#### Echo

`$ echo "Hello"` => `Hello`; text is printed to the screen

`$ echo "Hello, world" > hello.txt` => will save short strings to a file (overwriting file's current contents)

`$ echo "Hello again" >> hello.txt` => will save short strings to a file (appending to file's current contents)

#### Processes

`$ ps` => see what processes have been launched (within context of terminal)

`$ ps x` => see all processes runnign on your computer

`$ ps x | grep bash` => only show bash processes running on the system


#### vim

`vi myfile` => create new file or open existing file (using name as an argument)

`i` => enter 'insert' mode to insert text before cursor

`o` => open a new line after the current one

`dd` => delete current line and dozesn of others

`ESC` => move back to command mode

`:w` => tell vi to save the file (`w` = write); then after pressing 'Enter' the file will be written and you'll see the corresponding message

`:q` => quit the editor

`:q!` => quit the editor without saving changes


Links:
-------

[Makers Academy: Pre-course - Command Line](https://github.com/makersacademy/pre_course/blob/master/pills/command_line.md)

[Vi cheat sheet](http://www.lagmonster.org/docs/vi.html)

[Advanced vi cheat sheet](http://www.lagmonster.org/docs/vi2.html)

[Vim talk with Spike](https://www.youtube.com/watch?v=RWRzxQfXfEc&list=WL&index=11) (video)