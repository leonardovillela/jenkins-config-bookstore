node {
    try {
        slackSend(color: 'warning', message: "Deploy Started - ${env.JOB_NAME} ${env.BUILD_NUMBER}")
        
        stage 'Checkout'
            git url: 'https://github.com/leonardovillela/bookstore.git'
        
        stage 'Build Front-end'
            sh 'npm install'
            sh 'npm run build'
            
        stage 'Build Back-end'
            sh './gradlew clean build -x test'
            
        stage 'Test'
            sh './gradlew test'
            
        stage 'Deploy in prod'
            sh '/gradlew bootRun'
            
        slackSend(color: 'good', message: "Deploy has finished - ${env.JOB_NAME} ${env.BUILD_NUMBER}")
    } catch(err) {
        slackSend(color: 'danger', message: "Deploy has failed - ${env.JOB_NAME} ${env.BUILD_NUMBER}")
        throw err
    }
}
