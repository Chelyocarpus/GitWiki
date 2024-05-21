---
description: How to install and setup Photoprism with Docker
cover: >-
  https://images.unsplash.com/photo-1597600159211-d6c104f408d1?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw0fHxwcmlzbXxlbnwwfHx8fDE3MDY0NjMwNjB8MA&ixlib=rb-4.0.3&q=85
coverY: 0
layout:
  cover:
    visible: true
    size: hero
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

# 📷 PhotoPrism

### Prerequisites

* Docker

### Basic Setup

1. Create a folder where you want the data of Photoprism to be saved, for example "D:/Photoprism"
2. Get the latest "docker-compose.yml" from [Setup Using Docker Compose](https://docs.photoprism.app/getting-started/docker-compose/)
3. Paste/Save "docker-compose.yml" in the newly created directory "D:/Photoprism"

<figure><img src="https://user-images.githubusercontent.com/7150376/172752818-894b76f0-64b6-47c9-a1ab-00bb28b23355.png" alt="The picture shows a docker compose file in a newly created folder named Photoprism"><figcaption><p>The picture shows a docker-compose.yml file in a newly created folder named Photoprism</p></figcaption></figure>

1. Edit the "docker-compose.yml" to your liking. Recommended changes:

* PHOTOPRISM\_ADMIN\_PASSWORD: "insecure" > PHOTOPRISM\_ADMIN\_PASSWORD: "YOURPASSWORD"
* PHOTOPRISM\_ORIGINALS\_LIMIT: 5000 > PHOTOPRISM\_ORIGINALS\_LIMIT: 50000
* PHOTOPRISM\_JPEG\_QUALITY: 85 > PHOTOPRISM\_JPEG\_QUALITY: 100

1. Open the folder with Windows Terminal

<figure><img src="https://user-images.githubusercontent.com/7150376/172753447-24ed52fd-5ea1-4455-b114-bfbd8e06a2c0.png" alt="The picture shows a highlighted Open in Terminal after opening the context menu with a right click"><figcaption><p>The picture shows a highlighted Open in Terminal after opening the context menu with a right click</p></figcaption></figure>

1. Copy paste "docker-compose up -d" and press Enter

<figure><img src="https://user-images.githubusercontent.com/7150376/172754859-3d678b63-ace1-403e-aafa-00506c975c86.png" alt="The picture shows an opened Windows Terminal Window with the copy pasted docker compose command"><figcaption><p>The picture shows an opened Windows Terminal Window with the copy pasted docker compose command</p></figcaption></figure>

### Additional

* To add new/other folders for import/storage you'll have to add them to "volumes"

<figure><img src="https://user-images.githubusercontent.com/7150376/172755373-b2c8ece6-604d-4c48-9121-d2c6ac06df72.png" alt="The picture shows an overview of how the different Photoprism folders have been set up"><figcaption><p>The picture shows an overview of how the different Photoprism folders have been set up</p></figcaption></figure>

**Important:** Keep in mind that "photoprism/originals", "photoprism/storage" and "photoprism/import" are used as a variable, the pictures will be saved under "User/Pictures" **not** "User/Pictures/photoprism/originals"!

For additonal info about the folder structure see [Setup Using Docker Compose](https://docs.photoprism.app/getting-started/docker-compose/).

* You can use the "Import" function to import complete folders.
* To delete pictures you'll have to archieve them first.

### Image Folders on Windows

If you are using docker on Windows Subsystem for Linux (WSL2), you can access the images via hidden share:

`\wsl$\docker-desktop-data\version-pack-data\community\docker\overlay2`

The volums are also there at:

`\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes`

Source: [https://stackoverflow.com/a/68053068](https://stackoverflow.com/a/68053068)

### Unsolved Questions

* How do i backup data?
* What can i add to docker-compose.yml?
