pipeline {
	agent any
	stages{
	stage('Clone') {
		steps {
			sh 'cd ${env.WORKSPACE}'
			sh 'git clone https://github.com/rahulyerva/Jenkins.git'
		}
	}
	stage('Build') {
		steps {
			sh 'cd ${env.WORKSPACE}/project'
			sh 'mvn clean test'
		}
	}
	stage('Database') {
		steps {
			sh 'cd ${env.WORKSPACE}/database'
			sh 'mvn clean test -Dscope=FlywayMigration'
		}
	}
	stage('Deploy') {
		steps {
			sh 'cd ${env.WORKSPACE}/project'
			sh 'mvn clean install'
		}
	}
	stage('Run Parellel Tests') {
		parallel {
			stage('test performance') {
				steps{
					sh 'mvn clean test -Dscope=performance'
				}		
		}
			stage('test regression') {
				steps{
					sh 'mvn clean test -Dscope=regression; exit 1'
				}		
		}
			stage('test integration') {
				steps{
					sh 'mvn clean test -Dscope=integration'
				}		
		}
	}
	}
	}
	}
