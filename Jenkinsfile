pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/krishnain/maven23.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'bc706409-0ccb-4800-b629-d592b5179939', path: '', url: 'http://172.31.7.30:8080')], contextPath: 'mytestapp', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipleine1/testing.jar'
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                input message: 'Need approval from DM!', submitter: 'srinivas'
                deploy adapters: [tomcat9(credentialsId: 'bc706409-0ccb-4800-b629-d592b5179939', path: '', url: 'http://172.31.7.247:8080')], contextPath: 'myprodapp', war: '**/*.war'
            }
        }
        
        
    }
}
