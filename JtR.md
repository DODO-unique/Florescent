Steps on how to do it:

1. add john: `sudo apt install john`
2. create a hash with: `echo -n "password" | openssl dgst -sha256`
3. The result will look like this: `sha256(stdin)= 3c9909afec25354d551dae215bb2652697bce1e0d33e5c707525389658dbf84e`. In this copy the hash and save it in a file
4. run john on the file as: `john -format=Raw-SHA256 file.txt`
5. You will see the cracked password in the output (highlighted by orange)