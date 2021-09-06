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
                sh "mvn sonar:sonar -Dsonar.host.url=http://20.110.49.31:9000 -Dmaven.test.skip=true"
            }
        }
		stage('DeployToDevEnv') {
			steps {
				sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/demo-webapp-build/target/myshuttledev.war azureuser@20.110.17.156:/opt/tomcat/webapps"
			}
		}

    }
}
