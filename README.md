# demshin_platform

Aleksandr Demshin Platform repository

## Table of contents

- [Homework - 1. Kubernetes Intro](#homework---1-kubernetes-intro)
- [Homework - 2. Kubernetes Controllers](#homework---2-kubernetes-controllers)
- [Homewprk - 3. Kubernetes Security](#homework---3-kubernetes-security)
- [Homework - 4. Kubernetes Networks](#homework---4-kubernetes-networks)

## Homework - 1. Kubernetes Intro

## Вопрос

**Q:** Почему все pod в namespace kube-system восстановились после удаления?

**A:** Первое, посмотрим на список pod'ов

```bash
kubectl get pods -n kube-system
NAME                               READY   STATUS    RESTARTS   AGE
coredns-66bff467f8-rw9xq           1/1     Running   0          162m
etcd-minikube                      1/1     Running   0          162m
kube-apiserver-minikube            1/1     Running   0          162m
kube-controller-manager-minikube   1/1     Running   0          162m
kube-proxy-jfb4q                   1/1     Running   0          162m
kube-scheduler-minikube            1/1     Running   0          162m
```

coredns восстановился, потому что контроллируется ReplicaSet:

```bash
❯ kubectl describe -n=kube-system pod coredns-66bff467f8-rw9xq | grep Controlled
Controlled By:  ReplicaSet/coredns-66bff467f8
```

kube-proxy восстановился, потому что контроллируется DaemonSet:

```bash
❯ kubectl describe -n=kube-system pod kube-proxy-jfb4q | grep Controlled
Controlled By:  DaemonSet/kube-proxy
```

etcd-minikube, kube-controller-manager-minikube, kube-scheduler-minikube контроллируются kubelet:

```bash
❯ kubectl describe -n=kube-system pod etcd-minikube | grep Controlled
Controlled By:  Node/minikube
```

## Практическая часть

1. Работа с приложением web:
   1. Создан Dockerfile c публикацией образа в Docker Hub.
   2. Создан манифест для использование образа, собранного ранее, в кластере.
   3. Добавлен init-контейнер в pod'е выше, так же использованы volume'ы.
   4. Изучен port forwarding с использованием `kubectl port-forward` и Kube Forwarder
2. Работа с приложением Hipster Shop.
   1. Изучен способ запуска подов ad-hoc.
   2. Изучена генерация манифестов с использованием ad-hoc режима.
   3. Задание со 🌟. Выяснена и устранена причина ошибок при старте Hipster Shop frontend.

## Homework - 2. Kubernetes Controllers

1. Установлен Kind и запущен кластер. См. `kubernetes-controllers/kind-config.yaml`.
2. Изучен ReplicaSet.
3. Изучен Deployment, включая задание со 🌟.
4. Изучены Probes.
5. Изучен DaemonSet на примере Node Exporter, включая задания со 🌟 и 🌟🌟.

## Homework - 3. Kubernetes Security

Работа с ServiceAccounts, Roles, ClusterRoles, ClusterRoleBindings, RoleBindings, Namespaces.

## Homework - 4. Kubernetes Networks

