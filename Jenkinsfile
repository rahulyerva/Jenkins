pipeline {
	agent any
	stages{
	stage('Build') {
		steps {
			echo 'Build Successfull'
		}
	}
	stage('Database') {
		steps {
			echo 'Database Stage Successful'
		}
	}
	stage('Deploy') {
		steps {
			echo 'Deployment Successful'
		}
	}
	stage('Run Parellel Tests') {
		parallel {
			stage('test performance') {
				steps{
					echo 'performance test succefull'
				}		
		}
			stage('test regression') {
				steps{
					echo 'regression test successfully'
					echo 'exit 1'
				}		
		}
			stage('test integration') {
				steps{
					echo 'integration test successful'
				}		
		}
	}
	}
	}
	}
