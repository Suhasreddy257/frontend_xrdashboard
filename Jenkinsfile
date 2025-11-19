// pipeline {
//     agent any

//     environment {
//         GIT_CREDENTIALS = 'token'
//         REPO_URL        = 'https://github.com/Suhasreddy257/xrdashboard.git'

//         // PROJECT_DIR     = 'xr-dashbaoard-frontend-dev'
//         BUILD_OUTPUT    = 'dist\\xr-dashboard\\browser'

//         DEPLOY_PATH     = 'D:\\buildforpipeline'
//         NODE_PATH       = 'C:\\Program Files\\nodejs'
//         IIS_SITE_NAME   = 'XRdashboardfrontend'
//     }

//     // stages {
//     //     stage('Checkout & Build') {
//     //         steps {
//     //             withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {
//     //                 // Checkout the correct branch
//     //                 git branch: 'main', credentialsId: "${GIT_CREDENTIALS}", url: "${REPO_URL}"
 
//     //                 // Verify Node and npm
//     //                 bat 'node -v'
//     //                 bat 'npm -v'
 
//     //                 // Install dependencies & build
//     //                 bat 'npm install'
//     //                 bat 'npm run build'
//     //             }
//     //         }
//     //     }


//     stages {
//         stage('Checkout & Build') {
//             steps {
//                 withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {

//                     git branch: 'main',
//                         credentialsId: "${GIT_CREDENTIALS}",
//                         url: "${REPO_URL}"

//                     dir("${PROJECT_DIR}") {
//                         bat 'dir'
//                         bat 'node -v'
//                         bat 'npm -v'
//                         bat 'npm install'
//                         bat 'npm run build'
//                     }
//                 }
//             }
//         }

//         stage('Deploy to IIS') {
//             steps {
//                 withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {

//                     dir("${PROJECT_DIR}") {

//                         // bat """
//                         // IF NOT EXIST "${DEPLOY_PATH}" (
//                         //     mkdir "${DEPLOY_PATH}"
//                         // )
//                         // """

//                         bat """
//                         robocopy "${BUILD_OUTPUT}" "${DEPLOY_PATH}" /MIR
//                         IF %ERRORLEVEL% LEQ 3 (
//                             EXIT /B 0
//                         ) ELSE (
//                             EXIT /B %ERRORLEVEL%
//                         )
//                         """

//                         // Safe IIS restart
//                         bat """
//                         powershell -NoProfile -ExecutionPolicy Bypass -Command ^
//                           "Import-Module WebAdministration; ^
//                            if (Get-Command Stop-Website -ErrorAction SilentlyContinue) { ^
//                                Write-Host 'Restarting IIS site ${XRdashboardfrontend}...'; ^
//                                Stop-Website -Name '${XRdashboardfrontend}' -ErrorAction SilentlyContinue; ^
//                                Start-Website -Name '${XRdashboardfrontend}' -ErrorAction SilentlyContinue; ^
//                                Write-Host 'IIS restart complete.'; ^
//                            } else { ^
//                                Write-Host 'IIS Website cmdlets not available, skipping restart.' ^
//                            }"
//                         """

//                     }
//                 }
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Pipeline completed successfully!'
//         }
//         failure {
//             echo 'Pipeline failed!'
//         }
//     }
// }


// pipeline {
//     agent any
 
//     environment {
//         GIT_CREDENTIALS = 'token' // Jenkins Git credentials ID
//         REPO_URL = 'https://github.com/Suhasreddy257/dashboardproject.git'
//         DEPLOY_PATH = 'D:\\buildforpipeline'
//         NODE_PATH = 'C:\\Program Files\\nodejs'  // Node.js install path
//     }
 
//     stages {
//         stage('Checkout & Build') {
//             steps {
//                 withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {
//                     // Checkout the correct branch
//                     git branch: 'main', credentialsId: "${GIT_CREDENTIALS}", url: "${REPO_URL}"
 
//                     // Verify Node and npm
//                     bat 'node -v'
//                     bat 'npm -v'
 
//                     // Install dependencies & build
//                     bat 'npm install'
//                     bat 'npm run build'
//                 }
//             }
//         }
 
//         stage('Deploy') {
//             steps {
//                 withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {
//                     // Copy build to IIS folder
//                     bat "xcopy /E /Y dist ${DEPLOY_PATH}"
//                 }
//             }
//         }
//     }
 
//     post {
//         success {
//             echo 'Pipeline completed successfully!'
//         }
//         failure {
//             echo 'Pipeline failed!'
//         }
//     }
// }



// 
//working pipline and some error in the hosting path in the IIS

// pipeline {
//     agent any

