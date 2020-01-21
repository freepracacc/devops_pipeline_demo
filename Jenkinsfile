// Powered by Infostretch 

timestamps {

node () {

	stage ('Job1 - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '75434b7f-53ce-456d-91f4-3564024c55e4', url: 'https://github.com/freepracacc/devops_pipeline_demo.git']]]) 
	}
	stage ('Job1 - Build') {
 			// Shell build step
sh """ 
#!/bin/bash
echo ********- Starting CI CD Pipeline Tasks- ********
#- BUILD
echo ""
echo " Build Phase Started :: Compiling Source Code :: ...."
cd java_web_code
mvn install
#- BUILD (TEST)
echo " "
echo ".. . . Test Phase Started :: Testing via Automated Scripts :: ......"
cd ../integration-testing/
mvn clean verify -P integration-test 
 """		// Shell build step
sh """ 
#!/bin/bash
#- POSTBUILD (PROVISIONING DEPLOYMENT)
echo " "
echo " Integration Phase Started :: Copying Artifacts ::"
cd java_web_code/
/bin/cp target/wildfly-spring-boot-sample-1.0.0.war ../docker/
echo " "
echo " Provisioning Phase Started :: Building Docker Container :: ......"
cd ../docker/
sudo docker build -t devops_pipeline_demo . 
 """
// Unable to convert a build step referring to "com.symantec.cwp.jenkins.plugin.CWPBuilder". Please verify and convert manually if required.		// Shell build step
sh """ 
# run your container
echo " "
echo " Deployment Phase Started: Building Docker Container : "
sudo docker run -d -p 8180:8080 --name devops_pipeline_demo devops_pipeline_demo

#- Completion
echo " "
echo "View App deployed here: http://server-ip:8180/sample.txt" 
 """ 
	}
}
}