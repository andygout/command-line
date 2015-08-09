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

`$ ls -a` will list everything including invisible files

`$ ls -la` will list everything including invisible files in long format (displays user permissions); shorthand for `ls -l -a`, combining multiple switches (or parameters) in one command (`-l` = *long format*; `-a` = *all files*)


#### Print working directory

`$ pwd` => `/Users/andygout/desktop`


#### Changing directory

`cd ..` => change to parents directory
`cd .` => change to current directory (i.e. do no change position)
`cd documents/projects/command-line` => change to most inner directory given by path
`cd ~` => change to home directory


#### Creating and destroying files

`touch newfile.rb` => creates this file in current directory

`rm newfile.rb` => removes this file (N.B. difficult to recover)


#### Creating and destroying directories

`mkdir newdirectory` => creates this directory in current directory

`rmdir newdirectory` => removes this directory (providing empty)

`rmdir -r newdirectory` => removes this directory and all files within it (`-r` switch = tells remove command to recursively remove all files within the directory as well as the directory itself)


#### Additional rm parameters

`rm -i` => `-i` switch = *interactive*; will prompt you to confirm that you want to delete each file (useful for when you have lot of files but only want to delete a few)

`rm -f` => `-f` switch = *force*; will remove any file even if 'write protected'