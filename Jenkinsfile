pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'build.bat'
                mail bcc: '', body: "构建版本成功", cc: '', charset: 'UTF-8', from: 'wq18530929470@163.con', mimeType: 'text/plain', replyTo: '', subject: "构建版本成功", to: "867075698@qq.com";
            }
        }

        stage('Dev_Test'){
            steps {
                input '等待开发人员测试通过，通过后再继续'
            }
        }

        stage('QA_Test') {
            steps {
                echo '执行自动化部署...'
                bat 'python ‪D:\BaiduNetdiskDownload\restapi-teach\static\autodeploy'
                echo '执行自动化测试...'

                dir ('d:\\projects\\sonqqin\\restapi-autotest') {
                    bat 'robot --pythonpath . --name build_%BUILD_NUMBER% -L debug tc'
                }

            }
        }
    }
}