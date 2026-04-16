# Accessing my server

Welcome! This guide will walk you through how to access the server from your **phone**, **computer**, or **TV**.  

You will be able to use:

- **Jellyfin** – for movies, shows, music  
- **Jellyseerr** - request movies, shows, music for Jellyfin
- **Nextcloud** – for your personal files  
- **Immich** – for syncing photos from your phone  

> **Important:** You will get shared logins for Tailscale and Jellyfin, but you must create your own accounts for Nextcloud and Immich.

Logins for tailscale, jellyfin, and server addresses for all services, do not share this or password, if you want to grant access, tell them to contact me

[Logins](https://send.bitwarden.com/#8mgRWv2n3061M7QfAT5Y7w/HaRXDsbPnU4a6ZuVEN_OWQ) <- You will need access password from me, reach out if I have not provided this already

---

## 1️⃣ Common Step: Tailscale (All Devices)

Tailscale creates a secure connection to the server from anywhere.

### Instructions:

1. Go to [Tailscale download page](https://tailscale.com/download)  
2. Install the app on your device.  
   - **Phone:** App Store (iOS) / Google Play (Android)  
   - **Computer:** Windows / macOS / Linux  
   - **Raspberry Pi / TV device:** Let me know if you would like Jellyfin access on your TV and would like help setting this up. May require you purchasing a raspberry pi.
3. Open Tailscale and log in using the shared account credentials found in the secure share link.  
4. You should now see the server device listed inside Tailscale. This means your device is securely connected.

> Tailscale must be running whenever you want to use Jellyfin, Nextcloud, or Immich remotely.

---

## 2️⃣ Phone Instructions

### Nextcloud (Files & Documents)

1. Install the **Nextcloud app** from the App Store or Google Play.  
2. Open the app and tap **Register**  
3. Enter your email.
4. Nextcloud will send you a verification email, follow this to continue creating account  
5. Your personal files will now sync to your phone.  

> You will **not** have access to other users’ files. Other users, including me, will not be able to access your files either.

### Immich (Photos Backup)

1. Install **Immich** from App Store / Google Play.  
2. Send me the email you would like to use for your account and I will create the account and send you the password. 
3. Log in with your email and the password I provided.
4. You will be prompted to reset your password. Set it to something you will remember, as I have to reset your password if you forget it.  
5. Grant the app permission to access photos.  
6. Any new photos you take will automatically upload to Immich.

### Jellyfin (Media)

1. Install **Jellyfin** app from App Store / Google Play.  
2. Open the app and log in using the shared Jellyfin username and password.  
3. You can now stream movies, shows, and music from the server.

### Jellyseerr (Media request)

1. There is no mobile app for this one, so follow the same as the computer instructions in your browser

---

## 3️⃣ Computer Instructions

### Nextcloud

1. Open Nextcloud at http://axel-home-server:8080
2. Login with your info or select "Register"
3. Enter your personal Nextcloud account credentials.  
4. To sync local files, download the [Nextcloud Files Client](https://nextcloud.com/install/#desktop-files)
5. Connect to the server and login as before

### Immich

1. Open a browser and go to the Immich web URL http://axel-home-server:2283.  
2. Send me the email you would like to use for your account and I will create the account and send you the password. 
3. Log in with your email and the password I provided.
4. You will be prompted to reset your password. Set it to something you will remember, as I have to reset your password if you forget it.
5. You can now upload and view photos from your computer.

### Jellyfin

1. Open a web browser and go to the Jellyfin web URL http://axel-home-server:8096
2. Log in using the shared Jellyfin username and password
3. Stream media directly in your browser.

### Jellyseerr (Media Request)

1. Open a web browser and go to the Jellyseerr web URL http://axel-home-server:5055
2. Log in using the shared Jellyfin username and password
3. Search the Movie or TV Series you would like to request. Please don't request a super large series, as those take up a lot of space.
4. Click "request" and leave the default quality profile
5. Let me know you requested something, or I will check on it every so often.
6. I will likely just approve it, assuming it isn't too big. Since it is a shared account, you won't get a notification but I'll let you know when its available on jellyfin.
7. Wait for a while for the server to find and download the media. Movies shouldn't take more than an hour, series can take a while longer. If you don't see it in jellyfin, let me know, the download may have failed or the server was unable to find it.
8. If jellyseerr isn't working for you, you can also just reach out and request something directly.

---

## 4️⃣ TV Instructions

There are a couple options for setting up your TV to work with Jellyfin.
1. Download the Jellyfin app for your TV, this will vary based on your TV provider/smart TV capabilities. If your TV does not have a Jellyfin app, you cannot use it on your TV.
2. Download the Tailscale app for your TV. I am unsure if there are TVs that support this, so it is likely you will need to use a different option.

Otherwise this is a WIP, let me know if you would like to try to get it working and I can work with you.

---

## 5️⃣ Tips & Reminders

- **Keep Tailscale running** on all devices to stay connected to the server.  
- Only use your personal accounts for Nextcloud and Immich.  
- Jellyfin is shared; all users can see the same media.  
- If you lose access, contact the server administrator (me!) for credentials or troubleshooting.  
- Avoid sharing your personal Nextcloud or Immich accounts with anyone.  

---

## 6️⃣ Credentials You Will Receive

| Service      | Login Info           |
|-------------|-------------------|
| Tailscale    | Shared username + password |
| Jellyfin    | Shared username + password |
| Nextcloud   | Create your own account |
| Immich      | Create your own account |

