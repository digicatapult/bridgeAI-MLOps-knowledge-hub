---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

## GitOps Spike Content


GitOps is the pattern of using Git as the source of truth to achieve a particular state for clusters, applications, environments, files, and pipelines, typically with one or more Kubernetes controllers monitoring the target for change. It would serve to automate much of the control plane for MLOps and should be especially useful to demonstrate to AI/ML SMEs for that reason, to reduce the cognitive load of managing backends, clusters, and integration.

Two options for GitOps stand out, respectively **Argo CD** and **Flux**:

**Argo CD**
- [Argo project](https://argoproj.github.io/){:target="_blank"} 
- [Argo case studies](https://www.cncf.io/case-studies/?_sft_lf-project=argo){:target="_blank"} 

**Flux**
- [Flux project](https://fluxcd.io/){:target="_blank"} 
- [Flux case studies](https://www.cncf.io/case-studies/?_sft_lf-project=flux){:target="_blank"} 


Among the various case studies above, Intuit’s use and promotion of Argo CD is the clearest. They ended up buying Applatix, the developers behind Argo itself.


Both Argo and Flux are cloud native projects under the CNCF. We have used Flux v2 internally on various projects and that makes adoption somewhat easier, if reusing scripts to spin up clusters. However, it lacks a GUI out-of-the-box; integration with Weave Works' own UI isn’t an option anymore as that company shut down in February 2024. That doesn’t affect Flux itself, since the two organisations are distinct entities. But Argo CD does have its own working GUI bundled with it.

<br>

### Requirements
1. Should have a GUI and CLI
2. Should be well-maintained, either by corporates or the community
3. Should have up-to-date documentation
4. Should be able to sync with kubectl

**Note: GUIs are an easier sell in an SME solution.**


Since Weave Works closed, there have been various articles published about the implications for Flux’s own development. Selecting Flux for Bridge AI under those circumstances will likely force us to revisit the subject and explain why we selected a project that just lost a major component (through no fault of Flux’s own team), where there's no alternative UI integration available. We might be making future showcases simpler for ourselves, running with Argo’s own functional UI.

### Resources

1. [Argo](https://argoproj.github.io/){:target="_blank"}

2. [Flux](https://fluxcd.io/){:target="_blank"} 

3. [CNCF Case Studies](https://www.cncf.io/case-studies/){:target="_blank"} 