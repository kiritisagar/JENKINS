# JENKINS

Create a connection to your Jenkins job and your GitHub Repository 

# 1.GitHub-webhook:
Setting Up Webhooks in GitHub
To trigger Jenkins builds automatically when changes are made to the GitHub repository:

Go to Your GitHub Repository:

Navigate to the repository where you want to set up the webhook.
Configure Webhook:

Go to Settings > Webhooks.
Click Add webhook.
In the Payload URL, enter your Jenkins URL followed by /github-webhook/ (e.g., http://<your-jenkins-url>/github-webhook/).
Set Content type to application/json.
Choose Just the push event (or other events as needed).
Click Add webhook to save.
![image](https://github.com/user-attachments/assets/c5864f00-890b-48dd-8c13-124dce7ca92a)

![image](https://github.com/user-attachments/assets/21ff1291-95df-4db2-9740-eb1e77866374)


# 2. Build periodically(Scheduled job)
This trigger schedules builds to run at specified intervals, similar to cron jobs.

Use Case: Useful for regular, time-based builds such as nightly builds, or to periodically check for updates.

Setup:

Go to the job configuration page.
Scroll down to the Build Triggers section.
Check the Build periodically box.
In the Schedule field, enter a cron-like expression to define the build schedule. For example:
H 0 * * * (builds every day at midnight)
H */2 * * * (builds every 2 hours)
Save the configuration.

![image](https://github.com/user-attachments/assets/0e5bee5f-e1f7-4de4-baf9-68ff9fe3b0c7)


# 3. Poll SCM
Description: This trigger causes Jenkins to periodically check the source code repository (SCM) for changes. If changes are detected, Jenkins will start a build.

Use Case: Useful when you want Jenkins to check for changes in a repository at regular intervals, but do not have webhooks set up.

Setup:

Go to the job configuration page.
Scroll down to the Build Triggers section.
Check the Poll SCM box.
In the Schedule field, enter a cron-like expression to define how often Jenkins should check the repository. For example:
H/15 * * * * (polls every 15 minutes)
Save the configuration.

![image](https://github.com/user-attachments/assets/db8ee9f1-8319-44b5-9292-00b7e3df5e90)


# 4- Trigger builds remotely (e.g., from scripts)  --(Remote triggers)
Go to the job configuration page.
Scroll down to the Build Triggers section.
Check the Trigger builds remotely (e.g., from scripts) box.
Enter a unique Authentication Token (used to secure the remote trigger).
To trigger the build remotely, send an HTTP POST request to Jenkins using the URL format:
php
Copy code
http://<your-jenkins-url>/job/<job-name>/build?token=<token>
Save the configuration.



