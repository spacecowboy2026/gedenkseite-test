# How to publish this website on GitHub

A simple guide. No programming knowledge needed. It takes about ten minutes.

The website is already finished. You only have to put the files into the GitHub repository. There is nothing to install and nothing to build.

## Before you start
1. Unzip the file `olaf-margraf-gedenkseite-export.zip`.
2. You now have a folder called `olaf-margraf-gedenkseite`. Inside it you see `index.html`, `style.css`, the photos and a few small text files. There are no subfolders.

**Important:** what goes on GitHub is the *contents* of that folder, not the folder itself. All files, including the photos, must end up at the top level of the repository, next to `index.html`. If it ends up inside a subfolder, the website shows a "404 not found" page.

## Step 1: Remove the old website files
1. Open the repository on github.com.
2. If you see a file called `CNAME`, **leave it alone**. It contains the website's domain name.
3. Delete everything else that belongs to the old website:
   - For a folder: open it, click the three dots at the top right, choose **Delete directory**, then **Commit changes**.
   - For a single file: open it, click the three dots at the top right, choose **Delete file**, then **Commit changes**.

## Step 2: Upload the new files
1. On the main page of the repository click **Add file**, then **Upload files**.
2. Open the unzipped folder on your computer and select **everything inside it**.
3. Drag it all into the upload area in the browser.
4. Wait until all files are listed. There are about 30, most of them photos.
5. Click **Commit changes**.

Two files start with a dot, `.nojekyll` and `.gitignore`. Your computer may hide them. If they are missing from the upload, that is fine. The website works without them.

## Step 3: Switch on GitHub Pages
1. In the repository click **Settings**, then **Pages** in the left menu.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Choose the branch **main** and the folder **/ (root)**, then click **Save**.
4. Wait one to two minutes and reload the page. The address of the website appears at the top.

If Pages was already switched on for the old website, you do not need to change anything here.

## Step 4: Your own domain, optional
1. On the same **Pages** screen, type the domain into **Custom domain** and click **Save**.
2. Log in where the domain was bought and open its DNS settings.
3. For a domain without www, such as `example.com`, create four **A records** that point to:
   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```
4. For `www.example.com`, create one **CNAME record** that points to `YOUR-GITHUB-USERNAME.github.io`.
5. DNS changes can take from a few minutes up to a day.
6. Once GitHub shows a green tick next to the domain, tick **Enforce HTTPS**.

## Step 5: Check the website
Open the website and look for these things:
- The photos on the left change about every five seconds, with a soft fade.
- The round button at the bottom right switches between dark and light.
- Tapping "Naline, Rena und Ole mit Familien" makes small hearts float up.
- On a phone, the photos are on top and the text is below.

## If something goes wrong
- **"404 not found":** `index.html` is inside a subfolder. It must be at the top level of the repository.
- **The old website still shows:** wait two minutes, then reload with Ctrl+Shift+R, or Cmd+Shift+R on a Mac.
- **Photos are missing:** the photo files are not at the top level of the repository, or some were not uploaded. They must sit next to `index.html`. Upload them again.
- **The domain stopped working:** the `CNAME` file was deleted. Enter the domain again under Settings, Pages, Custom domain.

## Good to know
- The website can be found through Google. It can take a few days or weeks until a new page shows up in the search results.
- A public GitHub repository means that anyone can see the photos and names in it. A website is public anyway, so this is normal.
- You can also hand the file `README.md` to an AI assistant. It contains the same task as precise technical instructions.
