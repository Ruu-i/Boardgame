# create VMs

create 5 ec2 instances for:

(t2.medium and t2.large)

Master node

2 Slave nodes

Sonar Qube

nexus

Jenkins

monitor

#### Make sure to add a load balancer
```
scrape_configs:
  - job_name: 'blackbox'
    metrics_path: /probe
    params:
      module: [http_2xx]  # Look for a HTTP 200 response.
    static_configs:
      - targets:
        - http://prometheus.io    # Target to probe with http.
        - https://prometheus.io   # Target to probe with https.
        - http://example.com:8080 # Target to probe with http on port 8080.
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: 127.0.0.1:9115  # The blackbox exporter's real hostname:port.
  - job_name: 'blackbox_exporter'  # collect blackbox exporter's operational metrics.
    static_configs:
      - targets: ['127.0.0.1:9115']
```
#### add prometheus configuration


check PHASE folders

## Inbound rules ports



```bash
465
3000
6443
8080
30000
9115
8081
9000
9090
25
222
80
443
9100
```

## Nexus issues resolve

```The error you're encountering indicates that Maven 
failed to deploy the artifact to Nexus on the
 second attempt, and it received a HTTP 400 
status code, which means the request sent 
to Nexus was invalid. This often happens for one of the following reasons:

Artifact Version Conflict: Maven Central or Nexus
 repositories typically do not allow redeploying the same 
version of an artifact (in your case, 0.0.4) if it has already been deployed. 
You likely deployed this version
 (0.0.4) successfully on the first attempt, and 
Nexus won't allow uploading the same version again to the releases repository.

Solution:

Bump the version of your project in the pom.xml. For example, change the version from 0.0.4 to 0.0.5 or use a 
unique snapshot version if you're working on continuous development (e.g., 0.0.5-SNAPSHOT).
Repository Permissions: There could be a permissions issue preventing the deployment, especially 
if different credentials are used for the second deployment attempt.

Solution:

Double-check the user permissions in Nexus for 
the Maven releases repository. Ensure that the 
user Jenkins is using has the correct roles assigned to deploy artifacts.

```

## Check resources

[Configuring your Prometheus instances](https://prometheus.io/docs/guides/node-exporter/)

[Download grafana](https://grafana.com/grafana/download)

[black-box exporter](https://prometheus.io/download/#blackbox_exporter)

[youtube tutorial](https://www.youtube.com/watch?v=NnkUGzaqqOc&t=60s)



## License

[MIT](https://choosealicense.com/licenses/mit/)