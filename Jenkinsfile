

pipeline{

agent any

    environment{
        Register ="damier85/damier-raymond"
        RegisterCrudential ="Mydocker20"
        dockerImage =""
        forTheAWSecr="367484709954.dkr.ecr.us-east-2.amazonaws.com/caliber-config"
        Region ="ecr:us-east-2"
        ID="damierTestEcr"
        Svc_Name="caliber-config"


    }
     tools{
     maven 'maven-3'

     }
stages{

    stage ('Clonning from git'){

        steps
        {
            echo "Something here"
        }


    }

    stage('Version'){
            steps
                {
                sh 'mvn --version'
                }
          }
    
        stage ("initialize") {
        steps {
        sh '''
        echo "PATH = ${PATH}"
        echo "M2_HOME = ${M2_HOME}"
        '''
        }
        }

    
        stage('Compile the App'){
        steps
           {
            
            sh 'mvn compile'
          }
        }



stage('package the App'){
        steps
        {
            sh "mvn clean package"
        }
    }
 
   stage('AWS Building Bloc'){

        steps
        {
            script
            {
                dockerImage = docker.build("${forTheAWSecr}")
            }
        }
}
 
    stage ('Deploy image to AWS Ecr'){

        steps
        {
                script{
                  
                    docker.withRegistry('https://367484709954.dkr.ecr.us-east-2.amazonaws.com', "${REGION}:${ID}")
                    {
                        
                        dockerImage.push("latest")
                   
                    }
                }
            
        }

}

    stage ("Remove unUsed docker image"){
        steps
        {
            sh "docker rmi ${Register}:my-image"
        }
    }



}


}
