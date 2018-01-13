# Data Transfer

## Upload and download files between local computer and cloud storage
### Upload
1. Create a storage account and a file share: [https://docs.microsoft.com/en-us/azure/storage/common/storage-quickstart-create-storage-account-cli?toc=%2fazure%2fstorage%2fblobs%2ftoc.json](https://docs.microsoft.com/en-us/azure/storage/common/storage-quickstart-create-storage-account-cli?toc=%2fazure%2fstorage%2fblobs%2ftoc.json). You can also do it using GUI:
    * Menu - Resource groups, create a new resource group    
    ![Click Resource groups](https://github.com/jinangela/azure-notes/blob/master/Snip20171228_5.png)    
    ![Create a new resource group](https://github.com/jinangela/azure-notes/blob/master/Snip20171228_6.png)
    * Menu - Storage accounts, add a new storage account under the resource group you just created    
    ![Click Storage accounts](https://github.com/jinangela/azure-notes/blob/master/Snip20171228_1.png)    
    ![Add a new storage account](https://github.com/jinangela/azure-notes/blob/master/Snip20171228_3.png)    
    ![Under your resource group](https://github.com/jinangela/azure-notes/blob/master/Snip20171228_7.png)
2. Go to your storage account, click Files under FILE SERVICE, add a new file share    
![Click Files](https://github.com/jinangela/azure-notes/blob/master/Snip20171228_8.png)    
3. Click your file share, click Upload    
![Upload](https://github.com/jinangela/azure-notes/blob/master/Snip20171228_10.png)    

Alternatively, you can use CLI tool `blobxfer`: [https://github.com/Azure/blobxfer/blob/master/docs/10-cli-usage.md](https://github.com/Azure/blobxfer/blob/master/docs/10-cli-usage.md)    
In your local command line(iTerm), type in something like this: `blobxfer upload --mode file --storage-account YOUR-STORAGE-ACCOUNT --sas "YOUR-KEY" --remote-path YOUR-FILE-SHARE --local-path /path/to/file --file-md5 --file-attributes --exclude '*.bak'`. You need to fill in `YOUR-STORAGE-ACCOUNT`, `YOUR-KEY`, `YOUR-FILE-SHARE` and `/path/to/file` here.

### Download
You can simply click **download** in the options.
![Download](https://github.com/jinangela/azure-notes/blob/master/Snip20171228_11.png)

## File transfer between cloud storage file share and virtual machine
### Use AzCopy to physically transfer data
1. SSH into your VM: first create ssh keys ([https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys)), then in cloud shell, type `ssh username@public_ip_address`(replace username and public_ip_address with your own).    
2. Transfer data with AzCopy: [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-linux?toc=%2fazure%2fstorage%2ffiles%2ftoc.json](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-linux?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).     
   * Please use corresponding commands when you install .NET core on different versions of Ubuntu systems.    
   * You can find your own key at Storage accounts -> SETTINGS -> Access keys.
   * In `--destination`, you should replace `/mnt` with `/home/username`.
### Use mount to operate remotely
Detailed documentation: [https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-linux](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-linux)    
Note: If you create new folders under mymountpoint/, you will see warnings like `fchmod (file attributes) error: Operation not permitted
 (warning) cannot set modif./access times    Operation not permitted`. Not sure why this happens, but you can still perform the operations.