//     environment {
//         GIT_CREDENTIALS = 'token' // Jenkins Git credentials ID
//         REPO_URL        = 'https://github.com/Suhasreddy257/frontend_xrdashboard.git'

//         // Base deploy path
//         DEPLOY_BASE     = 'D:\\buildforpipeline'
//         // Final app folder path under base: D:\buildforpipeline\xr-dashboard\browser
//         APP_FOLDER      = 'xr-dashboard\\browser'

//         NODE_PATH       = 'C:\\Program Files\\nodejs'  // Node.js install path

//         // IIS details
//         IIS_SITE_NAME   = 'XRdashboardfrontend'
//         IIS_PORT        = '9005'   // Used only if binding on this port is missing

//         // Extra folder path to copy
//         EXTRA_FOLDER_SOURCE = 'D:\\extra'  // Specify path to your extra folder
//     }

//     stages {
//         stage('Checkout & Build') {
//             steps {
//                 withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {
//                     // Checkout branch
//                     git branch: 'main',
//                         credentialsId: "${GIT_CREDENTIALS}",
//                         url: "${REPO_URL}"

//                     // Verify Node and npm
//                     bat 'node -v'
//                     bat 'npm -v'

//                     // Install dependencies & build
//                     bat 'npm install'
//                     bat 'npm run build'
//                 }
//             }
//         }

//         stage('Deploy to Folder') {
//             steps {
//                 bat '''
//                 echo Cleaning old deploy folder...
//                 if exist "%DEPLOY_BASE%\\%APP_FOLDER%" (
//                     rmdir /S /Q "%DEPLOY_BASE%\\%APP_FOLDER%"
//                 )

//                 echo Creating target folder...
//                 mkdir "%DEPLOY_BASE%\\%APP_FOLDER%"

//                 echo Copying build output (dist) to target folder...
//                 xcopy /E /Y dist "%DEPLOY_BASE%\\%APP_FOLDER%\\"
                
//                 echo Copying EXTRA folder contents into deploy folder...
//                 if exist "%EXTRA_FOLDER_SOURCE%" (
//                     xcopy /E /I /Y "%EXTRA_FOLDER_SOURCE%\\*" "%DEPLOY_BASE%\\%APP_FOLDER%\\"
//                 ) else (
//                     echo EXTRA FOLDER NOT FOUND: %EXTRA_FOLDER_SOURCE%
//                 )
//                 '''
//             }
//         }

//         stage('Update IIS Site & Restart') {
//             steps {
//                 // Update IIS physical path and restart the site
//                 powershell '''
//                     Import-Module WebAdministration

//                     $siteName     = $env:IIS_SITE_NAME
//                     $physicalPath = "$env:DEPLOY_BASE\\$env:APP_FOLDER"
//                     $port         = [int]$env:IIS_PORT

//                     Write-Host "Using IIS site: $siteName"
//                     Write-Host "Setting physical path to: $physicalPath"

//                     # Get the site (will error if not existing)
//                     $site = Get-Item "IIS:\\Sites\\$siteName" -ErrorAction Stop

//                     # Set physical path for root application
//                     Set-ItemProperty "IIS:\\Sites\\$siteName" -Name physicalPath -Value $physicalPath

//                     # Build the pattern safely (no weird $variable: parsing)
//                     $pattern = "*:" + $port + ":*"

//                     # Check if a binding with that port already exists
//                     $bindings = $site.Bindings.Collection
//                     $hasPortBinding = $bindings | Where-Object {
//                         $_.bindingInformation -like $pattern
//                     }

//                     if (-not $hasPortBinding) {
//                         Write-Host "Binding on port $port not found. Adding HTTP binding..."
//                         New-WebBinding -Name $siteName -Protocol "http" -Port $port -IPAddress "*" -HostHeader ""
//                     } else {
//                         Write-Host "Binding on port $port already exists. No change."
//                     }

//                     Write-Host "Restarting IIS site $siteName ..."
//                     Restart-WebItem "IIS:\\Sites\\$siteName"

//                     Write-Host "IIS update and restart completed."
//                 '''
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Pipeline completed successfully!'
//         }
//         failure {
//             echo 'Pipeline failed!'
//         }
//     }
// }

// complete working code without error and hosting in the IIS properly
// pipeline {
//     agent any

//     environment {
//         GIT_CREDENTIALS = 'token'
//         REPO_URL        = 'https://github.com/Suhasreddy257/frontend_xrdashboard.git'

//         DEPLOY_BASE     = 'D:\\buildforpipeline'
//         APP_FOLDER      = 'xr-dashboard\\browser'

