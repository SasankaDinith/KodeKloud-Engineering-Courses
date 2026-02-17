## Task02: Linux String Substitute (sed)

There is some data on `Nautilus App Server 1` in `Stratos DC`. Data needs to be altered in several of the files. On `Nautilus App Server 1`, alter the `/home/BSD.txt` file as per details given below:


- Delete all lines containing word `following` and save results in `/home/BSD_DELETE.txt` file. (Please be aware of case sensitivity)

- Replace all occurrence of word `or` to `their` and save results in `/home/BSD_REPLACE.txt` file.

`Note:` Let's say you are asked to replace word `to` with `from`. In that case, make sure not to alter any words containing the string itself; for example upto, contributor etc.

---

## Answer:

Step01: Login to the App server 02 as root
``` bash
ssh steve@stapp02

sudo su
```

Step02: Switch to /home folder 
``` bash
cd /home
```
Step03: Open the BSD.txt file as vi editor
``` bash
vi BSD.txt
```

Step03: Delete all lines containing word `following` and save results in `/home/BSD_DELETE.txt` file.
``` bash
Use / operator to find that word `following`, then you can easily delete that word containing line

To save file with new name -> type `:w BSD_DELETE.txt` then press Enter
```
Step04: Replace all occurrence of word `or` to `their` and save results in `/home/BSD_REPLACE.txt` file.
``` bash
Use / operator to find that word `or`, then you can easily replace that word to `their`

To save file with new name -> type `:w BSD_REPLACE.txt` then press Enter
```

### Task is Completed!

