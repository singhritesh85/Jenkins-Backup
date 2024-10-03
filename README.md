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

![image](https://github.com/user-attachments/assets/ee4714c9-8d12-45f2-b81e-f56dbca53a06)

Create an Amazon S3 Bucket as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/a6d14832-2c40-4498-9261-ea57f7090b1a)

Create a An IAM User with Access Key and Secret Key which has sufficient privileges to access S3 bucket.

Do the configuration for Periodic backup with backup location as Amazon S3 as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/71a2c71e-1830-42ad-a34b-dfb035eb9665)
![image](https://github.com/user-attachments/assets/b2495542-9b2f-41e1-9de6-c25d08324419)
![image](https://github.com/user-attachments/assets/84c3c881-ea8e-43b2-b94b-0b9599865806)
![image](https://github.com/user-attachments/assets/42071511-67a1-4138-aa89-6e0053a388ee)

Backup is scheduled at 10:23 AM UTC daily as shown in the screenshot attached below. Daily one backup and total 30 backups will be stored, backup older than 30 days will be discarded.

After the cron job run as per the scheduled time as shown in the screenshot attached above the backup will be availabe in the S3 bucket as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/e04c0f49-cb11-4d6d-869a-84eecb3e9fd8)
![image](https://github.com/user-attachments/assets/12bde5bf-9520-4c1a-adb5-fa103c1e437e)

Before taking the backup there was a jenkins job with the name of test-1 was present but after backup I deleted the test-1 jenkins job as shown in the below screenshots.

![image](https://github.com/user-attachments/assets/a7eb1719-f4c1-4f49-b9de-f87eec5f31e5)
![image](https://github.com/user-attachments/assets/33c2fef7-df72-4fff-bbd8-08cbb767a454)

Now for Restoration of backup follow the steps as written below.

Go to **Manage Jenkins** > **Periodic Backup Manager** and restore as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/20ce1023-0016-4b4d-a3a6-c887cda3c9b7)

Checked the log and got verified that restoration has benn done.

![image](https://github.com/user-attachments/assets/943b9934-da1c-41f6-82fb-624647713698)
![image](https://github.com/user-attachments/assets/9a8eebbf-2fe7-468a-96cb-62e4f0a3d6f5)

Finally you will find the same jenkins job test-1 as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/22bf9e25-ee64-496a-8b3a-09b20bd2857a)

**(b) LocalDirectory**

Install the plugin for periodic backup as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/c9a53907-c36a-457c-9d8a-77ca39cab8d0)

To configure periodic backup in Jenkins do the configuration in Jenkins after installation of periodic backup plugin as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/243b80fe-1e71-47c9-9d9d-a3b563db21db)

Before proceeding further my first Aim is to create the temporary directory /opt/mederma, backup directory /opt/jenkins-backup and change it's ownership as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/4bda641d-8f55-476b-8e15-229254dde8c0)
![image](https://github.com/user-attachments/assets/4e1e3e1d-69e4-4602-8498-5c95970ffcbd)
![image](https://github.com/user-attachments/assets/c0ea7b7d-c7e1-4730-812a-efa1af339161)

Configuration for Periodic Backup Manager is as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/91c884e4-f1ea-4fff-bcf2-2b776e461913)
![image](https://github.com/user-attachments/assets/8701baa3-a20e-4674-a7d2-ba9c83fc12e3)
![image](https://github.com/user-attachments/assets/617a1a5c-73b3-4ba0-a999-e115abd1e57d)

Periodic backup will be taken daily at 06:05 AM daily and only 30 days backup will be stored locally, if a new backup tar file will be generated then oldest backup will be discarded.

Backup has been created at 06:05 AM UTC as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/c0b05360-a38d-4f70-b7b1-abb50d64e77b)

![image](https://github.com/user-attachments/assets/353ad8ab-7b7c-4e14-b1f6-659bdca2a703)

Befor running the Backup there was one Jenkins Job with the name test-1 and five builds as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/9b556874-f1c2-47f7-ba7b-2d56039bf68e)
![image](https://github.com/user-attachments/assets/94033cbd-f745-4f28-a0db-99fc0a62ebf4)

Now I deleted the Jenkins Job with the name test-1 as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/2aace4f9-220f-48e4-be96-9ad1895cdf22)

And Restore from the backup as shown from the screenshot attached below.

![image](https://github.com/user-attachments/assets/7a51613a-5c27-4957-9721-84c853aeb197)
![image](https://github.com/user-attachments/assets/748f9389-5989-4815-8304-5731694d0bbb)

The backup has been done as confirmed from the below screenshot.

![image](https://github.com/user-attachments/assets/386c8d95-b7fb-4b1e-8253-8c029214969b)
![image](https://github.com/user-attachments/assets/ec3f6855-7fbd-44e7-8b8a-6e92da5af4aa)

Finally we are able to see the deleted Jenkins Job and Builds as shown in the screenshot attached below.

![image](https://github.com/user-attachments/assets/ce0c3330-5752-4580-a9ea-8245e6e179af)
![image](https://github.com/user-attachments/assets/249f2a09-00ce-49b7-a1c4-c0f5807849d5)
