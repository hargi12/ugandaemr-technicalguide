# Guidelines for Customizing UgandaEMR

## Guidelines for Customizing and Building on UgandaEMR

This section provides guidelines for customizing and building on top of UgandaEMR to: 1. Ensure customizations are not lost during upgrades 2. New features built on top of UgandaEMR do not duplicate existing functionality to eliminate duplication of efforts 3. Customizations fit into the planned and future architecture

The approaches to be used will include and not be limited to the following: 1. Feature toggles - features can be turned on and off using feature toggles  
2. Permission Restrictions - features can only be available when specific security permissions are added to the user profile 3. Custom modules - this is an option for features that may not be needed by the rest of the UgandaEMR community

### Feature Toggles

The approach for feature toggles is as follows:

1. Add a global property ugandaemr.XXXX whose default value is false or an existing value being used within UgandaEMR 
2. Add checks to expose the new functionality only when the default value is changed 

## Permission Restrictions

This may need to done in a custom module in order to ensure that the changes can be turned off when needed

## Custom Modules

This approach is used to isolate specific functionality from UgandaEMR, however concepts need to coordinated with MoH and METS to ensure that future upgrades do not over-write them.

This process is further detailed in [Extending with a Custom Module](creating-a-custom-module.md) section

