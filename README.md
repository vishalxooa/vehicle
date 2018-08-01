# Deploy Xooa sample to Xooa platform
Xooa samples are repos already available in Github under Xooa org. Deploying this on Xooa backend gives you access to APIs to interact with the chanicode logic written with these samples. 

1. Go to Xooa platform located at <https://dashboard.xooa.com/>
2. **Login** to the platform. If you dont have an account, you can click on **Sign Up** to create a new account. Once logged in, you will be taken to the main Xooa dashboard. 
3. From the main dashboard, click on **Deploy New** on top left corner to start the deployment process.
3. The first step is to connect your new Xooa login to your Github account. In the main dashboard you should see the **Connect to Git** option. Click it and in the new browser window that opens up, allow Xooa to access your github account.
4. Enter **App Name** and **Description** for the app. These fields are for you to identify a particular app from list so make sure your values are relevant to the app you are deploying. Click **Next**.
5. Select the type of Github account you hold. Since we are working with Xooa organization's samples, select **public** and search for `xooa/vehicle-manufacture`. A list of repos matching the search criteria are shown below. In our case, vehicle-manufacture wil show up. Click **Select** and click **Next**.
6. The next step is deployment details. Select **master** as the branch and **vehicle-manufacturing** as the chaincode from the dropdowns available. Click **Deploy**.
7. Sit back and relax while Xooa sets up the backend. Once Xooa is finished with the process you will see **Success** for all the process listed on screen.
8. You will be redirected to app dashboard once the deployment is complete.

## API token and App ID
To connect UI with this deployed app, we will need the API token and App ID, both of which are provided by Xooa platform.

### App ID
From the app dashboard, click on `Basic Information` tab to see app details. Here you will see `App ID` listed. Copy this to a safe location on your computer.

### API token
From the app dashboard, click on `Identities` tab to see all identities enabled to work with the deployed app. For the identity listed, click on **Show API Token** and copy the token to a safe location on your computer.

# Connecting UI with Xooa platform
Now we will be cloning the UI repo. This will be connected to the app we deployed on Xooa platform


1. Go to your home folder
```
cd $HOME
```
2. Clone the sample from Xooa's github
```
git clone https://github.com/Xooa/vehicle-manufacture.git
```
3. Navigate to the config file `default.json`
```
cd vehicle-manufacture/config/
```
4. Open the config file `default.json` with your favourite text editor and modify the `webSocketURL` and `httpURL` by replacing `APP_ID` with the app ID we copied above
```
{
  "restServer": {
      "webSocketURL": "wss://api.xooa.com/api/APP_ID",
      "httpURL": "https://api.xooa.com/api/APP_ID"
  }
}
```
5. Add another key-pair called `authToken`. Here replace `YOUR_API_TOKEN` with the API token we copied above. Your `default.json` file should now look as below
```
{
  "restServer": {
      "webSocketURL": "wss://api.xooa.com/api/APP_ID",
      "httpURL": "https://api.xooa.com/api/APP_ID",
      "authToken": "bearer YOUR_API_TOKEN"  
  }
}
```
6. Go back to the root of our working directory
```
cd ..
```
7. Commit the changes to `default.json` by running the command below
```
git add config/default.json
git commit -m "Added chaincode App ID and API token"
```
8. Login to your github account and create a new repo called `vehicle-manufacture`. Copy the link for repo. Now go back to the terminal and add the link in place of `GITHUB_REPO_LINK` below and run the command
```
git remote set-url origin GITHUB_REPO_LINK
git push -u origin master
```

## Deploying on Heroku

1. Login/Signup to Heroku and navigate to new app menu located at <https://dashboard.heroku.com/new-app>.
2. Enter a relevant app name and click `Create App`.
3. On the next page, you will see a lot of sections about the app. Scroll down till you find `Deployment Method`
4. Select `Github` as the deployment method. A new section `Connect to Github` will load below.
5. Click on button `Connect to Github` and authorize Heroku to access your github.
6. `Connect to Github` sectin will now list all your repositories. Search for vehicle-manufacture-main and hit search.
7. Once the search lods, you will see the repo listed below. Click on the `Connect` button.
8. Two sections `Automatic deploys` and `Manual deploy` will show up. In the `Manual deploy` section, selected the master branch and click `Deploy Branch`.
9. Heroku will connect to github, host your app and then deploy it.
10. Once the process is done, you will see `View` button. Click it to load the app in your browser and bam! Congratulations!!!, you will see the app hosted and accessible from your browser.
