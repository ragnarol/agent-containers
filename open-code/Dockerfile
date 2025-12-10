# Build stage
FROM agent-base AS builder

# Install build dependencies and Open Code
RUN npm install -g opencode-ai && \
  echo "Installed Open Code version: $(/home/codeuser/.npm-global/bin/opencode --version)"

# Runtime stage
FROM agent-base

# Copy the installed Open Code from builder
COPY --from=builder /home/codeuser/.npm-global /home/codeuser/.npm-global

# Display version information
RUN echo "" && \
  echo "\e[34m=================================================================\e[0m" && \
  echo "\e[34m                   OPEN CODE VERSION                           \e[0m" && \
  echo "\e[34m=================================================================\e[0m" && \
  echo "\e[34m" && /home/codeuser/.npm-global/bin/opencode --version && \
  echo "\e[0m" && \
  echo ""

CMD ["/home/codeuser/.npm-global/bin/opencode"]
