release: heroku run pip uninstall python-dotenv && pipenv shell && python manage.py makemigrations && python manage.py migrate
web: gunicorn config.wsgi --log-file -
