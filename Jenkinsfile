pipeline{
    
    agent {label 'master'}
    // some block

    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
   
    stages {
        stage('clone'){
            steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/kliakos/sparkjava-war-example.git']]])
            }
        }

        stage('Build'){
            steps {
            sh "mvn clean package"
            }
        }

        stage('upload nexus'){
            steps {
            nexusArtifactUploader artifacts: [[artifactId: 'ram', classifier: '', file: 'target/sparkjava-hello-world-1.0.war', type: 'war']], credentialsId: 'nexus', groupId: 'ram', nexusUrl: '3.12.149.195:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'ram', version: '$BUILD_ID'
            }
       }
    }
    
}
