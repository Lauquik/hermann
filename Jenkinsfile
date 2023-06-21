properties([
    [$class: 'BuildDiscarderProperty',
        strategy: [$class: 'LogRotator', numToKeepStr: '10']]
])

node('docker-node') {
    stage('Build') {
        // Checkout
        checkout scm

        // Install required bundles
        sh 'bundle install'

        // Build and run tests with coverage
        sh 'bundle exec rake build spec'

        // Archive the built artifacts
        archive(includes: 'pkg/*.gem')

        // Publish HTML
        publishHTML([
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'coverage',
            reportFiles: 'index.html',
            reportName: 'RCov Report'
        ])
    }
}
