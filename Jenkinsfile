pipeline {

    agent any

    stages {

        stage('Build'){
            steps {
                

                sh "dotnet restore"
            }
        }

        stage('Test'){
            steps {
                
                sh "dotnet test"
            }

            post {
                always {
                    junit 'test/*.xml'
                }
            }
        }

        stage('sonar scan'){
            steps {
              sh 'dotnet sonarscanner begin /k:"assignment-2" /d:sonar.host.url="https://2a6d-54-226-50-200.ngrok.io"  /d:sonar.login="sqp_66df42127aa53c6da5a88df4329cac82e7ec7643"'
							sh 'dotnet build'
							sh 'dotnet sonarscanner end /d:sonar.login="sqp_93074ba7a088db5557cef6a05204b17342fc6ba0"'
            }
        }

        stage('Package'){
            steps {
                
                sh "dotnet publish"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/*.dll', followSymlinks: false
                }
            }
        }

    }

}