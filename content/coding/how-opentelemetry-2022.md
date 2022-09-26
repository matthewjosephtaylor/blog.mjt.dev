# How to use OpenTelemetry for TypeScript / JavaScript (and other languages) in 2022

I need to track how data flows throughout various processing pipelines.

I need this as a developer just to understand how and where things go wrong, without getting lost in the weeds.

Operations needs this to be able to monitor for trends and be alerted about potential and actual problems in the system.

Management needs this to have a fuller and more consistent picture of how things work.

The industry buzzword for this sort of thing is '[Observability](https://en.wikipedia.org/wiki/Observability)'.

This is an old problem. Fortunately today we have good tools, patterns and techniques. We no longer need to rely entirely on old-fashioned syslogs (though those continue to have their place as well).

## OpenTelemetry to the Rescue
Today I think [OpenTelemetry](https://opentelemetry.io/) is the way to go to solve the observability problem from a technology/coding side.

OpenTelemetry is more of an open source standard. It has [governance](https://github.com/open-telemetry/community/blob/main/governance-charter.md), which is to say it is a mature project, and takes its future seriously. There are a multitude of libraries in various languages. There are good set of services built on top of it for visualizations, alerting, monitoring, etc...

Being an open standard, I feel it gives good value for time/attention as I can adopt and use it whereever I go.

I note also that it has wide community and industry support. It isn't just me who thinks this is a good standard to follow.


## Exporters and Collectors

It is assumed that one is living in a world with multiple servers/services. One needs a way to _expose_ aka 'export' those traces/logs (spans) one is collecting. 

A [Collector](https://opentelemetry.io/docs/collector/) can be used as a service to collect all the span-data. Think of it a bit like [syslogd](https://linux.die.net/man/8/syslogd) for the old-school.

The [Community Supported Collector](https://github.com/open-telemetry/opentelemetry-collector) is written in Go.

Using a [Containerized Collector](https://opentelemetry.io/docs/collector/getting-started/#docker) is the easy way to get going for development.

There are many protocols for communicating back to the 'collector' available to choose from. One doesn't have to choose just one, but if I had to pick one I'd go with simple `http` as that can be used for both browser and backend servers. Thankfully the community supported Collector can handle them all, so no need to choose one.

### Deployment
It is recommended to have a collector running in the same host as the application in production. This allows the collector to efficiently offload the instrumentation traffic from the application (no waiting on communications outside the host).

One can then have the host-based collector forward the span-traffic to another Collector or Backend.

Useful article for debugging Collector:
- https://www.honeycomb.io/blog/test-span-opentelemetry-collector/

## Patterns for Usage

The beauty of building upon an established and well-loved standard, is one can lean on the community to provide software resources. Not need to invent a wheel, when one can simply pick one up off the shelf.


There are a host of [autoinstrumentation packages available](https://opentelemetry.io/registry/?language=js&component=instrumentation) for a variety of languages.

### TypeScript (Javascript)

#### Autoinstrumentation

[Express autoinstrumentation ](https://github.com/open-telemetry/opentelemetry-js-contrib/tree/main/plugins/node/opentelemetry-instrumentation-express)

[Node autoinstrumentation](https://github.com/open-telemetry/opentelemetry-js-contrib)

A gotcha with autoinstrumentation is that the autoinstrumentation MUST BE setup prior to the library being loaded into the javascript VM.

This requires the use of dynamic importing as follows:

// index.ts
```ts
(async () => {
  try {
    // setup OpenTelemetry and autoinstrumentation
    const { setupOpenTelemetry } = await import("./tracing");
    await setupOpenTelemetry();

    // main application entrypoint
    const { main } = await import("./main");
    main();
  } catch (reason) {
    console.error(reason);
  }
})();

```

// tracing.ts
```ts
import { diag, DiagConsoleLogger, DiagLogLevel } from "@opentelemetry/api";
import { getNodeAutoInstrumentations } from "@opentelemetry/auto-instrumentations-node";
import { NodeSDK, tracing } from "@opentelemetry/sdk-node";

export const setupOpenTelemetry = () => {
  diag.setLogger(new DiagConsoleLogger(), DiagLogLevel.INFO);

  const sdk = new NodeSDK({
    traceExporter: new tracing.ConsoleSpanExporter(),
    instrumentations: [getNodeAutoInstrumentations()],
  });
  return sdk.start();
};

```

One will then see lovely messages on the console for a simple express application like:

```js
{
  traceId: '166449d7554e44332899b0d763f7583c',
  parentId: undefined,
  name: 'GET /',
  id: 'a73fd1915a84d27f',
  kind: 1,
  timestamp: 1664217203085110,
  duration: 964,
  attributes: {
    'http.url': 'http://localhost:8080/',
    'http.host': 'localhost:8080',
    'net.host.name': 'localhost',
    'http.method': 'GET',
    'http.target': '/',
    'http.user_agent': 'curl/7.64.1',
    'http.flavor': '1.1',
    'net.transport': 'ip_tcp',
    'net.host.ip': '::1',
    'net.host.port': 8080,
    'net.peer.ip': '::1',
    'net.peer.port': 61373,
    'http.status_code': 200,
    'http.status_text': 'OK',
    'http.route': ''
  },
  status: { code: 0 },
  events: [],
  links: []
}
```

#### Exporter / Agent Setup

Install the exporter of choice:

```
$ npm install @opentelemetry/exporter-trace-otlp-http
```

Then modify the `NodeSDK` config

```ts
    traceExporter: new OTLPTraceExporter({
      url: "http://localhost:4318/v1/traces",
    }),
```

There are a few ways to skin the cat on where and how one wants to export.
The recommended way is to use a collector as a an 'agent' inside the container.

Here is how to do that in a Dockerfile
```Dockerfile
RUN apt-get update
RUN apt-get -y install wget systemctl
RUN wget https://github.com/open-telemetry/opentelemetry-collector-releases/releases/download/v0.60.0/otelcol_0.60.0_linux_amd64.deb
RUN dpkg -i otelcol_0.60.0_linux_amd64.deb

COPY /config.yaml /etc/otelcol/
```

The config.yaml for the OTEL collector will look something like ([Jaeger](https://www.jaegertracing.io/) 'backend' as an example, could forward to another collector, etc...):

```yaml
receivers:
  otlp:
    protocols:
      grpc:
      http:

exporters:
  logging:
    loglevel: info

  jaeger:
    # Specifying an IP _outside_ of the container to ease networking
    endpoint: "<jaeger-ip>:14250"
    tls:
      insecure: true

processors:
  batch:

extensions:
  health_check:
  pprof:
  zpages:

service:
  extensions: [pprof, zpages, health_check]
  pipelines:
    traces:
      receivers: [otlp]
      processors: [batch]
      exporters: [logging, jaeger]

```

Somewhere in application startup one will need to start the service like so.

```
systemctl restart otelcol
```