# workshop-cicd-2025

docker build -t first-app:v1 .
docker tag first-app:v1 localhost:5000/first-app:v1
docker push localhost:5000/first-app:v1
curl http://localhost:5000/v2/_catalog
curl http://localhost:5000/v2/first-app/tags/list