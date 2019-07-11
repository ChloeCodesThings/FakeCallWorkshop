# Chloe's Fake Call Workshop
A workshop to build your own fake boyfriend/boss/sibling/co-worker call with Azure &amp; Twilio

Today we will build a fake calling app using:

+ ⚡ [Azure Functions](https://azure.microsoft.com/en-us/services/functions/?WT.mc_id=github-workshop-chcondon)
+ ☎️ [Twilio](https://www.twilio.com/)
+ 🔘A [Flic button](http://flic.io/shop/flic-1pack?aff=10)
+ 📱Your cellphone 

Before we begin, if you're looking for a quick summary and overview on Azure Functions, I reccomend [starting here with our documentation](https://docs.microsoft.com/en-us/azure/azure-functions/?WT.mc_id=github-workshop-chcondon), or taking 4 minutes to read in more detail [how to create your first Azure Function](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function/?WT.mc_id=github-workshop-chcondon), so you have some context on how to use functions within Azure.

You can learn more about the original project [in my blog post](https://dev.to/azure/an-ambivert-s-guide-to-azure-functions-27b8)! And [the GitHub Repo](https://github.com/ChloeCodesThings/sos-plz-save-me) is open, available, and interested in contributions!

Happy coding, friends!
-Chloe 🎀 

## Let Us Begin!
Today we will build a fake calling app using Azure Functions, Twilio, and a Flic button. We will start by creating a Function App in Azure. Then we will create a Twilio account, create 2 Azure Functions, and test it out on our phones.

Here's a diagram of what we'll be doing:

![](https://res.cloudinary.com/practicaldev/image/fetch/s--wGlGfh8K--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/1600/1%2AepHpHigBLPGaCK5tuxzn4w.png)

### Create an Azure Function
For the sake of easy to understand visuals/screenshots for this workshop, we'll be using the [Azure portal](https://azure.microsoft.com/en-us/free/?WT.mc_id=github-workshop-chcondon) to create this. You can also use [VS Code](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-vs-code/?WT.mc_id=github-workshop-chcondon), the [Azure CLI](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function-azure-cli/?WT.mc_id=github-workshop-chcondon), etc. With Azure Functions you are given the the ability to code and test Functions locally on your machine without having to deploy to the cloud every single time you want to test (a huge time saver!).



