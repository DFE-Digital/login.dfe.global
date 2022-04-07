# Signin Global pipeline

Signin Global pipeline deploys azure keyVault in the all or selected environments

## Audience

This document refers to the DevOps engineers who will maintain this pipeline.Also, the responsibility to keep this document up to date with the latest information

## Prerequizet

1. Resources from DFE-Digital/operations-devops-pipeline-templates repo that code find in the .vsts.ci.yml lines 2-7

2. Use of two variables:
    - Group variable platform-global

## Stages

1. Deployment stage, repeats for all environments (dev, test, int, pp, pr) using the deploy.yaml and sending 7 parameters for the deployment that are specified for the for each environment.
    - Parameters: 
        - serviceConnection: That connects the subscription with the Azure DevOps for deployment. This value is located in the Group variable platform-global
        - subscriptionId: That is the subscription. This value is located in the Group variable platform-global we need to deploy
        - applicationName: The name of the application we deploy and set up in the Prerequizet as applicartionName
        - environmentId: The Id that uses for each environment.
        - environmentName: The name of each environment we deploy.
        - platformVariableGroupName: This variable group contains information that is used for the deployment of recourses in the specific environment. Located in the azure DevOps library 
    - For more information on what parameters to need for each environment check the appendix table of enviroments values 
    - What is deployed check [here](deployResources.md)
  
2. Permission stage repeats for all environments (dev, test, int, pp, pr) after each deployment stage using permissions.yml for set keyVault policies

# Appendix

1. ## Table of enviroments values
    Enviroment | Environment Id | Environment Name | serviceConnection | subscriptionId | platformVariableGroupName
    --- | --- | --- | --- | --- | ---
    s141-dfesignin-development | d01 | dev |devServiceConnection  | devSubscriptionId | platform-dev
    s141-dfesignin-test | t01 | test | testServiceConnection | testSubscriptionId | platform-test
    s141-dfesignin-test(INT) | t03 | int | testServiceConnection | testSubscriptionId | platform-int
    s141-dfesignin-test(PreProd) | t02 | pp | testServiceConnection | testSubscriptionId | platform-pp
    s141-dfesignin-production | p01 | pr | prodServiceConnection | prodSubscriptionId | platform-pr





