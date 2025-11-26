




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

// Jenkinsfile - robust pipeline that sends email notifications
// pipeline {
//     agent any

//     environment {
//         // Project settings
//         GIT_CREDENTIALS     = 'token'
//         REPO_URL            = 'https://github.com/Suhasreddy257/frontend_xrdashboard.git'

//         DEPLOY_BASE         = 'D:\\buildforpipeline'
//         APP_FOLDER          = 'xr-dashboard\\browser'

//         NODE_PATH           = 'C:\\Program Files\\nodejs'

//         IIS_SITE_NAME       = 'XRdashboardfrontend'
//         IIS_PORT            = '9005'

//         EXTRA_FOLDER_SOURCE = 'D:\\extra'

//         // Fallback recipient if credential 'personal-email' is not created.
//         // Recommended: create a Secret Text credential with ID 'personal-email' and value 'reddydr257@gmail.com'
//         PERSONAL_EMAIL      = 'reddydr257@gmail.com'
//     }

//     stages {
//         stage('Checkout & Build') {
//             steps {
//                 withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {
//                     // Checkout
//                     git branch: 'main',
//                         credentialsId: "${GIT_CREDENTIALS}",
//                         url: "${REPO_URL}"

//                     // Diagnostics
//                     bat 'node -v'
//                     bat 'npm -v'

//                     // Build
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
//         success {
//             script {
//                 echo "Build succeeded — preparing notification"

//                 // Determine recipient: prefer credential 'personal-email', else use env.PERSONAL_EMAIL
//                 def recipient = env.PERSONAL_EMAIL
//                 try {
//                     withCredentials([string(credentialsId: 'personal-email', variable: 'RECIPIENT')]) {
//                         if (env.RECIPIENT?.trim()) {
//                             recipient = env.RECIPIENT
//                         }
//                     }
//                 } catch (ignored) {
//                     // credential missing or inaccessible — already have fallback
//                     echo "personal-email credential not found; using PERSONAL_EMAIL fallback"
//                 }

//                 def subject = "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
//                 def htmlBody = """
//                     <html><body>
//                       <h2>Build Succeeded ✅</h2>
//                       <p><b>Job:</b> ${env.JOB_NAME}</p>
//                       <p><b>Build:</b> <a href='${env.BUILD_URL}'>#${env.BUILD_NUMBER}</a></p>
//                       <p><b>Node:</b> ${env.NODE_NAME ?: 'controller'}</p>
//                       <p>Deployment path: <code>${env.DEPLOY_BASE}\\${env.APP_FOLDER}</code></p>
//                       <hr/>
//                       <p>Regards,<br/>Jenkins</p>
//                     </body></html>
//                 """

//                 // Try emailext first; on failure print stacktrace and fallback to mail
//                 try {
//                     emailext(
//                         subject: subject,
//                         mimeType: 'text/html',
//                         to: recipient,
//                         body: htmlBody,
//                         attachLog: true
//                     )
//                     echo "Notification sent via emailext to ${recipient}"
//                 } catch (e) {
//                     echo "emailext failed to send email: ${e.toString()}"

//                     // Print full stacktrace for diagnosis (safe: does not include secrets)
//                     def sw = new StringWriter()
//                     e.printStackTrace(new PrintWriter(sw))
//                     echo "emailext stacktrace:\n${sw.toString()}"

//                     // Fallback to mail()
//                     try {
//                         mail to: recipient,
//                              subject: subject,
//                              body: "Build succeeded: ${env.JOB_NAME} #${env.BUILD_NUMBER}\n${env.BUILD_URL}"
//                         echo "Notification sent via mail() fallback to ${recipient}"
//                     } catch (e2) {
//                         echo "mail() fallback also failed: ${e2.toString()}"
//                         def sw2 = new StringWriter()
//                         e2.printStackTrace(new PrintWriter(sw2))
//                         echo "mail() fallback stacktrace:\n${sw2.toString()}"
//                     }
//                 }
//             }
//         }

//         failure {
//             script {
//                 echo "Build failed — preparing notification"

//                 def recipient = env.PERSONAL_EMAIL
//                 try {
//                     withCredentials([string(credentialsId: 'personal-email', variable: 'RECIPIENT')]) {
//                         if (env.RECIPIENT?.trim()) {
//                             recipient = env.RECIPIENT
//                         }
//                     }
//                 } catch (ignored) {
//                     echo "personal-email credential not found; using PERSONAL_EMAIL fallback"
//                 }

