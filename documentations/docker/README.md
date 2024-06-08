# 🐳 Docker

### Installation

* Don't install using double click on "Docker Desktop Installer.exe".
* Open windows terminal as Administrator.(Right click on the Terminal icon and click on Run as administrator).
* Goto the folder where "Docker Desktop Installer.exe" downloaded. And run `start /w "" "Docker Desktop Installer.exe" install -accept-license --installation-dir=E:\path\to\folder`

**Note: the WSL, image etc still will be in %HOME%\AppData\Local\Docker**. As noted in comments, you can change that too by adding: `--wsl-default-data-root=E:\path\to\data\folder`\
(for Windows 11, you might also check the another answer in this thread)

```
Start-Process -Wait -FilePath "Docker Desktop Installer.exe" -ArgumentList "install", "-accept-license", "--installation-dir=D:\Docker\Docker", "--wsl-default-data-root=D:\Docker\wsl", "--windows-containers-default-data-root=D:\\Docker"
```
