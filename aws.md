# Remote Jupyter Notebook via SSH on aws EC2 with VSCODE

1. Install the Remote-SSH extension on VSCode.
2. On the botton left corner click the ![image](https://github.com/JohnRomanelis/Quick-Cheat-Sheets/assets/48806065/20eede30-d4ca-4cdf-90aa-ec1f2e3c7edd) icon.
3. On the pop up menu select `Connect to Host...`
4. Select `Configure SSH Hosts...`
5. Then select the first option that should be something like `/home/usr/.ssh/config`
6. Edit the config file to be as the following:
 ```# Read more about SSH config files: https://linux.die.net/man/5/ssh_config
    Host {remote_pc_ip}
    HostName {remote_pc_ip}
    IdentityFile {path_to_key_pair.pem}
    User ubuntu
```
7. Save the file.
8. Follow steps 1-3 and then after pressing the `Connect to Hosts...` option you should the IP of the remote machine. Click on it.
9. A new visual studio window should open that is connected to the remote device.
10. Navigate to the desired path and activate the conda environment that has jupyter lab installed.
11. Run:  
```jupyter lab --no-browser --ip=0.0.0.0 --port=9000```
12. VSCode should create a pop up window that says that it has detected the jupyter notebook and gives you the option to open it on a browser. Click this option.
13. Go back to the terminal on the remote machine that is running jupyter lab and copy the token from the connection URLS. It is among the first messages that are displayed on the terminal after you run jupyter lab.
14. Past the token on the browser page that VSCODE opened before. (If page is blank you need to refresh it)

Otherwise:
12. If no pop-up appears open a terminal, on the local machine, navigate to the directory that contains the key-pair.pem file. 
13. Run `ssh -NL 1234:localhost:9000 remote_user@ip key-pair.pem`
14. Go on a browser and go to: http://localhost:1234/

In command 13 and 14:
- 1234: port to use on local device
- 9000: port to use on remote device

# Uploading/Downloading Data to/from S3
1. Create an IAM user and an ACCESS KEY.
2. On the EC2 instance connect to the aws cli. 
   ```aws configure```
3. Use the AWS CLI sync command to sync files:
   - To sync from EC2 to S3:
     ```aws s3 sync /path/to/local/directory s3://your-bucket-name```
   - To sync from S3 to EC2:
     ```aws s3 sync s3://your-bucket-name /path/to/local/directory```
