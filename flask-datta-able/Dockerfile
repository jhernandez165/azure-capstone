# Using an explicit multi-architecture base image
FROM --platform=linux/amd64 python:3.9

# Continue as normal
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV FLASK_APP run.py
ENV DEBUG True

COPY requirements.txt .

# Install dependencies
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

COPY env.sample .env
COPY . .

RUN flask db init
RUN flask db migrate
RUN flask db upgrade

CMD ["gunicorn", "--config", "gunicorn-cfg.py", "run:app"]
