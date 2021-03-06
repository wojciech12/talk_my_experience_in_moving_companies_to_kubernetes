Transformacja platformy e-commerce z instancji na AWS-ie do Kubernetes-a z Google Cloud Platform
================================================================================================

Interested in Kubernetes? Do you think how to get more independent from your cloud provider?

Kubernetes lets you to decouple your software from a cloud provider we are using. It becomes much easier to migrate your application from one provider to another. In my case, it was AWS to GCP. Still, having k8s, I can migrate back to the market leader (as in 2017) if needed.

Presentation
============

- you can also check the pdf export - index.pdf
- a reveals.js presentation, clone/download the repo, and open with your browser

Demo Part
=========

::

  # ingress:
  cat kube-ingress-stag.yaml
  kubectl get ing -l app=api-status
  kubectl get svc -l app=api-status
  kubectl get deployments -l app=api-status
  kubectl get pods -l app=api-status
  kubectl get po -l implementation=nginx
  kubectl get po -lapp=api-status -o jsonpath="{.items.metadata.name}"

  kubectl scale  --replicas=3 -f kube-nginx-stag.yaml
  kubectl get pods -l app=api-status
  kubectl get po -lapp=api-status -o jsonpath="{.items..metadata.name}" | tr ' ' '\n'
  kubectl scale  --replicas=1 -f kube-nginx-stag.yaml

  # bash
  kubectl exec -it api-status-nginx-56c47986cf-lhzqp /bin/bash
  # service is injected into pod dns:
  > apt-get update; apt-get install curl -qq
  > curl api-status
  > exit

  # kill the tainted pod and create new one:
  kubectl delete po api-status-nginx-56c47986cf-lhzqp


Generate PDF
============

::

  # you need to have docker installed
  make give_me_pdf


