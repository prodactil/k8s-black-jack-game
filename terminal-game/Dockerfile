FROM python:3.11-slim

# Instalăm dependințele necesare pentru a descărca și rula ttyd
RUN apt-get update && apt-get install -y \
    wget \
    libjson-c5 \
    libwebsockets16 \
    && rm -rf /var/lib/apt/lists/*

# Descărcăm ultima versiune ttyd (pentru arhitectura ta - probabil amd64)
RUN wget -O /usr/local/bin/ttyd https://github.com/tsl0922/ttyd/releases/latest/download/ttyd.x86_64 \
    && chmod +x /usr/local/bin/ttyd

# Setăm directorul aplicației
WORKDIR /terminal-game

# Copiem fișierele jocului
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY blackjack.py .

# Portul pe care rulează ttyd
EXPOSE 7681

# Rulăm ttyd care pornește jocul tău Python
CMD ["ttyd", "--port", "7681", "python3", "blackjack.py"]