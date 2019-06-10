FROM reckonsys/python:latest
COPY Pipfile Pipfile
COPY Pipfile.lock Pipfile.lock
RUN pipenv install
COPY . .
