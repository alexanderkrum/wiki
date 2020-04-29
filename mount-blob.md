# Mount Blob Storage on a Azure 
>> only for Ubuntu. 
>> 
>> Prerequisite is to have Vm and ssh into it


1. Install Microsoft Linux packages 
   - [source](https://docs.microsoft.com/en-gb/windows-server/administration/Linux-Package-Repository-for-Microsoft-Software)
```bash
 curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
 sudo apt-add-repository https://packages.microsoft.com/ubuntu/16.04/prod
 sudo apt-get update
```

2. Install blobfuse package
   - [source](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-how-to-mount-container-linux)
```bash
sudo apt-get install blobfuse
```

3. Create fuse connection file
   ```bash
      vim fuse_connection.cfg
   ```
   with the access data
   ```text
      accountName myaccount
      accountKey storageaccesskey
      containerName mycontainer
   ```

   restrict access
   ```bash
      chmod 600 fuse_connection.cfg
   ```

4. Create local container to mount to
   ```bash
      mkdir ~/mycontainer
   ```

5. Mount the blob
   ```bash
   sudo blobfuse ~/mycontainer --tmp-path=/mnt/resource/blobfusetmp  --config-file=/path/to/fuse_connection.cfg -o attr_timeout=240 -o entry_timeout=240 -o negative_timeout=120 -o -o allow_other -o nonempty
   ```
   