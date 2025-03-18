# GitOps: Learn Flux

This repo documents different FluxCD experiments and setups.  

## Follow Along

This repo uses tags to document each configuration. 

Explore tags with `git tag -l`

## Part 2

Multi-cluster.

Create an app dir.

`mkdir apps`

Create the flux objects for your apps


1. Create a helm repository object.

```
  flux create source helm podinfo \
    --url=https://stefanprodan.github.io/podinfo \
    --interval=10m \
    --export >> ./apps/base/repository.yaml
```

1. Create a helm release object.

```
 flux create hr podinfo \
    --interval=10m \
    --source=HelmRepository/podinfo \
    --chart=podinfo \
    --export >> ./apps/base/release.yaml
```

Now you need to generate a kustomization.yaml. Well, you don't have to, but its [best practice](https://fluxcd.io/flux/components/kustomize/kustomizations/#generating-a-kustomizationyaml-file). 
Note I had to download a standalone version of kustomize to get access to this command. 

```
# create kustomization.yaml
kustomize create --autodetect --recursive
```
