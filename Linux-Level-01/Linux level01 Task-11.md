# Task 11 - String Replacement

Within the Stratos DC, the backup server holds template XML files crucial for the Nautilus application. Before utilization, 
these files require valid data insertion. As part of routine maintenance, system admins at xFusionCorp Industries employ string and file manipulation commands. <br/><br/>



- Your task is to substitute `all occurrences` of the string `Sample` with `LUSV` within the XML file located at `/root/nautilus.xml` on the backup server.

 ---

# Answer : 

In this task you need to replace all Sample strings into LUSV string, You can use the sed command done this task 

``` bash
# Step 01 - Login to the backup server
ssh clint@stbkp01

# Step 02 - replace all occurrences of the string Sample with LUSV in the file /root/nautilus.xml
sudo sed -i 's/Sample/LUSV/g' /root/nautilus.xml
```

 Explanation: <br/>
- `sed` : Stream editor for filtering and transforming text.
- `-i` : Edits the file in-place.
- `'s/Sample/LUSV/g'`: Substitutes all (g for global) instances of Sample with LUSV.


To confirm the changes : 
```
grep 'LUSV' /root/nautilus.xml
```






