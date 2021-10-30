In this challenge, using the same supplied iso from Haunted Files - 1, we are looking at a second hidden flag. The following was given as a challenge description.
```
Hey I also forgot to mention, I am missing a picture of the group from last years
exorcism festival. Please let me know if you can find it. I would really appreciate it.
```
From the description, we know we are looking for a picture/image of some sort. First we can look for any image files stored on the iso.
___
Recursively search for an image
```
grep -r 'JPG|JPEG|JFIF|PNG' segment0/
```
From this, we do not see any image files. We will need to look for another avenue of attack.
It seems that since there are not any image files found, that the image we are looking for is hidden as another file type.
___
Recursively looking at the file types of every file and seeing if the headers are an image filetype.
```
find . -type f | file -f - | grep 'JPG|JPEG|JFIF|PNG'
```
This command starts with finding all files from the current directory(in this case, segment0). It is looking for the file types of each file within the iso.
This will take a while, as there are a large number of files within the iso.
Ultimately, you see the following file: segment0/ASYDV6YPZO/O2Y42NINX.txt is actually a JPEG file. You can make a copy of the file and give it the appropriate file type or open with an image viewer, to see the found flag!
___
<details>
  <summary>Flag:</summary>
  sp00ky{p0lt3rg31$t}
</details>
The idea behind this challenge was to be able to look through a massive amount of files and folder to look for a specific bit of text.
