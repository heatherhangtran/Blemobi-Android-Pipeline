node("linux && jdk8") {
    stage "Checkout"
    git url: "https://github.com/heatherhangtran/Blemobi-Android-Pipeline"
    
    stage "Build/Analyse/Test"
    sh "./gradlew clean build"
    archiveUnitTestResults()
    archiveCheckstyleResults()
}
    
    def archiveUnitTestResults() {
    step([$class: "JUnitResultArchiver", testResults: "build/**/TEST-*.xml"])
}
      
