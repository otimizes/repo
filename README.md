# repo

### Jar deploy
- If you want to upload a maven dependency jar here, execute the command:

```sh
mvn install:install-file -DgroupId=org.myfile -DartifactId=myfile -Dversion=4.0.0 -Dfile=myfile.jar \
-Dpackaging=jar -DgeneratePom=true -DlocalRepositoryPath=/home/user/otimizes/repo  -DcreateChecksum=true
```
### Project deploy
- If you want to deploy a java project here, add that to your pom.xml and execute mvn deploy:

```xml
<profiles>
    <profile>
        <id>default</id>
        <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
        <build>
            <plugins>
                <plugin>
                    <artifactId>maven-deploy-plugin</artifactId>
                    <version>2.8.2</version>
                    <configuration>
                        <altDeploymentRepository>internal.repo::default::file://${project.build.directory}/mvn-repo</altDeploymentRepository>
                    </configuration>
                </plugin>
                <plugin>
                    <groupId>com.github.github</groupId>
                    <artifactId>site-maven-plugin</artifactId>
                    <version>0.12</version>
                    <configuration>
                        <merge>true</merge>
                        <message>Maven artifacts for ${project.version}</message>
                        <noJekyll>true
                        </noJekyll>
                        <outputDirectory>${project.build.directory}/mvn-repo</outputDirectory>
                        <branch>refs/heads/mvn-repo</branch>
                        <includes>
                            <include>modules/architecture-representation</include>
                            <include>modules/opla-core</include>
                            <include>modules/opla-domain</include>
                            <include>modules/opla-patterns</include>
                            <include>modules/opla-persistence</include>
                        </includes>
                        <repositoryName>repo</repositoryName>
                        <repositoryOwner>otimizes</repositoryOwner>
                    </configuration>
                    <executions>
                        <execution>
                            <goals>
                                <goal>site</goal>
                            </goals>
                            <phase>deploy</phase>
                        </execution>
                    </executions>
                </plugin>
            </plugins>
        </build>
        <distributionManagement>
            <repository>
                <id>internal.repo</id>
                <name>Temporary Staging Repository</name>
                <url>file://${project.build.directory}/mvn-repo</url>
            </repository>
        </distributionManagement>
    </profile>
</profiles>
```

Obs: Do not forget to add a server xml tag in your .m2/settings.xml
