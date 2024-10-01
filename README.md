# Jenkins-Backup

Under the Jenkins Backup heading I am explaining two backups 
1. ThinBackup
2. Periodic Backup

### 1. ThinBackup

I have installed the jenkins plugin for ThinBackup as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/b6661e89-92da-4eb5-ae8d-04ad19793036)

Created backup direcitory and changed the owner and group for the directory as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/6cfb42b3-839b-4e83-a9df-b1c146f85e86)
![image](https://github.com/user-attachments/assets/f0352b3b-f1bf-428e-aa89-39f014735306)
![image](https://github.com/user-attachments/assets/634c9692-be00-46a8-be89-d1b5c932a24f)

Go to **Manage Jenkins** > **System**. Then go to ThinBackup Configuration as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/e1d62758-2a97-4248-ae7e-a43000d559ba)
![image](https://github.com/user-attachments/assets/bd3e82cc-c857-4c81-8247-cfac9d55e5b2)

In backup schedule for Full and differential backup cron job I used 9:10 AM UTC daily for backup. For the first time if no Full backup present then it will create it and from the next time onwards it will create the differential backup. In configuration I checked the option for **cleanup differential backups** and **Move old backups to zip files.** Which denotes the differential backup is removed and it will be removed before zipping happens when hence zip files contain no differential backup.

For **Max number of backup sets** I used the value 30 which means for one month I keep the backup and whenever a new backup will be generated the oldest one will be discarded.

The screenshot for backup directory before and after running the cronjob for ThinBackup is as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/8a4a3627-a9a5-4908-9ea7-83b9f7c73f66)
![image](https://github.com/user-attachments/assets/233573cf-6931-4ed8-8daa-5ca755dedeb1)

At present I have one Jenkins Job with the name of test-1 I will delete this Jenkins Job and restore from ThinBackup. **After restoring from ThinBackup restart the Jenkins.** Then you will find the deleted Jenkins Job.

![image](https://github.com/user-attachments/assets/7d7987ea-7bb4-4a92-a6fc-db2bdb1f919b)

Now I delete the test-1 Jenkins Job as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/81edf709-b52e-45c1-b693-e937383cf314)

Go to **Manage Jenkins** > **ThinBackup** then click on Restore option as shown in the screenshot attached below. Restore from the available Backup option as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/594aa3f2-beed-4318-a8d3-e49abe319227)

After the Restore I am unable to see the deleted Jenkins Job for that I restarted the Jenkins as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/19f1e9ec-2e62-4ed1-8f0f-f74ac8554835)

Restart the Jenkins

![image](https://github.com/user-attachments/assets/606e29aa-677d-43ba-a121-a2f54a668b2f)

![image](https://github.com/user-attachments/assets/7a0e54ba-41cc-40a2-8141-1643825453bd)

Same number of Builds are also present as it was earlier.

![image](https://github.com/user-attachments/assets/93aa587e-9068-41d2-860f-75c8e492d505)
