FROM python:3.11-slim

RUN apt-get update && apt-get install -y ttyd && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY blackjack.py .

EXPOSE 7681

CMD ["ttyd", "--port", "7681", "python3", "blackjack.py"]