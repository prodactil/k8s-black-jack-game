FROM python:3.11-slim

# Instalăm unelte de bază pentru descărcare
RUN apt-get update && apt-get install -y wget ca-certificates && rm -rf /var/lib/apt/lists/*

# Detectăm arhitectura și descărcăm binarul corect de ttyd
# (versiune stabilă și compatibilă cu amd64 și arm64)
RUN ARCH=$(dpkg --print-architecture) && \
    if [ "$ARCH" = "arm64" ]; then \
        wget -O /usr/local/bin/ttyd https://github.com/tsl0922/ttyd/releases/latest/download/ttyd.aarch64; \
    else \
        wget -O /usr/local/bin/ttyd https://github.com/tsl0922/ttyd/releases/latest/download/ttyd.x86_64; \
    fi && chmod +x /usr/local/bin/ttyd

# Setăm directorul de lucru
WORKDIR /terminal-game

# Copiem și instalăm dependințele Python
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copiem jocul
COPY blackjack.py .
COPY art.py .

# Expunem portul pe care rulează ttyd
EXPOSE 7681

# Pornim jocul prin ttyd
CMD ["ttyd", "--port", "7681", "python3", "blackjack.py"]