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
    
         stage("Build test base") {
             steps {                
                 bat "chcp 866\n vrunner init-dev --dt D:\\jenkins\\template\\dev.dt --src D:\\jenkins\\jenkins_repo\\src"
             }
         }       
//         stage("Syntax check") {
//             steps {                
//                 bat "chcp 65001\n vrunner syntax-check"
//             }
//         }
        // stage("Smoke tests") {
        //    steps {
        //         script {
        //             try {
        //                 bat "chcp 65001\n vrunner xunit"
        //             }
        //             catch(Exception Exc) {
        //                 currentBuild.result = 'UNSTABLE'
        //             }
        //         }                
        //     }
        // }
//         stage("Vanessa") {
//            steps {
//                 script {
                     try {
        //                 bat "chcp 65001\n vrunner vanessa"
//						   bat '"C:\\Program Files\\1cv8\\8.3.25.1520\\bin\\1cv8c" /N"admin" /TestManager /Execute "D:\\Program Files\\OneScript\\lib\\vanessa-automation\\vanessa-automation.epf" /IBConnectionString "File=""D:/1Ctemplates/testmanager"";" /C"StartFeaturePlayer;QuietInstallVanessaExt;VAParams=D:\\1Ctemplates\\vantest\\VAParams.json"'
//						 }
//                     catch(Exception Exc) {
//                         currentBuild.result = 'UNSTABLE'
//                     }
//                 }                
//             }
//         } 
        //stage("Sonar") {
        //    steps {
        //        script {
        //            scannerHome = tool 'sonar-scanner'
        //        }
        //        withSonarQubeEnv("sonar") {
        //            bat "chcp 65001\n ${scannerHome}/bin/sonar-scanner -D sonar.login=sqp_ff1f8486e5db41bcca28e81970a89395690440a4"
        //        }                
        //    }
        // } 
    }
}