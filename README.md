# Watch-Local-Folder-and-Sync-Changes-With-GitHub tested on Fedora 33

1. Publish a single file for linux in .NET5:
   ```
   dotnet publish -c Release -o publish -r linux-x64 /p:PublishSingleFile=true --self-contained true -p:IncludeNativeLibrariesForSelfExtract=true
   ```
    
2. Copy the executable "FOLDER_GIT_PUSH" from "publish" folder to your destination folder for file monitoring.

3. Provide permissions to the executable:
   ```
   sudo chmod +x FOLDER_GIT_PUSH
   ```
   
4. Install git in Fedora 33:
    ```
    sudo dnf -y install git
    ```
5. Clone your repo from GitHub.
   ```
   git clone URL
   ```
6. Cash GitHub cedentials :
   ```
   git config --global credential.helper store
   git config --global credential.helper cache
   ```
7. Create a Git Ignore file and ignore the following:
   ```
   *.sh
   FOLDER_GIT_PUSH
   appsettings.json
   ```
7. Create a bash script in the destination folder for file monitoring (git.sh) with the following lines:
   ```
   #!/bin/sh
   git add -A
   git commit -am "File Changed"
   git push origin main --force
   ```
 9. Create the config file "appsettings.json" example:
    ```
    {
       "FolderToWatcher": "/home/dev/www/",
       "FilterForFileExtension": "html"
    }
    ```
     
10. Run the Application from inside the destination folder for file monitoring. 
    ```
    ./FOLDER_GIT_PUSH
    ```
