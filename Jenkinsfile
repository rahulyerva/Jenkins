pipeline {
	agent any
	stages{
	stage('Clone') {
		steps {
			sh 'cd ${env.WORKSPACE}
			sh 'git clone https://github.com/rahulyerva/Jenkins.git'
		}
	}
	stage('Build') {
		steps {
			sh 'cd ${env.WORKSPACE}/project
			sh 'mvn clean test'
		}
	}
	post {
    failure {
        mail to: 'rahul.yerva789@gmail.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
    }
}
	stage('Database') {
		steps {
			sh 'cd ${env.WORKSPACE}/database
			sh 'mvn clean test -Dscope=FlywayMigration'
		}
	}
	post {
    failure {
        mail to: 'rahul.yerva789@gmail.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
    }
}
	stage('Deploy') {
		steps {
			sh 'cd ${env.WORKSPACE}/project
			sh 'mvn clean install'
		}
	}
	post {
    failure {
        mail to: 'rahul.yerva789@gmail.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
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
	post {
    failure {
        mail to: 'rahul.yerva789@gmail.com',
             subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             body: "Something is wrong with ${env.BUILD_URL}"
    }
}
	}
	}
