pipeline {
    agent any

    environment {
        PIPELINENAME          = "Test_Pipeline_CxPlugin_Sam"
        PIPELINEVERS          = "v1.1"

        CX_SERVER_URL         = "http://localhost"
		CX_USERNAME			  = "admin"
		CX_PASSWORD			  = "P@ssword1"
		    }
    stages {
        stage('Greeting') {
            steps {
                echo "Job [${JOB_NAME}] from ${PIPELINENAME} (${PIPELINEVERS}) - Build ${BUILD_NUMBER} - in the Workspace of [${WORKSPACE}]!"
                script {
                    if(isUnix()) {
                        sh "ls -lahR ${WORKSPACE} "
                        sh "cd ${WORKSPACE} "
                    } else {                       
                        bat "cd ${WORKSPACE}"
                    }
                }
            }
        }
        stage('run CxSCA') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'cxscarabiacreds', passwordVariable: 'CXSCAPSW', usernameVariable: 'CXSCAUSR')]) {
                    bat "echo $CXSCAUSR $CXSCAPSW"
                    bat "C:\\Users\\CxAdmin\\Documents\\SCA-Resolver\\ScaResolver.exe -s \"C:\\Users\\CxAdmin\\Documents\\SCA-Resolver\\JavaVulnerableLab-master\" -u $CXSCAUSR -p $CXSCAPSW -n \"jenkinsResolver\" -a sca_rabia_khanfir"
                }
            }
        }
	}
}
