node {
    echo "Running on branch: ${env.BRANCH_NAME}"

    // Check if the branch is correct
    if (env.BRANCH_NAME == null || env.BRANCH_NAME == 'feature-ci-pipeline') {
        env.PATH_TO_PROJECT_FILE = "C:\\Users\\jenkins\\Documents\\SEDO-Regular-Exam-2024-10\\HouseRentingSystem.sln"
        env.PATH_TO_UNIT_TESTS = "C:\\Users\\jenkins\\Documents\\SEDO-Regular-Exam-2024-10\\HouseRentingSystem.UnitTests\\HouseRentingSystem.UnitTests.csproj"
        env.PATH_TO_INTEGRATION_TESTS = "C:\\Users\\jenkins\\Documents\\SEDO-Regular-Exam-2024-10\\HouseRentingSystem.Tests\\HouseRentingSystem.Tests.csproj"

        stage('Clean Working Space') {
            cleanWs()
        }

        stage('Restore Project Packages') {
            bat "dotnet restore \"%PATH_TO_PROJECT_FILE%\""
            echo "Package restore done!"
        }

        stage('Build the Project') {
            bat "dotnet build \"%PATH_TO_PROJECT_FILE%\""
            echo "Build done!"
        }

        stage('Run Both Integration and Unit Tests') {
            bat """
            dotnet test \"%PATH_TO_UNIT_TESTS%\" --configuration Release
            dotnet test \"%PATH_TO_INTEGRATION_TESTS%\" --configuration Release
            echo Tests completed!
            """
        }
    } else {
        echo "Skipping pipeline execution because branch is not 'feature-ci-pipeline'"
    }
}
