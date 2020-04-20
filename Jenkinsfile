#!groovy
node{
    // Get Artifactory server instance, defined in the Artifactory Plugin administration page.
    def server = Artifactory.server "art-1"
    // Create an Artifactory Maven instance.
    def rtMaven = Artifactory.newMavenBuild()
    def buildInfo
    stage('Clone sources') {
        git url: 'https://github.com/nlilaramani/JenkinsPrj.git'
    }
    stage('Artifactory configuration') {
        // Tool name from Jenkins configuration
        rtMaven.tool = "Default Maven"
        // Set Artifactory repositories for dependencies resolution and artifacts deployment.
        rtMaven.deployer releaseRepo:'libs-release-local', snapshotRepo:'libs-snapshot-local', server: server
        rtMaven.resolver releaseRepo:'libs-release', snapshotRepo:'libs-snapshot', server: server
    }

    stage('Maven build') {
        jdk "Default JDK"
        env.JAVA_HOME="C:/Program Files/Java/jdk1.8.0_111"
        buildInfo = rtMaven.run pom: 'pom.xml', goals: 'clean install'
    }
}
