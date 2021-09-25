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
			sh "scp -o StrictHostKeyChecking=no target/myshuttledev.war azureuser@52.179.142.164:/opt/tomcat/webapps"
		}
	}
	stage('DeployToQAEnv') {
		steps {
			sh "scp -o StrictHostKeyChecking=no target/myshuttledev.war azureuser@20.65.11.148:/opt/tomcat/webapps"
		}
	}
	stage('DeployToProdEnv') {
		steps {
			sh "scp -o StrictHostKeyChecking=no target/myshuttledev.war azureuser@20.109.101.219:/opt/tomcat/webapps"
		}
	}

    }
}
