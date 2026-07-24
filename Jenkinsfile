pipeline
{
    agent any
    stages
    {
        stage('download')
        {
            steps
            {
             git 'https://github.com/IntelliqDevops/maven.git'
             }
        }
        stage('build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('deploy')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '329332aa-c8db-483e-8c9c-1d1c659b848f', path: '', url: 'http://51.20.193.82:8080')], contextPath: 'test', war: '**/*.war'
            }
        }
        stage('testing')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
            }
        }
        stage('delivery')
        {
            steps
            {
                sh 'java -jar /var/lib/jenkins/workspace/declarative/testing.jar'
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '329332aa-c8db-483e-8c9c-1d1c659b848f', path: '', url: 'http://51.21.182.17:8080')], contextPath: 'prod', war: '**/*.war'
            }
        }
        }
    }
