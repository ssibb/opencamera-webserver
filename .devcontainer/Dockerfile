# Inizia dall'immagine base con Java 17
FROM mcr.microsoft.com/devcontainers/java:1-17-bullseye

# Installa i pacchetti necessari e pulisci
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends wget unzip \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Imposta le variabili d'ambiente per Android
ENV ANDROID_HOME=/usr/local/android-sdk
ENV PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools

# Scarica e installa l'SDK di Android
RUN wget -q https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip -O /tmp/cmdline-tools.zip \
    && mkdir -p $ANDROID_HOME/cmdline-tools \
    && unzip -q /tmp/cmdline-tools.zip -d $ANDROID_HOME/cmdline-tools \
    && mv $ANDROID_HOME/cmdline-tools/cmdline-tools $ANDROID_HOME/cmdline-tools/latest \
    && rm /tmp/cmdline-tools.zip

# Accetta le licenze e installa i componenti necessari
RUN yes | sdkmanager --licenses > /dev/null \
    && sdkmanager "platforms;android-34" "build-tools;34.0.0" "platform-tools"
    
