## Setup monitoring using docker
If you want to set up monitoring using docker, you can use the following commands:

In the `monitoring` folder

Make sure your prometheus config [file](./prometheus.yml) is updated with the following
  * the metrics port (`EO_PROMETHEUS_PORT`) of the EO data validator

You have the option to submit your data validator metrics to the EO monitoring platform. If you want to do that, you will need to update the VM-agent config [file](./vmagent.yml) with the following
  * the metrics port (`EO_PROMETHEUS_PORT`) of the EO data validator
  * the operator address (`EO_MAIN_ADDRESS`)
  * the eochain (`eochain`) either mainnet or testnet

If you don't want to submit your metrics to the EO monitoring platform, you can remove the `vmagent` service from the `docker-compose.yml` file

Once correct config is set up, run the following command to start the monitoring stack
```bash
docker compose up -d
```

Since EO data fetcher is running in a different docker network we will need to have prometheus in the same network. To do that, run the following command:
```bash
docker network connect eoracle-data-fetcher prometheus
```
This will make sure `prometheus` can scrape the metrics from `EO data fetcher` service.


#### Useful Dashboards
We also provide a set of useful Grafana dashboards which would be useful for monitoring the EO data fetcher service. You can find them [here](../dashboards).
Once you have Grafana setup, feel free to import the dashboards.
