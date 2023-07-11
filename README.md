# Start the Redis Cluster (Run in Background)
docker-compose up -d

# Connection Example with `go-redis` client
```bash
go get -u github.com/redis/go-redis/v9
```

```go
package main

import (
	"context"
	"fmt"

	"github.com/redis/go-redis/v9"
)

func main() {
	client := redis.NewClusterClient(&redis.ClusterOptions{
		Addrs: []string{":7001", ":7002", ":7003", ":7004", ":7005", ":7006"},
		Password: "123456",
	})

	info, err := client.Do(context.TODO(), "CLUSTER", "INFO").Result()
	if err != nil {
		panic(err)
	}

	fmt.Println(info)
}
```

If succeed, you should see the output in console:
```text
cluster_state:ok
cluster_slots_assigned:16384
cluster_slots_ok:16384
cluster_slots_pfail:0
cluster_slots_fail:0
cluster_known_nodes:6
cluster_size:3
cluster_current_epoch:6
cluster_my_epoch:1
cluster_stats_messages_ping_sent:381
cluster_stats_messages_pong_sent:385
cluster_stats_messages_sent:766
cluster_stats_messages_ping_received:380
cluster_stats_messages_pong_received:381
cluster_stats_messages_meet_received:5
cluster_stats_messages_received:766
total_cluster_links_buffer_limit_exceeded:0
```


# Stop the Redis Cluster
docker-compose down
