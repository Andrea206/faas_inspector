# Faas Inspector Testing and Deployment Tools

One goal of FaaS Inspector is to support multiple FaaS platforms. Currently AWS Lambda, Google Cloud Functions, IBM Cloud Functions/OpenWhisk, and Azure Function are the supported platforms. A few scripts have been developed to aid in development, deployment, and testing of each platform.

### Project Structure
The project structure is meant to simplify deploying onto each of the supported platforms.

    📁 nodejs_template
        📁 src
            function.js
            Inspector.js
            package.json
        📁 test
            📁 node_modules
                ...
            config.json
            publish.sh
            partestcpu.sh
            local.js
        📁 platforms  
            ...
  

### 📁 src Folder

The src folder contains all of the code for your function. 

  * [**Inspector.js**](../src/Inspector.js) is the FaaS Inspector itself and is completely independent of any files or folders in this project. If you do not plan to use this file sctructure, Inspector.js can be used and moved to any Node.js project.
  
  * [**function.js**](../src/function.js) file is the handler that each cloud provider will execute. 

  * [**package.json**](../src/package.json) is where 3rd party dependencies must be defined (**WARNING:** If you are deploying onto Azure Functions, dependencies must also be downloaded into test/node_modules). 
    
### 📁 test Folder

This folder contains tools to help test and deploy serverless functions onto each supported platform. For more detailed documentation please see the comments at the beginning of each file. 

  * [**config.json**](./config.json) contains all of the neccessary variables to deploy a function. This includes the name of the function, the Azure Function app name, and other information.
  * [**publish.sh**](./publish.sh) is a script used to deploy a function onto each platform. This requires each each cloud providers CLI to be installed and properly configured.
  * [**partestcpu.sh**](./partestcpu.sh) is a script to test a function after it has been deployed. The script can make many calls in parallel to create stress on each platform.
  * [**local.js**](./local.js) is an additional handler used to execute a function locally. This can be useful to test a function before deploying onto the cloud.
    
### 📁 platforms Folder

This folder contains all of the platform specific files needed to deploy onto each cloud provider. NONE of these files need to be edited to deploy a function. The publish.sh script copies these files into the src folder, constructs the correct folder structure, deploys the function, and then cleans up the src folder back to its original state.
