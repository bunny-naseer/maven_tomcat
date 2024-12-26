
pipeline {
	agent any	
	
	stages{
		stage('Checkout Code'){
			steps{
				checkout scm
				}
			}
	
	stage('Build'){
		steps{
			sh "mvn clean install -Dmaven.test.skip=true"
		}
	}
	
	stage('Archive Artifact'){
		steps{
		archiveArtifacts artifacts:'target/*.war'
		}
	}
	 stage('deployment'){
                steps{
                deploy adapters: [tomcat9(url: 'http://localhost:8081/',
                              credentialsId: 'naseertom')],
                     war: 'var/lib/jenkins/workspace/tomcat_job/target/java-example.war',
                     contextPath: '/var/lib/tomcat9/webapps'
                }

        }

	stage('Notification'){
		steps{
		emailext(
			subject: "Job Completed",
			body: "Jenkins pipeline job for maven build job completed",
			to: "naseerahammed19@gmail.com"
		)
		}
	}
	}
}
