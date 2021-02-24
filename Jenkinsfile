node{ 
    stage('Git Pull'){
        git url: 'https://github.com/we45/Vulnerable-Flask-App.git'
    }   
    stage('Install tools'){
        sh '''
        pip3 install bandit safety
        '''
    }
    stage('Bandit - SAST'){
        sh '''
        bandit -f -r app/ -f html -o bandit-result.html | true
        '''
        archiveArtifacts allowEmptyArchive: true, artifacts: '**/bandit-result.html', onlyIfSuccessful: true
        publishHTML (target: [
          allowMissing: false,
          alwaysLinkToLastBuild: false,
          keepAll: true,
          reportDir: '.',
          reportFiles: 'bandit-result.html',
          reportName: "Bandit Report"
        ])
    }
    stage ('Safety - SCA') {
 
        sh '''
        safety check --json > sca-report.json | true
        '''
         
        archiveArtifacts allowEmptyArchive: true, artifacts: '**/sca-report.json', onlyIfSuccessful: true
        publishHTML (target: [
          allowMissing: false,
          alwaysLinkToLastBuild: false,
          keepAll: true,
          reportDir: '.',
          reportFiles: 'sca-report.json',
          reportName: "SCA Report"
        ])
    }    
}
