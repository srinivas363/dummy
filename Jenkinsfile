pipeline{
	agent any
	stages{
		stage("git checkout"){
				steps{
					git branch: 'main', url: 'https://github.com/srinivas363/dummy.git'
					}
						}
		stage("unit testing"){
				steps{
					script{
					sh 'mvn test'
					}
				}
						}
		stage("integration testing"){
				steps{
					script{
					sh 'mvn verify -DskipUnitTests'
					}
				}
						}
		stage('Maven build'){
            
            			steps{
                
                			script{
                    
                    			sh 'mvn clean install'
               					 }
           				 }
       				 }
		 stage('Static code analysis'){
            
            			steps{
                
               				script{
                    
                    			withSonarQubeEnv (credentialsId: 'sonar-api') {
                        
                       			sh 'mvn clean package sonar:sonar'
                    									}
                  				 }
                    
               				 }
            					}
		stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                    }
                }
            }
		stage("upload var file to nexus"){
			steps{
				script{
					def readPomVersion = readMavenPom file: 'pom.xml'
					
					def nexusRepo= readMavenPom.version.endsWith("SNAPSHOT") ? "demoapp-snapshot" : "demoapp-release"
					nexusArtifactUploader artifacts: 
				[
					[
						artifactId: 'springboot',
						classifier: '', file: 'target/Uber.jar',
						type: 'jar'
					]
				],
				credentialsId: 'nexus-auth',
				groupId: 'com.example',
				nexusUrl: '44.203.151.8:8081',
				nexusVersion: 'nexus3',
				protocol: 'http',
				repository: 'demoapp-release',
				version: "${readPomVersion.version}"
					
				}
			}
		}
}
	}
				
