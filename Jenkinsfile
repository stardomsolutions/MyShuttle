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
                sh "mvn sonar:sonar -Dsonar.host.url=http://20.110.15.29:9000 -Dmaven.test.skip=true"
            }
        }
	stage('DeployToDevEnv') {
		steps {
			sh "scp -o StrictHostKeyChecking=no target/myshuttledev.war azureuser@20.49.24.95:/opt/tomcat/webapps"
		}
	}

    }
}
