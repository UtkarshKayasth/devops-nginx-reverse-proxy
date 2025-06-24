FROM python:3.11-slim-bullseye

WORKDIR /app
COPY . .

# ✅ Add curl installation here
RUN apt-get update && apt-get install -y curl && apt-get clean

# Flask install
RUN pip install flask

EXPOSE 8002
CMD ["python", "app.py"]
