pipeline {
    agent {
        label "master"
    }
    tools {
        // Note: this should match with the tool name configured in your jenkins instance (JENKINS_URL/configureTools/)
        maven "maven"
    }
    environment {
        // This can be nexus3 or nexus2
        NEXUS_VERSION = "nexus3"
        // This can be http or https
        NEXUS_PROTOCOL = "http"
        // Where your Nexus is running
        NEXUS_URL = "localhost:8081"
        // Repository where we will upload the artifact
        NEXUS_REPOSITORY = "dvs-evn-spring"
        // Jenkins credential id to authenticate to Nexus OSS
        NEXUS_CREDENTIAL_ID = "nexus_credentials"
    }
    stages {
        stage("clone code") {
            steps {
                script {
                    // Let's clone the source
                    git 'https://github.com/maheshdevops09/pipline1.git';
                }
            }
        }
        stage("mvn build") {
            steps {
               // script {
                    // If you are using Windows then you should use "bat" step
                    // Since unit testing is out of the scope we skip them
                   // bat(/${MAVEN_HOME}\bin\mvn -Dmaven.test.failure.ignore clean package/)
                    sh "mvn clean install"
               // }
            }
        }
        stage("publish to nexus") {
            steps {
             nexusArtifactUploader artifacts: [
                [
                    artifactId: 'spring3-mvc-maven-xml-hello-world', 
                    classifier: '', 
                    file: 'target/spring3-mvc-maven-xml-hello-world-1.0.0.war', 
                    type: 'war'
                ]
            ], 
                    credentialsId: '433e7186-a8c3-4a43-ae22-d93d53ceebf2', 
                    groupId: 'com.madhu', 
                    nexusUrl: '18.220.238.138:8081/', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'simpleapp/', 
                    version: '1.0.0'
    }
}
    }
}
