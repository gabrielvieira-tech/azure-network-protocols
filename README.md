<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Group Policy, Managing accounts & Observing logs a</h1>
This section covers a few everyday tasks you’ll likely run into as an IT support or system admin. We’ll walk through how to deal with account lockouts, enable or disable users, and apply changes using Group Policy. You’ll also learn how to check for failed logins...useful for checking login issues or early signs of a security problem. Great, practical stuff you’ll use often.

<h2>Video Demonstration</h2>

- ### [YouTube: Managing accounts and Security Groups in Azure Virtual Machines](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Command-Line

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows Server 2022
  
<h2>High-Level Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<h2>Group policy setup</h2>
Start by logging into DC-1 as jane_admin. Pick any of the test user accounts you created earlier. On Client-1, try to log in using that account, but intentionally enter the wrong password about ten times. Right now, nothing will happen — we haven’t set any lockout policy yet.

Next, go back to DC-1 and open Group Policy Management. Create a new GPO and name it something like “Account Lockout Policy.” Edit it and navigate to:
Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.

Here’s what you want to configure:

-Set Account lockout threshold to 5 invalid attempts

-Set the lockout duration to 15 minutes

-Set the reset counter time to 15 minutes
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>Dealing with Account Lockouts</h2>
Once that’s done, wait a few minutes (or run gpupdate /force on Client-1), then try logging in again using the same user and a bad password — this time just six times. The account should now be locked.

Head back to ADUC on DC-1, find the locked account, open its properties, and under the Account tab, check the “Unlock account” box. You can also reset the password here if needed. After that, try logging in again with the correct password — and you should be good to go.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>Enabling and Disabling Accounts</h2>
To test how account disabling works, log into DC-1 as jane_admin and open Active Directory Users and Computers (ADUC). Find the same user account you’ve been using for testing, right-click on it, and choose Disable Account. You’ll see a small down arrow appear on the user icon, showing it’s been disabled.

Now, switch over to Client-1 and try logging in with that account. You’ll get an error message saying the account has been disabled — this is expected behavior.

Go back to DC-1, right-click the account again, and choose Enable Account. Once that’s done, try logging in from Client-1 again. You should now be able to sign in normally.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>Observing Logs</h2>
Sometimes it’s not enough to just see what happens — you’ll want to check the logs to confirm things like failed login attempts, lockouts, or account changes.

Start by logging into client-1 as jane_admin. Open Event Viewer and go to:
Windows Logs > Security

Here, you’ll see events like failed logins, account lockouts, and other important authentication activity. Look for event IDs like 4625 (failed login) or 4740 (account lockout) to get more details on what happened and when.

These logs are your go-to place when something goes wrong and you need to figure out why.

</p>
<br />

