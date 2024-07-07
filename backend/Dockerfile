FROM python:3.11-slim
RUN apt-get update \
    && apt-get install -y curl
RUN curl -sSL https://install.python-poetry.org | python3 -
ENV PATH="/root/.local/bin:$PATH"

# Copy the pyproject.toml and poetry.lock files
COPY pyproject.toml poetry.lock /app/

# Install Python dependencies using Poetry
RUN poetry config virtualenvs.create false \
    && poetry install --no-dev --no-interaction --no-ansi

# Copy the rest of the application code to the container
COPY . /app

# Ensure the prestart script has execution permissions
RUN chmod +x /app/prestart.sh

# Expose the port the app runs on
EXPOSE 5173

# Run the prestart script and then the application
CMD ["bash", "-c", "./prestart.sh && poetry run uvicorn app.main:app --reload --host 0.0.0.0 --port 5173"]
