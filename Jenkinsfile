pipeline {
    agent any
    tools{
        label "petclinic"
    }

    stages {
        stage ('Packer init') {
            steps {
                    echo 'initializing packer'
                    sh '/usr/bin/packer init aws-ami.pkr.hcl'
            }  
        }
        stage ('Packer fmt') {
            steps {
                script {
                    echo 'formatting packer code'
                    sh '/usr/bin/packer fmt aws-ami.pkr.hcl'
                }
            }  
        }
        stage ('Packer validate') {
            steps {
                script {
                    echo 'validating packer code'
                    sh '/usr/bin/packer validate aws-ami.pkr.hcl'
                }
            }  
        }
        stage ('packer build ami') {
            steps {
                    echo 'building ami'
                    sh '/usr/bin/packer build aws-ami.pkr.hcl'
            }  
        }
        
        stage ('Build jar') {
            steps {
                script {
                    echo 'Building jar'
                    sh 'mvn clean package -DskipTests=true'
                }
            }  
        }
        stage ('Build docker image') {
            steps {
                script {
                    echo 'Building docker image'
                            sh "docker build -t petclinic-java-app:$BUILD_NUMBER ."
                     }
                }
        }  
                
    }
}
