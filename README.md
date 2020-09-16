# repo

- If you want to upload a maven dependency here, execute the command:

```sh
mvn install:install-file -DgroupId=org.myfile -DartifactId=myfile -Dversion=4.0.0 -Dfile=myfile.jar \
-Dpackaging=jar -DgeneratePom=true -DlocalRepositoryPath=/home/user/otimizes/repo  -DcreateChecksum=true
```
