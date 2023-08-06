# monitoring-docker-base

A simple Docker setup for monitoring using [Prometheus](https://prometheus.io/docs/introduction/overview/) and [Grafana](https://grafana.com/docs/)

## Resources
- [Prometheus Docker installation guide](https://prometheus.io/docs/prometheus/latest/installation/#using-docker)
- [Blackbox Exporter repo with docs](https://github.com/prometheus/blackbox_exporter/tree/master)
- [Blackbox Exporter example config](https://github.com/prometheus/blackbox_exporter/blob/master/example.yml)
- [Grafana Docker image setup](https://grafana.com/docs/grafana/latest/setup-grafana/installation/docker/)
- [Grafana Docker custom configuration](https://grafana.com/docs/grafana/latest/setup-grafana/configure-docker/)
- [Using Grafana](https://grafana.com/docs/grafana/latest/getting-started/build-first-dashboard/)
- [Adding datasources to Grafana](https://grafana.com/docs/grafana/latest/datasources/)

## Notes

- When you add your Prometheus datasource to Grafana and they're running as part of the same Docker network (as they will be with this `docker-compose` config), you'll refer to Prometheus by its container name in the URL (see [screenshot](screenshots/grafana-datasource-config.png)).
- Be sure to review the `volume` and `port` sections of the `docker-compose` config and choose values that will work for you. I've configured the volumes as bind mounts, so they map to locations on your machine outside Docker. For example, a volume of `./prometheus:/etc/prometheus` means that when the container, internally, needs the `/etc/prometheus` directory, it actually uses a directory called `prometheus` in your current directory. Same for ports - if you already have something running on port 3000, for example, in the port section you can say `9876:3000` in order for the container's (Grafana, in this case) port 3000 to map to your port 9876. 
- The Grafana panel creation tools are super, super overwhelming at first. Take it slow, explore around, and maybe search for some example working panels that you can study to see how it all works. If you get frustrated, you're not alone. I've included a screenshot of a simple panel configuration showing the HTTP status of a website - it uses the metrics from Blackbox exporter that go to Prometheus. [Screenshot here](screenshots/grafana-panel-config.png)
