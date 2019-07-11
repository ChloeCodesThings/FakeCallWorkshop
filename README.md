# Chloe's Fake Call Workshop
A workshop to build your own fake boyfriend/boss/sibling/co-worker call with Azure &amp; Twilio

Today we will build a fake calling app using:

+ ⚡ [Azure Functions](https://azure.microsoft.com/en-us/services/functions/?WT.mc_id=github-workshop-chcondon)
+ ☎️ [Twilio](https://www.twilio.com/)
+ 🔘A [Flic button](http://flic.io/shop/flic-1pack?aff=10)
+ 📱Your cellphone 

Before we begin, if you're looking for a quick summary and overview on Azure Functions, I reccomend [starting here with our documentation](https://docs.microsoft.com/en-us/azure/azure-functions/?WT.mc_id=fakecallworkshop-github-chcondon), or taking 4 minutes to read in more detail [how to create your first Azure Function](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function/?WT.mc_id=fakecallworkshop-github-chcondon), so you have some context on how to use functions within Azure.

You can learn more about the original project [in my blog post](https://dev.to/azure/an-ambivert-s-guide-to-azure-functions-27b8)! And [the GitHub Repo](https://github.com/ChloeCodesThings/sos-plz-save-me) is open, available, and interested in contributions!

Happy coding, friends!
-Chloe 🎀 

## Let Us Begin!
Today we will build a fake calling app using Azure Functions, Twilio, and a Flic button. We will start by creating a Function App in Azure. Then we will create a Twilio account, create 2 Azure Functions, and test it out on our phones.

Here's a diagram of what we'll be doing:

![](https://res.cloudinary.com/practicaldev/image/fetch/s--wGlGfh8K--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1600/1%2AepHpHigBLPGaCK5tuxzn4w.png)

### Create an Azure Account!
Create your own Azure account for free [here](https://azure.microsoft.com/en-us/free/?WT.mc_id=fakecallworkshop-github-chcondon)!

### Create an Azure Function Resource
For the sake of easy to understand visuals/screenshots for this workshop, we'll be using the [Azure portal](https://azure.microsoft.com/en-us/free/?WT.mc_id=fakecallworkshop-github-chcondon) to create this. You can also use [VS Code](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-vs-code/?WT.mc_id=fakecallworkshop-github-chcondon), the [Azure CLI](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function-azure-cli/?WT.mc_id=fakecallworkshop-github-chcondon), etc. With Azure Functions you are given the the ability to code and test Functions locally on your machine without having to deploy to the cloud every single time you want to test (a huge time saver!).

To create an Azure function, you can just start from the Get Started menu and select Function App.

![](https://res.cloudinary.com/practicaldev/image/fetch/s--TnBmEJTg--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1200/1%2A0yImy-SW4IsrRgJN_UjP7Q.png)

Then you’ll need to fill in some basic info about your function here. Including the app name, the Azure subscription you’d like to use, a [resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview?WT.mc_id=devto-blog-chcondon/?WT.mc_id=fakecallworkshop-github-chcondon) (we will create a new one in this case), the Operating System you’d like to use, the [hosting plan](https://docs.microsoft.com/en-us/azure/azure-functions/functions-scale/?WT.mc_id=fakecallworkshop-github-chcondon) (I’m using consumption), the location I’d like to use (I’m in California, so West US 2 is usually my default), the runtime stack I’d like to use (I’m using JavaScript in this case), and I have the option to create new [storage](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction/?WT.mc_id=fakecallworkshop-github-chcondon) or use existing. I created a new one in this case.

![](https://res.cloudinary.com/practicaldev/image/fetch/s--aDEMnm-V--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1200/1%2AVqJso6NwUPMUnLDj-Mx-WA.png)

Once you have all these filled out, you can go ahead and deploy! Wait about a minute or two, then watch for the **Deployment succeeded** message.

Woo! If you followed those steps, we have our resource! Select **Go to resource** to view your new Function App. 

### Create Your Azure Functions
Now let's add our functions to our app. Select in-portal.
![](https://res.cloudinary.com/practicaldev/image/fetch/s---bwMvA0C--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1600/1%2AR7td7o0irI7STDwRsCnDDg.png)

And select Webhook + API
![](https://res.cloudinary.com/practicaldev/image/fetch/s--V8ROjeS5--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1600/1%2AOqn6uiCHsF2UStDnhj_T2w.png)

It will take about a minute to deploy and then you’ll have a fresh new Azure Function waiting to be called.

The default code is a simple hello world app. If you paste the function URL into your browser’s address bar. Add the query string value &name= to the end of this URL and press the Enter key on your keyboard to execute the request. You should see the response returned by the function displayed in the browser. **Try doing this once!**

### Let’s Create a Fake Boyfriend
##### (or aunt, or cousin, or coworker- whatever!)


