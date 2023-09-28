FROM python:3.10-slim as base

ENV PYTHONFAULTHANDLER=1 \
  PYTHONUNBUFFERED=1 \
  PYTHONHASHSEED=random \
  PIP_NO_CACHE_DIR=off \
  PIP_DISABLE_PIP_VERSION_CHECK=on \
  PIP_DEFAULT_TIMEOUT=100 \
  POETRY_NO_INTERACTION=1 \
  POETRY_VIRTUALENVS_CREATE=false \
  POETRY_VERSION=1.4.2

RUN apt-get update && apt-get install -y build-essential unzip wget
RUN pip install "poetry==$POETRY_VERSION"

WORKDIR /app
COPY pyproject.toml /app/
RUN poetry export --without-hashes --no-interaction --no-ansi -f requirements.txt -o requirements.txt
RUN pip install -r requirements.txt

COPY ./run.sh ./
RUN chmod +x run.sh
CMD ["sh", "./run.sh"]
