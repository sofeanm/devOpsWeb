pipeline {
    agent{
    	label 'JavaBuildServer'
    }
    
    tools {
        maven 'localMaven'
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
	    steps {
		echo "Deploying the Artifact"
		deploy adapters: [tomcat8(credentialsId: 'tomcatcred', path: '', url: 'http://13.234.120.154:8080/')], contextPath: null, war: '**/*.war'
	    }
	}
    }
}
