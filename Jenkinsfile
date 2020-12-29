pipeline{
	agent none
	stages{
		stage('Run'){
				parallel{
					stage('Server'){
						agent{
							docker{
								image 'jamesdbloom/docker-java8-maven:latest'
								args '-v /root/.m2:/root/.m2 -p 8072:8072'
							}
						}
						stages{
							stage('Clean'){
								steps{
									script{
										sh 'rm -rf spring'
									}
								}
							
							}
							stage('SCM-Checkout'){
								steps{
									script{
										sh 'git clone https://github.com/srinanpravij/jenkins.docker.spring.react.selenium_person-database.git $PWD/spring'
										sh 'ls'
									}
								}
							}
							stage('Build'){
								steps{
									script{
										dir('$PWD/spring'){
										sh 'mvn spring-boot:run'
										}
									}
								}
							
							}
						}
					}
					stage('Client'){
					agent{
							docker{
								image 'node:10'
								args '-v /root/.m2:/root/.m2 -p 8079:8079'
							}
						}
						environment {
                                 CI = 'true'
                        }
						stages{
							stage('Clean'){
								steps{
									script{
										sh 'rm -rf react'
									}
								}
							
							}
							stage('SCM-Checkout'){
								steps{
									script{
										sh 'git clone https://github.com/srinanpravij/jenkins.docker.spring.react.selenium_person-database.git $PWD/react'
										sh 'ls'
									}
								}
							
							}
							stage('Build'){
								steps{
									script{
										dir('$PWD/react/client'){
											sh 'npm install'
											sh 'npm start'
										}
									}
								}
							
							}
						}
					}
					
					stage('Integration-Testing') {
						agent {
							docker {
								image 'jamesdbloom/docker-java8-maven:latest'
								args '-v /root/.m2:/root/.m2 -p 8050:8050'
							}
						}
						stages {
							stage('Clean') {
								steps {
									script {
										sh 'rm -rf testing'
									}
								}
							}
							stage('SCM Checkout') {
								steps {
									script {
										sh 'git clone https://github.com/srinanpravij/jenkins.docker.spring.react.selenium_person-database.git $PWD/testing'
									}
								}
							}
							stage('Compile-Package-Test') {
								steps {
									script {
										dir('$PWD/testing/integration-testing') {
											sh "mvn package -Dmaven.test.failure.ignore=true"
										}
									}
								}
							}
						}
						
					}
				}
		}
	}

}