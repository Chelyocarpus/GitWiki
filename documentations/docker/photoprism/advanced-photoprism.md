---
description: >-
  How to set up PhotoPrism with rclone, Cloudflare R2 (Amazon S3), Amazon Lambda
  and Amazon ElasticCache
---

# 📸 Advanced PhotoPrism

## Step 1: Install `rclone`

1. **Download `rclone`**:
   * Go to the [rclone download page](https://rclone.org/downloads/).
   * Download the Windows version.
2. **Install `rclone`**:
   * Extract the downloaded zip file.
   * Move the `rclone.exe` file to a directory of your choice (e.g., `C:\rclone`).
3. **Add `rclone` to your PATH**:

<figure><img src="../../../.gitbook/assets/grafik.png" alt=""><figcaption><p>Overview of Environment Variables</p></figcaption></figure>

* Open the Start menu and search for "Environment Variables" ("Systemsumgebungsvariablen" in german).
* Click on "Edit the system environment variables".
* In the System Properties window, click on "Environment Variables".
* In the Environment Variables window, find the "Path" variable under System variables, select it, and click "Edit".

{% hint style="info" %}
Don't click on "New..", select "Path" and then click on "edit..." instead
{% endhint %}

<figure><img src="../../../.gitbook/assets/grafik (1).png" alt=""><figcaption><p>Inside the "Path" variable</p></figcaption></figure>

* Click "New" and add the path to your `rclone` directory (e.g., `C:\rclone`).
* Click "OK" on all windows to apply the changes.

{% hint style="success" %}
Once everything is correctly set up, you can easily run "rclone" directly from the command line without specifying any path or navigating to a specific folder. This method also applies to other command-line programs.
{% endhint %}

<figure><img src="../../../.gitbook/assets/grafik (2).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
If rclone cannot be found, check the path to your rclone folder and/or restart the command line after adding the variable to "Path". For more information, check [Troubleshooting](advanced-photoprism.md#troubleshooting).
{% endhint %}

## Step 2: Configure `rclone` for Cloudflare R2

1. **Open Command Prompt**:
   * Press `Win + R`, type `cmd`, and press Enter.
2. **Run `rclone config`**:
   * Type `rclone config` and press Enter.
   * You'll see a menu with options. Type `n` for "New remote" and press Enter.
3. **Set up the remote**:
   * You'll be prompted to enter a name for the remote. Enter a name (e.g., `cloudflare_r2`) and press Enter.
   * Choose the storage type by typing `s3` and pressing Enter.
   * You'll be asked for the provider. Type `Other` and press Enter.
   * You'll be asked how you want to enter the AWS credentials. Type `1` and press Enter.
   * Enter your Cloudflare account's access key ID and secret access key when prompted.
   * Leave the default region as an empty string and press Enter.
   * Set the location constraint (usually, you can leave this empty).
   * Leave the ACL (access control list) as the default and press Enter.
   * Skip any additional configuration options by pressing Enter.
   * Finally, you'll be asked if you want to use the new remote configuration. Type `y` and press Enter.

## Step 3: Mount the Cloudflare R2 Bucket

{% tabs %}
{% tab title="As A Drive" %}
**Mount the Bucket as a Drive**:

1. Open Command Prompt as an administrator (search for `cmd`, right-click, and select "Run as administrator").
2. Run the following command to mount the bucket as a drive (e.g., drive letter X:):

```shell
rclone mount cloudflare_r2:photoprism X: --vfs-cache-mode full
```

Replace `cloudflare_r2` with the name of your remote (=the chosen name in rclone) and `photoprism` with the name of your Cloudflare R2 bucket. Replace `X:` with the drive letter you want to use.

{% hint style="warning" %}
You might see the message "NOTICE: s3: s3 provider "other" not known - please set correctly" in the command line - you can ignore that.
{% endhint %}

When everything is set up correctly, it will look like this:&#x20;

<figure><img src="../../../.gitbook/assets/grafik (3).png" alt=""><figcaption><p>Our newly mounted drive. But wait a minute...</p></figcaption></figure>

As you can see, the name is a bit off. You can fix it by hardcoding the name in the Windows Registry (not recommended) or mounting the bucket a bit differently:

```bash
rclone mount photoprism: X: --vfs-cache-mode full
```

Will look like:

<figure><img src="../../../.gitbook/assets/grafik (4).png" alt=""><figcaption><p>Now that looks better</p></figcaption></figure>

{% hint style="danger" %}
This method creates a folder within the drive (X:\photoprism\\). All content must be placed in that folder.
{% endhint %}
{% endtab %}

{% tab title="As A Folder" %}
**Mount the Bucket as a Folder**:

1. Create a mount point (optional):
2. Create a directory on your computer where you want to mount the R2 bucket (e.g., `C:\cloudflare_r2`).
3.  **Mount the bucket**:

    * Open Command Prompt as an administrator (search for `cmd`, right-click, and select "Run as administrator").
    *   Run the following command to mount the bucket:

        ```bash
        rclone mount cloudflare_r2:bucket_name C:\cloudflare_r2 --vfs-cache-mode full
        ```

    Replace `cloudflare_r2` with the name of your remote (=the chosen name in rclone) and `bucket_name` with the name of your Cloudflare R2 bucket. Specify your desired folder path in place of `C:\cloudflare_r2`. If the folder does not already exist, it will be created automatically. For example:&#x20;

```bash
rclone mount photoprism:photoprism H:\photoprism_r2 --vfs-cache-mode full
```

{% hint style="warning" %}
You might see the message "NOTICE: s3: s3 provider "other" not known - please set correctly" in the command line - you can ignore that.
{% endhint %}
{% endtab %}
{% endtabs %}

## Step 4: Create a Batch File for Automatic Mounting (Optional)

1. **Create a new text file** and name it `mount_r2.bat`.
2.  **Edit the file** and add the following content:

    ```bash
    @echo off
    rclone mount cloudflare_r2:bucket_name C:\cloudflare_r2 --vfs-cache-mode full
    ```

    Replace `cloudflare_r2` with your remote name and `bucket_name` with your R2 bucket name.
3. **Save the file** and place it in a convenient location.
4. **Create a shortcut to the batch file** and place the shortcut in the Windows Startup folder:
   * Press `Win + R`, type `shell:startup`, and press Enter.
   * Move the shortcut to the Startup folder.

Now, whenever you start your computer, the batch file will run, and your Cloudflare R2 bucket will be mounted automatically.

By following these steps, you should be able to mount your Cloudflare R2 bucket on Windows 11 and use it just like a local drive.



## Troubleshooting

**Double-check the PATH Addition**:

* Open Command Prompt.
* Type `echo %PATH%` and press Enter. This will display the current PATH environment variable. Verify that your `rclone` directory is listed here.

