pipeline{
    tools{
        jdk 'JenkinsJDK'
        maven 'JenkinsMaven'
    }
    agent none
        stages{
             stage('Compile Stage'){
                agent any
                steps{
                    sh 'mvn compile'
                }
                
            }
            stage('CodeReview Stage'){
                agent any
                steps{
                    sh 'mvn pmd:pmd'
                }
              }
            stage('Unit Test Stage'){
                agent {label 'ec2_slave1'}
                steps{
                    git 'https://github.com/devops-trainer/DevOpsClassCodes.git'
                    sh 'mvn test'
                }
                
            }
            stage('Metric Check Stage'){
                agent any
                steps{
                    sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
                }
                post{
                    always{
                        cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                    }
                }
            }
            stage('Package Stage'){
                agent any
                steps{
                    sh 'mvn package'
                }
            }
            
        }
    
    }
