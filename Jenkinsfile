pipeline {
    agent any
  
  	tools { 
        maven 'maven-3.8.1'
        jdk 'jdk8' 
    }

    stages {
        stage('Build') {
            steps {
                // To run Maven on a Windows agent, use
                 bat 'mvn clean test'
		    
// 		fileOperations([folderCopyOperation(destinationFolderPath: 'QmetryReport/dashboard', sourceFolderPath: 'dashboard')])
// 		fileOperations([folderCopyOperation(destinationFolderPath: 'QmetryReport/img', sourceFolderPath: 'img')])
// 		fileOperations([folderCopyOperation(destinationFolderPath: 'QmetryReport/test-results', sourceFolderPath: 'test-results')])
// 		fileOperations([fileCopyOperation(excludes: '', flattenFiles: false, includes: 'dashboard.htm', renameFiles: false, sourceCaptureExpression: '', targetLocation: 'QmetryReport', targetNameExpression: '')])
// 		bat 'zip -r archieve.zip . -e'   
 		//zip zipFile: 'report.zip', archive: false, dir: 'QmetryReport', overwrite: true	
		
		dir("${WORKSPACE}/QmetryReport"){
   		 sh '7z a report.7z -psecret -mhe .'
		}
            }

            post {
                
                success {
             		echo 'success'
			
			//archiveArtifacts artifacts: 'dashboard.htm', onlyIfSuccessful: true
			emailext attachLog: false, attachmentsPattern: 'report.zip',
			to: 'lazio_karisma@manulife.com',
                	body: 'password lazio1234',
                	subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
          
                }
            }
        }
    }
}
