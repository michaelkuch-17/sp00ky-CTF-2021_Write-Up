### We are given a hash to crack.
### Here is the given information
```
Because the steaks are high!
Get cookin'! Here's your hash: 5c55d71b4c47d141072cf0540c046d07

flag format: sp00ky{cracked_hash_goes_here}
```
___
#### Running a hashid on the hash gives the following output.

```
$hashid -m "5c55d71b4c47d141072cf0540c046d07"
Analyzing '5c55d71b4c47d141072cf0540c046d07'
[+] MD2 
[+] MD5 [Hashcat Mode: 0]
[+] MD4 [Hashcat Mode: 900]
[+] Double MD5 [Hashcat Mode: 2600]
[+] LM [Hashcat Mode: 3000]
[+] RIPEMD-128 
[+] Haval-128 
[+] Tiger-128 
[+] Skein-256(128) 
[+] Skein-512(128) 
[+] Lotus Notes/Domino 5 [Hashcat Mode: 8600]
[+] Skype [Hashcat Mode: 23]
[+] Snefru-128 
[+] NTLM [Hashcat Mode: 1000]
[+] Domain Cached Credentials [Hashcat Mode: 1100]
[+] Domain Cached Credentials 2 [Hashcat Mode: 2100]
[+] DNSSEC(NSEC3) [Hashcat Mode: 8300]
[+] RAdmin v2.x [Hashcat Mode: 9900]

```
___
#### Seeing this, we have a couple of options to run. Running them in succession to hashcat, you can see the hash is an md5 hash.
#### We are able to run the appropriate commond into hashcat. (hash was stored in hashes.txt)
#### You will also need to choose a wordlist to crack the hash with, in this instance. rockyou.txt was chosen.
```
sudo hashcat -m 0 hashes.txt /usr/share/wordlists/rockyou.txt.gz 
```
#### Running this gets the following result, and the cracked hash!
```
Dictionary cache built:
* Filename..: /usr/share/wordlists/rockyou.txt.gz
* Passwords.: 14344392
* Bytes.....: 139921507
* Keyspace..: 14344385
* Runtime...: 3 secs

5c55d71b4c47d141072cf0540c046d07:blackcat        
                                                 
Session..........: hashcat
Status...........: Cracked
Hash.Name........: MD5
Hash.Target......: 5c55d71b4c47d141072cf0540c046d07
Time.Started.....: Mon Oct 18 13:04:45 2021 (1 sec)
Time.Estimated...: Mon Oct 18 13:04:46 2021 (0 secs)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt.gz)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:    36751 H/s (0.79ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests
Progress.........: 8192/14344385 (0.06%)
Rejected.........: 0/8192 (0.00%)
Restore.Point....: 0/14344385 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidates.#1....: 123456 -> whitetiger

```
___
<details>
  <summary>Flag:</summary>
  sp00ky{blackcat}
</details>
