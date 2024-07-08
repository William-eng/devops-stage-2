FROM python:3.11-slim
RUN apt-get update \
    && apt-get install -y curl
RUN curl -sSL https://install.python-poetry.org | python3 -
WORKDIR /app
ENV PATH="/root/.local/bin:$PATH"

# Copy the pyproject.toml and poetry.lock files
COPY . .

# Install Python dependencies using Poetry
RUN poetry install
RUN chmod +x /app/prestart.sh
RUN poetry run bash ./prestart.sh
# Expose the port the app runs on
EXPOSE 5173

# Run the prestart script and then the application
CMD ["bash", "-c", "poetry run uvicorn app.main:app --reload --host 0.0.0.0 --port 5173"]
