# Text editor: vi (vim) and nano

* Nano: easy to use; control short-curs are displayed on the screen;
* not so effective and fast; prefered by new comers.
```
# nano filenmae
```
* Vi (vim): Most powerful text editor; fastest text editor;
* tutorials require to use vi; most used editor on linux
```
# vi filename
```
* Mode
* |--execute (perform operations) * default mode (typing not allowed)
* |--insert (typing)

* Options
*  i                    -->  enter into insert mode
*  esc                  -->  enter into execution mode
*  esc:w                -->  write changes
*  esc:w /apple.txt     -->  write changes with file name
*  esc:wq               -->  write changes and quit the file
*  esc:wq /apple.txt    -->  write changes with file name
*  esc:q                -->  quit the file
*  esc:q!               -->  quit without saving changes
*  yy                   -->  to copy current line
*  p                    -->  to paste copied line below current line
*  10yy                 -->  copy 10 lines
*  dd                   -->  delete current lines
*  10dd                 -->  delete 10 lines
*  o                    -->  open a new line below current line
*  shfit + o            -->  open a new line above current line
*  u                    -->  undo changes
*  esc:81               -->  go to line 81
*  esc:$                -->  see line numbers
*  esc:set nu           -->  set line numbers
*  esc:set nonu         -->  hide line numbers
*  esc:/word            -->  jump to the number containing word/phrase

## diff commnad
* The diff command in Unix/Linux is used to compare two file line  by line display the differences between them.
* It provide insight into what has changes, been added, or been remove in text files.
```
# diff file1.txt file2.txt (compare two file)
# diff -y file1.txt file2.txt (show differences side-by-side)
# diff --suppress-common-lines -y file1.txt file2.txt (suppress common lines)
# diff -q file1.txt file2.txt  (output only whether files differ)
```

## 'patch' command
* The patch command reads a patch file (output of diff -u ) and  applies the differences to the original file(s), updating them as specified.
```
# diff -u original_file modified_file > changes.patch (using diff, create a unified diff file)
# patch original_file < changes.patch (to apply the patch to the original file)
# patch -R original_file < changes.patch (to undo a patch that was applied)
```

## sed commond
* sed --> Print the modified version of a file
* sed -i --> save modification in the file

```
# cat linux.txt
# sed s/unix/linux/ /linux.txt
# sed s/unix/linux/2 /linux.txt
# sed s/unix/linux/g /linux.txt
# cat linux.txt
# sed '3a This is a new line' /linux.txt
# sed '3i This is a new line' /linux.txt
# cat linux.txt
# sed -i 's/unix/linux/g;3d;$a This is new line' linux.txt
# cat linux.txt
```

## awk file programming
* The awk command is a powerful text processing tool commonly used in Unix/Linux environment for pattern scanning and processing.
* It processes text line-by-line and applies operations baesd on patterns and actions defined by the user.
* The default delimiter for awk is a space
```
# awk '{print}' filename (to print entire file)
# awk '{print $2}' filename {to print specific field like cut command}
# awk '/pattern/{print}' filename {to print lines containing pattern word.}
# awk '$3>50{print}' filename (to print lines with conditions. print lines whether value in the third column is greater than 50)
# awk -f "," '{print $1,$2}' filename (To specify a delimiter)
# awk '{print NR,$0}' filename (To print file with line number)
```
