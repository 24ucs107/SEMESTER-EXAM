# SEMESTER-EXAM
hello im in git hub
# Linux Practical: Directory and File Management

The following Linux practical demonstrates all 8 tasks using terminal commands. Run the commands in order.

## 1\. Create a directory named `LINUX_PRACTICAL` with three subdirectories

bash
```
mkdir -p LINUX_PRACTICAL
cd LINUX_PRACTICAL

mkdir subdir1 subdir2 subdir3
```

## 2\. Create files in each subdirectory and display the directory structure

bash
```
touch subdir1/file1.txt subdir1/file2.txt
touch subdir2/file3.txt subdir2/file4.txt
touch subdir3/file5.txt subdir3/file6.txt
```

Add some sample text to the files:

bash
```
echo "Linux is an operating system" > subdir1/file1.txt
echo "Linux commands are useful" > subdir1/file2.txt
echo "Learning Linux practical" > subdir2/file3.txt
echo "Linux file management" > subdir2/file4.txt
echo "Operating system practical" > subdir3/file5.txt
echo "Linux is powerful" > subdir3/file6.txt
```

Display the directory structure:

bash
```
tree
```

If `tree` is not installed, use:

bash
```
find . -print
```

Expected structure:

text
```
LINUX_PRACTICAL/
├── subdir1/
│   ├── file1.txt
│   └── file2.txt
├── subdir2/
│   ├── file3.txt
│   └── file4.txt
└── subdir3/
    ├── file5.txt
    └── file6.txt
```

## 3\. Copy and move files between subdirectories

Copy a file from `subdir1` to `subdir2`:

bash
```
cp subdir1/file1.txt subdir2/
```

Move a file from `subdir2` to `subdir3`:

bash
```
mv subdir2/file3.txt subdir3/
```

Verify the changes:

bash
```
find . -type f
```

## 4\. Change permissions and ownership of selected files

Change the permissions of `file1.txt`:

bash
```
chmod 644 subdir1/file1.txt
```

Give the owner read, write, and execute permissions:

bash
```
chmod 700 subdir1/file2.txt
```

Display file permissions:

bash
```
ls -l subdir1/
```

Change the ownership of a file (requires the appropriate privileges):

bash
```
sudo chown username:groupname subdir1/file1.txt
```

Replace `username` and `groupname` with an actual user and group on your system.

Verify ownership:

bash
```
ls -l subdir1/file1.txt
```

## 5\. Create hard links and soft links and verify them

Create a hard link:

bash
```
ln subdir1/file1.txt subdir1/file1_hardlink.txt
```

Create a soft (symbolic) link:

bash
```
ln -s file1.txt subdir1/file1_softlink.txt
```

Verify the links:

bash
```
ls -li subdir1/
```

- A hard link shares the same inode number as the original file.
- A soft link has its own inode and points to the original file by path.

Check the symbolic link target:

bash
```
readlink subdir1/file1_softlink.txt
```

Expected output:

text
```
file1.txt
```

## 6\. Use `find` to locate all `.txt` files

Run this command from inside `LINUX_PRACTICAL`:

bash
```
find . -type f -name "*.txt"
```

This finds regular files ending in `.txt`, including the hard-linked filename. Symbolic links are not followed by this command by default.

## 7\. Use `grep` to search the files for a specified pattern

Search all `.txt` files for the word `Linux`:

bash
```
grep -n "Linux" $(find . -type f -name "*.txt")
```

- `grep` searches for the specified pattern.
- `-n` displays the matching line number.
- `$(find ...)` supplies the filenames found by `find`.

A safer alternative, especially when filenames contain spaces, is:

bash
```
find . -type f -name "*.txt" -exec grep -nH "Linux" {} +
```

## 8\. Use a pipeline to count the matching records

Count the number of lines containing `Linux` across all `.txt` files:

bash
```
find . -type f -name "*.txt" -exec grep -h "Linux" {} + | wc -l
```

Here:

- `find` locates the `.txt` files.
- `grep -h "Linux"` prints matching lines without filenames.
- `|` passes the output to the next command.
- `wc -l` counts the matching lines.

To count matching lines per file, use:

bash
```
find . -type f -name "*.txt" -exec grep -cH "Linux" {} +
```

## Result

You have completed the practical operations:

1. Created a main directory with three subdirectories.
2. Created files and displayed the directory structure.
3. Copied and moved files.
4. Changed file permissions and ownership.
5. Created and verified hard and soft links.
6. Located `.txt` files using `find`.
7. Searched for a pattern using `grep`.
8. Counted matching records using a pipeline.
