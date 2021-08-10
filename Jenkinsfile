pipeline {
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
    agent none
    stages{
        stage('Git clone'){
            agent any
            steps{
               git 'https://github.com/Tom-cat-1/DevOpsClassCodes.git'
            }
        }
        stage('Compile'){
            agent any
            steps{
               git 'https://github.com/Tom-cat-1/DevOpsClassCodes.git'
               sh 'mvn compile'
            }
        }
        stage('Code Review'){
            agent any
            steps{
               git 'https://github.com/Tom-cat-1/DevOpsClassCodes.git'
               sh 'mvn pmd:pmd'
            }
        }
        stage('Unit test'){
            agent any
            steps{
               git 'https://github.com/Tom-cat-1/DevOpsClassCodes.git'
               sh 'mvn test'
            }
            post{
                success{
                    junit 'target/surefire-reports/*xml'
                }
            }
        }
        stage('Code coverage'){
            agent any
            steps{
               git 'https://github.com/Tom-cat-1/DevOpsClassCodes.git'
               sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
            post{
                success{
                    cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
                }
            }
        }
        stage('Package'){
            agent any
            steps{
               git 'https://github.com/Tom-cat-1/DevOpsClassCodes.git'
               sh 'mvn package'
            }
        }
    }
}
