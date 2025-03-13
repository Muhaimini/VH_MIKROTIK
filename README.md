run console:
docker-compose run vh_mikrotik_server rails console
docker-compose run vh_mikrotik_server bundle install

bundle install:
docker-compose run vh_mikrotik_server bash -c "sidekiq -C config/sidekiq.yml" || "bundle install && rails command"

run sidekiq:
docker-compose run vh_mikrotik_server bundle exec sidekiq

access db:
docker exec -it mikrotik_integration-db-1 psql -U vh -p 5432 -d mikrotik_db

docker exec -it mikrotik_integration-vh_mikrotik_server-1 bin/rails db:create
docker exec -it mikrotik_integration-vh_mikrotik_server-1 bin/rails db:migrate

console:
docker exec -it mikrotik_integration-vh_mikrotik_server-1 bash

aws check files:
aws --endpoint-url=http://localhost:4566 s3 ls s3://vh-mikrotik-bucket/mikrotik/

aws format URL:
"#{base_url}/#{aws_bucket}/mikrotik/#{file_name}"
http://localhost:4566/vh-mikrotik-bucket/mikrotik/backup_20250312181732.backup

logger:
docker-compose logs --follow
