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
}
	}
				
