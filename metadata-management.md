# Metadata Management

Metadata is used to configure forms and reports for data capture and reporting. The metadata is configured via Java classes, CSV \(comma delimited\) data files, XML files, SQL scripts and meta-data sharing packages.

At startup all the metadata is reset to the versions available in code to ensure that the setup is consistent across the different installations.

## Encounter Types

1. Add the definition of the encounter type to [https://github.com/METS-Programme/openmrs-module-aijar/blob/master/api/src/main/java/org/openmrs/module/aijar/metadata/core/EncounterTypes.java](https://github.com/METS-Programme/openmrs-module-aijar/blob/master/api/src/main/java/org/openmrs/module/aijar/metadata/core/EncounterTypes.java)
2. Install the newly defined encounter type through the CommonMetadataBundle at [https://github.com/METS-Programme/openmrs-module-aijar/blob/master/api/src/main/java/org/openmrs/module/aijar/api/deploy/bundle/CommonMetadataBundle.java](https://github.com/METS-Programme/openmrs-module-aijar/blob/master/api/src/main/java/org/openmrs/module/aijar/api/deploy/bundle/CommonMetadataBundle.java)

## Patient Identifiers

1. Add the defintion of the identifier type to [https://github.com/METS-Programme/openmrs-module-aijar/blob/master/api/src/main/java/org/openmrs/module/aijar/metadata/core/PatientIdentifierTypes.java](https://github.com/METS-Programme/openmrs-module-aijar/blob/master/api/src/main/java/org/openmrs/module/aijar/metadata/core/PatientIdentifierTypes.java)
2. Install the newly defined identifier through the CommonMetadataBundle at [https://github.com/METS-Programme/openmrs-module-aijar/blob/master/api/src/main/java/org/openmrs/module/aijar/api/deploy/bundle/CommonMetadataBundle.java](https://github.com/METS-Programme/openmrs-module-aijar/blob/master/api/src/main/java/org/openmrs/module/aijar/api/deploy/bundle/CommonMetadataBundle.java)

## Person Attributes

## Concepts

## Roles

## Privileges

