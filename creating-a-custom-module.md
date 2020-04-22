# Extending with a Custom Module

This section describes the process and rationale for creating a custom module on top of UgandaEMR. This is a recommended approach when customizations cannot be handled within the MoH guidelines to which UgandaEMR adheres.

## Prerequisites

See section for [Setting up a development environment](setup-dev-environment.md)

## Module Setup

The steps for creating a custom module that extends UgandaEMR are below: 1. Use the OpenMRS SDK to create a Reference Application module `mvn openmrs-sdk:create-project -Dtype=referenceapplication-module` 2. Create a new blank text file, openmrs-distro.properties and add it to api/src/main/resources folder 3. Add the following content to the file `name=UgandaEMR My Customization version=${project.parent.version} distro.aijar-api=${ugandaemrVersion} distro.aijar-api.groupId=org.openmrs.module omod.ugandaemr-iss=${project.parent.version}` 4. The versions are loaded from the dependencies in the api/pom.xml file for the module, an example is [https://github.com/METS-Programme/openmrs-module-aijar/blob/master/pom.xml](https://github.com/METS-Programme/openmrs-module-aijar/blob/master/pom.xml) 5. Add the following build information to the omod/pom.xml which will help build the custom war file

```text
<build>
        <finalName>${project.parent.artifactId}-${project.parent.version}</finalName>

        <plugins>
            <plugin>
                <groupId>org.openmrs.maven.plugins</groupId>
                <artifactId>maven-openmrs-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.openmrs.maven.plugins</groupId>
                <artifactId>openmrs-sdk-maven-plugin</artifactId>
                <version>3.13.1</version>
                <executions>
                    <execution>
                        <id>build-distro</id>
                        <phase>install</phase>
                        <goals>
                            <goal>build-distro</goal>
                        </goals>
                        <configuration>
                            <dir>${project.build.directory}/docker</dir>
                            <bundled>true</bundled>
                            <distro>${project.build.directory}/classes/openmrs-distro.properties</distro>
                            <batchAnswers>
                                <param>n</param>
                            </batchAnswers>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
```

1. 
