# batch-website-new-user

To be able to transfer data from Voucherify and set them as custom attributes for a given user in Batch, you need to create this specific user. 
Creating a user automatically by sending a distribution is not possible, the user must already exist in Batch for this data to be saved.
For example, we have a customer with source_id: `batch_distribution`, if we just send a distribution for him, we will not be able to find his data in Batch.
In order for a user to exist in Batch, it is necessary to "simulate" his activity on the website and set a `custom ID` for him. 
This is possible thanks by using the SDK that Batch provides. In our case, we will use [Web SDK](https://doc.batch.com/web/overview/). 
To do this, you need a basic HTML file with the appropriate data from Batch and `batchsdk-worker-loader.js`.

This repository contains a ready-made page that will run after filling in the credentials. 
After proper configuration, the user with your custom ID should be visible after searching in Settings -> Debug -> Search by Custom User ID.
When you will see that this user exists,  you can create a customer in Voucherify with exactly the same `source_id` as Batch's `Custom User ID` and start sending the distribution.