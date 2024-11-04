FROM python:3.10

WORKDIR /app

# Install mlflow and packages requied to interact with PostgreSQL and MinIO
RUN pip install mlflow psycopg2 boto3

USER 0

RUN mkdir -p mlartifacts && \
    chmod ugo+w,+t mlartifacts
