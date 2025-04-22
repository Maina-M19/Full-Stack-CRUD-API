FROM python:3.10-slim
WORKDIR /app
COPY . .
RUN pip install poetry
RUN poetry config virtualenvs.create false && poetry install
CMD ["python", "main.py"]