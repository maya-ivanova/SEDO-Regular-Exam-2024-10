node {
        stage('Define env variables'){
        env.GIT_BRANCH = 'refs/heads/feature-ci-pipeline' 
        env.PATH_TO_PROJECT_FILE = "C:\\Users\\jenkins\\Documents\\SEDO-Regular-Exam-2024-10\\HouseRentingSystem.sln"
        }

        stage('Clean Working Space') {
            cleanWs()
        }

        stage('Restore Project Packages') {
            bat "dotnet restore %PATH_TO_PROJECT_FILE%"
            echo "Package restore done!"
        }

        stage('Add final line') {
            echo "These were to check the env vars syntax on branch %GIT_BRANCH%"
        }
}
