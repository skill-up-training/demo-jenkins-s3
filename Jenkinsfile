def  BUCKET_NAME     = "demojenkinsskillup"
pipeline{
    agent any
    // environment {   
    // }
    stages{
        stage("Deploy static website on AWS S3"){
            steps{
              withAWS(credentials: "AWS-ID", region: 'us-east-1'){
                s3Upload(file:'public/index.html', bucket: "${BUCKET_NAME}", path:'')
                s3Upload(file:'public/error.html', bucket: "${BUCKET_NAME}", path:'')
                s3Upload(file:'public/css/style.css', bucket: "${BUCKET_NAME}", path:'css/')
                s3Upload(file:'public/js/script.js', bucket: "${BUCKET_NAME}", path:'js/')
                s3Upload(includePathPattern: '*', workingDir: 'public/images',  bucket: "${BUCKET_NAME}", path:'images/')
              }
            }
            post{
                always{
                     echo "Ce bloc s'affiche dans tous les cas"
                }
                success{
                    echo "Ce bloc s'affiche quand c'est tout est success"
                    // notification par mail, slack
                }
                failure{
                     echo "Ce bloc s'affiche quand y'a une erreur"
                    // notification par mail, slack
                }
            }
        }
        stage ("Second stage"){
            steps {
                echo "Second stage"
            }
        }
    }
    post{
        always{
            echo "Ce bloc s'affiche dans tous les cas"
        }
        success{
            echo "Ce bloc s'affiche quand c'est tout est success"
            mail to: "devsecure.io@gmail.com",
            subject: "Jenkins CI/CD pipeline",
            body: "Le pipeline Jenkins s'est exécuté avec succès"
        }
        failure{
           echo "Ce bloc s'affiche quand y'a une erreur"
           mail to: "devsecure.io@gmail.com",
           subject: "Jenkins CI/CD pipeline",
           body: "Le pipeline Jenkins s'est exécuté sans succès"
        }
    }
}

