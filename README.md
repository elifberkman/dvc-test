# Data Versioning Control

Test için oluşturuldu.

Docker compose ile minIO ayağa kaldır.

```bash
# Start the services in detached mode
docker compose up -d

# Stop and remove containers, networks, and volumes
docker compose down
```

Önce git projesi başlat.

```bash
# Install DVC and the S3 extension
pip install dvc 
pip install dvc[s3] 

# Initialize DVC repository
dvc init

# Track the username.csv file with DVC
dvc add username.csv

# Add the necessary files to Git
git add .gitignore username.csv.dvc

# List existing DVC remotes
dvc remote list

# Add a new remote storage named 'miniolocal'
dvc remote add -d miniolocal s3://dvc-test/test

# Configure MinIO as the remote storage
dvc remote modify miniolocal endpointurl http://localhost:9000
dvc remote modify miniolocal access_key_id admin
dvc remote modify miniolocal secret_access_key 12345678
dvc remote modify miniolocal use_ssl false
dvc remote modify miniolocal ssl_verify false

# Verify DVC configuration
dvc config --list

# Check the status of the DVC-tracked files
dvc status

# Push tracked files to the remote storage with verbose output
dvc push -v
```

Test başarılı oldu.