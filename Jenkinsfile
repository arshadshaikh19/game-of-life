pipeline{

        agent { label 'worker' }
tools{
                                jdk 'java-8'
                        }
         
         stages{
                stage('Source code'){
                        steps{
                               checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/arshadshaikh19/game-of-life.git']])
                        }
                }
                stage('Build code'){
                 
                        steps{
                                sh script: 'mvn package \
                                        -DskipTests'
                        }
                }
                stage('Code Analysis'){
                        // tools{
                        //         jdk 'java-17'
                        // }
                         
                        steps{
                            withSonarQubeEnv(credentialsId: 'sonarqube-user-token', installationName: 'Sonarqube-9.9.3') {
                                // some block
                                sh script: 'mvn clean verify sonar:sonar \
                                    -Desby.skip \
                                  -Dsonar.projectKey=demoapp-project \
                                  -Dsonar.host.url=http://34.131.143.64:9000 \
                                  -Dsonar.login=sqp_747d47cab6ed94468d1d1551694bfc9a77cf5287'
                            }
                        }
                }
                //  stage('Artifact'){
                //         steps{
                //                 dir('/home/my/workspace/Springpet/target'){
                //                     nexusArtifactUploader artifacts: [[artifactId: 'spring-boot-starter-parent', classifier: '', file: 'spring-petclinic-3.1.0-SNAPSHOT.jar', type: 'jar']], credentialsId: 'nexus', groupId: 'org.springframework.boot', nexusUrl: '34.131.45.90:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'testrepo', version: '3.1.0-SNAPSHOT'
                //                 }  
                //         }
                // }
        }
}
