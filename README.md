# OpenTelemetry Collector

This project builds a customized version of the OpenTelemetry Collector with support for exporting to Google Cloud.

## Build

```
$ GO111MODULE=on go install go.opentelemetry.io/collector/cmd/builder@v0.94.0
$ builder --config=otelcol-builder.yaml
```

## Deploy

The binary distribution `otelcol-pano-ec` will be pulled in by the `meta-pano` layer and built into the EC image. In the future, it would be great to build this custom OpenTelemetry Collector in Yocto, but without proper packaging of vendor dependencies, it makes writing the recipe to build this difficult. For now, the binary will be built with Github Actions and `meta-pano` will just pull down the binary at build time.

When a tag is pushed to this repo, it will trigger the release workflow. The output of the release workflow will produce the compiled binary. This binary should be added to the Releases section on this repo, which is what `meta-pano` will use to download the artifact.
