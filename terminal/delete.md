# The remove command
The rm command is used to delete files and directories in Unix/Linux systems. The basic usage is the next one:

```bash
rm file.txt                    # Delete a file
rm -r directory/               # Delete a directory recursively
rm -f file.txt                 # Force delete without confirmation
rm -i file.txt                 # Interactive mode (asks for confirmation)
```

for example:

```bash
rm -i *.pdf
rm: delete regular file 'file1.pdf'? (y/n) y
rm: delete regular file 'file2.pdf'? (y/n) n
rm: delete regular file 'file3.pdf'? (y/n) y
```

 :warning: Deleted files cannot be easily recovered.


## The find command

We can use the **find** command in combination with **rm** to delete files matching specific criteria. This is powerful but dangerous.

### Delete empty directories

```bash
find . -type d -empty -delete
```

we can preview what will be deleted first

```bash
find . -type d -empty -print
./logs/old_runs
./assets/temp_icons
./tests/unit/mocks
./empty_folder
```

### Remove except

Find command can be very handy when you want to delete all files in directory, except one:

```bash
find . -mindepth 1 -not -name 'keepme.txt' -exec rm -rf {} +
```

This command searches for all files and directories in the current directory (and all subdirectories), excluding the current directory (mindepth 1) itself and any file named keepme.txt, and deletes them.

Or if we want to exclude multiple files:

```bash
find . -mindepth 1 not  \( -name '*.txt' -o -name '*.md' \) -print
```

We can ignore the n children directories using the flag **mindepth n**. For example, supose we have this directory:

```bash
├── test1
│   ├── test1a
│   └── test1b
│       ├── test1b.md
│       └── test1b.txt
├── test2
│   ├── test2.txt
│   └── text2.md
├── test.md
└── test.txt
```

We want to delete all files that end with .md and .txt, but only those that are not in the current directory and the first and second children directories, i.e, we only want to delete test1b.md and test1b.txt, we can do this by using the following command:

```bash
find . -mindepth 3  \( -name '*.txt' -o -name '*.md' \) -print
./test1/test1b/test1b.txt
./test1/test1b/test1b.md
```
We use mindepth 3 because files also count as directories in some sense:

1.  test1/ (Depth 1)
2. test1b/ (Depth 2)
3. test1b.txt (Depth 3)

```bash
find . -mindepth 3  \( -name '*.txt' -o -name '*.md' \) -exec rm -rf {} +
```
