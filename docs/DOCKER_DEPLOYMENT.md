# Practical 10: Docker Containerization of the Iris ML Application

## 1. Objective

To containerize the Iris machine learning application using Docker, package a trained model, expose HTTP endpoints for predictions, and verify the application using health checks.

## 2. Tools and Technologies

- Docker Desktop
- Python 3.11
- scikit-learn
- pandas
- NumPy
- joblib
- Python http.server
- Git and GitHub

## 3. Implementation

The application uses a multi-stage Dockerfile.

### Builder stage

- Installs pinned Python dependencies.
- Reads the processed Iris dataset.
- Trains a Random Forest classifier.
- Saves the model and label encoder.

### Runtime stage

- Copies the installed Python packages.
- Copies the trained model.
- Copies src/serve.py.
- Exposes port 8000.
- Configures a Docker health check.

## 4. HTTP Endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| GET | /health | Checks application health |
| POST | /predict | Predicts Iris species |

## 5. Build and Run

Build:

docker build -t iris-classifier:v1 .

Run:

docker run -d --name iris-classifier-container -p 8000:8000 iris-classifier:v1

Check:

docker ps

## 6. Testing

Health endpoint:

curl http://localhost:8000/health

Expected:

{"status": "healthy"}

Prediction endpoint:

The application successfully returned an Iris prediction.

Invalid request:

The application returned HTTP 400 for missing required features.

## 7. Conclusion

The Iris ML application was successfully containerized using Docker. The model was trained during the Docker image build, the HTTP server returned predictions, and the health check successfully verified the running container.

## 8. Cleanup

docker stop iris-classifier-container

docker rm iris-classifier-container