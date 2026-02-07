# Build stage
FROM agent-base AS builder

# We act as 'node' user (inherited from base)
# Because we set NPM_CONFIG_PREFIX in base, this installs to /home/node/.npm-global
RUN npm install -g opencode-ai && \
  echo "Installed Open Code version: $(opencode --version)"

# Runtime stage
FROM agent-base


# Copy the installed global modules from builder
# We must use --chown to ensure the node user owns the copied files
COPY --from=builder --chown=node:node /home/node/.npm-global /home/node/.npm-global

# Display version information
RUN echo "" && \
  echo "\e[34m=================================================================\e[0m" && \
  echo "\e[34m                   OPEN CODE VERSION                           \e[0m" && \
  echo "\e[34m=================================================================\e[0m" && \
  echo "\e[34m" && opencode --version && \
  echo "\e[0m" && \
  echo ""


USER root
RUN wget https://packages.microsoft.com/config/debian/13/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
RUN dpkg -i packages-microsoft-prod.deb
RUN rm packages-microsoft-prod.deb
RUN apt-get update && \
  apt-get install -y dotnet-sdk-10.0
USER node

RUN npx get-shit-done-cc --opencode --global # Install to ~/.config/opencode/

CMD ["opencode"]
