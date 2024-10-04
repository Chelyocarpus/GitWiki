---
description: >-
  We install Nextcloud on Docker using a MariaDB database, set up the containers
  on a Docker network, and configure the Nextcloud web installer by providing
  the correct database credentials.
cover: >-
  https://images.unsplash.com/photo-1533812451773-f2b04c2bdeb2?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw2fHxjbG91ZHxlbnwwfHx8fDE3Mjc2NDc4MDV8MA&ixlib=rb-4.0.3&q=85
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# ☁️ Nextcloud

## To install **Nextcloud** on **Docker** in **Windows**, follow these steps:

#### 1. **Install Docker Desktop on Windows**

* **Download Docker Desktop** from [Docker's official site](https://www.docker.com/products/docker-desktop/).
* Install Docker and make sure it is running. Docker Desktop includes both Docker Engine and Docker Compose.

#### 2. **Enable WSL 2**

* Docker on Windows uses **Windows Subsystem for Linux (WSL 2)** for better performance. If it's not enabled, you can enable it:
  1. Open PowerShell as an Administrator.
  2.  Run the following command:

      ```bash
      wsl --install
      ```
  3. Reboot your computer when prompted.

#### 3. **Pull the Nextcloud and Database Images**

Nextcloud requires a database, usually **MariaDB** or **PostgreSQL**.

Open a terminal (or PowerShell) and pull the images using Docker:

```bash
docker pull nextcloud
docker pull mariadb
```

#### 4. **Create Docker Network**

Create a Docker network to ensure the Nextcloud and database containers can communicate.

```bash
docker network create nextcloud-network
```

#### 5. **Create a MariaDB Container**

Create a MariaDB container that Nextcloud will use as a database:

```bash
docker run -d `
  --name nextcloud-db `
  --network nextcloud-network `
  -e MYSQL_ROOT_PASSWORD=your_root_password `
  -e MYSQL_PASSWORD=your_nextcloud_password `
  -e MYSQL_DATABASE=nextcloud `
  -e MYSQL_USER=nextcloud `
  mariadb
```

Replace `your_root_password` and `your_nextcloud_password` with secure passwords of your choice.

#### 6. **Create Nextcloud Container**

Now, create the Nextcloud container and link it to the database:

```bash
docker run -d --name nextcloud --network nextcloud-network -p 8080:80 -v nextcloud-data:/var/www/html nextcloud
```

* This command exposes Nextcloud on **port 8080**.
* The data volume (`nextcloud-data`) ensures persistence.

#### 7. **Configure Nextcloud**

* Open your browser and go to `http://localhost:8080`.
* Follow the on-screen instructions to complete the Nextcloud setup:
  * Enter the admin username and password.
  * Enter the database information:
    * **Database user**: `nextcloud`
    * **Database password**: The password you defined earlier.
    * **Database name**: `nextcloud`
    * **Database host**: `nextcloud-db`

#### 8. **Persist Data (Optional)**

For long-term storage, you can map volumes for database and Nextcloud data:

* Add the following volume options in both the **MariaDB** and **Nextcloud** containers.

Example:

```bash
-v /path/to/nextcloud/data:/var/www/html \
-v /path/to/db/data:/var/lib/mysql \
```

#### 9. **Access Nextcloud**

* Once the setup is complete, you can access Nextcloud via `http://localhost:8080`.

You now have Nextcloud running inside Docker on your Windows machine! Let me know if you need any clarification.



***

## To run the `docker run` command in **PowerShell** (or Command Prompt) on Windows, follow these steps:

1. **Open PowerShell** or **Command Prompt** as Administrator:
   * Right-click on the **Start** button and choose **Windows PowerShell (Admin)** or **Command Prompt (Admin)**.
   * This ensures that Docker has the necessary permissions to run containers.
2.  **Run the `docker run` Command:**

    Paste the following command into PowerShell, but make sure to replace `your_root_password` and `your_nextcloud_password` with your desired passwords.

    ```bash
    docker run -d `
      --name nextcloud-db `
      --network nextcloud-network `
      -e MYSQL_ROOT_PASSWORD=your_root_password `
      -e MYSQL_PASSWORD=your_nextcloud_password `
      -e MYSQL_DATABASE=nextcloud `
      -e MYSQL_USER=nextcloud `
      mariadb
    ```

    **Explanation of each option:**

    * `-d`: Runs the container in detached mode (in the background).
    * `--name nextcloud-db`: Names the container `nextcloud-db`.
    * `--network nextcloud-network`: Connects the container to the `nextcloud-network` you created earlier.
    * `-e`: Sets environment variables for configuring MariaDB:
      * `MYSQL_ROOT_PASSWORD`: Root password for the MariaDB instance.
      * `MYSQL_PASSWORD`: Password for the `nextcloud` user.
      * `MYSQL_DATABASE`: Creates the `nextcloud` database.
      * `MYSQL_USER`: Creates a `nextcloud` user with access to the `nextcloud` database.
3.  **Check if the Container is Running:** To verify that the container is running, use the following command:

    ```bash
    docker ps
    ```

    You should see an entry with `nextcloud-db` in the list of running containers. If it's running correctly, your database container is ready for Nextcloud.

Let me know if you run into any issues!

***

## In **PowerShell**, the line continuation character is the backtick (`\``) instead of a backslash (`\`). You can also run the entire command on a single line without any continuation characters if you prefer.

Here’s the correctly formatted command for **PowerShell**:

```bash
docker run -d `
  --name nextcloud `
  --network nextcloud-network `
  -p 8080:80 `
  -v nextcloud-data:/var/www/html `
  nextcloud
```

Alternatively, if you prefer to run it all on a single line, you can use:

```bash
docker run -d --name nextcloud --network nextcloud-network -p 8080:80 -v nextcloud-data:/var/www/html nextcloud
```

#### Explanation of the command:

* `-d`: Runs the container in detached mode (in the background).
* `--name nextcloud`: Names the container `nextcloud`.
* `--network nextcloud-network`: Connects the container to the previously created Docker network `nextcloud-network`.
* `-p 8080:80`: Maps port **8080** on your Windows host machine to port **80** in the Nextcloud container. You will access Nextcloud via `http://localhost:8080`.
* `-v nextcloud-data:/var/www/html`: Mounts a Docker volume named `nextcloud-data` to the Nextcloud data directory inside the container to ensure data persistence.
* `nextcloud`: The Nextcloud Docker image.

Let me know if you need further assistance!

***

> how do i enter the mariadb in the nextloud installation setup window

## In the Nextcloud installation setup window, you'll need to provide the correct database connection information to link Nextcloud with your **MariaDB** container. Here’s how to enter the information:

#### 1. **Database type**: Choose **MySQL/MariaDB**.

#### 2. **Database user**:

Enter the username you provided when creating the MariaDB container. From the `docker run` command:

```bash
-e MYSQL_USER=nextcloud
```

The database user is **`nextcloud`**.

#### 3. **Database password**:

Enter the password you set for the `nextcloud` user when you created the MariaDB container. From the `docker run` command:

```bash
-e MYSQL_PASSWORD=your_nextcloud_password
```

Replace `your_nextcloud_password` with the password you chose.

#### 4. **Database name**:

Enter the database name you provided during the MariaDB container creation:

```bash
-e MYSQL_DATABASE=nextcloud
```

The database name is **`nextcloud`**.

#### 5. **Database host**:

Since you are using Docker, the host for the database is the **name of the MariaDB container**. In this case, from your `docker run` command, you named it `nextcloud-db`:

```bash
--name nextcloud-db
```

So, the database host is **`nextcloud-db`**.

#### 6. **Optional: Database port**:

If you used the default settings, MariaDB listens on the default port **3306**, so you don't need to change anything. If you modified the port, enter that custom port.

#### Summary of inputs for the Nextcloud setup window:

* **Database type**: MySQL/MariaDB
* **Database user**: `nextcloud`
* **Database password**: (your MariaDB password)
* **Database name**: `nextcloud`
* **Database host**: `nextcloud-db`
* **Database port**: (leave it as default, unless you changed it)

#### Example:

If you used the following in your Docker run command:

```bash
docker run -d \
  --name nextcloud-db \
  --network nextcloud-network \
  -e MYSQL_ROOT_PASSWORD=your_root_password \
  -e MYSQL_PASSWORD=your_nextcloud_password \
  -e MYSQL_DATABASE=nextcloud \
  -e MYSQL_USER=nextcloud \
  mariadb
```

In the Nextcloud setup, you would enter:

* **Database user**: `nextcloud`
* **Database password**: `your_nextcloud_password`
* **Database name**: `nextcloud`
* **Database host**: `nextcloud-db`

Once you input these details, Nextcloud will connect to your MariaDB database, and you can proceed with the installation.

***

> What is meant by this: Persist Data (Optional)
>
> For long-term storage, you can map volumes for database and Nextcloud data:
>
> ```
> Add the following volume options in both the MariaDB and Nextcloud containers.
> ```
>
> Example:
>
> bash
>
> \-v /path/to/nextcloud/data:/var/www/html\
> \-v /path/to/db/data:/var/lib/mysql \\

## Explanation of Volume Mapping

{% hint style="info" %}

{% endhint %}

When you use Docker, by default, any data created inside a container is ephemeral. This means that once the container is removed, all the data within it is lost. To prevent this, you can use Docker volumes to store data outside of the container’s filesystem. Here’s a breakdown of the volume mappings mentioned in your example:

#### Volume Mappings

1.  **Nextcloud Data Volume**:

    ```bash
    -v /path/to/nextcloud/data:/var/www/html \
    ```

    * **Left Side (`/path/to/nextcloud/data`)**: This is the path on your host machine (the physical server or computer running Docker) where the Nextcloud data will be stored. You need to replace this with an actual path on your system.
    * **Right Side (`/var/www/html`)**: This is the path inside the Nextcloud container where the application expects to find its data. By mapping these two locations, any files uploaded to Nextcloud will be stored persistently on your host machine, allowing you to retain your data even if the container is stopped or removed.
2.  **MariaDB Data Volume**:

    ```bash
    -v /path/to/db/data:/var/lib/mysql \
    ```

    * **Left Side (`/path/to/db/data`)**: This is the path on your host machine where the MariaDB data files will be stored. Again, replace this with an actual path on your system.
    * **Right Side (`/var/lib/mysql`)**: This is the path inside the MariaDB container where the database files are stored. Mapping this ensures that your database data is saved on the host and can be accessed later even if the MariaDB container is removed.

#### Example of Running Containers with Volume Mapping

Here’s how you might run both containers with the volume mappings included:

```bash
# Run the MariaDB container
docker run -d \
  --name nextcloud-db \
  --network nextcloud-network \
  -e MYSQL_ROOT_PASSWORD=your_root_password \
  -e MYSQL_PASSWORD=your_nextcloud_password \
  -e MYSQL_DATABASE=nextcloud \
  -e MYSQL_USER=nextcloud \
  -v /path/to/db/data:/var/lib/mysql \
  mariadb

# Run the Nextcloud container
docker run -d \
  --name nextcloud \
  --network nextcloud-network \
  -p 8080:80 \
  -v /path/to/nextcloud/data:/var/www/html \
  nextcloud
```

#### Benefits of Using Volumes

* **Data Persistence**: Your data will not be lost when the container stops or is removed.
* **Backup and Restore**: You can easily back up the data from the host machine by copying the files from the mapped directories.
* **Data Migration**: You can move the data to another system by transferring the contents of the host directories.

By using volume mapping as described, you ensure that both your Nextcloud application data and your database are securely stored and persist beyond the lifecycle of the containers themselves.&#x20;

***

> so how can i backup the data on for example onedrive

## Here’s a step-by-step example setup for **Nextcloud** with **rclone** installed directly in the Nextcloud Docker container to back up your data to **OneDrive**.

#### Example Setup

**Step 1: Set Up Nextcloud and MariaDB in Docker**

1.  **Create a Docker Network**:

    ```bash
    docker network create nextcloud-network
    ```
2.  **Run MariaDB Container**:

    ```bash
    docker run -d \
      --name nextcloud-db \
      --network nextcloud-network \
      -e MYSQL_ROOT_PASSWORD=your_root_password \
      -e MYSQL_PASSWORD=your_nextcloud_password \
      -e MYSQL_DATABASE=nextcloud \
      -e MYSQL_USER=nextcloud \
      mariadb
    ```
3.  **Run Nextcloud Container**:

    ```bash
    docker run -d \
      --name nextcloud \
      --network nextcloud-network \
      -p 8080:80 \
      -v nextcloud-data:/var/www/html \
      nextcloud
    ```

**Step 2: Access the Nextcloud Web Interface**

1.  Open your web browser and go to:

    ```
    http://localhost:8080
    ```
2. Complete the Nextcloud setup by entering the database connection details:
   * **Database user**: `nextcloud`
   * **Database password**: (your\_nextcloud\_password)
   * **Database name**: `nextcloud`
   * **Database host**: `nextcloud-db`
   * **Database port**: (leave default, 3306)

**Step 3: Install rclone in the Nextcloud Container**

1.  **Access the Nextcloud Container**:

    ```bash
    docker exec -it nextcloud bash
    ```
2.  **Install rclone**:&#x20;

    For Debian or Ubuntu-based containers:

    ```bash
    apt-get update && apt-get install -y rclone
    ```
3.  **Verify rclone Installation**:

    ```bash
    rclone --version
    ```

**Step 4: Configure rclone for OneDrive**

1.  **Run rclone config**:

    ```bash
    rclone config
    ```
2. **Follow the prompts**:
   * Type `n` to create a new remote.
   * Name it (e.g., `onedrive`).
   * Select **OneDrive** from the list.
   * Follow the authentication prompts (this may involve visiting a URL to authorize access).
3.  **Verify Configuration**: You can list your OneDrive files to ensure the configuration works:

    ```bash
    rclone ls onedrive:
    ```

**Step 5: Back Up Nextcloud Data to OneDrive**

1.  **Run the Backup Command**: In the Nextcloud container, execute the following command to back up your data:

    ```bash
    rclone copy /var/www/html/nextcloud-data onedrive:/NextcloudBackup
    ```

**Step 6: Automate Backups (Optional)**

1.  **Create a Backup Script**: Inside the Nextcloud container, create a script:

    ```bash
    echo '#!/bin/sh' > /usr/local/bin/backup.sh
    echo 'rclone copy /var/www/html/nextcloud-data onedrive:/NextcloudBackup' >> /usr/local/bin/backup.sh
    chmod +x /usr/local/bin/backup.sh
    ```
2.  **Set Up Cron Job**: Install cron if not already available:

    ```bash
    apt-get install -y cron
    ```

    Then edit the cron file:

    ```bash
    crontab -e
    ```

    Add a line to schedule your backup (e.g., daily at 2 AM):

    ```
    0 2 * * * /usr/local/bin/backup.sh
    ```

#### Summary

This setup allows you to run Nextcloud in a Docker container, install rclone for backup, and configure it to back up data to OneDrive. You can manually trigger backups or set them up to run automatically using cron.

***

## Steps for Manual OAuth Token Setup in Rclone:

1.  **Start the Configuration Process**:

    * Run `rclone config` in your terminal to start the setup.

    ```bash
    rclone config
    ```
2. **Choose the Remote to Configure**:
   * If you're adding a new remote, choose `n` for a new remote. Then follow the prompts to choose the storage provider (Google Drive, OneDrive, etc.).
3. **When Prompted to Use Auto Config, Select No**:
   *   During the setup, Rclone will ask:

       ```
       Use auto config?
       ```
   * Type `n` and press **Enter**. This tells Rclone you want to perform the OAuth setup manually.
4. **Get the Authentication URL**:
   *   Rclone will generate a URL for you. It will look something like this:

       ```
       Please go to the following link: https://accounts.google.com/o/oauth2/auth?client_id=...
       ```
   * Copy this URL and open it in your web browser.
5. **Authorize Rclone**:
   * In your browser, authorize Rclone to access your cloud storage by logging into your account and approving the access.
6. **Receive the Code**:
   *   After authorizing, you’ll be redirected to a page that displays a code. It will look something like:

       ```
       4/XXXXX
       ```
7. **Copy the Code into Rclone**:
   *   Go back to your terminal and paste the code when Rclone prompts you for it:

       ```
       Enter verification code>
       ```
8. **Complete Configuration**:
   * Rclone will verify the token and continue with the setup process.
   * After it successfully obtains and verifies the OAuth token, it will save the configuration. Follow the remaining prompts for your specific remote.
9. **Test the Configuration**:
   *   Once completed, you can test your remote connection by running:

       ```bash
       rclone lsd <remote_name>:
       ```

This method bypasses the need to start a local web server and directly performs the OAuth authentication via a browser. Let me know if you encounter any issues!

***

> ok so how do i backup a named volume on windows?

To back up a **named volume** on Docker for **Windows**, you need to copy the data from the Docker-managed volume to a location on your host machine. Since Docker manages named volumes internally, you can’t access them directly via the filesystem, but there are ways to extract the data using Docker commands.

Here’s how you can back up a named volume, such as `nextcloud-data`, on Windows.

## Step-by-Step Backup Process

**Step 1: Identify the Volume**

First, ensure you know the name of the volume you want to back up. In this case, it's `nextcloud-data`, but you can list all volumes on your system with:

```bash
docker volume ls
```

**Step 2: Create a Temporary Container to Access the Volume**

Since named volumes aren’t directly accessible from the host, we can use a temporary container to mount the volume and copy the data.

Run the following command to start a temporary Docker container and mount the `nextcloud-data` volume:

```bash
docker run --rm -v nextcloud-data:/data -v C:/backup:/backup busybox \
  sh -c "cp -r /data/* /backup"
```

Here’s what’s happening:

* `--rm`: Automatically remove the container once the command finishes.
* `-v nextcloud-data:/data`: Mount the `nextcloud-data` volume to the `/data` directory inside the container.
* `-v C:/backup:/backup`: Mount a directory on your **Windows host** (`C:/backup`) to the `/backup` directory inside the container.
* The `cp -r /data/* /backup` command copies the contents of the named volume to the `C:/backup` directory on your Windows host.

**Step 3: Verify the Backup**

Once the command completes, all data from the `nextcloud-data` volume should be copied to `C:/backup` on your Windows system. You can now inspect the files in this directory to ensure everything was copied correctly.

#### Step 4: (Optional) Automate the Backup Process

If you want to automate this process, you can create a batch script (`.bat`) and schedule it using **Task Scheduler** on Windows.

Here’s a sample batch script (`backup_nextcloud.bat`):

```bat
@echo off
docker run --rm -v nextcloud-data:/data -v C:/backup:/backup busybox sh -c "cp -r /data/* /backup"
echo Backup completed!
```

#### Step 5: Restore the Volume (If Needed)

If you need to restore the data to the named volume at any point, you can do it using a similar approach. First, ensure that the `nextcloud-data` volume is empty or available, then run:

```bash
docker run --rm -v nextcloud-data:/data -v C:/backup:/backup busybox \
  sh -c "cp -r /backup/* /data"
```

This command will copy the backed-up data from `C:/backup` on your Windows host back into the `nextcloud-data` volume.

#### Conclusion

* To back up a Docker named volume on Windows, you can use a temporary container with the volume mounted and copy the data to your host.
* The backup is saved to a specific directory on your Windows system, and you can automate the process using scripts and Task Scheduler.
* You can restore the backup by copying the data back into the Docker volume in a similar manner.

Let me know if you need any more help!
