pipeline{
        agent any
        stages{
            stage('Make Directory'){
                steps{
                    sh "mkdir ~/palette-generator1"
                }
            }
            stage('Make Files'){
                steps{
                    sh "touch ~/palette-generator1/file1 ~/palette-generator1/file2"
                }
            }
        }
}