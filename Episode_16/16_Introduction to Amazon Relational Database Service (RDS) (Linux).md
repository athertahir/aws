Introduction to Amazon Relational Database Service (RDS) (Linux)
================================================================

- Overview
- Start Lab
- Task 1: Create an RDS Instance
- Task 2: Login to Your EC2 Instance
- Task 3: Access the Database
- Conclusion
- End Lab

Overview
--------

This lab introduces you to Amazon RDS using the AWS Management Console.

### What is Amazon RDS?

Amazon Relational Database Service (Amazon RDS) is a web service that
makes it easy to setup, operate, and scale relational databases in the
cloud. It allows you to create and use MySQL, PostgreSQL, Oracle, or
Microsoft SQL Server databases. This means the code, applications, and
tools you already use today with your existing databases, can be used
with Amazon RDS.

### Topics covered

By the end of this lab, you will be able to:

-   Create an Amazon RDS instance
-   Connect to the RDS Instance with client software

Start Lab
---------

-   Open https://808477742599.signin.aws.amazon.com/console
-   Enter login credentials

Task 1: Create an RDS Instance
------------------------------

In this task, you will create an Amazon RDS database for MySQL.

3.  In the **AWS Management Console**, on the Services menu, click
    **RDS**.

4.  In the left navigation pane, click **Databases**.

If **Databases** is not visible, click the **Navigation** icon in
the left and then click **Databases**.

5.  Click Create database then configure:

    -   **Engine type:** *MySQL*
    -   **Templates:** *Dev/Test*

6.  In the **Settings** section, configure:

    -   **DB instance identifier:** `my-rds`
    -   **Master username:** `student`
    -   **Master password:** `Pass.123`
    -   **Confirm password:** `Pass.123`

7.  In the **DB instance size** section, configure:

    -   *Burstable classes*
    -   *db.t2.micro*

8.  In the **Availability & durability** section for *Multi-AZ
    deployment*, select **Do not create a standby instance**.

9.  In the **Connectivity** section, configure:

    -   **Virtual Private Cloud (VPC):** *Lab VPC*
    -   Expand **Additional connectivity configuration**
    -   **Publicly accessible:** *No*
    -   **Existing VPC security groups:**
        -   Select **RDS Security Group**
        -   Remove **default**

10. Expand **Additional configuration**, then configure:

    -   **Initial database name**
    -   De-select **Enable automatic backups**
    -   De-select **Enable Enhanced monitoring**
    -   De-select **Enable auto minor version upgrade**

11. Scroll to the bottom of the screen, then click Create database

This page shows you the details for your newly launched RDS instance.
The RDS instance will take about 10 minutes to create.

Please continue to the next task. There is no need to wait for your
database to launch.

Task 2: Login to Your EC2 Instance p4
----------------------------------

During the lab setup, an Amazon EC2 Linux instance was created. You will
now log in to the EC2 instance.

### Windows Users: Using SSH to Connect

These instructions are for Windows users only.

If you are using Mac or Linux, skip to the next section.

12. **Create/Download PPK** using AWS Console.

13. Save the file to the directory of your choice.

You will use PuTTY to SSH to Amazon EC2 instances.

If you do not have PuTTY installed on your computer, [download it
here](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe).

14. Open PuTTY.exe

15. Configure the PuTTY to not timeout:

-   Click **Connection**
-   Set **Seconds between keepalives** to

This allows you to keep the PuTTY session open for a longer period of
time.

16. Configure your PuTTY session:

    -   Click **Session**
    -   **Host Name (or IP address):** Copy and paste the **EC2PublicIP**
        shown to the left of these instructions
    -   In the **Connection** list, expand **SSH**
    -   Click **Auth** (don't expand it)
    -   Click **Browse**
    -   Browse to and select the PPK file that you downloaded
    -   Click **Open** to select it
    -   Click **Open**

17. Click **Yes**, to trust the host and connect to it.

18. When prompted **login as**, enter: `ec2-user`

This will connect to your EC2 instance.

19. Windows Users: skip ahead to the next task.

### Mac and Linux Users

These instructions are for Mac/Linux users only. If you are a Windows
user, skip ahead to the next task.

20. **Create/Download PEM** using AWS Console.

21. Save the file to the directory of your choice.

22. Copy this command to a text editor:

``` 
chmod 400 KEYPAIR.pem

ssh -i KEYPAIR.pem ec2-user@EC2PublicIP
```

23. Replace *KEYPAIR.pem* with the path to the PEM file you downloaded.

24. Replace *EC2PublicIP* with the value of EC2PublicIP shown to the
    left of these instructions.

25. Paste the command into the Terminal window and run it.

26. Type `yes` when prompted to allow a first connection to this remote SSH
    server.

Because you are using a key pair for authentication, you will not be
prompted for a password.

Task 3: Access the Database
---------------------------

You will now connect to the RDS database by using the **mysql** client
installed on the EC2 instance.

First, gather the connection details to create the new connection.

27. Return to the **AWS Management Console**.

28. In the left navigation pane, click **Databases**.

29. Wait for your **my-rds** instance to display a status of **
    **Available**.

You can click refresh every 60 seconds to update the console.

30. Click your **my-rds** instance.

31. Under the **Connectivity & security** section, copy the **Endpoint**
    to a text editor.

It will look similar to:\
 *my-rds.cmq1uckiyvci.us-west-2.rds.amazonaws.com*

32. In your SSH session, do the following:

    -   Paste `mysql --user student --password --host ENDPOINT`
    -   Replace **ENDPOINT** with the RDS endpoint that you copied to your
        text editor
    -   Press **Enter**
    -   When prompted for a password, enter: `Pass.123`

Now you are logged in to the MySQL console. You should see the
**mysql\>** prompt.

33. Copy and paste the following command:

```
CREATE TABLE lab.staff (firstname text, lastname text, phone text);

INSERT INTO lab.staff VALUES ("John", "Smith", "555-1234");

INSERT INTO lab.staff VALUES ("Sarah", "Jones", "555-8866");
```

These commands create a new table and insert some data into the
database.

You can now query the database.

34. Copy and paste the following command:

```
SELECT * FROM lab.staff WHERE firstname = "Sarah";
```

Sarah's details will be displayed.

Feel free to experiment with more SQL commands if you wish.

Conclusion
----------

**Congratulations!** You now have successfully:

-   Created a RDS (RDS) Instance
-   Connected to the RDS Instance with Client Software

End Lab
-------

Follow these steps to close the console, end your lab, and evaluate the
experience.

35. Return to the AWS Management Console.

36. On the navigation bar, click **awsstudent@\<AccountNumber\>**, and
    then click **Sign Out**.
