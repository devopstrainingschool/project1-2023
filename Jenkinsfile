node {
    // Git checkout before load source the file
    checkout scm

    // To know files are checked out or not
    sh '''
        ls -lhrt
    '''

    def rootDir = pwd()
    println("Current Directory: " + rootDir)

    // point to exact source file
    def example = load "${rootDir}/Example.Groovy"

    example.exampleMethod()
    example.otherExampleMethod()
# https://stackoverflow.com/questions/37800195/how-do-you-load-a-groovy-file-and-execute-it
