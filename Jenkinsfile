pipeline{
    agent any
    stages{

        stage(Checkout){
            steps{
                git branch: 'main',
                url:'https://github.com/Insaf-Badri/Jenkins-CI-CD.git'
            }
        }

        stage(Setup){
            steps{
                bat """
                python -m venv .venv

                call .venv\\Scripts\\activate
                python -m pip install --upgrade pip
                pip install -r requirements.txt
                """
            }
        }

        stage(Tests){
            parallel{
                stage(test1){
                    steps{
                         bat """
                        call .venv\\Scripts\\activate
                        python -m pytest test_app.py -v
                        """
                    }
                }

                stage(test2){
                    steps{
                         bat """
                        call .venv\\Scripts\\activate
                        python -m pytest test_app_2.py -v
                        """
                    }
                }
            }
        }

        stage(Deploy){
             steps {
                echo 'Starting Flask app locally using Gunicorn...'
                bat """
                call .venv\\Scripts\\activate
                start /B gunicorn --bind 127.0.1.1:5000 app:app > gunicorn.log 2>&1
                echo Gunicorn started on http:/127.0.1.1:5000
                """
            }
        }

    }

}
    









