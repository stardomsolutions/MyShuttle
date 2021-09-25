pipeline {
    agent any

    tools {
        maven "maven3"
    }

    stages {
        stage('Build') {
            steps {
                sh "mvn clean package -Dmaven.test.skip=true"
            }
        }
        stage('CodeQuality') {
            steps {
                sh "mvn sonar:sonar -Dsonar.host.url=http://20.65.124.225:9000 -Dmaven.test.skip=true"
            }
        }
	stage('DeployToDevEnv') {
		steps {
			sh "scp -o StrictHostKeyChecking=no target/myshuttledev.war azureuser@20.65.34.68:/opt/tomcat/webapps"
		}
	}
	stage('DeployToQAEnv') {
		steps {
			sh "scp -o StrictHostKeyChecking=no target/myshuttledev.war azureuser@20.97.168.24:/opt/tomcat/webapps"
		}
	}
	stage('DeployToProdEnv') {
		steps {
			sh "scp -o StrictHostKeyChecking=no target/myshuttledev.war azureuser@20.65.106.125:/opt/tomcat/webapps"
		}
	}

    }
}
