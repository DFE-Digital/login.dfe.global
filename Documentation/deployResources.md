# Signin Global Deploy Resources

The deploy.yml deploys the global keyVault

## Variables

The deploy.yml variables for the deployment of the resources

 1. Group variable that is send from the .vsts.ci.yml
 2. resourceGroupName that is value create be compine the projectIdentifier, environmentId, globalName & globalSuffix
 3. globalName with value signin
 4. globalSuffix with value global

## Steps of Deployment

1. Calling the /Infrastructure/steps/deploy-template.yml from the DFE-Digital/operations-devops-pipeline-templates and pass 8 parameters.

    - Parameters:
        - serviceConnection: That is passed as Parameter from .vsts.ci.yml
        - subscriptionId: That is passed as Parameter from .vsts.ci.yml
        - resourceGroupName: That is created in the variables
        - location: That is an empty as not been set in .vsts.ci.yml
        - tags: They are part of the group variable that is sent from the .vsts.ci.yml 
        - templateFilePath: The file path sends the location of the arm template.json that will deploy. That is located in arm/template.json
        - armParameterOverrideString: Sending the parameters to need override in the template.json
        - processOutputs: Boolean variable when `false` shows the output results
    
    - Resources that Deployed from the template.json:
        - KeyVault

        *Note*: The above resource uses a template of deployment from the DFE-Digital/login.dfe.infrastructure repo. Any changes to how resources are deployed need to update the above repo infrastructure and the template URL need to update in the branch location that changes happen until the move to master
    
    - Outputs from the template.json:
        
