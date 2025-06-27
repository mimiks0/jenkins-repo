pipeline
{
    agent {
        label 'Server-1C-wndows'
    }

    environment {
        envString = 'true'
    }

    post {
        always {            
            allure includeProperties: false, jdk: '', results: [[path: 'out/syntax-check/allure'], [path: 'out/smoke/allure/']]
            junit allowEmptyResults: true , testResults: 'out/smoke/junit/*.xml'
        }

        failure {
            bat "echo failure"
        }

        success {
            bat "echo succes"
        }

    }

    stages {
         stage("Sync local repo form gitgub") {
             steps {                
//                 bat 'rmdir /s /q "D:\\\\1Ctemplates\\\\jenkins-repo'
				 bat '''cd /d D:\\\\1Ctemplates\\\\jenkins-repo
                     git fetch --all'''
             }
         }
	
    
         stage("Build test base") {
             steps {                
//                 bat 'chcp 65001\n vrunner init-dev --dt D:\\jenkins\\template\\dev.dt --src D:\\jenkins\\jenkins_repo\\src'

				 bat '''chcp 866&"C:\\Program Files\\1cv8\\8.3.25.1520\\bin\\ibcmd" infobase restore --db-path="D:\\1Ctemplates\\dev" "D:\\1Ctemplates\\dev.dt" --user="admin"

                 chcp 866&"C:\\Program Files\\1cv8\\8.3.25.1520\\bin\\ibcmd" infobase config import --db-path="D:\\1Ctemplates\\dev"  "D:\\1Ctemplates\\jenkins-repo\\src" --user="admin"

                 chcp 866&"C:\\Program Files\\1cv8\\8.3.25.1520\\bin\\ibcmd" infobase config apply   --db-path="D:\\1Ctemplates\\dev" --user="admin" --force'''
             }
         }       
         stage("Smoke tests") {
            steps {
                 script {
                     try {
                         bat "chcp 65001\n vrunner xunit"
                     }
                     catch(Exception Exc) {
                         currentBuild.result = 'UNSTABLE'
                     }
                 }                
             }
         }
         stage("Vanessa") {
            steps {
                 script {
                     try {
        //                 bat "chcp 65001\n vrunner vanessa"
						   bat '"C:\\Program Files\\1cv8\\8.3.25.1520\\bin\\1cv8c" /N"admin" /TestManager /Execute "D:\\Program Files\\OneScript\\lib\\vanessa-automation\\vanessa-automation.epf" /IBConnectionString "File=""D:/1Ctemplates/testmanager"";" /C"StartFeaturePlayer;QuietInstallVanessaExt;VAParams=D:\\1Ctemplates\\vantest\\VAParams.json"'
						 }
                    catch(Exception Exc) {
                        currentBuild.result = 'UNSTABLE'
                     }
                 }                
             }
         } 
        stage("Sonar") {
           steps {
              script {
                   

                   bat '''cd /d D:\\1Ctemplates\\jenkins-repo\\src
                   chcp 65001&sonar-scanner.bat -D"sonar.projectKey=Ci_Code" -D"sonar.sources=." -D"sonar.host.url=http://192.168.1.35:9000" -D"sonar.token=sqp_6b9737b082b6e223cf015aeb6144590b0944f2ce""'''
				   
               }                
            }
         } 
    }
}