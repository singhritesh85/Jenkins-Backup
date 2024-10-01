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

### 2. Periodic Backup

For periodic backup, installation of Jenkins plugin Periodic Backup has been done as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/39c49c0c-6676-419b-a1fb-cb1fe28b34d6)

**Backup Location**
(a) Amazon S3

(b) LocalDirectory

**(a) Amazon S3**

create a temporary directory and change its ownership as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/236687cd-4f82-4675-839e-d393d792e15d)

Create an Amazon S3 Bucket as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/a6d14832-2c40-4498-9261-ea57f7090b1a)

Create a An IAM User with Access Key and Secret Key which has sufficient privileges to access S3 bucket.

Do the configuration for Periodic backup with backup location as Amazon S3 as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/c55103d2-6801-434e-99fe-d3e4eaf524f3)
![image](https://github.com/user-attachments/assets/b2495542-9b2f-41e1-9de6-c25d08324419)
![image](https://github.com/user-attachments/assets/84c3c881-ea8e-43b2-b94b-0b9599865806)
![image](https://github.com/user-attachments/assets/42071511-67a1-4138-aa89-6e0053a388ee)

Backup is scheduled at 11:00 AM UTC daily as shown in the screenshot attached below. Daily one backup and total 30 backups will be stored, backup older than 30 days will be discarded.

After the cron job run as per the scheduled time as shown in the screenshot attached above the backup will be availabe in the S3 bucket as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/e04c0f49-cb11-4d6d-869a-84eecb3e9fd8)
![image](https://github.com/user-attachments/assets/4b310dbc-73a1-44d0-93e6-5e73adefc268)

Before taking the backup there was a jenkins job with the name of test-1 was present but after backup I deleted the test-1 jenkins job as shown in the below screenshots.

![image](https://github.com/user-attachments/assets/a7eb1719-f4c1-4f49-b9de-f87eec5f31e5)
![image](https://github.com/user-attachments/assets/33c2fef7-df72-4fff-bbd8-08cbb767a454)

Now for Restoration of backup follow the steps as written below.

![image](https://github.com/user-attachments/assets/5a6a1d9a-dcf1-4937-b6bd-881dac4bd634)
![image](https://github.com/user-attachments/assets/e96674d9-4965-431c-acae-e3c3e14e54e2)
![image](https://github.com/user-attachments/assets/b7538228-4b6a-40a4-bea4-ce7795e828d6)
![image](https://github.com/user-attachments/assets/ce0fd74d-2386-4177-8a47-a09c7218e527)

Finally you will find the same jenkins job test-1 as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/22bf9e25-ee64-496a-8b3a-09b20bd2857a)
