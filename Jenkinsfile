node {
    stage 'Stage Checkout'
    checkout scm
    
    sh 'git submodule update --init'
    
    stage 'Stage Build'
    echo "My branch is: ${env.BRANCH_NAME)"

    def flavor = flavor(env.BRANCH_NAME)
    echo "Building flavor ${flavor}"
    
    sh "./gradlew clean assemble${flavor}Debug -PBUILD_NUMBER=${env.BUILD_NUMBER}"

    stage 'Stage Archive'
 
    step([$class: 'ArtifactArchiver', artifacts: 'App/build/outputs/apk/*.apk', fingerprint: true])

    stage 'Stage Upload To Fabric'
    sh "./gradlew crashlyticsUploadDistribution${flavor}Debug  -PBUILD_NUMBER=${env.BUILD_NUMBER}"
}

@NonCPS
def flavor(branchName) {
    def matcher = (env.BRANCH_NAME =~ /QA_([a-z_]+)/)
    assert matcher.matches()
    matcher[0][1]
}
    /*
    git url: "https://github.com/heatherhangtran/Blemobi-Android-Pipeline"
    
    stage "Build"
    sh "./gradlew clean build"
    sh "./gradlew assemble"
    */
      
