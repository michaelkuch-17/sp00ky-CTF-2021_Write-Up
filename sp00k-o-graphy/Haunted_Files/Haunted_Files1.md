In this challenge, you are given an iso filled with files and folders. The following was given as a challenge description.
```
Hey, I just got back from the weekly exorcism and I have a problem. My hard drive seems to have taken a beating
from whatever spawn of satan we sent back this week.
I'm looking for the password that I saved in a text file. Let me know if you can find it.
```
From this we are able to assume the challenge flag was stored somewhere in the iso. Most likely in text, it would be trivial to look through each file for the flag.
With each file/folder being named in what seems a random fashion, we will need to look through each file for the flag.
We need to be able to recursively look through each file to try and search for the flag, if this does not work, we will need to look for another avenue of attack.
___
Recursively search for flag header
```
grep -r sp00ky segment0/
```
From this, we see that within the file located at: segment0/LIM6TZDTK/AC1Y8V/BFZZL.txt, the flag header is found using grep. You are able to see the flag in plain text.
___
<details>
  <summary>Flag:</summary>
  sp00ky{ph4n70m}
</details>
The idea behind this challenge was to be able to look through a massive amount of files and folder to look for a specific bit of text.
