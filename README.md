# Start the Redis Cluster
ip=$(ipconfig getifaddr en0) docker-compose up -d

# Stop the Redis Cluster
docker-compose down