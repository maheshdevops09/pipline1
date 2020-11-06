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
                    sh "mvn clean install "
               // }
            }
        }
        stage("publish to nexus") {
            steps {
                def mavenPom = readMavenPom 'pom.xml'
             nexusArtifactUploader artifacts: [
  [
    artifactId: 'spring3-mvc-maven-xml-hello-world', 
    classifier: '', 
      file: "target/spring3-mvc-maven-xml-hello-world-${mavenPom.version}.war", 
    type: 'war'
    ]
    ], 
    credentialsId: 'nexus3', 
    groupId: 'com.madhu', 
    nexusUrl: '172.31.40.80:8081', 
    nexusVersion: 'nexus3', 
    protocol: 'http', 
    repository: 'simpleapp', 
    version: "${mavenPom.version}"
    }
}
    }
}