//                 def subject = "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
//                 def htmlBody = """
//                     <html><body>
//                       <h2>Build Failed ❌</h2>
//                       <p><b>Job:</b> ${env.JOB_NAME}</p>
//                       <p><b>Build:</b> <a href='${env.BUILD_URL}'>#${env.BUILD_NUMBER}</a></p>
//                       <p>Please review the console output for details.</p>
//                       <hr/>
//                       <p>Regards,<br/>Jenkins</p>
//                     </body></html>
//                 """

//                 try {
//                     emailext(
//                         subject: subject,
//                         mimeType: 'text/html',
//                         to: recipient,
//                         body: htmlBody,
//                         attachLog: true
//                     )
//                     echo "Failure notification sent via emailext to ${recipient}"
//                 } catch (e) {
//                     echo "emailext failed to send failure email: ${e.toString()}"
//                     def sw = new StringWriter()
//                     e.printStackTrace(new PrintWriter(sw))
//                     echo "emailext stacktrace:\n${sw.toString()}"

//                     try {
//                         mail to: recipient,
//                              subject: subject,
//                              body: "Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}\n${env.BUILD_URL}"
//                         echo "Failure notification sent via mail() fallback to ${recipient}"
//                     } catch (e2) {
//                         echo "mail() fallback also failed: ${e2.toString()}"
//                         def sw2 = new StringWriter()
//                         e2.printStackTrace(new PrintWriter(sw2))
//                         echo "mail() fallback stacktrace:\n${sw2.toString()}"
//                     }
//                 }
//             }
//         }

//         always {
//             echo "Post actions finished."
//         }
//     }
// }



// pipeline {
//     agent any

//     environment {
//         GIT_CREDENTIALS     = 'token'
//         REPO_URL            = 'https://github.com/Suhasreddy257/frontend_xrdashboard.git'

//         DEPLOY_BASE         = 'D:\\buildforpipeline'
//         APP_FOLDER          = 'xr-dashboard\\browser'

//         NODE_PATH           = 'C:\\Program Files\\nodejs'

//         IIS_SITE_NAME       = 'XRdashboardfrontend'
//         IIS_PORT            = '9005'

//         EXTRA_FOLDER_SOURCE = 'D:\\extra'

//         // Your email – used by the mail() step
//         PERSONAL_EMAIL      = 'reddydr257@gmail.com'
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
//         success {
//             echo 'Build succeeded — sending success email...'

//             mail to: "${env.PERSONAL_EMAIL}",
//                  subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
//                  body: """Hello Suhas,

// The Jenkins job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} completed SUCCESSFULLY.

// Job name : ${env.JOB_NAME}
// Build URL: ${env.BUILD_URL}

// Regards,
// Jenkins
// """
//         }

//         failure {
//             echo 'Build failed — sending failure email...'

//             mail to: "${env.PERSONAL_EMAIL}",
//                  subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
//                  body: """Hello Suhas,

// The Jenkins job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} has FAILED.

// Job name : ${env.JOB_NAME}
// Build URL: ${env.BUILD_URL}

// Please check the console output in Jenkins for details.

// Regards,
// Jenkins
// """
//         }

//         always {
//             echo 'Post actions finished.'
//         }
//     }
// }
//in the above pipeline is getting succes with all requirement up to succes email 

pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = 'token'
        REPO_URL        = 'https://github.com/Suhasreddy257/frontend_xrdashboard.git'

        // Base deploy directory (no timestamp here)
        DEPLOY_BASE     = 'D:\\buildforpipeline'
        APP_FOLDER      = 'xr-dashboard\\browser'

        NODE_PATH       = 'C:\\Program Files\\nodejs'

        IIS_SITE_NAME   = 'XRdashboardfrontend'
        IIS_PORT        = '9005'

        EXTRA_FOLDER_SOURCE = 'D:\\extra'

        // Your email – used by the mail() step
        PERSONAL_EMAIL  = 'reddydr257@gmail.com'
    }

    stages {

        stage('Prepare Deploy Folder') {
            steps {
                script {
                    // Example: 2025-11-21_10-45-30
                    def ts = new Date().format("yyyy-MM-dd_HH-mm-ss")

                    // Folder name WITH timestamp (relative under DEPLOY_BASE)
                    // e.g. xr-dashboard\browser_2025-11-21_10-45-30
                    env.DEPLOY_FOLDER_NAME = "${APP_FOLDER}_${ts}"

                    // Full path, e.g. D:\buildforpipeline\xr-dashboard\browser_2025-11-21_10-45-30
                    env.DEPLOY_TARGET = "${DEPLOY_BASE}\\${env.DEPLOY_FOLDER_NAME}"

                    echo "Deploy timestamp       : ${ts}"
                    echo "Deploy target full path: ${env.DEPLOY_TARGET}"
                }
            }
        }

        stage('Checkout & Build') {
            steps {
                withEnv(["PATH=${NODE_PATH};${env.PATH}"]) {
                    git branch: 'main',
                        credentialsId: "${GIT_CREDENTIALS}",
                        url: "${REPO_URL}"

                    bat 'node -v'
                    bat 'npm -v'

                    bat 'npm install'
                    bat 'npm run build'
                }
            }
        }

        stage('Deploy to Folder') {
            steps {
                bat '''
                echo Creating target folder (older builds are kept)...
                if not exist "%DEPLOY_TARGET%" (
                    mkdir "%DEPLOY_TARGET%"
                )

                echo Copying ONLY inner build folder to %DEPLOY_TARGET% ...
                xcopy /E /I /Y "dist\\xr-dashboard\\browser\\*" "%DEPLOY_TARGET%\\"

                echo Copying EXTRA folder (if exists)...
                if exist "%EXTRA_FOLDER_SOURCE%" (
                    xcopy /E /I /Y "%EXTRA_FOLDER_SOURCE%\\*" "%DEPLOY_TARGET%\\"
                ) else (
                    echo EXTRA FOLDER NOT FOUND: %EXTRA_FOLDER_SOURCE%
                )

                echo Deploy completed into: %DEPLOY_TARGET%
                '''
            }
        }

        stage('Update IIS Site & Restart') {
            steps {
                powershell '''
                    Import-Module WebAdministration

                    $siteName     = $env:IIS_SITE_NAME
                    $physicalPath = $env:DEPLOY_TARGET   # full timestamped path
                    $port         = [int]$env:IIS_PORT

                    Write-Host "Setting IIS Physical Path to $physicalPath"

                    $site = Get-Item ("IIS:\\Sites\\" + $siteName) -ErrorAction Stop

                    # Point site to the new timestamped folder
                    Set-ItemProperty ("IIS:\\Sites\\" + $siteName) -Name physicalPath -Value $physicalPath

                    # Ensure binding exists for the configured port
                    $pattern = "*:" + $port + ":*"
                    $bindings = $site.Bindings.Collection
                    $hasPortBinding = $bindings | Where-Object { $_.bindingInformation -like $pattern }

                    if (-not $hasPortBinding) {
                        New-WebBinding -Name $siteName -Protocol "http" -Port $port -IPAddress "*" -HostHeader ""
                    }

                    Restart-WebItem ("IIS:\\Sites\\" + $siteName)

                    Write-Host "IIS site '$siteName' now points to: $physicalPath"
                '''
            }
        }
    }

    post {
        success {
            echo 'Build succeeded — sending success email...'

            mail to: "${env.PERSONAL_EMAIL}",
                 subject: "FRONTEND SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """Hello Suhas,

The FRONTEND Jenkins job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} completed SUCCESSFULLY.

Details:
- Job name      : ${env.JOB_NAME}
- Build URL     : ${env.BUILD_URL}
- Deploy folder : ${env.DEPLOY_TARGET}
- IIS site      : ${env.IIS_SITE_NAME}
- Port          : ${env.IIS_PORT}

Older deploy folders are kept under:
${env.DEPLOY_BASE}

Regards,
Jenkins (Frontend pipeline)
"""
        }

        failure {
            echo 'Build failed — sending failure email...'

            mail to: "${env.PERSONAL_EMAIL}",
                 subject: "FRONTEND FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """Hello Suhas,

The FRONTEND Jenkins job '${env.JOB_NAME}' build #${env.BUILD_NUMBER} has FAILED.

Job name  : ${env.JOB_NAME}
Build URL : ${env.BUILD_URL}

(If a deploy folder was created before failure, the last target was:)
${env.DEPLOY_TARGET}

Please check the console output in Jenkins for details.

Regards,
Jenkins (Frontend pipeline)
"""
        }

        always {
            echo 'Post actions finished.'
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