//         NODE_PATH       = 'C:\\Program Files\\nodejs'

//         IIS_SITE_NAME   = 'XRdashboardfrontend'
//         IIS_PORT        = '9005'

//         EXTRA_FOLDER_SOURCE = 'D:\\extra'
//     }

//     stages {

//         stage('Checkout & Build') {
//             steps {
//                 withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {

//                     git branch: 'main',
//                         credentialsId: "${GIT_CREDENTIALS}",
//                         url: "${REPO_URL}"

//                     bat 'node -v'
//                     bat 'npm -v'

//                     bat 'npm install'
//                     bat 'npm run build'
//                 }
//             }
//         }

//         stage('Deploy to Folder') {
//             steps {
//                 bat '''
//                 echo Cleaning old deploy folder...
//                 if exist "%DEPLOY_BASE%\\%APP_FOLDER%" (
//                     rmdir /S /Q "%DEPLOY_BASE%\\%APP_FOLDER%"
//                 )

//                 echo Creating target folder...
//                 mkdir "%DEPLOY_BASE%\\%APP_FOLDER%"

//                 echo Copying ONLY inner build folder...
//                 xcopy /E /I /Y "dist\\xr-dashboard\\browser\\*" "%DEPLOY_BASE%\\%APP_FOLDER%\\"

//                 echo Copying EXTRA folder...
//                 if exist "%EXTRA_FOLDER_SOURCE%" (
//                     xcopy /E /I /Y "%EXTRA_FOLDER_SOURCE%\\*" "%DEPLOY_BASE%\\%APP_FOLDER%\\"
//                 ) else (
//                     echo EXTRA FOLDER NOT FOUND: %EXTRA_FOLDER_SOURCE%
//                 )
//                 '''
//             }
//         }

//         stage('Update IIS Site & Restart') {
//             steps {
//                 powershell '''
//                     Import-Module WebAdministration

//                     $siteName     = $env:IIS_SITE_NAME
//                     $physicalPath = "$env:DEPLOY_BASE\\$env:APP_FOLDER"
//                     $port         = [int]$env:IIS_PORT

//                     Write-Host "Setting IIS Physical Path to $physicalPath"

//                     $site = Get-Item "IIS:\\Sites\\$siteName" -ErrorAction Stop

//                     Set-ItemProperty "IIS:\\Sites\\$siteName" -Name physicalPath -Value $physicalPath

//                     $pattern = "*:" + $port + ":*"
//                     $bindings = $site.Bindings.Collection
//                     $hasPortBinding = $bindings | Where-Object { $_.bindingInformation -like $pattern }

//                     if (-not $hasPortBinding) {
//                         New-WebBinding -Name $siteName -Protocol "http" -Port $port -IPAddress "*" -HostHeader ""
//                     }

//                     Restart-WebItem "IIS:\\Sites\\$siteName"
//                 '''
//             }
//         }
//     }

//     post {
//         success { echo 'Pipeline completed successfully!' }
//         failure { echo 'Pipeline failed!' }
//     }
// }

