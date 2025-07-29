---
title: Configuration Examples
date: 2023-05-17T12:59:39.000Z
lastmod: 2025-02-24T00:00:00.000Z
draft: false
images: []
menu:
  docs:
    parent: reference
weight: 110
toc: true
tags:
  - open source
  - team
  - enterprise
description: Examples of basic and advanced configuration files, including templating and all available options.
---

To help you get started, here are examples of a basic configuration file, and a complete configuration file containing all fields.

## Basic `config.json`

```json
{
  "target": "pod/bear-pod",
  "feature": {
    "env": true,
    "fs": "read",
    "network": true
  }
}
```

## Basic `config.json` with templating

```json
{
  "target": "{{ get_env(name="TARGET", default="pod/fallback") }}",
  "feature": {
    "env": true,
    "fs": "read",
    "network": true
  }
}
```

## Complete `config.json`

Don't use this example as a starting point, it's just here to show you all the available options.

```json
{
  "accept_invalid_certificates": false,
  "skip_processes": "ide-debugger",
  "target": {
    "path": "pod/bear-pod",
    "namespace": "default"
  },
  "connect_tcp": null,
  "agent": {
    "log_level": "info",
    "json_log": false,
    "labels": { "user": "meow" },
    "annotations": { "cats.io/inject": "enabled" },
    "namespace": "default",
    "image": "ghcr.io/metalbear-co/mirrord:latest",
    "image_pull_policy": "IfNotPresent",
    "image_pull_secrets": [{ "secret-key": "secret" }],
    "ttl": 30,
    "ephemeral": false,
    "communication_timeout": 30,
    "startup_timeout": 360,
    "network_interface": "eth0",
    "flush_connections": true,
    "metrics": "0.0.0.0:9000"
  },
  "feature": {
    "env": {
      "include": "DATABASE_USER;PUBLIC_ENV",
      "exclude": "DATABASE_PASSWORD;SECRET_ENV",
      "override": {
        "DATABASE_CONNECTION": "db://localhost:7777/my-db",
        "LOCAL_BEAR": "panda"
      },
      "mapping": {
        ".+_TIMEOUT": "1000"
      }
    },
    "fs": {
      "mode": "write",
      "read_write": ".+\\.json",
      "read_only": [".+\\.yaml", ".+important-file\\.txt"],
      "local": [".+\\.js", ".+\\.mjs"]
    },
    "network": {
      "incoming": {
        "mode": "steal",
        "http_filter": {
          "header_filter": "host: api\\..+"
        },
        "port_mapping": [[7777, 8888]],
        "ignore_localhost": false,
        "ignore_ports": [9999, 10000]
      },
      "outgoing": {
        "tcp": true,
        "udp": true,
        "filter": {
          "local": ["tcp://1.1.1.0/24:1337", "1.1.5.0/24", "google.com", ":53"]
        },
        "ignore_localhost": false,
        "unix_streams": "bear.+"
      },
      "dns": {
        "enabled": true,
        "filter": {
          "local": ["1.1.1.0/24:1337", "1.1.5.0/24", "google.com"]
        }
      }
    },
    "copy_target": {
      "scale_down": false
    }
  },
  "operator": true,
  "kubeconfig": "~/.kube/config",
  "sip_binaries": "bash",
  "telemetry": true,
  "kube_context": "my-cluster"
}
```
