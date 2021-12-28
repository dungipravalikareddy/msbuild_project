pipeline {
    agent any
    
    environment {
        
        dotnet='C:\\Program Files (x86)\\dotnet'
        awscli = "C:\\Program Files\\Amazon\\AWSCLIV2\\awscli"
    }

    stages {
        stage('Checkout') {
            steps {
             git 'https://github.com/dungipravalikareddy/msbuild_project.git'   
            }
        }
        stage('Restore') {
            steps {
                bat 'dotnet restore C:\\WINDOWS\\system32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\dotnet6\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'
            }
        }
        stage('Clean') {
            steps {
                bat 'dotnet clean C:\\WINDOWS\\system32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\dotnet6\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'
            }
        }
        stage('Build') {
            steps {
                bat 'dotnet build C:\\WINDOWS\\system32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\dotnet6\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj --configuration Release'
            }
        }
        stage('Unit Test') {
            steps {
                bat 'dotnet test C:\\WINDOWS\\system32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\dotnet6\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'
            }
        }
        stage('Publish') {
            steps {
                bat 'dotnet publish C:\\WINDOWS\\system32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\dotnet6\\ConsoleApp\\ConsoleApp\\ConsoleApp.csproj'
            }   
        }
        
       
        stage('Uploading') {
               steps {
      // you need cloudbees aws credentials
                    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '0e6c4ec2-57e5-4bee-b36b-8de0ab7fdbe8', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
                {
                    bat 'aws s3 ls'
                    bat 'aws s3 cp C:\\Windows\\System32\\config\\systemprofile\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\dotnet6\\ConsoleApp\\ConsoleApp\\bin\\Debug\\netcoreapp3.1\\ConsoleApp.dll  s3://awscli-upload/hi/ConsoleApp.dll'
                }
            }
        }
    }
}
