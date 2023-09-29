# batch-website-new-user

## Why

To be able to transfer data from Voucherify and set them as custom attributes for a given user in Batch, you need to create this specific user. 
Creating a user automatically by sending a distribution is not possible, the user must already exist in Batch for this data to be saved.
For example, we have a customer with source_id: `batch_distribution`, if we just send a distribution for him, we will not be able to find his data in Batch.
In order for a user to exist in Batch, it is necessary to "simulate" his activity on the website and set a `custom ID` for him. 
This is possible thanks by using the SDK that Batch provides. In our case, we will use [Web SDK](https://doc.batch.com/web/overview/). 
To do this, you need a basic HTML file with the appropriate data from Batch and `batchsdk-worker-loader.js`.

This repository contains a ready-made page that will run after filling in the credentials. 
After proper configuration, the user with your custom ID should be visible after searching in Settings -> Debug -> Search by Custom User ID.
When you will see that this user exists,  you can create a customer in Voucherify with exactly the same `source_id` as Batch's `Custom User ID` and start sending the distribution.

## Guide

1. After cloning this repository locally you can open it in code editor like WebStorm (JetBrains) or Visual Studio Code.
To open the page in WebStorm just right-click on `index.html` and select **Open In -> Browser**.
2. To run this in VSC you will need to use Live Server (it can be downloaded from Extension tab). After install, right-click on the `index.html` file and select `Open With Live Server`.
Batch Dashboard:
1. Log in to your account.
2. Click `Add a new app or website` (or select already created website from the list)
3. Select `Web`, click `Continue`.
4. Enter the URL of your locally hosted website, for example: `http://127.0.0.1:5500/index.html`
5. Enter the website name. Click `Add your website`.
6. Add team members.
7. From the modal section: `Setup the SDK` copy the fragment with credentials: `batchSDK('setup', {...})`
8. Find the place in `index.html` with similar code and replace it. 
9. In order for your site to be able to send requests to Batch, you need to add it to `allowed origins`. To do this, go to **Settings -> Push Settings -> Allowed dev origins** and paste here your page url, for example: `http://127.0.0.1:5500/index.html`
10. After completing this step and opening the page again, no errors should be displayed in the console, only the following information:
   - Batch - Starting version 3.5.0 in development mode. Environment: Fully secure
   - Batch - Installation ID: <installation_id>

important: The id you set in HTML file by: `batchSDK(api => {api.setCustomUserID("test_batch_user")});` will be the custom user ID that you will find in **Settings -> Debug** in Batch Dashboard.
important: do not share your keys outside Batch.
