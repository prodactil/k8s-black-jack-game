FROM python:3.11-slim

# 1. Instalăm uneltele necesare
# Inclusiv coreutils (pentru stty), wget, ca-certificates și bsdutils.
RUN apt-get update && apt-get install -y \
        coreutils \
        wget \
        ca-certificates \
        bsdutils \
        && rm -rf /var/lib/apt/lists/*

# 2. Instalarea ttyd (Detectare Arhitectură)
RUN ARCH=$(dpkg --print-architecture) && \
    if [ "$ARCH" = "arm64" ]; then \
        wget -O /usr/local/bin/ttyd https://github.com/tsl0922/ttyd/releases/latest/download/ttyd.aarch64; \
    else \
        wget -O /usr/local/bin/ttyd https://github.com/tsl0922/ttyd/releases/latest/download/ttyd.x86_64; \
    fi && chmod +x /usr/local/bin/ttyd

# Director de lucru
WORKDIR /terminal-game

# 3. Creăm scriptul de start (pentru a forța I/O corect)
RUN echo '#!/bin/bash\n\n# Resetează terminalul pentru I/O corect\nstty sane\n\n# Rulează jocul\npython3 -u blackjack.py' > /terminal-game/start.sh
RUN chmod +x /terminal-game/start.sh

# 4. Copiem și instalăm dependințele Python
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 5. Copiem jocul
COPY blackjack.py .
COPY art.py .

# Expunem portul ttyd
EXPOSE 7681

# 6. Pornim ttyd cu scriptul de start
CMD ["ttyd", "--port", "7681", "./start.sh"]