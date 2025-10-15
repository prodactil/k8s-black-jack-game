FROM python:3.11-slim

RUN apt-get update && apt-get install -y \
        wget \
        ca-certificates \
        bsdutils \
        && rm -rf /var/lib/apt/lists/*

# Instalăm ttyd
RUN ARCH=$(dpkg --print-architecture) && \
    if [ "$ARCH" = "arm64" ]; then \
        wget -O /usr/local/bin/ttyd https://github.com/tsl0922/ttyd/releases/latest/download/ttyd.aarch64; \
    else \
        wget -O /usr/local/bin/ttyd https://github.com/tsl0922/ttyd/releases/latest/download/ttyd.x86_64; \
    fi && chmod +x /usr/local/bin/ttyd

WORKDIR /terminal-game

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY blackjack.py .
COPY art.py .

EXPOSE 7681

# CMD final: pseudo-terminal complet, input funcțional în browser
CMD ["ttyd", "--port", "7681", "script", "-q", "-c", "python3 -u blackjack.py", "/dev/null"]