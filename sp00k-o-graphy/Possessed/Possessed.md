# Possessed
###
##### In this challenge you are given a photo and told that there might be something hidden within.
##### Downloading the file, you have a couple of avenues of attack on this one.
___
### Route 1 - Strings
With strings, we are able to find text within the file, in hopes of an easy find for this flag
```
strings halloweenParty2021.jpeg
```
Which we do! Getting the following output:


___
### Route 2 - Cat
With cat, we are able to view the contents of the file, in hopes of an easy find for this flag.
```
cat halloweenParty2021.jpeg
```
We do once again, getting the following output(a nice an ugly way of finding the flag):

___
### Using Grep with Strings/Cat
Using grep, we can have less garbage displayed when using strings and cat to look for the flag in this file.

```
cat halloweenParty2021.jpeg | grep -a "{.*}"
strings halloweenParty2021.jpeg | grep -a "{.*}"
```
<details>
  <summary>Flag:</summary>
  sp00ky{5c4ry_st3g0}
</details>
