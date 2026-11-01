# Voice Typing Automation (YouTube to Google Docs)

This Java-based automation script utilizes Selenium WebDriver, Java AWT Robot, and the Google Drive API to automatically transcribe YouTube videos. It works by playing a YouTube video via an embedded iframe in one browser window while using the Voice Typing feature in an automatically generated Google Doc in another window.

## Prerequisites

### 1. System Requirements
* **Java Development Kit (JDK):** Version 8 or higher.
* **Google Chrome:** Installed on your local machine.
* **ChromeDriver:** 
  * You must download the `chromedriver.exe` that matches your current Google Chrome version.
  * **Path Configuration:** By default, the script looks for `chromedriver.exe` in your system's Home Directory (`FileSystemView.getFileSystemView().getHomeDirectory().getPath()`). Place the executable there, or modify the `defaultPath` variable in the code to point to your driver's location.

### 2. Audio Hardware / Channel Setup (Critical)
Because the script relies on Google Docs listening to the audio from the YouTube video, you must route your system's audio output directly into your microphone input.
* **Windows Stereo Mix:** Go to Windows Sound Settings -> Recording tab -> Enable **Stereo Mix** and set it as the default recording device.
* **Virtual Audio Cable (VAC):** If Stereo Mix is unavailable, install a Virtual Audio Cable to bridge the system speaker output to the microphone input.

## Dependencies

If you are using Maven, add the dependencies named `requirment.xml` in this libarary. These include Selenium for browser automation and Google Client Libraries for Drive API integration.

## Google API Configuration
This script relies on the Google Drive API to create documents and set permissions. 
1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Enable the **Google Drive API**.
3. Create OAuth 2.0 Client ID credentials.
4. Download the `credentials.json` file and place it in your project directory (as required by your `GoogleDriverHandler` implementation).

## Required Custom Classes
The provided code references several custom classes and models that are specific to your project architecture. Ensure the following classes are implemented and imported correctly for the script to compile:

* `CommonAPI.GoogleDriverHandler`: Handles Google API OAuth authentication, creating the Google Doc (`createDoc`), and modifying file permissions (`createPermissionForFile`).
* `CommonAPI.YoutubeCommon`: Handles YouTube metadata retrieval, including fetching the title (`getTitile`), fetching the duration (`getDuration`), and converting ISO 8601 time strings to seconds (`parseISO8601StringToSecond`).
* `videoInfo`: A POJO/Bean used to store and update video metadata (e.g., `setId`, `setDocId`, `setVideoTextLink`).
