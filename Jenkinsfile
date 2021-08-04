pipeline{
    tools{
        jdk 'JenkinsJDK'
        maven 'JenkinsMaven'
    }
    agent none
        stages{
             stage('Compile'){
                agent any
                steps{
                    sh 'mvn compile'
                }
                
            }
            stage('CodeReview'){
                agent any
                steps{
                    sh 'mvn pmd:pmd'
                }
              }
            stage('Test'){
                agent {label 'win_slave'}
                steps{
                    git 'https://github.com/devops-trainer/DevOpsClassCodes.git'
                    bat 'mvn test'
                }
                
            }
            stage('MetriCheck'){
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
            stage('Package'){
                agent any
                steps{
                    sh 'mvn package'
                }
            }
            
        }
    
    }
