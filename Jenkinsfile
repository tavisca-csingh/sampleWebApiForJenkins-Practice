pipeline {
    agent any
    parameters {
        string(defaultValue: 'https://github.com/tavisca-csingh/sampleWebApiForJenkins-Practice.git', name: 'GIT_SSH_PATH')
        string(defaultValue: 'WebApi.sln', name: 'SOLUTION_FILE_PATH')
        string(defaultValue: 'WebApi.Tests/WebApi.Tests.csproj', name: 'TEST_PROJECT_PATH')
    }
    stages {
        stage('Build') {
            steps {
                powershell '''dotnet restore ${SOLUTION_FILE_PATH} --source https://api.nuget.org/v3/index.json
                dotnet build  ${SOLUTION_FILE_PATH} -p:Configuration=release -v:n'''
            }
        }
        stage('Test') {
            steps {
                powershell '''dotnet test ${TEST_PROJECT_PATH}'''
            }
        }
		stage{'Publish'}
		{
		steps{
		powershell '''dotnet publish sampleWebApiForJenkins-Practice -c Release -o artifacts''' 
		}}
		stage{'Archive'}
		{
		steps{
		powershell '''compress-archive sampleWebApiForJenkins-Practice/artifacts published.zip -Update'''
		archiveArtifacts artifacts:'published.zip'
		}}


    }
	post{
	always
	{
	deleteDir()
	}}
}
