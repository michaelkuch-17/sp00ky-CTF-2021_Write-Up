## Known Information
### Disclaimer! Unintended Solution Found - proper solution tbf
##### username: user666
##### password: sp00kysandbox
---
##### First step was to ssh into the shell and find the usable commands.
```
ssh user666@spookyctf.net -p(given port)
```
##### On password prompt, enter given password
---
##### On entering the shell, many commands are unavailable or are disabled by the administrator. Common commands such as ls, cat, vi, vim, etc. are not usable.
##### Within the /home/user666 directory, through alternative commands we are able to find any files/directorys are available.
```
$ echo *
```
##### This shows that flag.txt is stored here. We now have our objective in scope, view the contents of flag.txt to secure the flag!
---
##### From here, we want to be able to read to contents of the flag file. Since we are not able to cat, 
##### The short answer to this is that the flag was found accidentally. Running, `$ source flag.txt`, you are able to read out the contents of the flag.txt file.
##### For reference to why this works, check out the source man page here, [Source man page](https://linuxcommand.org/lc3_man_pages/sourceh.html)
<details>
  <summary>Flag:</summary>
  sp00ky{https://youtu.be/esYeUeiG_n8}
</details>
