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

	stage('DeployToDevEnv') {
		steps {
			sh "scp -o StrictHostKeyChecking=no target/myshuttledev.war azureuser@20.49.24.95:/opt/tomcat/webapps"
		}
	}
	stage('DeployToQAEnv') {
		steps {
			sh "scp -o StrictHostKeyChecking=no target/myshuttledev.war azureuser@20.98.240.26:/opt/tomcat/webapps"
		}
	}
	stage('DeployToProdEnv') {
		steps {
			sh "scp -o StrictHostKeyChecking=no target/myshuttledev.war azureuser@104.46.111.104:/opt/tomcat/webapps"
		}
	}

    }
}