// Jenkinsfile - complete working pipeline with secure email notifications
pipeline {
    agent any

    environment {
        GIT_CREDENTIALS     = 'token'
        REPO_URL            = 'https://github.com/Suhasreddy257/frontend_xrdashboard.git'

        DEPLOY_BASE         = 'D:\\buildforpipeline'
        APP_FOLDER          = 'xr-dashboard\\browser'

        NODE_PATH           = 'C:\\Program Files\\nodejs'

        IIS_SITE_NAME       = 'XRdashboardfrontend'
        IIS_PORT            = '9005'

        EXTRA_FOLDER_SOURCE = 'D:\\extra'

        // NOTE: don't store the recipient here if you created the 'personal-email' credential.
        // PERSONAL_EMAIL = 'reddydr257@gmail.com'
    }

    stages {

        stage('Checkout & Build') {
            steps {
                withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {
                    // Checkout
                    git branch: 'main',
                        credentialsId: "${GIT_CREDENTIALS}",
                        url: "${REPO_URL}"

                    // Diagnostics
                    bat 'node -v'
                    bat 'npm -v'

                    // Install & build
                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        stage('Deploy to Folder') {
            steps {
                bat '''
                echo Cleaning old deploy folder...
                if exist "%DEPLOY_BASE%\\%APP_FOLDER%" (
                    rmdir /S /Q "%DEPLOY_BASE%\\%APP_FOLDER%"
                )

                echo Creating target folder...
                mkdir "%DEPLOY_BASE%\\%APP_FOLDER%"

                echo Copying ONLY inner build folder...
                xcopy /E /I /Y "dist\\xr-dashboard\\browser\\*" "%DEPLOY_BASE%\\%APP_FOLDER%\\"

                echo Copying EXTRA folder...
                if exist "%EXTRA_FOLDER_SOURCE%" (
                    xcopy /E /I /Y "%EXTRA_FOLDER_SOURCE%\\*" "%DEPLOY_BASE%\\%APP_FOLDER%\\"
                ) else (
                    echo EXTRA FOLDER NOT FOUND: %EXTRA_FOLDER_SOURCE%
                )
                '''
            }
        }

        stage('Update IIS Site & Restart') {
            steps {
                powershell '''
                    Import-Module WebAdministration

                    $siteName     = $env:IIS_SITE_NAME
                    $physicalPath = "$env:DEPLOY_BASE\\$env:APP_FOLDER"
                    $port         = [int]$env:IIS_PORT

                    Write-Host "Setting IIS Physical Path to $physicalPath"

                    $site = Get-Item "IIS:\\Sites\\$siteName" -ErrorAction Stop

                    Set-ItemProperty "IIS:\\Sites\\$siteName" -Name physicalPath -Value $physicalPath

                    $pattern = "*:" + $port + ":*"
                    $bindings = $site.Bindings.Collection
                    $hasPortBinding = $bindings | Where-Object { $_.bindingInformation -like $pattern }

                    if (-not $hasPortBinding) {
                        New-WebBinding -Name $siteName -Protocol "http" -Port $port -IPAddress "*" -HostHeader ""
                    }

                    Restart-WebItem "IIS:\\Sites\\$siteName"
                '''
            }
        }
    }

    post {
        // Using credential to fetch recipient securely
        // Create a Jenkins "Secret text" or "String" credential with ID 'personal-email' and value 'reddydr257@gmail.com'
        success {
            echo "Build succeeded — sending notification email."

            // Retrieve the recipient address from Jenkins credentials
            withCredentials([string(credentialsId: 'personal-email', variable: 'RECIPIENT')]) {

                // Preferred: rich email using Email Extension plugin (emailext).
                // Requires: Email Extension Plugin installed and Extended E-mail Notification (or global SMTP) configured.
                // This will send HTML email and attach the build log.
                // If you do not have the plugin, comment the emailext block and uncomment the mail fallback below.
                emailext (
                    subject: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    mimeType: 'text/html',
                    to: "${RECIPIENT}",
                    body: """
                        <html>
                        <body>
                            <h2>Build Succeeded ✅</h2>
                            <p><b>Job:</b> ${env.JOB_NAME}</p>
                            <p><b>Build number:</b> <a href='${env.BUILD_URL}'>#${env.BUILD_NUMBER}</a></p>
                            <p><b>Node:</b> ${env.NODE_NAME ?: 'built-on-controller'}</p>
                            <p>Deployment path: <code>${env.DEPLOY_BASE}\\${env.APP_FOLDER}</code></p>
                            <hr/>
                            <p>Regards,<br/>Jenkins</p>
                        </body>
                        </html>
                    """,
                    attachLog: true
                )

                // Fallback (if you do NOT have emailext): uncomment below and comment out the emailext block above
                /*
                mail to: "${RECIPIENT}",
                     subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                     body: """Hello,

The Jenkins job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} succeeded.

Job: ${env.JOB_NAME}
Build URL: ${env.BUILD_URL}

Regards,
Jenkins
"""
                */
            }
        }

        failure {
            echo "Build failed — sending failure notification."

            withCredentials([string(credentialsId: 'personal-email', variable: 'RECIPIENT')]) {

                // Send failure notification (emailext recommended)
                emailext (
                    subject: "❌ FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    mimeType: 'text/html',
                    to: "${RECIPIENT}",
                    body: """
                        <html>
                        <body>
                            <h2>Build Failed ❌</h2>
                            <p><b>Job:</b> ${env.JOB_NAME}</p>
                            <p><b>Build number:</b> <a href='${env.BUILD_URL}'>#${env.BUILD_NUMBER}</a></p>
                            <p><b>Failed on node:</b> ${env.NODE_NAME ?: 'controller'}</p>
                            <p>Please review the console output for error details.</p>
                            <hr/>
                            <p>Regards,<br/>Jenkins</p>
                        </body>
                        </html>
                    """,
                    attachLog: true
                )

                // Fallback mail (uncomment if you don't have Email Extension plugin)
                /*
                mail to: "${RECIPIENT}",
                     subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                     body: """Hello,

The Jenkins job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} has FAILED.

Job: ${env.JOB_NAME}
Build URL: ${env.BUILD_URL}

Please check the console output for details.

Regards,
Jenkins
"""
                */
            }
        }

        always {
            echo "Post actions completed."
        }
    }
}








// pipeline {
//     agent any

//     environment {
//         GIT_CREDENTIALS = 'token'
//         REPO_URL        = 'https://github.com/Suhasreddy257/frontend_xrdashboard.git'

//         // Base deploy folder
//         DEPLOY_BASE     = 'D:\\buildforpipeline'

//         // Final deploy folder → D:\buildforpipeline\xr-dashboard\browser
//         APP_FOLDER      = 'xr-dashboard\\browser'

//         NODE_PATH       = 'C:\\Program Files\\nodejs'

//         IIS_SITE_NAME   = 'XRdashboardfrontend'
//         IIS_PORT        = '9005'

//         // EXTRA FOLDER LOCATION YOU GAVE
//         EXTRA_FOLDER_SOURCE = 'D:\\extra'
//     }

//     stages {

//         stage('Checkout & Build') {
//             steps {
//                 withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {

//                     git branch: 'main',
//                         credentialsId: "${GIT_CREDENTIALS}",
//                         url: "${REPO_URL}"

//                     bat 'node -v'
//                     bat 'npm -v'

//                     bat 'npm install'
//                     bat 'npm run build'
//                 }
//             }
//         }

//         stage('Deploy to Folder') {
//             steps {
//                 bat '''
//                 echo Cleaning old deploy folder...

//                 if exist "%DEPLOY_BASE%\\%APP_FOLDER%" (
//                     rmdir /S /Q "%DEPLOY_BASE%\\%APP_FOLDER%"
//                 )

//                 echo Creating deploy directory...
//                 mkdir "%DEPLOY_BASE%\\%APP_FOLDER%"

//                 echo Copying build output...
//                 xcopy /E /I /Y dist "%DEPLOY_BASE%\\%APP_FOLDER%\\"

//                 echo Copying EXTRA FOLDER from D:\\extra ...
//                 if exist "%EXTRA_FOLDER_SOURCE%" (
//                     xcopy /E /I /Y "%EXTRA_FOLDER_SOURCE%\\*" "%DEPLOY_BASE%\\%APP_FOLDER%\\"
//                 ) else (
//                     echo EXTRA FOLDER NOT FOUND: %EXTRA_FOLDER_SOURCE%
//                 )
//                 '''
//             }
//         }

//         stage('Update IIS Site & Restart') {
//             steps {
//                 powershell '''
//                     Import-Module WebAdministration

//                     $siteName = $env:IIS_SITE_NAME
//                     $physicalPath = "$env:DEPLOY_BASE\\$env:APP_FOLDER"
//                     $port = [int]$env:IIS_PORT

//                     Write-Host "Setting IIS site path to: $physicalPath"

//                     $site = Get-Item "IIS:\\Sites\\$siteName" -ErrorAction Stop

//                     Set-ItemProperty "IIS:\\Sites\\$siteName" -Name physicalPath -Value $physicalPath

//                     $pattern = "*:" + $port + ":*"
//                     $bindings = $site.Bindings.Collection

//                     $hasPortBinding = $bindings | Where-Object {
//                         $_.bindingInformation -like $pattern
//                     }

//                     if (-not $hasPortBinding) {
//                         Write-Host "Adding port $port binding..."
//                         New-WebBinding -Name $siteName -Protocol "http" -Port $port -IPAddress "*" -HostHeader ""
//                     }

//                     Write-Host "Restarting IIS site..."
//                     Restart-WebItem "IIS:\\Sites\\$siteName"

//                     Write-Host "IIS update completed successfully"
//                 '''
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Pipeline completed successfully!'
//         }
//         failure {
//             echo 'Pipeline failed!'
//         }
//     }
// }

// today updated pipeline working 18-11
// pipeline {
//     agent any

//     environment {
//         GIT_CREDENTIALS = 'token'
//         REPO_URL        = 'https://github.com/Suhasreddy257/frontend_xrdashboard.git'

//         // Base deploy folder
//         DEPLOY_BASE     = 'D:\\buildforpipeline'

//         // Final deploy folder → D:\buildforpipeline\xr-dashboard\browser
//         APP_FOLDER      = 'xr-dashboard\\browser'

//         NODE_PATH       = 'C:\\Program Files\\nodejs'

//         IIS_SITE_NAME   = 'XRdashboardfrontend'
//         IIS_PORT        = '9005'

//         // EXTRA FOLDER LOCATION
//         EXTRA_FOLDER_SOURCE = 'D:\\extra'
//     }

//     stages {

//         stage('Checkout & Build') {
//             steps {
//                 withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {

//                     git branch: 'main',
//                         credentialsId: "${GIT_CREDENTIALS}",
//                         url: "${REPO_URL}"

//                     bat 'node -v'
//                     bat 'npm -v'

//                     bat 'npm install'
//                     bat 'npm run build'
//                 }
//             }
//         }

//         stage('Deploy to Folder') {
//             steps {
//                 bat '''
//                 echo Cleaning old deploy folder...

//                 if exist "%DEPLOY_BASE%\\%APP_FOLDER%" (
//                     rmdir /S /Q "%DEPLOY_BASE%\\%APP_FOLDER%"
//                 )

//                 echo Creating deploy directory...
//                 mkdir "%DEPLOY_BASE%\\%APP_FOLDER%"

//                 echo Copying build output...
//                 xcopy /E /I /Y dist "%DEPLOY_BASE%\\%APP_FOLDER%\\"

//                 echo Copying EXTRA FOLDER into deployed browser folder...
//                 if exist "%EXTRA_FOLDER_SOURCE%" (
//                     xcopy /E /I /Y "%EXTRA_FOLDER_SOURCE%\\*" "%DEPLOY_BASE%\\%APP_FOLDER%\\"
//                 ) else (
//                     echo EXTRA FOLDER NOT FOUND: %EXTRA_FOLDER_SOURCE%
//                 )
//                 '''
//             }
//         }

//         stage('Update IIS Site & Restart') {
//             steps {
//                 powershell '''
//                     Import-Module WebAdministration

//                     $siteName = $env:IIS_SITE_NAME
//                     $physicalPath = "$env:DEPLOY_BASE\\$env:APP_FOLDER"
//                     $port = [int]$env:IIS_PORT

//                     Write-Host "Setting IIS site path to: $physicalPath"

//                     $site = Get-Item "IIS:\\Sites\\$siteName" -ErrorAction Stop

//                     Set-ItemProperty "IIS:\\Sites\\$siteName" -Name physicalPath -Value $physicalPath

//                     $pattern = "*:" + $port + ":*"
//                     $bindings = $site.Bindings.Collection

//                     $hasPortBinding = $bindings | Where-Object {
//                         $_.bindingInformation -like $pattern
//                     }

//                     if (-not $hasPortBinding) {
//                         Write-Host "Adding port $port binding..."
//                         New-WebBinding -Name $siteName -Protocol "http" -Port $port -IPAddress "*" -HostHeader ""
//                     }

//                     Write-Host "Restarting IIS site..."
//                     Restart-WebItem "IIS:\\Sites\\$siteName"

//                     Write-Host "IIS update completed successfully"
//                 '''
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Pipeline completed successfully!'
//         }
//         failure {
//             echo 'Pipeline failed!'
//         }
//     }
// }

// pipeline {
//     agent any

//     environment {
//         GIT_CREDENTIALS = 'token'
//         REPO_URL        = 'https://github.com/Suhasreddy257/frontend_xrdashboard.git'

//         // Base deploy folder
//         DEPLOY_BASE     = 'D:\\buildforpipeline'

//         // Final deploy folder → D:\buildforpipeline\xr-dashboard\browser\xr-dashboard\browser
//         APP_FOLDER      = 'xr-dashboard\\browser\\xr-dashboard\\browser'

//         NODE_PATH       = 'C:\\Program Files\\nodejs'

//         IIS_SITE_NAME   = 'XRdashboardfrontend'
//         IIS_PORT        = '9005'

//         // EXTRA FOLDER LOCATION
//         EXTRA_FOLDER_SOURCE = 'D:\\extra'
//     }

//     stages {

//         stage('Checkout & Build') {
//             steps {
//                 withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {

//                     git branch: 'main',
//                         credentialsId: "${GIT_CREDENTIALS}",
//                         url: "${REPO_URL}"

//                     bat 'node -v'
//                     bat 'npm -v'

//                     bat 'npm install'
//                     bat 'npm run build'
//                 }
//             }
//         }

//         stage('Deploy to Folder') {
//             steps {
//                 bat '''
//                 echo Cleaning old deploy folder...

//                 if exist "%DEPLOY_BASE%\\%APP_FOLDER%" (
//                     rmdir /S /Q "%DEPLOY_BASE%\\%APP_FOLDER%"
//                 )

//                 echo Creating deploy directory...
//                 mkdir "%DEPLOY_BASE%\\%APP_FOLDER%"

//                 echo Copying build output...
//                 xcopy /E /I /Y dist "%DEPLOY_BASE%\\%APP_FOLDER%\\"

//                 echo Copying EXTRA FOLDER into deployed browser folder...
//                 if exist "%EXTRA_FOLDER_SOURCE%" (
//                     xcopy /E /I /Y "%EXTRA_FOLDER_SOURCE%\\*" "%DEPLOY_BASE%\\%APP_FOLDER%\\"
//                 ) else (
//                     echo EXTRA FOLDER NOT FOUND: %EXTRA_FOLDER_SOURCE%
//                 )
//                 '''
//             }
//         }

//         stage('Update IIS Site & Restart') {
//             steps {
//                 powershell '''
//                     Import-Module WebAdministration

//                     $siteName = $env:IIS_SITE_NAME
//                     $physicalPath = "$env:DEPLOY_BASE\\$env:APP_FOLDER"
//                     $port = [int]$env:IIS_PORT

//                     Write-Host "Setting IIS site path to: $physicalPath"

//                     $site = Get-Item "IIS:\\Sites\\$siteName" -ErrorAction Stop

//                     Set-ItemProperty "IIS:\\Sites\\$siteName" -Name physicalPath -Value $physicalPath

//                     $pattern = "*:" + $port + ":*"
//                     $bindings = $site.Bindings.Collection

//                     $hasPortBinding = $bindings | Where-Object {
//                         $_.bindingInformation -like $pattern
//                     }

//                     if (-not $hasPortBinding) {
//                         Write-Host "Adding port $port binding..."
//                         New-WebBinding -Name $siteName -Protocol "http" -Port $port -IPAddress "*" -HostHeader ""
//                     }

//                     Write-Host "Restarting IIS site..."
//                     Restart-WebItem "IIS:\\Sites\\$siteName"

//                     Write-Host "IIS update completed successfully"
//                 '''
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Pipeline completed successfully!'
//         }
//         failure {
//             echo 'Pipeline failed!'
//         }
//     }
// }


// pipeline {
//     agent any

//     environment {
//         GIT_CREDENTIALS = 'token'
//         REPO_URL        = 'https://github.com/Suhasreddy257/frontend_xrdashboard.git'

//         // Base deploy folder
//         DEPLOY_BASE     = 'D:\\buildforpipeline'

//         // Final deploy folder → D:\buildforpipeline\xr-dashboard\browser\xr-dashboard\browser
//         APP_FOLDER      = 'xr-dashboard\\browser'

//         NODE_PATH       = 'C:\\Program Files\\nodejs'

//         IIS_SITE_NAME   = 'XRdashboardfrontend'
//         IIS_PORT        = '9005'

//         // EXTRA FOLDER LOCATION
//         EXTRA_FOLDER_SOURCE = 'D:\\extra'
//     }

//     stages {

//         stage('Checkout & Build') {
//             steps {
//                 withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {

//                     git branch: 'main',
//                         credentialsId: "${GIT_CREDENTIALS}",
//                         url: "${REPO_URL}"

//                     bat 'node -v'
//                     bat 'npm -v'

//                     bat 'npm install'
//                     bat 'npm run build'
//                 }
//             }
//         }

//         stage('Deploy to Folder') {
//             steps {
//                 bat '''
//                 echo Cleaning old deploy folder...
//                 if exist "%DEPLOY_BASE%\\%APP_FOLDER%" (
//                     rmdir /S /Q "%DEPLOY_BASE%\\%APP_FOLDER%"
//                 )

//                 echo Creating deploy directory...
//                 mkdir "%DEPLOY_BASE%\\%APP_FOLDER%"

//                 echo Copying build output...
//                 xcopy /E /I /Y dist "%DEPLOY_BASE%\\%APP_FOLDER%\\"

//                 echo Copying EXTRA FOLDER contents directly into deployed browser folder...
//                 if exist "%EXTRA_FOLDER_SOURCE%" (
//                     xcopy /E /I /Y "%EXTRA_FOLDER_SOURCE%\\*" "%DEPLOY_BASE%\\%APP_FOLDER%\\"
//                 ) else (
//                     echo EXTRA FOLDER NOT FOUND: %EXTRA_FOLDER_SOURCE%
//                 )
//                 '''
//             }
//         }

//         stage('Update IIS Site & Restart') {
//             steps {
//                 powershell '''
//                     Import-Module WebAdministration

//                     $siteName = $env:IIS_SITE_NAME
//                     $physicalPath = "$env:DEPLOY_BASE\\$env:APP_FOLDER"
//                     $port = [int]$env:IIS_PORT

//                     Write-Host "Setting IIS site path to: $physicalPath"

//                     $site = Get-Item "IIS:\\Sites\\$siteName" -ErrorAction Stop

//                     Set-ItemProperty "IIS:\\Sites\\$siteName" -Name physicalPath -Value $physicalPath

//                     $pattern = "*:" + $port + ":*"
//                     $bindings = $site.Bindings.Collection

//                     $hasPortBinding = $bindings | Where-Object {
//                         $_.bindingInformation -like $pattern
//                     }

//                     if (-not $hasPortBinding) {
//                         Write-Host "Adding port $port binding..."
//                         New-WebBinding -Name $siteName -Protocol "http" -Port $port -IPAddress "*" -HostHeader ""
//                     }

//                     Write-Host "Restarting IIS site..."
//                     Restart-WebItem "IIS:\\Sites\\$siteName"

//                     Write-Host "IIS update completed successfully"
//                 '''
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Pipeline completed successfully!'
//         }
//         failure {
//             echo 'Pipeline failed!'
//         }
//     }
// }


// some change is doing frorm next pipeline code 
// pipeline {
//     agent any

//     environment {
//         GIT_CREDENTIALS = 'token'
//         REPO_URL        = 'https://github.com/Suhasreddy257/frontend_xrdashboard.git'

//         // Base deploy folder
//         DEPLOY_BASE     = 'D:\\buildforpipeline'

//         // Final deploy folder → D:\buildforpipeline\xr-dashboard\browser\xr-dashboard\browser
//         APP_FOLDER      = 'xr-dashboard\\browser\\xr-dashboard\\browser'

//         NODE_PATH       = 'C:\\Program Files\\nodejs'

//         IIS_SITE_NAME   = 'XRdashboardfrontend'
//         IIS_PORT        = '9005'

//         // Extra folder location
//         EXTRA_FOLDER_SOURCE = 'D:\\extra'
//     }

//     stages {

//         stage('Checkout & Build') {
//             steps {
//                 withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {

//                     git branch: 'main',
//                         credentialsId: "${GIT_CREDENTIALS}",
//                         url: "${REPO_URL}"

//                     bat 'node -v'
//                     bat 'npm -v'

//                     bat 'npm install'
//                     bat 'npm run build'
//                 }
//             }
//         }

//         stage('Deploy to Folder') {
//             steps {
//                 bat '''
//                 echo Cleaning old deploy folder...
//                 if exist "%DEPLOY_BASE%\\%APP_FOLDER%" (
//                     rmdir /S /Q "%DEPLOY_BASE%\\%APP_FOLDER%"
//                 )

//                 echo Creating deploy directory...
//                 mkdir "%DEPLOY_BASE%\\%APP_FOLDER%"

//                 echo Copying build output to deploy folder...
//                 REM Copy only contents of dist, not dist folder itself
//                 xcopy /E /I /Y "dist\\*" "%DEPLOY_BASE%\\%APP_FOLDER%\\"

//                 echo Copying EXTRA folder contents into deploy folder...
//                 if exist "%EXTRA_FOLDER_SOURCE%" (
//                     xcopy /E /I /Y "%EXTRA_FOLDER_SOURCE%\\*" "%DEPLOY_BASE%\\%APP_FOLDER%\\"
//                 ) else (
//                     echo EXTRA FOLDER NOT FOUND: %EXTRA_FOLDER_SOURCE%
//                 )
//                 '''
//             }
//         }

//         stage('Update IIS Site & Restart') {
//             steps {
//                 powershell '''
//                     Import-Module WebAdministration

//                     $siteName = $env:IIS_SITE_NAME
//                     $physicalPath = Join-Path $env:DEPLOY_BASE $env:APP_FOLDER
//                     $port = [int]$env:IIS_PORT

//                     Write-Host "Setting IIS site path to: $physicalPath"

//                     # Ensure IIS site exists
//                     $site = Get-Item "IIS:\\Sites\\$siteName" -ErrorAction Stop

//                     # Update physical path
//                     Set-ItemProperty "IIS:\\Sites\\$siteName" -Name physicalPath -Value $physicalPath

//                     # Check if port binding exists
//                     $pattern = "*:" + $port + ":*"
//                     $bindings = $site.Bindings.Collection
//                     $hasPortBinding = $bindings | Where-Object { $_.bindingInformation -like $pattern }

//                     if (-not $hasPortBinding) {
//                         Write-Host "Adding port $port binding..."
//                         New-WebBinding -Name $siteName -Protocol "http" -Port $port -IPAddress "*" -HostHeader ""
//                     }

//                     Write-Host "Restarting IIS site..."
//                     Restart-WebItem "IIS:\\Sites\\$siteName"

//                     Write-Host "IIS update completed successfully"
//                 '''
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Pipeline completed successfully!'
//         }
//         failure {
//             echo 'Pipeline failed!'
//         }
//     }
// }

