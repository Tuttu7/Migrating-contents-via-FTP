#### We can use the following command to migrate website contents from a remote server via FTP. Details needed - FTP hostname, FTP username & password of the account in remote server.

```
wget -m --user="username" --password='Password' ftp://serverIP/*
```


Alternate command 

```
wget -m -N --header='Accept-Encoding: gzip' --ftp-user=user --ftp-password='password' -nH -P /home/user/public_html ftp://serverIP:/
```


```
-m - Turn on options suitable for mirroring. This option turns on recursion and time-stamping, sets infinite recursion depth and keeps FTP directory listings. 


'Accept-Encoding: gzip' - To send gzip encoding request so the download time of the files 


-N - Turn on time-stamping.


-nc - When running Wget without ‘-N’, ‘-nc’, ‘-r’, or ‘-p’, downloading the same file in the same directory will result in the original copy of file being preserved and the second copy being named ‘file.1’. If that file is downloaded yet again, the third copy will be named ‘file.2’, and so on.When ‘-nc’ is specified, this behavior is suppressed, and Wget will refuse to download newer copies of ‘file’. 
 

--header - Send header-line along with the rest of the headers in each HTTP request. The supplied header is sent as-is, which means it must contain name and value separated by colon, and must not contain newlines. 
    

-P -  Set directory prefix to prefix. The directory prefix is the directory where all other files and subdirectories will be saved to, i.e. the top of the retrieval tree. The default is . (the current directory). 

 
-H - Enable spanning across hosts when doing recursive retrieving. 

Additional options 

-q - Turn off wget's output

--show-progress - Force wget to display the progress bar no matter what its verbosity level is set to.

```


One of the most important aspects of mirroring information from the Internet is updating your archives.

Downloading the whole archive again and again, just to replace a few changed files is expensive, both in terms of wasted bandwidth and money, and the time to do the update. This is why all the mirroring tools offer the option of incremental updating.

Such an updating mechanism means that the remote server is scanned in search of new files. Only those new files will be downloaded in the place of the old ones.

A file is considered new if one of these two conditions are met:

    A file of that name does not already exist locally.
    A file of that name does exist, but the remote file was modified more recently than the local file. 

To implement this, the program needs to be aware of the time of last modification of both local and remote files. We call this information the time-stamp of a file.

The time-stamping in GNU Wget is turned on using ‘--timestamping’ (‘-N’) option, or through timestamping = on directive in .wgetrc. With this option, for each file it intends to download, Wget will check whether a local file of the same name exists. If it does, and the remote file is not newer, Wget will not download it.

If the local file does not exist, or the sizes of the files do not match, Wget will download the remote file no matter what the time-stamps say. 


