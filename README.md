# Project Athena

In Greek mythology, Athena was supposedly born, fully formed, from the head of Zeus. In many ways that's what we're trying to do here.

Specifically, **Project Athena** is a cross Filecoin project to make setting up of the various components that make up the IPFS/Filecoin network. These include:

## Near Term Goal

From a user experience perspective, IDEALLY we would have the following setup experience. 

Assuming a current Kubernetes cluster is available.
```
NUMBER_OF_LOTUS_NODES=10 helm install -f local_values.yaml lotus
```

Inside `local_values.yaml` would be all environment specific configurations. 

**NOTE:** The above is highly implementation specific (e.g. using helm and Kubernetes). We are not suggesting these are *necessarily* the right technology choices, but this clean experience, with single line declarative setup and well separated environment variables will dramatically improve setup and adoption.

Types of setup that we would need declarative setup for include:
- Lotus
- Gateways
- File servers (e.g. NFS?)
- ...
- ...

## Lotus as First Effort

The Lotus Miner is a good first effort for exploration. One thing that we have discovered is that there are a variety of "profiles" that need Lotus. These include:
- lotus newbies
- storage providers
- application developers
- API providers

It may be interesting to build a sample profile for each, and describe what the criteria are for setting up according to that profile. 

This requirements should include:

- cpu
- memory
- stoarge
- networking
- secrets

At the end, we could see what commonalities and where the variables are, and use that as a mechanism to understand what to parameterize.

## End goal
For each setup construct, we should plan on having a minimum of two profiles for each service:
- A highly instrumented, full log export reference architecture. This will likely not be particularly efficient, but will allow for simplified debugging of new deployments.
- A fairly efficient deployment.

In both cases, these are reference architectures, fully open sourced and forkable. Ideally, new participants in the Filecoin ecosystem could use these architectures as starting points and re-use components that make sense to them (e.g. containers).

Additionally, we should plan on integrating all components here into native build, CI/CD and test systems. So, every time a new release is tagged, new containers are built, the system goes through high level smoke tests and bugs are visible in test coverage (or filed with the appropriate teams).
