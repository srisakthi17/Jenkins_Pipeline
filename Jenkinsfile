pipeline{ 
	agent any
		tools {
			maven 'Maven_3.9.5'
			}
	stages{ 
		stage('SCM Checkout'){
			steps{
				checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/srisakthi17/Java.git']])
				}
			}
		stage('Maven-Build'){
			steps{
				sh 'mvn clean install'
				}
					}
		stage('Sonar Scan'){
			steps{
				withSonarQubeEnv(Sonarqube) {
					sh "${tool("Sonar_7.1")}/bin/sonar-scanner -Dsonar.host.url=http://ec2-65-1-136-155.ap-south-1.compute.amazonaws.com:9000 \
										-Dsonar.login=sqp_0209fb6bac04c46d59a63b3dec1b81585b51c62c \
										-Dsonar.projectKey=MavenRepo \
										-Dsonar.java.binaries=target"
								}
				}
					}
		stage('Nexus Upload'){
			steps{
				sh 'mvn -s settings.xml clean deploy'
				}
					}
	}
}
