FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
COPY elt_script.py .

RUN apt-get update && apt-get install -y \
    gcc \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir -r requirements.txt

CMD ["python", "elt_script.py"]