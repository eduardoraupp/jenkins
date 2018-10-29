pipeline {
    agent any
    parameters {
	booleanParam(defaultValue: false, description: 'is parent release?', name: 'isParentRelease')
	//booleanParam(defaultValue: false, description: 'is child release?', name: 'isChildRelease')
        booleanParam(defaultValue: false, description: 'Release dependency 1', name: 'dependency1')
        booleanParam(defaultValue: false, description: 'Release dependency 2', name: 'dependency2')
        string(defaultValue: 'X.X.X', description: 'Parent dependency version', name: 'parentDependencyVersion')
        //string(defaultValue: 'X.X.X', description: 'dependency2CurrentVersion', name: 'dependency2CurrentVersion')
        //string(defaultValue: 'X.X.X', description: 'dependency1NextVersion', name: 'dependency1NextVersion')
        //string(defaultValue: 'X.X.X', description: 'dependency2NextVersion', name: 'dependency2NextVersion')
    }
    stages {
        stage("Build Parent project") {
            steps {
               build job: 'independent', propagate: true, parameters: [[$class: 'BooleanParameterValue', name: 'isParentRelease', value: params.isParentRelease]]
            }
        }
        stage("build child 1") {
            when {
                expression {
                    return params.dependency1;
                }
            }
            steps {
                    build job: 'dependency1', propagate: true, parameters: [[$class: 'StringParameterValue', name: 'parentDependencyVersion', value: params.parentDependencyVersion], [$class: 'BooleanParameterValue', name: 'isParentRelease', value: params.isParentRelease]]
            }
        }
        stage("build child 2") {
            when {
                expression {
                    return params.dependency2;
                }
            }
            steps {
                    build job: 'dependency2', propagate: true, parameters: [[$class: 'StringParameterValue', name: 'parentDependencyVersion', value: params.parentDependencyVersion], [$class: 'BooleanParameterValue', name: 'isParentRelease', value: params.isParentRelease]]
            }
        }
    }
}

