FROM python:3.13.11-slim

# copy uv binary from official uv image
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/

# setting working directory inside container
WORKDIR /app

# add virtual environment path to env to use installed packages
ENV PATH="/app/.venv/bin:$PATH"


# Copy dependency files first (better layer caching)
COPY "pyproject.toml" "uv.lock" ".python-version" ./

# Install dependencies from lock file (ensures reproducible builds)
RUN uv sync --locked

# Copy application code
COPY pipeline.py pipeline.py

# Set entry point
ENTRYPOINT ["uv", "run", "python", "pipeline.py"]