[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
[![unofficial Google Analytics for GitHub](https://gaforgithub.azurewebsites.net/api?repo=CKAD-exercises)](https://github.com/dgkanatsios/gaforgithub)


# CKA Exercises

A set of exercises that helped me prepare for the [Certified Kubernetes Administrator](https://www.cncf.io/certification/cka/) exam, offered by the Cloud Native Computing Foundation, organized by curriculum domain. They may as well serve as learning and practicing with Kubernetes.

## CKA Environment
- This is the [Official CNCF document](https://www.cncf.io/certification/tips), with some tips for you who will try to do the CKA exam.
- There's a table of the clusters you will be using during the exam.
- Each question on this exam must be completed on a designated cluster/configuration context.
- To minimize switching, the questions are grouped so that all questions on a given cluster appear consecutively.
- There are six clusters (CKA) that comprise the exam environment, made up of varying numbers of containers, as follows:


Cluster | Members | CNI | Description
--- | --- | --- | ---
k8s | 1 etcd, 1 master, 2 worker | flannel | k8s cluster |
hk8s | 1 etcd, 1 master, 2 worker | calico | k8s cluster |
bk8s | 1 etcd, 1 master, 1 worker | flannel | k8s cluster |
wk8s | 1 etcd, 1 master, 2 worker | flannel | k8s cluster |
ek8s | 1 etcd, 1 master, 2 worker | flannel | k8s cluster |
ik8s | 1 etcd, 1 master, 1 base node | loopback | Missing worker node

## Contents
- [Core Concepts 19%](CKA/a.core_concepts.md)
- [Installation, Configuration & Validation 12%](CKA/b.installation_configuration_and_validation.md)
- [Security 12%](CKA/c.security.md)
- [Networking 11%](CKA/d.networking.md)
- [Cluster Maintenance 11%](CKA/e.cluster_maintainance.md)
- [Troubleshooting 10%](CKA/f.troubleshooting.md)
- [Storage 7%](CKA/g.security.md)
- [Application Lifecycle Management 8%](CKA/h.application_lifecycle_management.md)
- [Scheduling 5%](CKA/i.scheduling.md)
- [Logging/Monitoring 5%](CKA/j.logging_monitoring.md)


# CKAD Exercises 

A set of exercises that helped me prepare for the [Certified Kubernetes Application Developer](https://www.cncf.io/certification/ckad/) exam, offered by the Cloud Native Computing Foundation, organized by curriculum domain. They may as well serve as learning and practicing with Kubernetes.

## CKAD Environment
- This is the [Official CNCF document](https://www.cncf.io/certification/tips), with some tips for you try to practise the CKAD exam.
- There's a table of the clusters you will be using during the exam.
- Each question on this exam must be completed on a designated cluster/configuration context.
- To minimize switching, the questions are grouped so that all questions on a given cluster appear consecutively.
- There are four clusters (CKAD) that comprise the exam environment, made up of varying numbers of containers, as follows:


Cluster | Members | CNI | Description
--- | --- | --- | ---
k8s | 1 etcd, 1 master, 2 worker | flannel | k8s cluster |
dk8s | 1 etcd, 1 master, 1 worker | flannel | k8s cluster |
nk8s | 1 etcd, 1 master, 2 worker | calico | k8s cluster |
sk8s | 1 etcd, 1 master, 1 worker | flannel | k8s cluster |

## Contents

- [Core Concepts - 13%](CKAD/a.core_concepts.md)
- [Multi-container pods - 10%](CKAD/b.multi_container_pods.md)
- [Pod design - 20%](CKAD/c.pod_design.md)
- [Configuration - 18%](CKAD/d.configuration.md)
- [Observability - 18%](CKAD/e.observability.md)
- [Services and networking - 13%](CKAD/f.services.md)
- [State persistence - 8%](CKAD/g.state.md)

### Can I PR? There is an error/an alternative way/an extra question/solution I can offer

Absolutely! Feel free to PR and edit/add questions and solutions, but please stick to the existing format.

### References
- [here](https://github.com/twajr/ckad-prep-notes) from twajr
- [here](https://www.reddit.com/r/kubernetes/comments/9uydc1/passed_the_ckad_special_thanks_to_the_linux/) from Blockchain0
- [here](https://medium.com/devopslinks/my-story-towards-cka-ckad-and-some-tips-daf495e711a9) from abdennour
- [here](https://medium.com/chotot-techblog/tips-tricks-to-pass-certified-kubernetes-application-developer-ckad-exam-67c9e1b32e6e) from Anh Dang

> Disclamer: Most of this content already been published online by others, I just spent sometime collecting and organizing some content that helped me passing CKA and CKAD exams. Please make a pull request if there something that should be added here.

