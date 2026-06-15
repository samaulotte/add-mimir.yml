# add-mimir.yml

target: all,alertmanager,overrides-exporter

# Configure Mimir to use Minio as object storage backend.

common:
  storage:
    backend: s3
    s3:
      endpoint: minio:9000
      access_key_id: admin
      secret_access_key: totototo
      insecure: true
      bucket_name: mimir

# Blocks storage requires a prefix when using a common object storage bucket.

blocks_storage:
  storage_prefix: blocks
  tsdb:
    dir: /data/ingester

# Use memberlist, a gossip-based protocol, to enable the 3 Mimir replicas to communicate.

memberlist:
  join_members:
    - mimir-1
    - mimir-2
    - mimir-3

server:
  log_level: warn
