pipeline {
	agent any
	stages {
		stage("Build another job") {
			build job: 'dependency1', propagate: true
		}
	}
}

