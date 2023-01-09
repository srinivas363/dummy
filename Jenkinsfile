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
}
	}
				
