# Azure Guidance - VistA-in-the-Cloud

The guidelines below will ensure that you are able to utilize Azure to perform work in a manner that is both effcient and meets all stated requirments.  Please review the guidelines and utlize the example templates to help speed along deployments. 

**Note:** *The guidance below can be modified if required, to request modifications please contact OSEHRA for approval*

## Approved Locations - Azure Regions

For the purposes of this project, all deployments will occur within the Azure Region, "US Gov Virginia".  When createing templates or deploying resources via the [Azure portal](http://portal.azure.us), please be sure to select Virginia as the deployment location.

## Approved Virtual Machine Sizes

The five following Virtual Machine sizes are avaliable for use during this project.  When deploying virtual machines, please utilize one of the five SKU as follows:

Name | CPU Count | RAM (GB) | Maximum Number of Disks | Maximum Volume Size (TB)
---- | --------- | --- | ----------------------- | -------------------
Standard_D1_v2 | 1 | 3.5 | 2 | 2
Standard_D2_v2 | 2 | 7 | 4 | 4
Standard_D3_v2 | 4 | 14 | 8 | 8
Standard_D12_v2 | 4 | 28 | 8 | 8
Standard_D13_v2 | 8 | 56 | 16 | 16

## Scheduled Tasks - VM Power States

All Azure resource groups and virtual machines are evaulated once per hour.  The evauluation is a simple mechanism which determines if the virtual machines need to be in a powered on or powered off state.  When the script runs, it utilizes the following logic:  If the resource group or virtul machine has a tag named "AutoShutdownPolicy" applied, then the value of the tag is evaluated according to the table below. 

* If the tag does not exist, then no action is taken.
* If the value of the tag is malformed/undreadable, then the VM is started or left on; but not powered off.

Shown below are examples of the value of the AutoShutdownPolicy tag and the resulting action which will take place.

**Note:** Please [convert](http://www.timeanddate.com/worldclock/converter.html) all times to GMT/UTC time zone to ensure proper execution.  

Description | Tag Value
----------- | ---------
Shut down from 10PM to 6 AM UTC every day | 10pm -> 6am
Shut down from 10PM to 6 AM UTC every day (different format, same result as above) | 22:00 -> 06:00
Shut down from 8PM to 12AM and from 2AM to 7AM UTC every day (bringing online from 12-2AM for maintenance in between) | 8PM -> 12AM, 2AM -> 7AM
Shut down all day Saturday and Sunday (midnight to midnight) | Saturday, Sunday
Shut down from 2AM to 7AM UTC every day and all day on weekends | 2:00 -> 7:00, Saturday, Sunday
Shut down on Christmas Day and New Year’s Day | December 25, January 1
Shut down from 2AM to 7AM UTC every day, and all day on weekends, and on Christmas Day | 2:00 -> 7:00, Saturday, Sunday, December 25
Shut down always – I don’t want this VM online, ever |0:00 -> 23:59:59

**Credit/Reference:** https://automys.com/library/asset/scheduled-virtual-machine-shutdown-startup-microsoft-azure

## Azure Templates

The following templates will deploy the specified version of CentOS (6.x, 7.x) and execute a bash script.  The first template deploys a single virtual machine  The second deploys virtual machines at scale.  Please start with the first to get familiar, and then move to the second if needed.

*  Template One :  [Simple Linux - Solo](https://github.com/OSEHRA/VistA-in-the-Cloud/tree/master/Azure/Simple%20Linux%20-%20Solo)
*  Template Two :  Work in progress (Coming soon)

## Azure Resource Manager - Learning Templates

The following links will be of benifit when begining development of Azure Resource Manager (ARM) templates.

* [Azure Resource Manager Documentation](https://docs.microsoft.com/en-us/azure/azure-resource-manager/)
* [Azure Resource Manager - Create your first ARM template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template)
* [Azure Resource Manager - Deploy Multiple Instances of a Resource](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-multiple)