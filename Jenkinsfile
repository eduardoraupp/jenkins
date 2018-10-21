def deployDependency1 = '${dependency1}'
def deployDependency2 = '${dependency2}'
def dependency1CurrentVersion = '${dependency1CurrentVersion}'
def dependency2CurrentVersion = '${dependency2CurrentVersion}'
def dependency1NextVersion = '${dependency1NextVersion}'
def dependency2NextVersion = '${dependency2NextVersion}'

def prepareRelease() {
    try {
        sh "mvn versions:set -DnewVersion=${dependency1CurrentVersion.toString()}"
    } catch (err) {
        throw err
    }
}

def getPom(){
    return this.readMavenPom([ file: this.generatePomLocation() ])
}

def getGAVFromPom() {
    def auxPom = this.getPom()
    return [auxPom.groupId.toString(), auxPom.artifactId.toString(), auxPom.version.toString()]
}
pipeline {
    agent any
    parameters {
            booleanParam(defaultValue: false, description: 'dependency1', name: 'dependency1')
        booleanParam(defaultValue: false, description: 'dependency2', name: 'dependency2')
        string(defaultValue: 'X.X.X', description: 'dependency1CurrentVersion', name: 'dependency1CurrentVersion')
        string(defaultValue: 'X.X.X', description: 'dependency2CurrentVersion', name: 'dependency2CurrentVersion')
        string(defaultValue: 'X.X.X', description: 'dependency1NextVersion', name: 'dependency1NextVersion')
        string(defaultValue: 'X.X.X', description: 'dependency2NextVersion', name: 'dependency2NextVersion')
    }
    stages {
        stage("Build Parent project") {
            steps {
               // build job: 'independent', propagate: true
            }
        }
        stage("build child 1") {
            when {
                expression {
                    return '${params.dependency1}';
                }
            }
            steps {
                    build job: 'dependency1', propagate: true
            }
        }
        stage("build child 2") {
            when {
                expression {
                    return '${params.dependency2}';
                }
            }
            steps {
                    build job: 'dependency2', propagate: true
            }
        }
    }
}

