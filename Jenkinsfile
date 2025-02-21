node {
    // Print the detected branch name
    echo "Running on branch: ${env.GIT_BRANCH}"

    // Handle branch name detection issues
    if (env.GIT_BRANCH == null) {
        script {
            env.GIT_BRANCH = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()
        }
        echo "Manually detected branch: ${env.GIT_BRANCH}"
    }

    // Check if it's the correct branch
    if (env.GIT_BRANCH == 'refs/heads/feature-ci-pipeline' || env.GIT_BRANCH == 'feature-ci-pipeline' || env.GIT_BRANCH == 'origin/feature-ci-pipeline') {
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
        echo "Skipping pipeline execution because branch is not 'feature-ci-pipeline'. Detected: ${env.GIT_BRANCH}"
    }
}
