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
					sh 'mvn test'
					}
						}
		stage("integration testing"){
				steps{
					sh 'mvn verify DiskipUnitTests'
					}
						}		
}
	}
				
