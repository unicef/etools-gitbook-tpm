---
description: Etools Third Party Monitoring Front-End module
---

# Frontend

This module was developed using the [Polymer](https://www.polymer-project.org/) library \(version 1.x\) and [Material Design](https://material.io/) concept. [Polytempl](https://www.npmjs.com/package/polytempl) plugin was used as helper in development process and [Gulp](https://gulpjs.com/) was used to [build]() application.

## Installation

Using git, clone to a local directory:

```bash
$ git clone https://github.com/unicef/etools-tpm.git
```

Assuming node and npm are already installed, make sure bower is also installed, if not run:

```bash
$ npm install -g bower
```

Install packages:

```bash
$ npm install
$ bower install
```

This application is part of [etools-infra](https://github.com/unicef/etools-infra) and runs under a customized setup of etools apps. After `etools-infra` is installed the TPM application can be accessed for devs at `http://localhost:8082/tpm/`

## How to run tests

To run tests you can use:

```bash
$ gulp test
```

