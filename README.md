# Chloe's Fake Call Workshop
☎️ *A workshop to build your own fake boyfriend/boss/sibling/co-worker call with Azure &amp; Twilio* ☎️

![](https://camo.githubusercontent.com/306aca34bdd2e5664a12eb2f81bcafe047e8a5e7/68747470733a2f2f6d656469612e67697068792e636f6d2f6d656469612f6e6e6d394e4f6c56613879715762776172762f67697068792e676966)

Today we will build a fake calling app using:

+ ⚡ [Azure Functions](https://azure.microsoft.com/services/functions/?WT.mc_id=academic-0000-chcondon)
+ ☎️ [Twilio](https://www.twilio.com/)
+ 🔘A [Flic button](http://flic.io/shop/flic-1pack?aff=10)
+ 📱Your cellphone 

If you don't own a Flic Button, [you can purchase one at a discounted rate here](http://flic.io/shop/flic-1pack?aff=10). If you're looking for a group purchase for a workshop, or are interested in custom logo buttons- [reach out directly](https://twitter.com/ChloeCondon) and I can help! 🙋‍♀️

⚠️ **YOU DO NOT NEED A FLIC BUTTON TO COMPLETE THIS WORKSHOP** ⚠️
(However, it's [a lot more fun](https://www.youtube.com/watch?v=kAjrKYstfDM) with one! 🙃)



Before we begin, if you're looking for a quick summary and overview on Azure Functions (or found this page early and would like to get a headstart), I recommend [starting here with our documentation](https://docs.microsoft.com/azure/azure-functions/?WT.mc_id=academic-0000-chcondon), or taking 4 minutes to read in more detail [how to create your first Azure Function](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function/?WT.mc_id=academic-0000-chcondon), so you have some context on how to use functions within Azure.

You can learn more about the original project [in my blog post](https://dev.to/azure/an-ambivert-s-guide-to-azure-functions-27b8)!

Happy coding, friends!
-[Chloe 🎀](https://twitter.com/ChloeCondon)

## Let Us Begin!
Today we will build a fake calling app using Azure Functions, Twilio, and a Flic button. We will start by creating a Function App in Azure. Then we will create a Twilio account, create 2 Azure Functions, and test it out on our phones.

Here's a diagram of what we'll be doing:

![](https://res.cloudinary.com/practicaldev/image/fetch/s--wGlGfh8K--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1600/1%2AepHpHigBLPGaCK5tuxzn4w.png)

### Create an Azure Account!
If you don't already have one, create an Azure account for free [here](https://azure.microsoft.com/free/?WT.mc_id=academic-0000-chcondon)!

I know what you may be thinking... "but Chloe- I'm a developer... this is much too bright for me!". Don't worry- there's a dark mode option. 😎

![](https://i.imgur.com/i2qeQFm.png)

If you already have an Azure account, yay! 

### Create an Azure Function Resource
For the sake of easy to understand visuals/screenshots for this workshop, we'll be using the [Azure portal](https://azure.microsoft.com/free/?WT.mc_id=academic-0000-chcondon) to create this. You can also use [VS Code](https://docs.microsoft.com/azure/azure-functions/functions-create-first-function-vs-code/?WT.mc_id=academic-0000-chcondon), the [Azure CLI](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function-azure-cli/?WT.mc_id=academic-0000-chcondon), etc. With Azure Functions you are given the the ability to code and test Functions locally on your machine without having to deploy to the cloud every single time you want to test (a huge time saver!).

To create an Azure Function, you can just start from the Get Started menu and select Function App.

![](https://res.cloudinary.com/practicaldev/image/fetch/s--TnBmEJTg--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1200/1%2A0yImy-SW4IsrRgJN_UjP7Q.png)

Then you’ll need to fill in some basic info about your function here. Including the app name, the Azure subscription you’d like to use, a [resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview?WT.mc_id=academic-0000-chcondon) (create a new one in this case), the Operating System you’d like to use (please select **Windows** for this workshop), the [hosting plan](https://docs.microsoft.com/azure/azure-functions/functions-scale/?WT.mc_id=academic-0000-chcondon) (I’m using consumption), the location you’d like to use (I’m based in California, so West US is usually my default), the runtime stack I’d like to use (I’m using NodeJS in this case), and we have the option to create new [storage](https://docs.microsoft.com/azure/storage/common/storage-introduction/?WT.mc_id=academic-0000-chcondon) or use existing. We'll create a new one in this case.

![](https://i.imgur.com/rEdUcjS.png)

Once you have all these filled out, you can go ahead and deploy! Wait about a minute or two, then watch for the **Deployment succeeded** message.

🎊 Woo! If you followed those steps, we have our resource! Select **Go to resource** in your notifications (top right corner) to view your new Function App. 

### Create Your First Azure Function
Now we'll add our functions to our app, starting with a function to send a text message. Click the plus sign in the left-hand side navigation, or select **Add Function** towards the center/bottton of the screen.

Select in-portal.
![](https://res.cloudinary.com/practicaldev/image/fetch/s---bwMvA0C--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1600/1%2AR7td7o0irI7STDwRsCnDDg.png)

And select Webhook + API
![](https://res.cloudinary.com/practicaldev/image/fetch/s--V8ROjeS5--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1600/1%2AOqn6uiCHsF2UStDnhj_T2w.png)

It will take about a minute to deploy and then you’ll have a fresh new Azure Function waiting to be called.

The default code is a simple hello world app. If you paste the function URL (located above your function under the link **</> Get function URL**) into your browser’s address bar with the query string value &name= to the end of this URL and press the Enter key on your keyboard, you should be able to execute the request. You should see the response returned by the function displayed in the browser.

**Try doing this once!** Add the URL with *&name=your-name-here* added to it, and test out that the function works in your browser.

### Let’s Create a Fake Boyfriend (or aunt, or cousin, or coworker- whatever!) with Twilio
In a new tab, head over to [Twilio.com](https://www.twilio.com/) and sign up for an account if you don't have one already. Add a trial phone number to your account that has calling and SMS capabilitites (if you'd like to not work in trial mode- you can use code **CHLOE20** to upgrade your account at any point).

Once you have a trial number, head back to the dashbaord. You'll see a **ACCOUNT SID** and **AUTH TOKEN** for your project. 🚨 Do not share/screenshot/commit these numbers 🚨 Think of them as your username and password for our Twilio number- we will securely store these in Azure shortly.

### Add Sample Code to our Function

Navigate back to the Azure portal, and replace the exsiting code wiith the following code in your index.js file:

```
const accountSid = process.env.TWILIO_SID;
const authToken = process.env.TWILIO_TOKEN;
const client = require('twilio')(accountSid, authToken);

// This can also be accomplished with a Twilio output binding- you can read more on this at http://aka.ms/AA4n3j3

module.exports = function (context) {
 client.messages
 .create({ from: process.env.SENDER_NUMBER,
           body: 'Woohoo- it worked!',
           to: process.env.RECIPIENT_NUMBER
       })
        .then(message => {             
           context.log("Message sent");
           context.res = {
               // status: 200, /* Defaults to 200 */
               body: 'Text successfully sent'
           };                                
           context.done();
        }).catch(err => {
          context.log.error("Twilio Error: " + err.message + " -- " + err.code);
          context.res = {
                   status: 500,
                   body: `Twilio Error Message: ${err.message}\nTwilio Error code: ${err.code}`
               };
          context.done();
        });
}
```

This will be the code that is run when our function is called.

**Take a moment to read and understand the code.** 🕵️‍♀️ You'll see that we're setting our accountSid & authToken (with credentials we have set in our function's Application Settings). We then have a function that creates a message sent from SENDER_NUMBER, to RECIPIENT_NUMBER (with credentials we have set in our function's Application Settings as well). Next, we're logging that our message is sent, and setting our context as done. Alternatively , if there's an error, we'll log it and set our context to done.

Once you have an understanding of this code, click **Save**.

### Add package.json file to Function

Add a package.json file to your function. You can do this by navigating to the top-right corner of your function, and adding a file as pictured below (⚠️ Can't find it? The 'View Files' tab is collapsed- scroll *alllllll* the way to the right of your screen):

![](https://i.imgur.com/EWUt68c.png)

Add the following code to your package.json file (adding your desired app name/description/etc):

```
{
  "name": "your-app-name",
  "version": "1.0.0",
  "description": "Fake text/call functions",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "your-name",
  "license": "MIT",
  "dependencies": {
    "twilio": "^3.33.1"
  }
}
```

Click **Save**, and navigate back to your **index.js** file.

### Install the Twilio Node.js Module

Install the Twilio Node helper library using npm. This will install the twilio module so that Node.js scripts in the current directory can use it. Access the Azure console at the bottom of the screen

![](https://i.imgur.com/fY6npig.png)

In the console, enter the following:

```
npm install twilio
```

This may take a couple minutes (if you're looking for a good time to go grab a coffee/LaCroix/bathroom break- this is it! ☕️🍕🚽). 

You may see a warnings/notice here- don't worry, you can ignore this. This is notifying us a package-lock.json file has been created.

### Add Credential Values Securely in Azure

Head over to **Configuration** under your Function App in the Azure portal (highlighted in pink, below- click on your Function App Name on the left-hand side).

![](https://i.imgur.com/WDjoqff.png)

Add 2 new application settings named **TWILIO_SID** and **TWILIO_TOKEN**- storing with them the credentials provided to us from Twilio.

Additionally, add a setting for **SENDER_NUMBER** (adding your Twilio trial number in the format of plus-sign, country code, and number like so as the value: *[+19168675309](https://www.youtube.com/watch?v=6WTdTwcmxyo)*) as well as **RECIPIENT_NUMBER** (add your cell phone number in the same format of *[+19168675309](https://www.youtube.com/watch?v=6WTdTwcmxyo)* as the value for now to test our app).

![](https://i.imgur.com/LNf0Sxy.png)

😳😭 Totally lost? Can't find your credentials? ☎️ Log into [Twilio](https://www.twilio.com/) to find them!

Click **Save**, and navigate back to your function in the console.

### Test Your First Azure Function

Click the **Run** button at the top of your function. Your logs should pop up and show that your function has been called. **This may take a couple minutes on your 1st try, so stay patient!** If all goes smoothly, you should receive a text saying "Woohoo- it worked!". You can also run and test this function by copying and pasting the function URL (located in the **</> Get function URL** link above your function) in your browser.

📝 NOTE: If you are still using a trial account, texts and calls from Twilio will have a *Sent from your Twilio trial account* message before it. If you'd like to remove this, consider upgrading and adding code **CHLOE20** for some credits.

🎊 Great job! 🎊 You made your first Azure function using Twilio to send a text! Feel free to switch the **RECIPIENT_NUMBER** value if you'd prefer to have the app alert a friend (vs. send a message to yourself). Of course, if you're testing- it's easiest to keep your own number for now. Here's [a funny story about that](https://twitter.com/ChloeCondon/status/1105613535487225857). 🙈

### Create Your Second Azure Function

![](https://media.giphy.com/media/3orieJT6srEZntBhE4/giphy.gif)

Now we'll add our 2nd function to our app- this time, with the code to send a call (vs. a text).

Add another function to your app (as we did before on our 1st function- click the plus sign in the left-hand side navigation), and select **HTTPTrigger** again.

### Add Sample Code to our Function

In the Azure portal, replace the exsiting code with the following code in your index.js file:

```
const accountSid = process.env.TWILIO_SID;
const authToken = process.env.TWILIO_TOKEN;
const client = require('twilio')(accountSid, authToken);

    module.exports = function (context) {
       client.calls
       .create({
                 url: process.env.TWIML_URL,
                 to: process.env.RECIPIENT_NUMBER,
                 from: process.env.SENDER_NUMBER,
           })
      .then(call => {
           context.log("Call sent");
           context.res = {
               // status: 200, /* Defaults to 200 */
               body: 'Call successfully sent'
           };
           context.done();
       }).catch(err => {
           context.log.error("Twilio Error: " + err.message + " -- " + err.code);
           context.res = {
               status: 500,
               body: `Twilio Error Message: ${err.message}\nTwilio Error code: ${err.code}`
           };
           context.done();
       });
   }
```
This will be the code that is run when our call function is called.

**Take a moment to read and understand the code for your call function.** You'll see that we're again setting our accountSid & authToken (with credentials we have set in our function's Application Settings). We then have a function that creates a call sent from **SENDER_NUMBER**, to **RECIPIENT_NUMBER**, with a url of **TWIML_URL** (this will be set-up with credentials we have set in our function's Application Settings as well). Next, we're logging that our call is sent, and setting our context as done. Alternatively , if there's an error, we'll log it and set our context to done.

Click **Save**.

### Add package.json file to Function

Add a package.json file to your function (as we did before on our 1st function). 

Add the following code to your package.json file:

```
{
  "name": "your-app-name",
  "version": "1.0.0",
  "description": "Fake text/call functions",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "your-name",
  "license": "MIT",
  "dependencies": {
    "twilio": "^3.33.1"
  }
}
```

Click Save, and navigate back to your index.js file.

### Install the Twilio Node.js Module

Once again, we'll install the Twilio Node helper library using npm. This will install the twilio module so that Node.js scripts in the current directory can use it. Access the Azure console at the bottom of the screen.

In the console, enter the following:

```
npm install twilio
```

Again, this may take a couple minutes (if you're looking for a good time to go grab *another* coffee/LaCroix/bathroom break- this is it! ☕️🍕🚽).

You may see a warnings/notice here- don't worry, you can ignore this. This is notifying us a package-lock.json file has been created.

Our configurations are already set in Azure, so no need to add our **TWILIO_SID**, **TWILIO_TOKEN**, **SENDER_NUMBER**, or **RECIPIENT_NUMBER** again.

### Create Twilio Asset

Now we'll create a Twilio Asset to hold our fake call's recorded voice message.

Download the following MP3 by [clicking here](https://github.com/ChloeCodesThings/FakeCallWorkshop/raw/master/sampleaudio.mp3). Alternatively, you can record [your own MP3 here](https://online-voice-recorder.com/) (or, use whatever MP3 you'd like!)

Head back to Twilio, and navigate to the **...*** section of the left-side navigation. Select Runtime > Assets.

![](https://i.imgur.com/9l3GwAU.png)

Add or drag/drop the Mp3 file, and copy the path of the URL.

### Create a TwiML Bin

Navigate to Runtime > TwiML Bins in the left-side navigation.

We'll now create a TwiML Bin. TwiML Bins allow you to write TwiML that Twilio will host for you - so you can quickly prototype a solution without spinning up a web server.

Add the following to your TwiML bin- **make sure to replace **URL-OF-YOUR-TWILIO-ASSET** with the url of the Twilio Asset you just created!** This will play our MP3 when a call is made to the **RECIPIENT_NUMBER**:

```
<?xml version="1.0" encoding="UTF-8"?>

<Response>
  <Say voice="man">Hey- congrats! Everything is working. You are awesome. You did it- yay!</Say>
  <Play>URL-OF-YOUR-TWILIO-ASSET</Play>
</Response>
```

This TwiML will speak the <Say> text, and <Play> the URL of the Twilio Asset URL you provide it.
 
![](https://i.imgur.com/r9zLG4Y.png) 

Save your TwiML bin, and **copy the URL**.

### Add TwiML URL to Application Settings

Navigate to **Configuration** once again to add **TWIML_URL** with the value of your recently created/copied TwiML URL to your **Application Settings**.

![](https://i.imgur.com/OBkv4mI.png)

Click **Save**.

### Test call

Navigate to your call function and click **Run** to test the call.

*This can sometimes take a minute or two, so be patient- and only click run once (otherwise, you may get multiple calls back to back)!*

📝 NOTE: If you are still using a trial account, texts and calls from Twilio will have a *Sent from your Twilio trial account* message before it (with calls, you'll need to press any number to run your code). If you'd like to remove this, consider upgrading and adding code **CHLOE20** for some credits.

🎊 YOU DID IT!!! 🎊 You made your second Azure function using Twilio to send a call! Feel free to play and switch the **RECIPIENT_NUMBER** value as you wish. Again, I'll reiterate: if you're testing- it's easiest to keep your own number for now. Here's [a funny story about that](https://twitter.com/ChloeCondon/status/1105613535487225857). 🙈

If all goes well, you'll soon get a call and will be a victim of Rick-Rolling! 😁☎️

![](https://media.giphy.com/media/QG9DL5hAYZWVO/giphy.gif)

Feel free to play around with the **TWIML_URL** and add/remove your own MP3 Assests within Twilio. Your call can be whatever you'd like it to be! Your mom, dad, cousin, aunt, uncle, sister, brother, co-worker, boss, Rupaul, Justin Trudeau, Barack Obama, or Beyonce-- your choice! Get creative and experiment with your fake call- **if we have time, we'll share it with the group.**

### Add URL to Flic Button

The next steps of this workshop require a Flic Button. If you don't own a Flic Button, [you can purchase one at a discounted rate here](http://flic.io/shop/flic-1pack?aff=10). If you're looking for a group purchase for a workshop, or are interested in custom logo buttons- [reach out directly](https://twitter.com/ChloeCondon) and I can help! 🙋‍♀️

For our final step, we'll need to add our Azure Function URLs to the Flic Button app! Download the Flic Button app to your phone on [Google Play](https://play.google.com/store/apps/details?id=io.flic.app&hl=en_US) or [Apple](https://apps.apple.com/us/app/flic-app/id977593793).

Create an account, and login. Add a button to your phone by clicking the plus sign.

![](https://i.imgur.com/sIFBORa.png)

Click your Flic buttton to add it to your phone (**Note: in a workshop setting, this may be tricky with so many buttons! Make sure you get matched to the correct buttton**)

![](https://i.imgur.com/lQCvZIG.png)

Name your Flic button a unique name, and click **Done**.

![](https://i.imgur.com/4g2aYRr.png)

Now we'll program our Flic button to send a text when clicked once. Select **Click >**.

![](https://i.imgur.com/SZdABfJ.png)

And navigate to **Tools**

![](https://i.imgur.com/QXiu0h0.png)

Select **Internet Request** (circled in pink below):

![](https://i.imgur.com/5ecOOYT.png)

Now, add the URL of our 1st function (the message/texting function) here. Select **GET** request. You do not need to provide Headers or change anything else here. **Save Action** to continue.

Once saved, test that your function works with 1 click! You should recieve a text shortly.

Do the same steps for the **Double Click >** option, navigate to Tools > Internet Request URL and add your call function URL as a GET request.

Save again, and test that your function works with a double-click! You should recieve a call shortly (don't click the button too many times- be patient!).

### Add Contact to Phone

Now for the cherry-on-top finishing touch! 🍒🍦

![](https://media.giphy.com/media/fMB1tYyIWercF01GmL/giphy.gif)

Add a contact to your phone for your Twilio number, and name it whatever you'd like. For example, if you'd like to trigger a fake call from "your BFF" you could upload a picture of The Rock to your contacts, and label it "The Rock". [Here's an example of mine](https://www.youtube.com/watch?v=lCpO16JjoM8) (I used "💕My Boyfriend💕" as the contact with an image of my boo):

![](https://camo.githubusercontent.com/306aca34bdd2e5664a12eb2f81bcafe047e8a5e7/68747470733a2f2f6d656469612e67697068792e636f6d2f6d656469612f6e6e6d394e4f6c56613879715762776172762f67697068792e676966)

If you've made it this far- CONGRATS! 🎊 You have successfully created 2 Azure Functions, connected them with Twilio, and are now able to trigger them from a Flic Button!

Here's a diagram you can print and hang on your fridge to remember this moment forever and ever (also, so you can review what we've just accomplished 😉):

![](https://res.cloudinary.com/practicaldev/image/fetch/s--wGlGfh8K--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1600/1%2AepHpHigBLPGaCK5tuxzn4w.png)

![](https://media.giphy.com/media/qK6ccDxjSmmre/giphy.gif)

If you're interested in learning more about Azure Functions and want to continue learning, here are some great resources to get started:

+ [Create your first function using Visual Studio Code](https://docs.microsoft.com/azure/azure-functions/functions-create-first-function-vs-code/?WT.mc_id=academic-0000-chcondon)

+ [Create a function in Azure that is triggered by a timer](https://docs.microsoft.com/azure/azure-functions/functions-create-scheduled-function/?WT.mc_id=academic-0000-chcondon)

+ [Create a function triggered by Azure Cosmos DB](https://docs.microsoft.com/azure/azure-functions/functions-create-cosmos-db-triggered-function/?WT.mc_id=academic-0000-chcondon)

+ [Create a function triggered by Azure Blob storage](https://docs.microsoft.com/azure/azure-functions/functions-create-storage-blob-triggered-function/?WT.mc_id=academic-0000-chcondon)

+ [Create a function triggered by Azure Queue storage](https://docs.microsoft.com/azure/azure-functions/functions-create-storage-queue-triggered-function/?WT.mc_id=academic-0000-chcondon)

+ [Azure Functions developer reference](https://docs.microsoft.com/azure/azure-functions/functions-reference/?WT.mc_id=academic-0000-chcondon) (provides more technical information about the Azure Functions runtime and a reference for coding functions and defining triggers and bindings)

+ [Testing Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-test-a-function/?WT.mc_id=academic-0000-chcondon)

+ [Azure Functions scale and hosting](https://docs.microsoft.com/azure/azure-functions/functions-scale/?WT.mc_id=academic-0000-chcondon)

+ [Learn more about Azure App Service](https://docs.microsoft.com/azure/app-service/overview/?WT.mc_id=academic-0000-chcondon)
