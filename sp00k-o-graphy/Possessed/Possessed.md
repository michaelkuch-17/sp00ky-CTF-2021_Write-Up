# Possessed
###
##### In this challenge you are given a photo and told that there might be something hidden within.
##### Downloading the file, you have a couple of avenues of attack on this one.
___
### Route 1 - Strings

'''

'''
___
### Route 2 - Cat

___
### Using Grep with Strings/Cat
Using grep, we can have less garbage displayed when using strings and cat to look for the flag in this file.

```
cat halloweenParty2021.jpeg | grep -a "{.*}"
strings halloweenParty2021.jpeg | grep -a "{.*}"
```
<details>
  <summary>Flag:</summary>
  ```
  sp00ky{5c4ry_st3g0}
  ```
</details>
