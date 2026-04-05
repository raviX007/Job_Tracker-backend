FROM python:3.12-slim

RUN groupadd --gid 1000 appuser && \
    useradd --uid 1000 --gid appuser --shell /bin/bash --create-home appuser

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY --chown=appuser:appuser . .

# Create logs directory with correct permissions
RUN mkdir -p /app/logs && chown -R appuser:appuser /app/logs

USER appuser

EXPOSE 8008

CMD ["uvicorn", "api.server:app", "--host", "0.0.0.0", "--port", "8008"]