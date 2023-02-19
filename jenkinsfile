pipeline {
    tools{
        maven 'mymaven'
    }
    agent any
    
    stages{
        stage('1.clone and compile'){
            steps {
                git 'https://github.com/itonix/DevOpsCodeDemo.git'
                echo 'CLONE REPOSITORY TO WORKSPACE'
                sh 'mvn compile'
                }
        }
        stage('2.codereview'){
            steps {
                git 'https://github.com/itonix/DevOpsCodeDemo.git'
                echo 'CODE Review using PMD'
                sh 'mvn pmd:pmd'
                }
            post{
                success{
                    scanForIssues tool: pmdParser(pattern: '**/pmd.xml')
                }
            }
        }
        stage('3.test unittest'){
            steps {
                git 'https://github.com/itonix/DevOpsCodeDemo.git'
                echo 'Test codes-unit test'
                catchError(buildResult: 'SUCCESS', message: 'Error caught while testing junit', stageResult: 'FAILURE') {
                    sh 'mvn test'
                }              
                
            }
        }
    
        stage('4.package'){
            steps {
                git 'https://github.com/itonix/DevOpsCodeDemo.git'
                echo 'Packaging to War package'
                sh 'mvn package'
                }
        }
    
    }
}

