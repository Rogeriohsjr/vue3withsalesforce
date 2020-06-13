# vue3withsalesforce

This project shows how to add vuejs 3 into salesforce.

Here are the steps that we will take:

1. Making sure you have a Salesforce Org
2. Installing Vuejs
3. Setting up vuejs to work with Salesforce
4. Deploying your vue app to Salesforce


# 1. Make sure you have a DevOrg that you can work.
1. Any org you can create a domain and component should work.
1.1. You also need the My Domain.
1.1. Here is a quickly doc on how to do it.


# 2. Installing Vue

1. Create a folder called vue3withSalesforce
    1. mkdir vue3withSalesforce
2. Access the folder and install vue3 using VueCli
    1. cd vue3withSalesforce
    2. npm install -g @vue/cli
    3. vue create vue-app
    4. I selected every option as default on vue installation.
3. Testing your app
    1. cd vue-app
    2. npm run serve


# 3. Setting up vuejs to work with Salesforce

1. Changing Vue Configuration
    1. We also need to tell vue to change the path of the file.
    2. Create a file in the root(same place as you have the package.json) called vue.config.js
    3. Add this content in the vue.config.js

module.exports = {
    // options...
    publicPath: './',
};

# 4. Deploying your vue app to Salesforce

1. Let’s compile and deploy the app to Salesforce
2. In the vue-app folder build the app
    1. npm run build
        1. This command will create a dist folder
3. Creating the static resource
    1. Go inside of dist folder in your Windows Explore or Finder
    2. Select all the files and zip/compress that
        1. Do NOT zip the dist folder, zip only the files
    3. You can give any name, Ex. vueapp
    4. Go to your salesforce org
    5. Setup >> Static Resources >> Import that file
4. Now we need to create the Salesforce Container that will use that static file.
5. Open the Developer Console
6. File >> New >> Lightning Component
    1. Name: vueappbundle
    2. Enable the Lightning Page.
    3. Click on Submit.
7. The component will open for you.
8. Click on Component
9. Add the code below
<aura:component implements="flexipage:availableForAllPageTypes" access="global" >
	<lightning:container src="{!$Resource.vueapp + '/index.html'}" />
</aura:component>
10. Add these styles to make your iframe responsive.
/** Making the iFrame Responsive - Begin **/
.THIS.lightningContainer>iframe{
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    width: 100%;
    height: 100%;
}

.THIS.lightningContainer {
    position: relative;
    overflow: hidden;
    width: 100%;
    padding-top: 56.25%;
}
/** Making the iFrame Responsive - End **/
1. 
2. Your component is ready to be added into a page.

Adding the Component in a Record Page.

1. Go to Services App in Salesforce
2. Click on Account Tab
3. Select an Account
4. Click on the Engine Icon close to your name, and click Edit Page.
5. In your left menu, you will see your component
6. Drag and drop your component and it should render.