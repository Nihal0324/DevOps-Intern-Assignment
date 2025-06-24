FROM python:3.11-slim

# Install uv
RUN pip install uv

# Set working directory
WORKDIR /app

# Copy the source code
COPY . .

# Create virtual environment
RUN uv venv .venv

# Set environment variables to use the virtual env
ENV VIRTUAL_ENV=/app/.venv
ENV PATH="/app/.venv/bin:$PATH"

# Install dependencies using pyproject.toml
RUN uv pip install --upgrade pip && \
    uv pip install .

# Expose FastAPI port
EXPOSE 8002

# Run the FastAPI app using uv
CMD ["uv", "run", "app.py"]

