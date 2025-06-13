FROM python:3.11-alpine

RUN apk update && apk upgrade && apk add --no-cache gcc musl-dev

RUN addgroup -g 1000 appuser && adduser -D -s /bin/sh -u 1000 -G appuser appuser

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir --upgrade pip setuptools>=78.1.1

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN chown -R appuser:appuser /app

USER appuser

EXPOSE 8000

HEALTHCHECK --interval=30s --timeout=10s --retries=3 \
    CMD python -c "import requests; requests.get('http://localhost:8000/time')" || exit 1

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]