They key to solving this challange was to determine what mask to use in john for cracking the 3 hashes found in the masks.txt file. John should autodetect the hashing algorithm.
`john --mask'?l?l?d?d?u?u?s' masks.txt`
The time taken to crack will go down significantley as each hash is cracked because each hash is salted meaning that hashes need to be calculated 3 times for each plaintext until one is racked.
