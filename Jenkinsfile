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
                sh "mvn sonar:sonar -Dsonar.host.url=http://20.97.240.130:9000 -Dmaven.test.skip=true"
            }
        }
		stage('DeployToDevEnv') {
			steps {
				sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/demo-webapp-build/target/myshuttledev.war azureuser@20.98.254.228:/opt/tomcat/webapps"
			}
		}
		stage('DeployToQAEnv') {
			steps {
				sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/demo-webapp-build/target/myshuttledev.war azureuser@52.177.65.202:/opt/tomcat/webapps"
			}
		}
		stage('DeployToProdEnv') {
			steps {
				sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/demo-webapp-build/target/myshuttledev.war azureuser@104.46.113.236:/opt/tomcat/webapps"
			}
		}
    }
}
