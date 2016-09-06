# graphite-stack
Docker container running carbon-cache, graphite-web, statsite and grafana


This docker image is based on the [synthesize](https://github.com/obfuscurity/synthesize).

Like [synthesize](https://github.com/obfuscurity/synthesize) this image provices a complete installation of Graphite.


## Provides

* Graphite 0.9.15 ([graphite-web](https://github.com/graphite-project/graphite-web), [carbon](https://github.com/graphite-project/carbon), [whisper](https://github.com/graphite-project/whisper))
* StatsD ([statsite](https://github.com/armon/statsite))
* Grafana (latest nightly build)

## Usage

To get started, just start a container.

```
docker run -d --name graphite -p3000:3000 -p2003:2003 -p443:443 -p8125:8125 raintank/graphite-stack
```

The stack will listen on the following ports:

- 2003 tcp (metrictank's carbon input)
- 8125 udp (statsd endpoint)
- 3000 tcp (grafana's http port)
- 443 tcp (graphite-web and the graphite query api.)

### carbon
Start sending metrics directly using the carbon protocol.
For details see the [graphite documentation](https://graphite.readthedocs.io/en/latest/feeding-carbon.html)

### statsd
Start sending metrics dirctly using the statsD protocol.
refer to the [statsite documentation](https://github.com/armon/statsite#protocol)

### Graphite
The original Graphite UI is available at https://localhost/.  If you are using Docker Toolbox on MacOS, then change localhost to the IP of the Virtualbox VM running docker. This IP can be retreived with `docker-machine ip`

There is a superuser (Django) account that grants access to the administrative features in the backend Django database. The default credentials are:

* username `admin`
* password `graphite_me_synthesize`

### Grafana
The grafana UI is available at http://localhost:3000/.  If you are using Docker Toolbox on MacOS, then change localhost to the IP of the Virtualbox VM running docker. This IP can be retreived with `docker-machine ip`

The default user credentials are:

* username: `admin`
* password: `admin`

Once logged into grafana you will need to add the datasource. Navigate to http://localhost:3000/datasources/new
Then enter the following information

* Name: graphite
* Default: true
* Type: Graphite
* Url: https://localhost/
* Access: proxy

Then click "Add"


