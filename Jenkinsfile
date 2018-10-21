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
	stages {
		stage("Build another job") {
			steps {
				build job: 'dependency1', propagate: true
			}
		}
	}
}

