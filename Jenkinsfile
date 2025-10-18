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
            steps{
                bat """
                python -m pytest test_app.py -v
                """
            }
        }

        stage(Deploy){
             steps {
                echo 'Starting Flask app locally using Gunicorn...'
                bat """
                call %VENV_DIR%\\Scripts\\activate
                start /B gunicorn --bind 127.0.1.1:5000 app:app > gunicorn.log 2>&1
                echo Gunicorn started on http:/127.0.1.1:5000
                """
            }
        }

    }

}
    




