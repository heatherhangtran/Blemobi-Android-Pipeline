node("linux && jdk8") {
    stage "Checkout"
    git url: "https://github.com/heatherhangtran/Blemobi-Android-Pipeline"
    
    stage "Build"
    sh "./gradlew clean build"
    sh "./gradlew assemble"
}
      
