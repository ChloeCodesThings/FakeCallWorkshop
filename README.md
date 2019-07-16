# Chloe's Fake Call Workshop
*A workshop to build your own fake boyfriend/boss/sibling/co-worker call with Azure &amp; Twilio*

Today we will build a fake calling app using:

+ ⚡ [Azure Functions](https://azure.microsoft.com/en-us/services/functions/?WT.mc_id=github-workshop-chcondon)
+ ☎️ [Twilio](https://www.twilio.com/)
+ 🔘A [Flic button](http://flic.io/shop/flic-1pack?aff=10)
+ 📱Your cellphone 

Before we begin, if you're looking for a quick summary and overview on Azure Functions (or found this page early and would like to get a headstart), I reccomend [starting here with our documentation](https://docs.microsoft.com/en-us/azure/azure-functions/?WT.mc_id=fakecallworkshop-github-chcondon), or taking 4 minutes to read in more detail [how to create your first Azure Function](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function/?WT.mc_id=fakecallworkshop-github-chcondon), so you have some context on how to use functions within Azure.

You can learn more about the original project [in my blog post](https://dev.to/azure/an-ambivert-s-guide-to-azure-functions-27b8)! And [the GitHub Repo](https://github.com/ChloeCodesThings/sos-plz-save-me) is open, available, and interested in contributions!

Happy coding, friends!
-Chloe 🎀 

## Let Us Begin!
Today we will build a fake calling app using Azure Functions, Twilio, and a Flic button. We will start by creating a Function App in Azure. Then we will create a Twilio account, create 2 Azure Functions, and test it out on our phones.

Here's a diagram of what we'll be doing:

![](https://res.cloudinary.com/practicaldev/image/fetch/s--wGlGfh8K--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1600/1%2AepHpHigBLPGaCK5tuxzn4w.png)

### Create an Azure Account!
If you don't already have one, create an Azure account for free [here](https://azure.microsoft.com/en-us/free/?WT.mc_id=fakecallworkshop-github-chcondon)!

I know what you may be thinking... "but Chloe- I'm a developer... this is much too bright for me!". Don't worry- there's a dark mode option. 😎

![](https://i.imgur.com/i2qeQFm.png)

### Create an Azure Function Resource
For the sake of easy to understand visuals/screenshots for this workshop, we'll be using the [Azure portal](https://azure.microsoft.com/en-us/free/?WT.mc_id=fakecallworkshop-github-chcondon) to create this. You can also use [VS Code](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-vs-code/?WT.mc_id=fakecallworkshop-github-chcondon), the [Azure CLI](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function-azure-cli/?WT.mc_id=fakecallworkshop-github-chcondon), etc. With Azure Functions you are given the the ability to code and test Functions locally on your machine without having to deploy to the cloud every single time you want to test (a huge time saver!).

To create an Azure Function, you can just start from the Get Started menu and select Function App.

![](https://res.cloudinary.com/practicaldev/image/fetch/s--TnBmEJTg--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1200/1%2A0yImy-SW4IsrRgJN_UjP7Q.png)

Then you’ll need to fill in some basic info about your function here. Including the app name, the Azure subscription you’d like to use, a [resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview?WT.mc_id=devto-blog-chcondon/?WT.mc_id=fakecallworkshop-github-chcondon) (create a new one in this case), the Operating System you’d like to use, the [hosting plan](https://docs.microsoft.com/en-us/azure/azure-functions/functions-scale/?WT.mc_id=fakecallworkshop-github-chcondon) (I’m using consumption), the location you’d like to use (I’m based in California, so West US 2 is usually my default), the runtime stack I’d like to use (I’m using JavaScript in this case), and we have the option to create new [storage](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction/?WT.mc_id=fakecallworkshop-github-chcondon) or use existing. We'll create a new one in this case.

![](https://i.imgur.com/rEdUcjS.png)

Once you have all these filled out, you can go ahead and deploy! Wait about a minute or two, then watch for the **Deployment succeeded** message.

🎊 Woo! If you followed those steps, we have our resource! Select **Go to resource** in your notifications (top right corner) to view your new Function App. 

### Create Your First Azure Function
Now we'll add our functions to our app, starting with a function to send a text message.

Select in-portal.
![](https://res.cloudinary.com/practicaldev/image/fetch/s---bwMvA0C--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1600/1%2AR7td7o0irI7STDwRsCnDDg.png)

And select Webhook + API
![](https://res.cloudinary.com/practicaldev/image/fetch/s--V8ROjeS5--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1600/1%2AOqn6uiCHsF2UStDnhj_T2w.png)

It will take about a minute to deploy and then you’ll have a fresh new Azure Function waiting to be called.

The default code is a simple hello world app. If you paste the function URL into your browser’s address bar. Add the query string value &name= to the end of this URL and press the Enter key on your keyboard to execute the request. You should see the response returned by the function displayed in the browser.

**Try doing this once!** Add the URL with *&name=your-name-here* added to it, and test out that the function works in your browser.

### Let’s Create a Fake Boyfriend (or aunt, or cousin, or coworker- whatever!) with Twilio
In a new tab, head over to [Twilio.com](https://www.twilio.com/) and sign up for an account if you don't have one already. Add a trail phone number to your account that has calling and SMS capabilitites (if you'd like to not work in trial mode- you can use code **CHLOE20** to upgrade your account at any point).

Once you have a trail number, you'll see a **ACCOUNT SID** and **AUTH TOKEN** created for your number. 🚨 Do not share/screenshot/commit these numbers 🚨 Think of them as your username and password for our Twilio number- we will securely store these in Azure shortly.

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

**Take a moment to read and understand the code.** You'll see that we're setting our accountSid & authToken (with credentials we have set in our function's Application Settings). We then have a function that creates a message sent from SENDER_NUMBER, to RECIPIENT_NUMBER (with credentials we have set in our function's Application Settings as well). Next, we're logging that our message is sent, and setting our context as done. Alternatively , if there's an error, we'll log it and set our context to done.

Once you have an understanding of this code, click **Save**.

### Add package.json file to Function

Add a package.json file to your function. You can do this by navigating to the top-right corner of your function, and adding a file as pictured below:

![](https://i.imgur.com/EWUt68c.png)

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

Click **Save**, and navigate back to your **index.js** file.

### Install the Twilio Node.js Module

Install the Twilio Node helper library using npm. This will install the twilio module so that Node.js scripts in the current directory can use it. Access the Azure console at the bottom of the screen

![](https://i.imgur.com/fY6npig.png)

In the console, enter the following:

```
npm install twilio
```

This may take a couple minutes (if you're looking for a good time to go grab a coffee/LaCroix/bathroom break- this is it!). 

You may see 2 warnings/notices here- you can ignore these.

### Add Credential Values Securely in Azure

Head over to **Configuration** under your Function App in the Azure portal (highlighted in pink, below).

![](https://i.imgur.com/WDjoqff.png)

Add 2 new application settings named **TWILIO_SID** and **TWILIO_TOKEN**- storing with them the credentials provided to us from Twilio.

Additionally, add a setting for **SENDER_NUMBER** (adding your Twilio trial number in the format of plus-sign, country code, and number like so: *+12222222222* as the value) as well as **RECIPIENT_NUMBER** (add your cell phone number as the value for now to test our app).

![](https://i.imgur.com/LNf0Sxy.png)

😳 Totally lost? Can't find your credentials? Log into [Twilio](https://www.twilio.com/) to find them!

Click **Save**, and navigate back to your function in the console.

Click the **Run** button at the top of your function. Your logs should pop up and show that your function has been called. If all goes smoothly, you should receive a text saying "Woohoo- it worked!"

### Create Your Second Azure Function

Now we'll add our 2nd function to our app- this time, with the code to send a call.

Add another function to your app (as we did before on our 1st function), and select **HTTPTrigger** again.

### Add Sample Code to our Function

In the Azure portal, replace the exsiting code wiith the following code in your index.js file:

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

**Take a moment to read and understand the code for your call function.** You'll see that we're again setting our accountSid & authToken (with credentials we have set in our function's Application Settings). We then have a function that creates a call sent from SENDER_NUMBER, to RECIPIENT_NUMBER, with a url of TWIML_URL (set-up with credentials we have set in our function's Application Settings as well). Next, we're logging that our call is sent, and setting our context as done. Alternatively , if there's an error, we'll log it and set our context to done.

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

Again, this may take a couple minutes (if you're looking for a good time to go grab *another* coffee/LaCroix/bathroom break- this is it!).

You may see 2 warnings/notices here- you can ignore these.

Our configurations are already set in Azure, so no need to add our **TWILIO_SID**, **TWILIO_TOKEN**, **SENDER_NUMBER**, or **RECIPIENT_NUMBER** again.

### Create Twilio Asset

Now we'll create a Twilio Asset to hold our fake call's recorded voice message.

Download the following MP3 by [clicking here](https://github.com/ChloeCodesThings/FakeCallWorkshop/raw/master/sampleaudio.mp3).

Head back to Twilio, and navigate to Runtime > Assets in the left-side navigation.

Add the Mp3 file and copy the path.

### Create a TwiML Bin

Navigate to Runtime > TwiML Bins in the left-side navigation.

We'll now create a TwiML Bin. TwiML Bins allow you to write TwiML that Twilio will host for you - so you can quickly prototype a solution without spinning up a web server.

Add the following to your TwiML bin (make sure to replace **URL-OF-YOUR-TWILIO-ASSET** with the url of the Twilio Asset you just created!):

```
<?xml version="1.0" encoding="UTF-8"?>

<Response>
  <Say voice="man">Hey- congrats! Everything is working. You are awesome. You did it- yay!</Say>
  <Play>URL-OF-YOUR-TWILIO-ASSET</Play>
</Response>
```

This TwiML will speak the <Say> text, and <Play> the URL of the Twilio Asset URL you provide it.

Save your TwiML bin, and **copy the URL**.

### Add TwiML URL to Application Settings

Navigate to **Application Settings** once again to add **TWIML_URL** with the value of your recently created/copied TwiML URL.

Click **Save**.

### Test call

Navigate to your call function and click **Run** to test the call.

If all goes well, you'll soon get a call and will be a victim of Rick-Rolling! 😁☎️

### Add URL to Flic Button

(additional directions/screenshots coming soon!)

- Download Flic app
- For Click command, navigate to Tools > Internet Request URL and add message function as a GET request.
- For Double Click command, navigate to Tools > Internet Request URL and add call function as a GET request.
- Test Click + Double Click on button to trigger text + call

### Add Contact to Phone
