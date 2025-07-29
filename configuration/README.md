---
title: Configuration
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
description: Config
---

# Configuration

mirrord allows for a high degree of customization when it comes to which features you want to enable, and how they should function.

All of the configuration fields have a default value, so a minimal configuration would be no configuration at all.

The configuration supports templating using the [Tera](https://keats.github.io/tera/docs/) template engine. Currently we don't provide additional values to the context, if you have anything you want us to provide please let us know.

To use a configuration file in the CLI, use the `-f <CONFIG_PATH>` flag. Or if using VSCode Extension or JetBrains plugin, simply create a `.mirrord/mirrord.json` file or use the UI.

