FROM python:3.13.11-slim
# copy uv binary from official uv image
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/

WORKDIR /app
# add virtual environment path to env to use installed packages
ENV PATH="/app/.venv/bin:$PATH"

# Copy dependency files first (better layer caching)
COPY "pyproject.toml" "uv.lock" ".python-version" ./

# Install dependencies from lock file (ensures reproducible builds)
RUN uv sync --locked

# Copy application code
COPY ingest_data.py .

# Set entry point
ENTRYPOINT ["python", "ingest_data.py"]