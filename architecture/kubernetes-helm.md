# Kubernetes и Helm

---

## Оглавление

- **[Часть I. Kubernetes](#часть-i-kubernetes)**
  - [Введение: что такое Kubernetes и зачем он нужен](#введение-что-такое-kubernetes-и-зачем-он-нужен)
  - [История возникновения](#история-возникновения)
  - [Архитектура Kubernetes](#архитектура-kubernetes)
    - [Control Plane (управляющий слой)](#control-plane-управляющий-слой)
      - [kube-apiserver](#kube-apiserver)
      - [etcd](#etcd)
      - [kube-scheduler](#kube-scheduler)
      - [kube-controller-manager](#kube-controller-manager)
      - [cloud-controller-manager](#cloud-controller-manager)
    - [Worker Nodes (рабочие узлы)](#worker-nodes-рабочие-узлы)
      - [kubelet](#kubelet)
      - [kube-proxy](#kube-proxy)
      - [Container Runtime](#container-runtime)
    - [Addons (дополнения)](#addons-дополнения)
  - [Основные объекты Kubernetes](#основные-объекты-kubernetes)
    - [Pod](#pod)
    - [Pod Lifecycle Hooks](#pod-lifecycle-hooks)
    - [ReplicaSet](#replicaset)
    - [Deployment](#deployment)
    - [StatefulSet](#statefulset)
    - [DaemonSet](#daemonset)
    - [Job и CronJob](#job-и-cronjob)
  - [Сетевые объекты и Service Discovery](#сетевые-объекты-и-service-discovery)
    - [Service](#service)
      - [ClusterIP](#clusterip)
      - [NodePort](#nodeport)
      - [LoadBalancer](#loadbalancer)
      - [ExternalName](#externalname)
      - [Headless Service](#headless-service)
    - [Ingress](#ingress)
    - [Gateway API](#gateway-api)
    - [NetworkPolicy](#networkpolicy)
  - [Конфигурация и секреты](#конфигурация-и-секреты)
    - [ConfigMap](#configmap)
    - [Secret](#secret)
  - [Хранение данных](#хранение-данных)
    - [Volume](#volume)
    - [PersistentVolume (PV) и PersistentVolumeClaim (PVC)](#persistentvolume-pv-и-persistentvolumeclaim-pvc)
    - [StorageClass](#storageclass)
    - [CSI (Container Storage Interface)](#csi-container-storage-interface)
  - [Управление доступом: RBAC](#управление-доступом-rbac)
    - [ServiceAccount](#serviceaccount)
    - [Role и ClusterRole](#role-и-clusterrole)
    - [RoleBinding и ClusterRoleBinding](#rolebinding-и-clusterrolebinding)
  - [Custom Resource Definitions (CRD) и Operator Pattern](#custom-resource-definitions-crd-и-operator-pattern)
  - [Планирование и масштабирование](#планирование-и-масштабирование)
    - [Планирование (Scheduling)](#планирование-scheduling)
    - [Affinity и Anti-affinity](#affinity-и-anti-affinity)
    - [Taints и Tolerations](#taints-и-tolerations)
    - [Topology Spread Constraints](#topology-spread-constraints)
    - [ResourceQuota и LimitRange](#resourcequota-и-limitrange)
    - [PriorityClass](#priorityclass)
    - [Horizontal Pod Autoscaler (HPA)](#horizontal-pod-autoscaler-hpa)
    - [Vertical Pod Autoscaler (VPA)](#vertical-pod-autoscaler-vpa)
    - [Cluster Autoscaler](#cluster-autoscaler)
    - [KEDA (Kubernetes Event-Driven Autoscaler)](#keda-kubernetes-event-driven-autoscaler)
    - [PodDisruptionBudget (PDB)](#poddisruptionbudget-pdb)
  - [Отладка: Ephemeral Containers](#отладка-ephemeral-containers)
  - [Service Mesh](#service-mesh)
    - [Что такое Service Mesh](#что-такое-service-mesh)
    - [Istio](#istio)
    - [Linkerd](#linkerd)
  - [Мониторинг и Observability](#мониторинг-и-observability)
    - [Metrics Server и метрики](#metrics-server-и-метрики)
    - [Prometheus и Grafana](#prometheus-и-grafana)
    - [Логирование (EFK / ELK Stack)](#логирование-efk--elk-stack)
    - [Distributed Tracing](#distributed-tracing)
  - [Безопасность Kubernetes](#безопасность-kubernetes)
    - [Pod Security Standards (PSS)](#pod-security-standards-pss)
    - [SecurityContext](#securitycontext)
    - [Network Policies](#network-policies)
    - [Image Policy Webhook](#image-policy-webhook)
    - [Secrets Management](#secrets-management)
    - [cert-manager](#cert-manager)
    - [Policy as Code: OPA/Gatekeeper и Kyverno](#policy-as-code-opagatekeeper-и-kyverno)
    - [Лучшие практики безопасности](#лучшие-практики-безопасности)
  - [kubectl: шпаргалка](#kubectl-шпаргалка)
  - [Лучшие практики Kubernetes](#лучшие-практики-kubernetes)

- **[Часть II. Helm](#часть-ii-helm)**
  - [Введение: что такое Helm и зачем он нужен](#введение-что-такое-helm-и-зачем-он-нужен-1)
  - [История и эволюция](#история-и-эволюция)
  - [Архитектура и основные понятия](#архитектура-и-основные-понятия)
    - [Chart (чарт)](#chart-чарт)
    - [Repository (репозиторий)](#repository-репозиторий)
    - [Release (релиз)](#release-релиз)
    - [Revision (ревизия)](#revision-ревизия)
  - [Структура Chart](#структура-chart)
    - [Обязательные файлы](#обязательные-файлы)
    - [Необязательные файлы и директории](#необязательные-файлы-и-директории)
    - [Chart.yaml подробно](#chartyaml-подробно)
  - [Шаблонизация: синтаксис Go Templates](#шаблонизация-синтаксис-go-templates)
    - [Основы синтаксиса](#основы-синтаксиса)
    - [Встроенные объекты (Built-in Objects)](#встроенные-объекты-built-in-objects)
    - [Values (values.yaml)](#values-valuesyaml)
    - [Функции и pipelines](#функции-и-pipelines)
    - [Условные операторы](#условные-операторы)
    - [Циклы и диапазоны](#циклы-и-диапазоны)
    - [Именованные шаблоны (Named Templates / Partials)](#именованные-шаблоны-named-templates--partials)
  - [Helm Hooks](#helm-hooks)
    - [Жизненный цикл и доступные хуки](#жизненный-цикл-и-доступные-хуки)
    - [Политики удаления хуков](#политики-удаления-хуков)
  - [Управление зависимостями](#управление-зависимостями)
    - [Chart.yaml dependencies](#chartyaml-dependencies)
    - [Chart.lock](#chartlock)
    - [Library Charts](#library-charts)
  - [Helm CLI: шпаргалка](#helm-cli-шпаргалка-1)
  - [Тестирование чартов](#тестирование-чартов)
    - [helm lint](#helm-lint)
    - [helm template](#helm-template)
    - [helm unittest (плагин)](#helm-unittest-плагин)
  - [Helm vs Kustomize](#helm-vs-kustomize)
  - [Лучшие практики Helm](#лучшие-практики-helm-1)
    - [Структура и названия](#структура-и-названия)
    - [Values](#values-1)
    - [Шаблонизация](#шаблонизация)
    - [Безопасность](#безопасность-2)

- **[Часть III. Практические сценарии и референс-архитектуры](#часть-iii-практические-сценарии-и-референс-архитектуры)**
  - [Типовой CI/CD с Docker и Kubernetes](#типовой-cicd-с-docker-и-kubernetes)
  - [Локальная разработка: Dev-контур](#локальная-разработка-dev-контур)
  - [Production-grade кластер: чек-лист](#production-grade-кластер-чек-лист)
  - [Миграция с Docker Compose на Kubernetes](#миграция-с-docker-compose-на-kubernetes)

- **[Заключение](#заключение)**

---

## Часть I. Kubernetes

### Введение: что такое Kubernetes и зачем он нужен

**Kubernetes (K8s)** — это платформа с открытым исходным кодом для автоматизации развертывания, масштабирования и управления контейнеризированными приложениями. Kubernetes — это **оркестратор контейнеров**.

Если Docker отвечает на вопрос «как упаковать и запустить одно приложение в контейнере», то Kubernetes отвечает на вопрос «как управлять сотнями и тысячами контейнеров на десятках и сотнях серверов».

#### Что даёт Kubernetes?

| Возможность | Без Kubernetes | С Kubernetes |
|------------|----------------|--------------|
| **Размещение контейнеров** | Решаем вручную, на каком сервере что запускать | Планировщик (scheduler) автоматически выбирает оптимальный узел |
| **Самовосстановление** | Перезапуск вручную, мониторинг вручную | Автоматический перезапуск упавших контейнеров, замена «зависших» узлов |
| **Масштабирование** | Ручное добавление серверов и контейнеров | Автоматическое горизонтальное масштабирование (HPA) по метрикам |
| **Обнаружение сервисов** | Ручная настройка DNS, балансировщиков | Встроенный DNS, Service discovery, автоматический load balancing |
| **Обновления без простоя** | Сложные скрипты, ручное переключение трафика | Rolling updates с контролируемым темпом, автоматический rollback |
| **Управление конфигурацией** | Конфиги разбросаны по серверам | ConfigMaps и Secrets — централизованно, версионировано |
| **Секреты** | В переменных окружения, файлах на сервере | Secrets с шифрованием, интеграция с Vault/облачными KMS |
| **Service Mesh** | Недоступно | Istio/Linkerd — advanced traffic management, mTLS, observability |
| **Multi-tenancy** | Отдельные серверы для разных команд | Namespaces, ResourceQuotas, RBAC — всё в одном кластере |

#### Ключевые концепции (на бегу)

- **Pods** — минимальная единица развертывания (один или несколько контейнеров с общим сетевым namespace)
- **Services** — стабильная точка доступа к группе Pod (IP + DNS, не меняется при пересоздании Pod)
- **Deployments** — декларативное описание желаемого состояния приложения
- **Controllers** — циклы управления, которые приводят реальное состояние к желаемому
- **Namespaces** — виртуальные кластеры внутри физического (изоляция команд/проектов)

---

### История возникновения

**Kubernetes** родился в Google из внутреннего опыта управления контейнерами в масштабе всей планеты:

1. **2000-е**: Google создаёт **Borg** — внутреннюю систему оркестрации контейнеров, управлявшую сотнями тысяч задач на десятках тысяч машин.
2. **~2013**: Google создаёт **Omega** — следующее поколение оркестратора с более гибким планировщиком.
3. **Июнь 2014**: Google open-sourc'ит Kubernetes, основанный на опыте Borg и Omega, но перепроектированный для general-purpose использования.
4. **Июль 2015**: Kubernetes 1.0, Google передаёт проект Cloud Native Computing Foundation (CNCF).
5. **2016—настоящее время**: Kubernetes становится стандартом де-факто для контейнерной оркестрации. Все основные облачные провайдеры предлагают managed Kubernetes (EKS, GKE, AKS).

**Почему Kubernetes победил конкурентов (Swarm, Mesos, Nomad)?**
- Модульная архитектура (можно заменить почти любой компонент)
- Декларативная модель (желаемое состояние, а не процедурные шаги)
- Мощная экосистема (CNCF, сотни проектов, операторы для всего)
- Поддержка Google + крупнейших компаний
- Активное сообщество

---

### Архитектура Kubernetes

Kubernetes-кластер состоит из двух типов узлов: **Control Plane** и **Worker Nodes**.

```
┌────────────────────────────────────────────────────────────────────────────┐
│                              КЛАСТЕР KUBERNETES                              │
│                                                                            │
│  ┌─────────────────────────────────────────┐   ┌─────────────────────────┐ │
│  │           CONTROL PLANE                  │   │     WORKER NODE 1       │ │
│  │                                         │   │                         │ │
│  │  ┌───────────────┐  ┌────────────────┐  │   │  ┌───────────────────┐  │ │
│  │  │  kube-        │  │  kube-         │  │   │  │   kubelet         │  │ │
│  │  │  apiserver    │  │  controller-   │  │   │  │                   │  │ │
│  │  │               │  │  manager       │  │   │  └───────────────────┘  │ │
│  │  └───────────────┘  └────────────────┘  │   │  ┌───────────────────┐  │ │
│  │                                         │   │  │   kube-proxy      │  │ │
│  │  ┌───────────────┐  ┌────────────────┐  │   │  │                   │  │ │
│  │  │  kube-        │  │  cloud-        │  │   │  └───────────────────┘  │ │
│  │  │  scheduler    │  │  controller-   │  │   │  ┌───────────────────┐  │ │
│  │  │               │  │  manager       │  │   │  │ Container Runtime │  │ │
│  │  └───────────────┘  └────────────────┘  │   │  │ (containerd,      │  │ │
│  │                                         │   │  │  CRI-O, etc.)     │  │ │
│  │  ┌───────────────┐                      │   │  └───────────────────┘  │ │
│  │  │    etcd       │                      │   │  ┌───────────────────┐  │ │
│  │  │  (хранилище)  │                      │   │  │      Pods         │  │ │
│  │  └───────────────┘                      │   │  └───────────────────┘  │ │
│  └─────────────────────────────────────────┘   └─────────────────────────┘ │
│                                                                            │
│                           ┌─────────────────────────┐                      │
│                           │     WORKER NODE 2       │                      │
│                           │        ...              │                      │
│                           └─────────────────────────┘                      │
└────────────────────────────────────────────────────────────────────────────┘
```

#### Control Plane (управляющий слой)

Control Plane принимает глобальные решения о кластере и реагирует на события.

##### kube-apiserver

**kube-apiserver** — единая точка входа в кластер. Это REST API-сервер, через который проходят **все** операции: и внешние (`kubectl`, CI/CD), и внутренние (взаимодействие компонентов).

**Ключевые свойства:**
- **Единственный компонент, работающий с etcd напрямую** — все остальные компоненты общаются через API-сервер
- Горизонтально масштабируется (несколько экземпляров)
- Поддерживает аутентификацию (certificates, tokens, OIDC) и авторизацию (RBAC, ABAC, Webhook)
- Admission Controllers — плагины, модифицирующие/валидирующие запросы до их сохранения в etcd

```
kubectl → kube-apiserver → аутентификация → авторизация → admission → etcd
```

##### etcd

**etcd** — распределённое, высоконадёжное key-value хранилище. **Единый источник истины** (source of truth) для всего кластера — в etcd хранится состояние всех объектов (Pods, Services, Deployments, ConfigMaps, и т.д.).

**Важные аспекты:**
- Использует **Raft** для консенсуса (требуется нечётное количество узлов, минимум 3)
- **Резервное копирование etcd = резервное копирование всего кластера**
- При потере etcd кластер можно восстановить, но это сложно

##### kube-scheduler

**kube-scheduler** — отвечает на вопрос «на каком узле запустить Pod?». Он не запускает Pod сам — он лишь назначает Pod на узел.

**Процесс планирования (два этапа):**

1. **Filtering (фильтрация)**: исключение неподходящих узлов
   - Недостаточно ресурсов (CPU, память)
   - Taints/Tolerations не совпадают
   - NodeSelector/Affinity не соответствует
   - Порты заняты (HostPort conflict)

2. **Scoring (ранжирование)**: выбор лучшего из оставшихся
   - NodeResourcesFit (балансировка загрузки)
   - ImageLocality (наличие образа на узле)
   - PodTopologySpread (равномерное распределение)
   - Inter-pod Affinity

##### kube-controller-manager

**controller-manager** — запускает набор контроллеров. Каждый контроллер — это **цикл управления**:

```
Наблюдать текущее состояние → Сравнить с желаемым → Предпринять действия
```

Основные контроллеры:

| Контроллер | Что делает |
|-----------|-----------|
| **Deployment Controller** | Управляет ReplicaSet, обеспечивает rolling update |
| **ReplicaSet Controller** | Поддерживает нужное количество Pod |
| **Node Controller** | Следит за состоянием узлов, удаляет Pod на недоступных узлах |
| **Service Controller** | Создаёт облачные LoadBalancer'ы |
| **EndpointSlice Controller** | Отслеживает Pod, связанные с Service |
| **Job Controller** | Управляет Job (запуск до завершения) |
| **PV Controller** | Связывает PersistentVolume и PersistentVolumeClaim |
| **Namespace Controller** | Управляет жизненным циклом Namespace |

##### cloud-controller-manager

Облачный контроллер — отдельный процесс, взаимодействующий с API облачного провайдера. Выделен, чтобы облачные интеграции не смешивались с core-логикой.

| Контроллер | Что делает |
|-----------|-----------|
| **Node Controller** | Проверяет, существует ли узел в облаке после его удаления из кластера |
| **Route Controller** | Настраивает маршруты в облачной VPC |
| **Service Controller** | Создаёт облачные LoadBalancer'ы для Service типа LoadBalancer |

#### Worker Nodes (рабочие узлы)

##### kubelet

**kubelet** — агент, работающий на каждом узле. Он:
- Получает PodSpecs от kube-apiserver
- Запускает контейнеры через Container Runtime Interface (CRI)
- Мониторит состояние Pod и контейнеров
- Сообщает статус узла и Pod в API-сервер
- Выполняет liveness/readiness/startup probes
- Управляет томами, монтирует их в Pod

##### kube-proxy

**kube-proxy** — сетевой прокси на каждом узле. Реализует концепцию Service: перенаправляет трафик на нужные Pod.

Режимы работы:
- **iptables** (по умолчанию): правила iptables для случайного выбора Pod
- **IPVS**: более производительный, поддерживает разные алгоритмы балансировки (rr, lc, sh, dh)
- **nftables** (с 1.29, beta): преемник iptables, более современный и производительный

##### Container Runtime

**Container Runtime** — ПО, которое непосредственно запускает контейнеры. Kubernetes поддерживает любой runtime, совместимый с CRI (Container Runtime Interface):

| Runtime | Статус |
|---------|--------|
| **containerd** | Стандарт де-факто |
| **CRI-O** | Легковесный, специально для Kubernetes |
| **Docker Engine** | Устарел (dockershim удалён в 1.24, используйте cri-dockerd) |

#### Addons (дополнения)

Addons — это Kubernetes-ресурсы, расширяющие функциональность кластера:

| Addon | Назначение |
|-------|-----------|
| **CoreDNS** | DNS-сервер для service discovery внутри кластера |
| **Metrics Server** | Сбор метрик ресурсов для HPA и `kubectl top` |
| **Dashboard** | Web UI для управления кластером |
| **Ingress Controller** | Реализация Ingress (Nginx, Traefik, HAProxy, etc.) |
| **Network Plugin (CNI)** | Сетевая фабрика (Calico, Flannel, Cilium, etc.) |
| **CSI Driver** | Подключение облачных хранилищ |

**Выбор CNI-плагина — критическое решение:**

| CNI | Особенности | NetworkPolicy | eBPF | Когда использовать |
|-----|------------|:---:|:---:|--------------------|
| **Flannel** | Простейший, только overlay | ❌ | ❌ | Минимальные требования (dev, learning) |
| **Calico** | Overlay + BGP, производительный | ✅ | ✅ (Calico eBPF) | Стандартный выбор для production |
| **Cilium** | eBPF-основанный, высокая производительность | ✅ | ✅ (нативный) | Современный production, observability, kube-proxy replacement |
| **Weave Net** | Mesh-сеть, не требует etcd | ✅ | ❌ | Простые сети с политиками |

> **eBPF** — революционная технология ядра Linux, позволяющая выполнять программы в ядре без перекомпиляции. В контексте Kubernetes Cilium использует eBPF для замены kube-proxy (ускорение сетевого стека), реализации NetworkPolicy, сбора метрик и создания Service Mesh без sidecar-прокси. Если вы начинаете новый проект в 2024+, отдавайте предпочтение Cilium.


---

### Основные объекты Kubernetes

#### Pod

**Pod** — минимальная развертываемая единица в Kubernetes. Это группа из **одного или нескольких контейнеров**, которые:

- **Разделяют network namespace** (один IP-адрес, могут общаться через localhost)
- **Разделяют IPC namespace** (могут использовать System V IPC, POSIX message queues)
- **Могут разделять тома** (volume sharing)
- **Всегда запускаются на одном узле** (co-located)

```
┌─────────────────────────────────────────────┐
│                  Pod                         │
│  ┌──────────────────┐  ┌──────────────────┐ │
│  │   Контейнер A    │  │   Контейнер B    │ │
│  │   (основной)     │  │   (sidecar)      │ │
│  │                  │  │                  │ │
│  │   localhost:8080 │◀│─ curl            │ │
│  │                  │  │   localhost:8080 │ │
│  └──────────────────┘  └──────────────────┘ │
│  ┌────────────────────────────────────────┐  │
│  │         Shared Volume                   │  │
│  └────────────────────────────────────────┘  │
│  IP: 10.244.1.5                              │
└─────────────────────────────────────────────┘
```

**Паттерны использования Pod:**

| Паттерн | Описание | Пример |
|---------|----------|--------|
| **Один контейнер** | Стандартный случай | Приложение в одном контейнере |
| **Sidecar** | Вспомогательный контейнер расширяет основной | Приложение + прокси для логирования/метрик (Envoy, Fluentd) |
| **Ambassador** | Прокси-контейнер для внешних соединений | Основной контейнер → Ambassador → Внешняя БД |
| **Adapter** | Приводит вывод к стандартному формату | Адаптер переформатирует логи/метрики основного контейнера |
| **Init Container** | Контейнер, выполняющийся до основных | Миграции БД, ожидание готовности зависимостей, установка прав |

> **Sidecar-контейнеры с Kubernetes 1.29+** получили нативную поддержку через `restartPolicy: Always` у init-контейнеров:
> ```yaml
> initContainers:
> - name: sidecar-proxy
>   image: envoyproxy/envoy:v1.30
>   restartPolicy: Always      # запускается до основных и перезапускается при падении
> ```

**Манифест Pod:**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  initContainers:                      # init-контейнеры (выполняются до основных)
  - name: init-db
    image: busybox:1.36
    command: ['sh', '-c', 'until nc -z postgres 5432; do sleep 2; done']
  
  containers:
  - name: app
    image: myapp:1.2.3
    ports:
    - containerPort: 8080
      protocol: TCP
    resources:                         # запросы и лимиты
      requests:
        cpu: 100m                      # 0.1 CPU
        memory: 128Mi
      limits:
        cpu: 500m                      # 0.5 CPU
        memory: 512Mi
    livenessProbe:                     # жив ли контейнер?
      httpGet:
        path: /healthz
        port: 8080
      initialDelaySeconds: 15
      periodSeconds: 10
    readinessProbe:                    # готов принимать трафик?
      httpGet:
        path: /ready
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 5
    startupProbe:                      # стартанул ли? (для тяжелых приложений)
      httpGet:
        path: /startup
        port: 8080
      failureThreshold: 30
      periodSeconds: 10
    env:
    - name: DB_HOST
      valueFrom:
        secretKeyRef:
          name: db-secret
          key: host
    volumeMounts:
    - name: app-data
      mountPath: /data

  - name: log-collector                # sidecar
    image: fluent/fluent-bit:3.1
    volumeMounts:
    - name: logs
      mountPath: /var/log

  volumes:
  - name: app-data
    persistentVolumeClaim:
      claimName: app-pvc
  - name: logs
    emptyDir: {}
```

##### Probes (пробы)

| Probe | Назначение | Что при неудаче |
|-------|-----------|----------------|
| **livenessProbe** | Жив ли контейнер? Не завис ли deadlock? | Перезапуск контейнера |
| **readinessProbe** | Готов ли принимать запросы? | Удаление из Service (не шлём трафик) |
| **startupProbe** | Завершена ли инициализация? | Блокирует liveness и readiness до успеха |

**Важно:** livenessProbe и readinessProbe не должны проверять внешние зависимости (БД, API). Если readiness зависит от БД, а БД упала — Service уберёт все Pod'ы и приложение станет полностью недоступно. Используйте readiness только для проверки внутреннего состояния приложения.

#### Pod Lifecycle Hooks

Помимо probes, Pod поддерживает два хука жизненного цикла:

**`postStart`** — выполняется сразу после создания контейнера (до старта probes). Используется для:
- Регистрации сервиса в service discovery
- Отправки нотификации о старте
- Инициализации, которую нельзя сделать в entrypoint

**`preStop`** — выполняется перед тем, как контейнер получит SIGTERM. Используется для:
- Graceful shutdown: закрытие соединений, завершение in-flight запросов
- Дерегистрация из service discovery
- Сохранение состояния перед остановкой

```yaml
containers:
- name: app
  image: myapp:1.2.3
  lifecycle:
    postStart:
      exec:
        command: ["/bin/sh", "-c", "curl -X POST http://consul:8500/v1/agent/service/register -d @/etc/consul/register.json"]
    preStop:
      exec:
        command: ["/bin/sh", "-c", "sleep 15 && curl -X POST http://consul:8500/v1/agent/service/deregister/myapp"]
```

**Порядок завершения Pod:**
1. Pod переходит в состояние `Terminating`
2. Выполняется `preStop` хук
3. Отправляется `SIGTERM` (или `STOPSIGNAL`)
4. Если контейнер не завершился за `terminationGracePeriodSeconds` (по умолчанию 30с) — `SIGKILL`

#### ReplicaSet

**ReplicaSet** — гарантирует, что указанное количество Pod работает в любой момент времени.

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-rs
spec:
  replicas: 3                          # желаемое количество Pod
  selector:                            # какие Pod'ы считать «своими»
    matchLabels:
      app: myapp
  template:                            # шаблон Pod (как Pod spec)
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: app
        image: myapp:1.2.3
```

**Обычно ReplicaSet не создают вручную** — его создаёт и управляет им Deployment.

#### Deployment

**Deployment** — декларативное описание приложения. Это самый распространённый способ управления Pod. Deployment управляет ReplicaSet, а ReplicaSet управляет Pod.

```
Deployment
    │
    └── ReplicaSet v1 (replicas: 0)
    │       ├── Pod v1 (terminating)
    │
    └── ReplicaSet v2 (replicas: 3)
            ├── Pod v2-a (running)
            ├── Pod v2-b (running)
            └── Pod v2-c (running)
```

**Стратегии обновления (updateStrategy):**

| Стратегия | Как работает | Плюсы | Минусы |
|-----------|-------------|-------|--------|
| **RollingUpdate** | Постепенно заменяет старые Pod новыми | Ноль простоя | Временно работают две версии |
| **Recreate** | Удаляет все старые Pod, создаёт новые | Просто, нет двух версий | Простой |

**Конфигурация RollingUpdate:**

```yaml
spec:
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1       # макс. недоступных Pod (можно 25%)
      maxSurge: 1             # макс. лишних Pod сверх replicas (можно 25%)
```

| Параметр | Значение | Поведение |
|----------|---------|----------|
| maxUnavailable: 0, maxSurge: 1 | Ни одного недоступного Pod | Требует ресурсов на лишний Pod |
| maxUnavailable: 1, maxSurge: 0 | Без дополнительных ресурсов | Временно на 1 Pod меньше |

**Манифест Deployment:**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  replicas: 3
  revisionHistoryLimit: 10             # сколько старых ReplicaSet хранить
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
        version: v2
    spec:
      containers:
      - name: app
        image: myapp:1.2.3
        ports:
        - containerPort: 8080
        resources:
          requests:
            cpu: 100m
            memory: 128Mi
          limits:
            cpu: 500m
            memory: 512Mi
```

**Rollback:**

```bash
kubectl rollout history deployment/myapp           # история
kubectl rollout undo deployment/myapp              # откат на предыдущую
kubectl rollout undo deployment/myapp --to-revision=2  # откат на конкретную
kubectl rollout status deployment/myapp            # статус обновления
kubectl rollout pause deployment/myapp             # приостановить (canary)
kubectl rollout resume deployment/myapp            # возобновить
```

#### StatefulSet

**StatefulSet** — контроллер для stateful-приложений (БД, Kafka, Redis Cluster, и т.п.).

**Отличия от Deployment:**

| Аспект | Deployment | StatefulSet |
|--------|-----------|-------------|
| Идентификаторы Pod | Случайные (`myapp-5d8f7b9c6-x7k2j`) | Предсказуемые, порядковые (`myapp-0`, `myapp-1`, `myapp-2`) |
| Порядок запуска/остановки | Параллельный | Последовательный (0 → 1 → 2, стоп: 2 → 1 → 0) |
| Сетевая идентичность | Service + случайный IP | Headless Service + стабильный DNS (`myapp-0.myapp.ns.svc.cluster.local`) |
| Хранение данных | Общий PVC (если используется) | Каждому Pod свой PVC (volumeClaimTemplates) |
| Обновление | RollingUpdate по одному | RollingUpdate по одному, в обратном порядке |

**Манифест StatefulSet:**

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: postgres
spec:
  serviceName: postgres-headless      # Headless Service
  replicas: 3
  podManagementPolicy: OrderedReady   # или Parallel
  selector:
    matchLabels:
      app: postgres
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
      - name: postgres
        image: postgres:16
        volumeMounts:
        - name: data
          mountPath: /var/lib/postgresql/data
  volumeClaimTemplates:               # каждому Pod — свой PVC
  - metadata:
      name: data
    spec:
      accessModes: ["ReadWriteOnce"]
      storageClassName: fast-ssd
      resources:
        requests:
          storage: 100Gi
```

#### DaemonSet

**DaemonSet** — гарантирует, что на **каждом** узле кластера запущен экземпляр Pod (или на каждом подходящем узле). Используется для инфраструктурных сервисов:

- Сбор логов (Fluentd, Filebeat)
- Мониторинг узлов (Node Exporter, Datadog Agent)
- Сетевые плагины (Calico, Weave)
- Кэширующие прокси

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: node-exporter
spec:
  selector:
    matchLabels:
      app: node-exporter
  template:
    metadata:
      labels:
        app: node-exporter
    spec:
      hostNetwork: true               # доступ к сети хоста
      hostPID: true                   # доступ к PID namespace хоста
      containers:
      - name: node-exporter
        image: prom/node-exporter:v1.8.0        # всегда фиксируйте версию, не используйте :latest
        volumeMounts:
        - name: proc
          mountPath: /host/proc
          readOnly: true
      volumes:
      - name: proc
        hostPath:
          path: /proc
```

#### Job и CronJob

**Job** — запускает Pod до успешного завершения. Используется для пакетных задач, миграций, ETL.

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: db-migration
spec:
  backoffLimit: 3                     # сколько раз перезапускать при ошибке
  completions: 1                      # сколько успешных завершений нужно
  parallelism: 1                      # сколько Pod одновременно
  ttlSecondsAfterFinished: 300        # автоудаление через 5 минут
  template:
    spec:
      restartPolicy: Never            # OnFailure или Never (не Always!)
      containers:
      - name: migrator
        image: myapp-migrator:latest
```

**CronJob** — Job, запускаемая по расписанию (Cron-формат):

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: daily-backup
spec:
  schedule: "0 2 * * *"               # каждый день в 2:00
  concurrencyPolicy: Forbid           # Allow / Forbid / Replace
  startingDeadlineSeconds: 300        # максимум опоздания
  successfulJobsHistoryLimit: 3       # хранить 3 успешных
  failedJobsHistoryLimit: 1           # хранить 1 неудачный
  jobTemplate:
    spec:
      template:
        spec:
          restartPolicy: Never
          containers:
          - name: backup
            image: backup-tool:latest
```

---

### Сетевые объекты и Service Discovery

#### Service

**Service** — абстракция, предоставляющая стабильный IP-адрес и DNS-имя для доступа к набору Pod. Pod создаются и умирают, их IP меняются, но Service всегда доступен по одному адресу.

```
                  ┌─────────────────────────────────┐
                  │     Service: myapp              │
                  │     ClusterIP: 10.96.100.50     │
                  │     DNS: myapp.default.svc...   │
                  │                                 │
Клиент ──────────▶│     selector: app=myapp         │
                  │                                 │
                  │  ┌──────────┐  ┌──────────┐     │
                  │  │ Pod A    │  │ Pod B    │     │
                  │  │10.244.1.5│  │10.244.2.3│     │
                  │  └──────────┘  └──────────┘     │
                  └─────────────────────────────────┘
```

##### ClusterIP

**ClusterIP** — тип по умолчанию. Сервис доступен **только внутри кластера**.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp
spec:
  type: ClusterIP
  selector:
    app: myapp
  ports:
  - name: http
    port: 8080              # порт Service
    targetPort: 8080        # порт контейнера
    protocol: TCP
  sessionAffinity: None     # или ClientIP (sticky sessions)
```

##### NodePort

**NodePort** — открывает порт на каждом узле кластера (30000-32767). Сервис доступен по `<NodeIP>:<NodePort>` извне.

```yaml
spec:
  type: NodePort
  ports:
  - port: 8080
    targetPort: 8080
    nodePort: 30080         # опционально (можно указать явно)
```

##### LoadBalancer

**LoadBalancer** — создаёт облачный балансировщик нагрузки, который направляет трафик на NodePort.

```yaml
spec:
  type: LoadBalancer
  loadBalancerIP: 1.2.3.4   # опционально (статический IP в облаке)
```

##### ExternalName

**ExternalName** — не балансирует, а просто создаёт CNAME-запись в DNS кластера. Используется для интеграции с внешними сервисами:

```yaml
spec:
  type: ExternalName
  externalName: database.rds.amazonaws.com
```

##### Headless Service

**Headless Service** (`clusterIP: None`) — не имеет ClusterIP, DNS возвращает IP всех Pod напрямую. Используется со StatefulSet:

```yaml
spec:
  clusterIP: None
  selector:
    app: postgres
```

#### Ingress

**Ingress** — объект, описывающий правила маршрутизации HTTP/HTTPS-трафика к Service'ам внутри кластера. Это **L7-балансировщик** (уровень приложений).

Для работы Ingress нужен **Ingress Controller** (Nginx, Traefik, HAProxy, AWS ALB Ingress Controller, etc.).

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myapp-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    cert-manager.io/cluster-issuer: letsencrypt-prod
spec:
  ingressClassName: nginx
  tls:
  - hosts:
    - api.myapp.com
    secretName: api-tls-secret
  rules:
  - host: api.myapp.com
    http:
      paths:
      - path: /users
        pathType: Prefix
        backend:
          service:
            name: user-service
            port:
              number: 8080
      - path: /orders
        pathType: Prefix
        backend:
          service:
            name: order-service
            port:
              number: 8080
```

**pathType:**
- `Prefix` — все пути, начинающиеся с `/users` (включая `/users/123`)
- `Exact` — точное совпадение
- `ImplementationSpecific` — зависит от контроллера

#### Gateway API

**Gateway API** — современная замена Ingress (CNCF, GA с 2023), более гибкая и основанная на ролевой модели. В отличие от Ingress, Gateway API разделяет ответственность между ролями:

```
┌───────────────────────────────────────────────────────────┐
│                      Gateway API                           │
│                                                           │
│  GatewayClass (инфраструктурный провайдер)                │
│       └── Gateway (кластерный оператор/SRE)               │
│               ├── HTTPRoute (разработчик приложения)      │
│               ├── TLSRoute                                 │
│               ├── TCPRoute                                 │
│               └── GRPCRoute                                │
└───────────────────────────────────────────────────────────┘
```

**Ролевая модель:**

| Ресурс | Кто управляет | Что описывает |
|--------|--------------|---------------|
| **GatewayClass** | Инфраструктурная команда | Какой контроллер реализует шлюз (istio, nginx, envoy) |
| **Gateway** | Кластерный оператор/SRE | Конкретный экземпляр шлюза (порты, TLS, IP) |
| **HTTPRoute / TCPRoute / GRPCRoute** | Разработчик приложения | Правила маршрутизации для своего сервиса |

**Пример Gateway + HTTPRoute:**

```yaml
---
# Gateway: создаёт точку входа (оператор кластера)
apiVersion: gateway.networking.k8s.io/v1
kind: Gateway
metadata:
  name: prod-gateway
  namespace: infra
spec:
  gatewayClassName: nginx
  listeners:
  - name: http
    port: 80
    protocol: HTTP
    allowedRoutes:
      namespaces:
        from: All                     # принимать маршруты из всех namespace
  - name: https
    port: 443
    protocol: HTTPS
    tls:
      mode: Terminate
      certificateRefs:
      - name: wildcard-tls
    allowedRoutes:
      namespaces:
        from: Selector
        selector:
          matchLabels:
            gateway-access: "true"

---
# HTTPRoute: правила маршрутизации (разработчик)
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: myapp-route
  namespace: myapp
spec:
  parentRefs:
  - name: prod-gateway
    namespace: infra
  hostnames:
  - api.myapp.com
  rules:
  - matches:
    - path:
        type: PathPrefix
        value: /users
    backendRefs:
    - name: user-service
      port: 8080
      weight: 90                   # 90% трафика
    - name: user-service-v2
      port: 8080
      weight: 10                   # 10% — canary
  - matches:
    - path:
        type: PathPrefix
        value: /orders
    backendRefs:
    - name: order-service
      port: 8080
  - matches:
    - headers:                     # маршрутизация по заголовкам
      - name: x-canary
        value: "true"
    backendRefs:
    - name: user-service-canary
      port: 8080
```

**Gateway API vs Ingress:**

| Критерий | Ingress | Gateway API |
|----------|---------|-------------|
| Ролевая модель | Нет (всё в одном объекте) | Есть (GatewayClass → Gateway → Route) |
| Протоколы | HTTP/HTTPS | HTTP, TCP, TLS, gRPC |
| Canary / A/B тестирование | Через аннотации (зависит от контроллера) | Нативно (weight, header matching) |
| Cross-namespace | Аннотации | Нативно (allowedRoutes, ReferenceGrant) |
| Статус проекта | Стабилен, но «заморожен» | Активно развивается, будущее K8s-роутинга |
| Поддержка контроллеров | Все Ingress-контроллеры | Istio, Nginx Gateway Fabric, Envoy Gateway, Cilium |

#### NetworkPolicy

**NetworkPolicy** — правила файрвола для Pod. По умолчанию Pod открыт для всего трафика. NetworkPolicy позволяет ограничить входящий (ingress) и исходящий (egress) трафик.

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: backend-policy
spec:
  podSelector:
    matchLabels:
      app: backend
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - podSelector:                      # разрешить Pod с label app=frontend
        matchLabels:
          app: frontend
    - namespaceSelector:                # разрешить всё из namespace monitoring
        matchLabels:
          name: monitoring
    - ipBlock:                          # разрешить конкретные IP
        cidr: 10.0.0.0/8
        except:
        - 10.0.0.0/16
    ports:
    - protocol: TCP
      port: 8080
  egress:
  - to:
    - podSelector:
        matchLabels:
          app: database
    ports:
    - protocol: TCP
      port: 5432
```

**Важно:** NetworkPolicy требует CNI-плагина с поддержкой политик (Calico, Cilium, Weave; Flannel — без политик).

---

### Конфигурация и секреты

#### ConfigMap

**ConfigMap** — объект для хранения несекретных конфигурационных данных. Отделяет конфигурацию от кода и образа.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:                                  # текстовые данные
  app.properties: |
    server.port=8080
    log.level=INFO
    db.timeout=30s
  nginx.conf: |
    server {
        listen 8080;
        location / { proxy_pass http://backend; }
    }
binaryData:                            # бинарные данные (base64)
  cert.pem: LS0tLS1CRUdJTi...
```

**Использование ConfigMap:**

```yaml
# 1. Как переменные окружения
env:
- name: LOG_LEVEL
  valueFrom:
    configMapKeyRef:
      name: app-config
      key: log.level

# 2. Все ключи как переменные
envFrom:
- configMapRef:
    name: app-config

# 3. Как файлы (монтирование)
volumes:
- name: config
  configMap:
    name: app-config
    items:
    - key: app.properties
      path: application.properties

# 4. Как аргументы командной строки
command: ["java", "-jar", "app.jar", "--server.port=$(SERVER_PORT)"]
env:
- name: SERVER_PORT
  valueFrom:
    configMapKeyRef:
      name: app-config
      key: server.port
```

#### Secret

**Secret** — аналог ConfigMap для чувствительных данных. По умолчанию хранится в etcd без шифрования (нужно включить Encryption at Rest).

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
stringData:                            # в открытом виде (закодируется в base64)
  username: admin
  password: super_secret_password
# или
data:                                  # уже в base64
  username: YWRtaW4=
  password: c3VwZXJfc2VjcmV0X3Bhc3N3b3Jk
```

**Типы Secret:**
| Тип | Назначение |
|-----|-----------|
| `Opaque` | Произвольные данные (по умолчанию) |
| `kubernetes.io/tls` | TLS-сертификат и ключ |
| `kubernetes.io/dockerconfigjson` | Учётные данные для Docker Registry |
| `kubernetes.io/basic-auth` | Basic-аутентификация |
| `kubernetes.io/ssh-auth` | SSH-ключи |
| `kubernetes.io/service-account-token` | Токен ServiceAccount |

---

### Хранение данных

#### Volume

**Volume** в Pod — каталог с данными, доступный контейнерам в Pod. В отличие от Docker-томов, том в Kubernetes живёт столько же, сколько Pod.

**Типы томов (избранные):**

| Тип | Описание |
|-----|----------|
| `emptyDir` | Временная директория на узле. Создаётся при запуске Pod, удаляется при удалении Pod. Используется для кэшей, IPC. |
| `hostPath` | Монтирование файла/директории с узла. Используется для DaemonSet (логи, метрики). **Не для production-приложений!** |
| `configMap` | Монтирование ConfigMap как файлов |
| `secret` | Монтирование Secret как файлов |
| `persistentVolumeClaim` | Подключение PersistentVolume (основной способ) |
| `nfs` | Сетевое NFS-хранилище |
| `csi` | Том через CSI-драйвер |
| `projected` | Объединяет несколько источников (ConfigMap, Secret, downward API, ServiceAccountToken) в одну директорию |

#### PersistentVolume (PV) и PersistentVolumeClaim (PVC)

**PV (PersistentVolume)** — это ресурс хранилища в кластере, предоставленный администратором (или созданный динамически через StorageClass). Это аналог «диска».

**PVC (PersistentVolumeClaim)** — запрос приложения на хранилище. Это аналог «запроса на диск»: «нужно 10 ГБ с ReadWriteOnce».

```
Администратор          Пользователь (разработчик)
┌──────────┐          ┌───────────┐
│   PV     │◀─────────│   PVC     │── Pod
│  10 ГБ   │   Bind   │ "10 ГБ"   │
│  SSD     │          │           │
└──────────┘          └───────────┘
```

**PV:**
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: app-pv
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce           # один узел, чтение/запись
  persistentVolumeReclaimPolicy: Retain  # Retain / Recycle / Delete
  storageClassName: fast-ssd
  hostPath:                   # только для примера!
    path: /mnt/data
```

**PVC:**
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: app-pvc
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: fast-ssd
  resources:
    requests:
      storage: 10Gi
```

**accessModes:**

| Режим | Аббревиатура | Описание |
|-------|-------------|----------|
| ReadWriteOnce | RWO | Чтение/запись одним узлом |
| ReadOnlyMany | ROX | Только чтение многими узлами |
| ReadWriteMany | RWX | Чтение/запись многими узлами |
| ReadWriteOncePod | RWOP | Чтение/запись одним Pod (K8s 1.22+) |

**Reclaim Policy:**
- `Retain` — PV не удаляется автоматически, требует ручной очистки
- `Delete` — PV удаляется вместе с PVC (для динамических томов)
- `Recycle` — устарел, очистка данных и переиспользование

#### StorageClass

**StorageClass** — позволяет динамически создавать PV при создании PVC. Без StorageClass администратор должен вручную создавать PV.

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-ssd
  annotations:
    storageclass.kubernetes.io/is-default-class: "true"
provisioner: ebs.csi.aws.com      # AWS EBS CSI Driver
parameters:
  type: gp3
  encrypted: "true"
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
reclaimPolicy: Delete
```

**volumeBindingMode:**
- `Immediate` — PV создаётся сразу при создании PVC
- `WaitForFirstConsumer` — PV создаётся, когда Pod, использующий PVC, готов к планированию (оптимально для зональных дисков)

#### CSI (Container Storage Interface)

CSI — стандартный интерфейс для подключения хранилищ к Kubernetes. Заменяет in-tree плагины (которые требовали изменения кода Kubernetes).

```
┌──────────────────────────────────────────────────────┐
│                    Kubernetes                         │
│  ┌──────────────┐  ┌───────────────┐                 │
│  │ CSI Sidecar  │  │  CSI Sidecar  │  ...            │
│  │ provisioner  │  │  attacher     │                 │
│  └──────┬───────┘  └───────┬───────┘                 │
│         │                  │                         │
│         └────────┬─────────┘                         │
│                  │ gRPC                              │
│         ┌────────┴─────────┐                         │
│         │   CSI Driver     │                         │
│         │   (Node Plugin)  │                         │
│         └──────────────────┘                         │
└──────────────────────────────────────────────────────┘
```

---

### Управление доступом: RBAC

RBAC (Role-Based Access Control) — механизм управления правами в Kubernetes.

#### ServiceAccount

**ServiceAccount** — учётная запись для Pod (не для людей). Pod использует ServiceAccount для доступа к API-серверу Kubernetes.

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: myapp-sa
  namespace: default
```

#### Role и ClusterRole

**Role** — набор правил (permissions) в рамках одного namespace.
**ClusterRole** — набор правил на уровне всего кластера (или во всех namespace).

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]                      # "" = core API group
  resources: ["pods", "pods/log"]
  verbs: ["get", "list", "watch"]
- apiGroups: ["apps"]
  resources: ["deployments"]
  verbs: ["get", "list"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: node-reader
rules:
- apiGroups: [""]
  resources: ["nodes", "nodes/metrics"]
  verbs: ["get", "list"]
```

#### RoleBinding и ClusterRoleBinding

**RoleBinding** — связывает Role с субъектами (ServiceAccount, User, Group) в рамках namespace.
**ClusterRoleBinding** — связывает ClusterRole на уровне кластера.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
- kind: ServiceAccount
  name: myapp-sa
  namespace: default
roleRef:
  kind: Role                  # или ClusterRole (можно биндить ClusterRole через RoleBinding)
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

---

### Custom Resource Definitions (CRD) и Operator Pattern

**CRD (Custom Resource Definition)** — механизм расширения Kubernetes API собственными типами ресурсов. С помощью CRD вы можете добавить в кластер новые `kind`'ы (например, `MySQLCluster`, `PrometheusRule`, `Certificate`) и работать с ними через `kubectl` как с нативными ресурсами.

**Operator** — паттерн, реализующий контроллер для CRD, который автоматизирует полный жизненный цикл приложения:

```
Пользователь → создаёт CR (Custom Resource) → Operator (контроллер) → создаёт/управляет нативными ресурсами (Pod, Service, PVC, ...)
```

Оператор инкапсулирует экспертные знания о том, как устанавливать, настраивать, обновлять, бэкапировать и восстанавливать конкретное приложение (базу данных, message broker, etc.).

**Пример CRD:**

```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: mysqlclusters.database.example.com
spec:
  group: database.example.com
  names:
    kind: MySQLCluster
    plural: mysqlclusters
    singular: mysqlcluster
    shortNames:
      - mysql
  scope: Namespaced
  versions:
  - name: v1
    served: true
    storage: true
    schema:
      openAPIV3Schema:
        type: object
        properties:
          spec:
            type: object
            properties:
              replicas:
                type: integer
                minimum: 1
                maximum: 10
              version:
                type: string
                enum: ["8.0", "8.1", "8.2"]
              storageSize:
                type: string
            required: ["replicas", "version"]
```

**Использование CR:**

```yaml
apiVersion: database.example.com/v1
kind: MySQLCluster
metadata:
  name: my-production-db
spec:
  replicas: 3
  version: "8.0"
  storageSize: 100Gi
```

**Фреймворки для создания операторов:**

| Инструмент | Описание | Для чего |
|-----------|----------|---------|
| **Operator SDK** | Фреймворк от Red Hat (на Go, Ansible, Helm) | Полнофункциональные операторы |
| **Kubebuilder** | Набор инструментов и библиотек для Go | Операторы на Go (стандарт CNCF) |
| **Kopf** | Python-фреймворк для Kubernetes операторов | Простые операторы на Python |
| **Metacontroller** | Обобщённый контроллер (правила на JS/Python) | Простые контроллеры без написания Go-кода |

**Operator vs Helm:**

| Критерий | Helm | Operator |
|----------|------|----------|
| Сложность | Низкая (YAML + шаблоны) | Высокая (Go/Python код) |
| Day-1 операции (установка) | ✅ Отлично | ✅ Хорошо |
| Day-2 операции (обновление, бэкап, восстановление) | Ограничен (только upgrade) | ✅ Полный контроль |
| Управление состоянием | Статическое (желаемое состояние — разово) | Динамическое (реагирует на изменения постоянно) |
| Типовой сценарий | Стандартные приложения (web, API) | Stateful-приложения (БД, очереди), сложная логика |

**Популярные операторы:**
- **Prometheus Operator** — управление Prometheus, Alertmanager, ServiceMonitor
- **cert-manager** — автоматическое управление TLS-сертификатами
- **Strimzi** — управление Kafka-кластерами
- **Zalando Postgres Operator** — управление PostgreSQL
- **RabbitMQ Cluster Operator** — управление RabbitMQ
- **Istio Operator** — управление Service Mesh

---

### Планирование и масштабирование

#### Планирование (Scheduling)

Планирование определяет, **на каком узле** запустится Pod.

**nodeSelector** — простейший способ, жёстко задаёт узел по label:

```yaml
spec:
  nodeSelector:
    disktype: ssd
    zone: eu-west-1a
```

#### Affinity и Anti-affinity

**Affinity** — более гибкий аналог nodeSelector с правилами «обязательно» и «желательно».

```yaml
spec:
  affinity:
    nodeAffinity:                        # правила по узлам
      requiredDuringSchedulingIgnoredDuringExecution:   # hard
        nodeSelectorTerms:
        - matchExpressions:
          - key: topology.kubernetes.io/zone
            operator: In
            values:
            - eu-west-1a
            - eu-west-1b
      preferredDuringSchedulingIgnoredDuringExecution:  # soft
      - weight: 100
        preference:
          matchExpressions:
          - key: instance-type
            operator: In
            values:
            - c5.xlarge

    podAffinity:                         # разместить Pod рядом с другими
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchLabels:
            app: redis-cache
        topologyKey: topology.kubernetes.io/hostname

    podAntiAffinity:                     # разместить Pod подальше друг от друга
      preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 100
        podAffinityTerm:
          labelSelector:
            matchLabels:
              app: myapp
          topologyKey: topology.kubernetes.io/zone
```

#### Taints и Tolerations

**Taint** (на узле) — «узел отталкивает Pod, если у Pod нет соответствующего toleration».
**Toleration** (на Pod) — «Pod может терпеть этот узел».

```bash
# Добавить taint на узел
kubectl taint nodes node1 dedicated=database:NoSchedule
```

```yaml
# Toleration на Pod
spec:
  tolerations:
  - key: "dedicated"
    operator: "Equal"
    value: "database"
    effect: "NoSchedule"
```

**effect:**
- `NoSchedule` — не планировать новые Pod без toleration
- `PreferNoSchedule` — постараться не планировать
- `NoExecute` — не планировать + эвакуировать существующие Pod без toleration

#### Topology Spread Constraints

Равномерно распределяет Pod по топологиям (зонам, узлам):

```yaml
spec:
  topologySpreadConstraints:
  - maxSkew: 1
    topologyKey: topology.kubernetes.io/zone
    whenUnsatisfiable: ScheduleAnyway   # или DoNotSchedule
    labelSelector:
      matchLabels:
        app: myapp
```

#### ResourceQuota и LimitRange

**ResourceQuota** — ограничивает суммарное потребление ресурсов в namespace:

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: team-quota
  namespace: team-a
spec:
  hard:
    requests.cpu: "20"
    requests.memory: "40Gi"
    limits.cpu: "40"
    limits.memory: "80Gi"
    persistentvolumeclaims: "10"
    pods: "50"
    services: "20"
    secrets: "50"
    configmaps: "50"
```

**LimitRange** — задаёт значения по умолчанию и границы для ресурсов Pod в namespace:

```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: default-limits
  namespace: team-a
spec:
  limits:
  - type: Container
    default:
      cpu: 500m
      memory: 512Mi
    defaultRequest:
      cpu: 100m
      memory: 128Mi
    max:
      cpu: "4"
      memory: "8Gi"
    min:
      cpu: 50m
      memory: 64Mi
```

#### PriorityClass

**PriorityClass** — определяет приоритет Pod при планировании. Pod с более высоким приоритетом может вытеснить (preempt) Pod с низким приоритетом, если ресурсов не хватает:

```yaml
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: high-priority
value: 1000000
globalDefault: false
description: "Для критичных production-сервисов"

---
# Использование
spec:
  priorityClassName: high-priority
```

#### Horizontal Pod Autoscaler (HPA)

**HPA** автоматически изменяет количество реплик (Deployment/StatefulSet) на основе метрик:

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: myapp-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: myapp
  minReplicas: 2
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70        # среднее потребление CPU = 70%
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
  - type: Pods                       # кастомные метрики (Prometheus)
    pods:
      metric:
        name: http_requests_per_second
      target:
        type: AverageValue
        averageValue: "1000"
  behavior:                          # настройка скорости масштабирования
    scaleDown:
      stabilizationWindowSeconds: 300
      policies:
      - type: Percent
        value: 50
        periodSeconds: 60
    scaleUp:
      stabilizationWindowSeconds: 0
      policies:
      - type: Percent
        value: 100
        periodSeconds: 15
      - type: Pods
        value: 4
        periodSeconds: 15
      selectPolicy: Max              # Max = самое агрессивное, Min = самое осторожное
```

#### Vertical Pod Autoscaler (VPA)

**VPA** автоматически изменяет requests/limits Pod'ов на основе исторического использования. Требует отдельной установки.

#### Cluster Autoscaler

**Cluster Autoscaler** добавляет/удаляет узлы кластера в зависимости от загрузки:

```
Не хватает ресурсов для Pod → Cluster Autoscaler добавляет узел
Узел недозагружен и Pod можно эвакуировать → Cluster Autoscaler удаляет узел
```

#### KEDA (Kubernetes Event-Driven Autoscaler)

**KEDA** — расширение HPA, позволяющее масштабироваться на основе количества событий из внешних источников (Kafka, RabbitMQ, Azure Service Bus, AWS SQS, Prometheus, cron и десятки других). KEDA может масштабировать Deployment до **нуля** реплик (чего не умеет нативный HPA), а при появлении событий — поднимать обратно.

```
События (Kafka message lag) → KEDA → HPA → Deployment (replicas: 0 ↔ N)
```

**ScaledObject — основной ресурс KEDA:**

```yaml
apiVersion: keda.sh/v1alpha1
kind: ScaledObject
metadata:
  name: kafka-consumer-scaler
spec:
  scaleTargetRef:
    name: my-consumer
  minReplicaCount: 0                    # может масштабироваться до 0!
  maxReplicaCount: 30
  pollingInterval: 15                   # как часто проверять метрики (сек)
  cooldownPeriod: 300                   # время ожидания перед scale-down (сек)
  triggers:
  - type: kafka
    metadata:
      bootstrapServers: kafka-broker:9092
      consumerGroup: my-group
      topic: orders
      lagThreshold: "100"               # 1 Pod на каждые 100 отстающих сообщений
  - type: cron                          # плановое масштабирование
    metadata:
      timezone: Europe/Moscow
      start: "30 8 * * 1-5"
      end: "30 20 * * 1-5"
      desiredReplicas: "5"              # в рабочее время минимум 5 реплик
```

**KEDA vs HPA:**

| Характеристика | HPA | KEDA |
|---------------|-----|------|
| Метрики | CPU, память, кастомные (Prometheus) | 60+ коннекторов к внешним системам |
| Масштабирование до нуля | ❌ | ✅ (позволяет экономить ресурсы в простое) |
| Архитектура | Встроен в K8s | Отдельный оператор (устанавливается в кластер) |
| Типовой сценарий | Веб-приложения, API | Event-driven: очереди, стриминг, батчи |

#### PodDisruptionBudget (PDB)

**PodDisruptionBudget** — ограничивает количество одновременно недоступных Pod при **добровольных** (voluntary) прерываниях: обслуживание узлов (drain, cordon), обновление кластера, деплой изменений в StatefulSet. PDB **не защищает** от **непроизвольных** (involuntary) прерываний: падение узла, аппаратный сбой.

```yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: myapp-pdb
spec:
  minAvailable: 2          # минимум 2 Pod всегда должны быть доступны
  # или
  # maxUnavailable: 1      # максимум 1 Pod может быть недоступен
  selector:
    matchLabels:
      app: myapp
```

**Важно:** `kubectl drain` будет ждать, пока PodDisruptionBudget не позволит эвакуировать Pod. Если PDB слишком строгий (например, `minAvailable: 3` при 3 репликах), drain зависнет навсегда — в этом случае используйте `--disable-eviction` для принудительного удаления Pod.

**Типичные сценарии настройки:**

| Сценарий | PDB | Почему |
|----------|-----|-------|
| Stateless web (3 реплики) | `maxUnavailable: 1` | Допустима потеря 1 Pod при обслуживании |
| Critical API (5 реплик) | `minAvailable: 4` | Максимум 1 Pod может быть недоступен |
| База данных (3 реплики, leader-follower) | `maxUnavailable: 1` | Минимум 2 узла должны работать для кворума |
| Single-replica (dev) | Не использовать | PDB с minAvailable: 1 при 1 реплике заблокирует drain |

---

### Отладка: Ephemeral Containers

**Ephemeral Containers** (Kubernetes 1.25+) — временные контейнеры для отладки существующих Pod, особенно distroless-образов, где нет shell:

```bash
# Запустить временный контейнер в существующем Pod
kubectl debug myapp-pod -it --image=busybox --target=app

# Отладка узла
kubectl debug node/my-node -it --image=busybox

# Создать копию Pod с заменённой командой (удобно для отладки)
kubectl debug myapp-pod -it --copy-to=myapp-debug --container=app -- sh
```

Ephemeral-контейнеры не перезапускаются, не имеют probes и не могут иметь `ports` или `resources`. Это чисто диагностический инструмент.

---

### Service Mesh

#### Что такое Service Mesh

**Service Mesh** — инфраструктурный слой для управления взаимодействием сервисов. Вместо того чтобы каждый сервис реализовывал retry, circuit breaking, mTLS, метрики — это берёт на себя sidecar proxy (обычно Envoy).

```
Без Service Mesh:
┌──────┐   HTTP    ┌──────┐   HTTP    ┌──────┐
│Svc A │──────────▶│Svc B │──────────▶│Svc C │
└──────┘           └──────┘           └──────┘
(сам реализует retry, TLS, metrics)

С Service Mesh:
┌──────┐   HTTP    ┌──────┐   mTLS    ┌──────┐   HTTP    ┌──────┐
│Svc A │──────────▶│Proxy │──────────▶│Proxy │──────────▶│Svc C │
└──────┘           │(Envoy)│          │(Envoy)│          └──────┘
                   └──┬───┘           └──┬───┘
                      │                  │
                      └──────┬───────────┘
                             │
                    ┌────────┴────────┐
                    │ Control Plane   │
                    │ (Istio, Consul) │
                    └─────────────────┘
```

**Возможности Service Mesh:**
- **mTLS** — автоматическое взаимное TLS между сервисами
- **Traffic Splitting** — направление процента трафика в разные версии (canary, blue-green)
- **Circuit Breaking** — автоматическое отключение нездоровых сервисов
- **Retries и Timeouts** — без изменений в коде
- **Observability** — метрики, трейсинг, логи для всего трафика
- **Fault Injection** — внедрение ошибок для тестирования

#### Istio

**Istio** — самый популярный Service Mesh. Архитектура:

```
┌──────────────────────────────────────────────────────┐
│                     Istio                             │
│                                                      │
│  ┌──────────────────┐    ┌────────────────────────┐  │
│  │   istiod          │    │   Ingress Gateway      │  │
│  │   (Control Plane) │    │   (входной трафик)     │  │
│  │                   │    └────────────────────────┘  │
│  │  - Pilot          │                               │
│  │  - Citadel (mTLS) │    ┌────────────────────────┐  │
│  │  - Galley         │    │   Egress Gateway        │  │
│  └──────────────────┘    │   (исходящий трафик)    │  │
│                          └────────────────────────┘  │
│                                                      │
│  Каждый Pod: sidecar Envoy Proxy                     │
└──────────────────────────────────────────────────────┘
```

**Основные CRD (Custom Resources) Istio:**

```yaml
# VirtualService: правила маршрутизации
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: reviews-route
spec:
  hosts:
  - reviews
  http:
  - match:
    - headers:
        end-user:
          exact: jason
    route:
    - destination:
        host: reviews
        subset: v2          # пользователь jason → v2
  - route:
    - destination:
        host: reviews
        subset: v3
      weight: 10            # 10% трафика → v3 (canary)
    - destination:
        host: reviews
        subset: v1
      weight: 90            # 90% → v1

---
# DestinationRule: правила для целевого сервиса (балансировка, TLS)
apiVersion: networking.istio.io/v1beta1
kind: DestinationRule
metadata:
  name: reviews
spec:
  host: reviews
  trafficPolicy:
    loadBalancer:
      simple: RANDOM
    connectionPool:
      tcp:
        maxConnections: 100
      http:
        http1MaxPendingRequests: 1
        maxRequestsPerConnection: 1
    outlierDetection:              # circuit breaker
      consecutiveErrors: 5
      interval: 30s
      baseEjectionTime: 30s
  subsets:
  - name: v1
    labels:
      version: v1
  - name: v2
    labels:
      version: v2
  - name: v3
    labels:
      version: v3
```

#### Linkerd

**Linkerd** — более легковесный Service Mesh на Rust. Меньше функциональности, но проще в установке и эксплуатации. Подходит для команд, которым нужны mTLS и базовые метрики без сложности Istio.

| Характеристика | Istio | Linkerd |
|---------------|-------|---------|
| Сложность | Высокая | Низкая |
| Производительность | Средняя (Envoy на C++) | Высокая (proxy на Rust) |
| Канареечные деплои | ✅ Богатые возможности | ✅ Базовые (TrafficSplit) |
| mTLS | ✅ | ✅ |
| Circuit Breaking | ✅ | ❌ (ограниченно) |
| Multi-cluster | ✅ | ✅ (с 2.10) |
| Экосистема | Огромная | Меньше |
| Типовой сценарий | Крупные enterprise-кластеры | Средние кластеры, простота |

---

### Мониторинг и Observability

#### Metrics Server и метрики

**Metrics Server** — кластерный агрегатор метрик ресурсов (CPU, память). Требуется для:
- `kubectl top` команд
- HPA на основе ресурсов

```bash
kubectl top nodes
kubectl top pods
```

#### Prometheus и Grafana

Это стандартная связка для мониторинга Kubernetes:

```
┌─────────────────────────────────────────────────────────────┐
│                    Мониторинг                                │
│                                                             │
│  ┌──────────┐   scrape    ┌─────────────┐   query   ┌──────┐│
│  │  Targets  │────────────▶│  Prometheus  │──────────▶│Grafana│
│  │  (Pods,   │             │  (хранение,  │           │(UI)  ││
│  │   Nodes)  │             │   алертинг)  │           │      ││
│  └──────────┘              └──────┬──────┘           └──────┘│
│                                  │                          │
│                          ┌───────┴────────┐                 │
│                          │ Alertmanager    │                 │
│                          │ (оповещения)    │                 │
│                          └────────────────┘                 │
└─────────────────────────────────────────────────────────────┘
```

**Prometheus Operator / kube-prometheus-stack** — стандартный способ установки через Helm:

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install monitoring prometheus-community/kube-prometheus-stack
```

**Ключевые метрики Kubernetes:**
- `node_cpu_seconds_total` — CPU узлов
- `node_memory_MemAvailable_bytes` — доступная память
- `container_cpu_usage_seconds_total` — CPU контейнеров
- `kube_pod_status_phase` — статус Pod
- `kube_deployment_spec_replicas` / `kube_deployment_status_replicas_available` — реплики деплоймента
- `apiserver_request_duration_seconds` — latency API-сервера
- `etcd_disk_backend_commit_duration_seconds_bucket` — перформанс etcd

#### Логирование (EFK / ELK Stack)

```
┌────────────────────────────────────────────────────┐
│                Логирование                          │
│                                                    │
│  ┌──────────┐    ┌──────────────┐    ┌──────────┐  │
│  │ Fluentd/  │───▶│Elasticsearch │───▶│  Kibana  │  │
│  │ Fluent Bit│    │ (хранение)   │    │  (UI)    │  │
│  │(сбор логов)│   └──────────────┘    └──────────┘  │
│  └──────────┘                                       │
└────────────────────────────────────────────────────┘
```

Альтернативный легковесный стек: **Grafana Loki** (хранение логов) + **Fluent Bit** (сбор) + **Grafana** (UI).

**Fluent Bit** (легковесный) на каждом узле как DaemonSet:
```yaml
# Сбор логов всех контейнеров на узле
volumes:
- name: varlog
  hostPath:
    path: /var/log
- name: varlibdockercontainers
  hostPath:
    path: /var/lib/docker/containers
```

#### Distributed Tracing

**Distributed Tracing** — трассировка запроса через все микросервисы:

```
Клиент → Service A → Service B → Service C
        │           │           │
        └───────────┴───────────┘
                    │
            ┌───────┴───────┐
            │  Jaeger /     │
            │  Tempo /      │
            │  Zipkin       │
            └───────────────┘
```

**OpenTelemetry** — стандарт для трейсинга, метрик и логов. Позволяет отправлять данные в разные бэкенды (Jaeger, Grafana Tempo, Datadog, etc.).

---

### Безопасность Kubernetes

#### Pod Security Standards (PSS)

PSS определяет три уровня безопасности Pod:

| Уровень | Описание | Примеры ограничений |
|--------|----------|--------------------|
| **Privileged** | Минимум ограничений | Всё разрешено |
| **Baseline** | Защита от известных эскалаций привилегий | Запрещены hostPath, hostNetwork, hostPID, привилегированные контейнеры |
| **Restricted** | Максимальная изоляция, best practices | Baseline + запрет на runAsNonRoot: false, capabilities |

**Pod Security Admission** (встроен в K8s с 1.25, заменяет PSP):

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: secure-ns
  labels:
    pod-security.kubernetes.io/enforce: restricted
    pod-security.kubernetes.io/enforce-version: latest
    pod-security.kubernetes.io/audit: baseline
    pod-security.kubernetes.io/warn: baseline
```

#### SecurityContext

**SecurityContext** — настройки безопасности на уровне Pod или контейнера:

```yaml
spec:
  securityContext:                     # на уровне Pod
    runAsNonRoot: true
    runAsUser: 1001
    runAsGroup: 1001
    fsGroup: 1001
    seccompProfile:
      type: RuntimeDefault
  
  containers:
  - name: app
    securityContext:                   # на уровне контейнера
      allowPrivilegeEscalation: false
      readOnlyRootFilesystem: true
      capabilities:
        drop:
        - ALL
        add:
        - NET_BIND_SERVICE
      privileged: false
```

#### Network Policies

См. раздел [NetworkPolicy](#networkpolicy). Ключевой принцип — **deny all, allow explicitly**:

```yaml
# Базовые политики для namespace
---
# 1. Запретить весь входящий трафик
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all-ingress
spec:
  podSelector: {}
  policyTypes:
  - Ingress
---
# 2. Разрешить только DNS (kube-system)
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-dns
spec:
  podSelector: {}
  policyTypes:
  - Egress
  egress:
  - to:
    - namespaceSelector:
        matchLabels:
          kubernetes.io/metadata.name: kube-system
    ports:
    - protocol: UDP
      port: 53
```

#### Image Policy Webhook

Позволяет валидировать образы перед запуском: проверка подписей, разрешённые registry, запрет `:latest`.

#### Secrets Management

Рекомендуется использовать внешние secret-manager'ы:

| Инструмент | Описание |
|-----------|----------|
| **External Secrets Operator** | Синхронизирует секреты из AWS Secrets Manager, GCP Secret Manager, Azure Key Vault, HashiCorp Vault в Kubernetes Secrets |
| **Sealed Secrets** | Позволяет хранить зашифрованные секреты в Git (публичный ключ в кластере, приватный в etcd) |
| **Vault Sidecar Injector** | Внедряет секреты из Vault напрямую в Pod (без создания Kubernetes Secret) |

#### cert-manager

**cert-manager** — оператор Kubernetes для автоматического управления TLS-сертификатами. Создаёт, обновляет и перевыпускает сертификаты от различных CA (Let's Encrypt, HashiCorp Vault, Venafi, самоподписанные).

**Основные CRD cert-manager:**

```yaml
---
# Issuer: выпускает сертификаты в одном namespace
apiVersion: cert-manager.io/v1
kind: Issuer
metadata:
  name: letsencrypt-staging
  namespace: myapp
spec:
  acme:
    server: https://acme-staging-v02.api.letsencrypt.org/directory
    email: admin@company.com
    privateKeySecretRef:
      name: letsencrypt-staging-key
    solvers:
    - http01:
        ingress:
          class: nginx

---
# ClusterIssuer: то же, но на уровне всего кластера
apiVersion: cert-manager.io/v1
kind: ClusterIssuer
metadata:
  name: letsencrypt-prod
spec:
  acme:
    server: https://acme-v02.api.letsencrypt.org/directory
    email: admin@company.com
    privateKeySecretRef:
      name: letsencrypt-prod-key
    solvers:
    - http01:
        ingress:
          class: nginx
    - dns01:                              # DNS-валидация (для wildcard-сертификатов)
        route53:
          region: eu-west-1
          hostedZoneID: Z1234567890

---
# Certificate: запрос на конкретный сертификат
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
  name: myapp-tls
  namespace: myapp
spec:
  secretName: myapp-tls-secret            # куда сохранить сертификат
  issuerRef:
    name: letsencrypt-prod
    kind: ClusterIssuer
  dnsNames:
  - api.myapp.com
  - '*.myapp.com'                        # wildcard (требует DNS01)
  duration: 2160h                        # 90 дней
  renewBefore: 360h                      # обновить за 15 дней до истечения
```

**Challenges (способы подтверждения владения доменом):**
- **HTTP01** — cert-manager размещает временный файл на Ingress, Let's Encrypt проверяет его доступность (проще, но требует открытого 80 порта)
- **DNS01** — cert-manager создаёт TXT-запись в DNS (поддерживает wildcard, не требует открытых портов)

#### Policy as Code: OPA/Gatekeeper и Kyverno

Policy as Code позволяет описывать и автоматически проверять правила безопасности, конфигурации и compliance в Kubernetes.

**Сравнение инструментов:**

| Характеристика | OPA Gatekeeper | Kyverno |
|---------------|----------------|---------|
| Язык правил | Rego (специализированный язык) | YAML (нативный для K8s) |
| Сложность изучения | Высокая (новый язык) | Низкая (тот же YAML) |
| Экосистема | Большая (CNCF graduated) | Меньше, но быстро растёт |
| Mutation (изменение ресурсов) | Через отдельный проект (gator) | Встроенная |
| Генерация ресурсов | Ограничена | Встроенная (generate rules) |
| Типовой сценарий | Enterprise с выделенной командой | Команды разработки, простота |

**Примеры правил Kyverno:**

```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: require-resources
spec:
  validationFailureAction: Enforce        # или Audit (только логирование)
  rules:
  - name: check-resources
    match:
      any:
      - resources:
          kinds:
          - Pod
    validate:
      message: "Все контейнеры должны иметь requests и limits"
      pattern:
        spec:
          containers:
          - resources:
              requests: "?*"              # ? = любой ключ, * = любое значение
              limits: "?*"

---
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: disallow-latest-tag
spec:
  validationFailureAction: Enforce
  rules:
  - name: disallow-latest
    match:
      any:
      - resources:
          kinds:
          - Pod
    validate:
      message: "Запрещено использовать образы с тегом :latest"
      pattern:
        spec:
          containers:
          - image: "!*:latest"            # отрицание паттерна
```

**Пример правил OPA Gatekeeper:**

```yaml
apiVersion: templates.gatekeeper.sh/v1
kind: ConstraintTemplate
metadata:
  name: k8srequiredlabels
spec:
  crd:
    spec:
      names:
        kind: K8sRequiredLabels
      validation:
        openAPIV3Schema:
          type: object
          properties:
            labels:
              type: array
              items:
                type: string
  targets:
  - target: admission.k8s.gatekeeper.sh
    rego: |
      package k8srequiredlabels
      violation[{"msg": msg, "details": {"missing_labels": missing}}] {
        provided := {label | input.review.object.metadata.labels[label]}
        required := {label | label := input.parameters.labels[_]}
        missing := required - provided
        count(missing) > 0
        msg := sprintf("Отсутствуют обязательные labels: %v", [missing])
      }
---
apiVersion: constraints.gatekeeper.sh/v1beta1
kind: K8sRequiredLabels
metadata:
  name: require-team-label
spec:
  match:
    kinds:
    - apiGroups: [""]
      kinds: ["Namespace"]
  parameters:
    labels: ["team", "environment"]
```

**Рекомендация:** Kyverno проще для начала (пишется на YAML, ближе к K8s-разработчику), OPA/Gatekeeper — для сложных enterprise-сценариев с выделенной командой безопасности.

#### Лучшие практики безопасности

1. **Pod Security Standards: Restricted** — используйте `restricted` для всех namespace по умолчанию.
2. **RBAC: минимальные права** — каждый ServiceAccount должен иметь только необходимые права.
3. **Network Policies** — начинайте с deny-all, добавляйте только нужные разрешения.
4. **Не храните секреты в Git** — используйте Sealed Secrets или External Secrets Operator.
5. **Encryption at Rest** — шифруйте Secrets в etcd.
6. **Private Registry** — используйте приватный registry, сканируйте образы на CVE.
7. **Аудит** — включите audit logging и анализируйте подозрительную активность.
8. **Обновляйте кластер** — следите за новыми версиями Kubernetes (патчи безопасности).
9. **Policy as Code** — внедрите Kyverno или OPA/Gatekeeper для автоматической проверки compliance.
10. **cert-manager** — автоматизируйте управление TLS-сертификатами, не используйте самоподписанные сертификаты в production.

---

### kubectl: шпаргалка

```bash
# === Контекст и конфигурация ===
kubectl config view                           # просмотр конфига
kubectl config get-contexts                   # список контекстов
kubectl config use-context CONTEXT            # переключить контекст
kubectl config set-context --current --namespace=NS  # сменить namespace по умолчанию

# === Просмотр ===
kubectl get pods                              # Pod в текущем namespace
kubectl get pods -A                           # Pod во всех namespace
kubectl get pods -o wide                      # с IP и узлами
kubectl get pods -o yaml                      # YAML манифест
kubectl get pods --show-labels                # с label'ами
kubectl get pods -l app=myapp                 # фильтрация по label
kubectl get pods --field-selector status.phase=Running  # по полю
kubectl describe pod NAME                     # подробное описание + события
kubectl get events --sort-by='.lastTimestamp'  # события

# === Операции с Pod ===
kubectl logs POD                              # логи
kubectl logs POD -c CONTAINER                 # логи конкретного контейнера
kubectl logs -f POD                           # следить за логами
kubectl logs --tail=100 POD                   # последние 100 строк
kubectl exec -it POD -- sh                    # интерактивный shell
kubectl exec POD -- ls /app                   # выполнить команду
kubectl port-forward POD 8080:8080            # пробросить порт
kubectl cp POD:/path/file ./local-file        # скопировать файл
kubectl delete pod NAME                       # удалить Pod
kubectl delete pod NAME --force --grace-period=0  # жёстко удалить
kubectl top pod                               # потребление ресурсов

# === Управление ресурсами ===
kubectl apply -f file.yaml                    # применить манифест
kubectl apply -k ./directory                  # применить kustomize
kubectl delete -f file.yaml                   # удалить ресурс
kubectl create deployment NAME --image=IMAGE  # императивное создание
kubectl scale deployment/NAME --replicas=5    # масштабировать
kubectl rollout restart deployment/NAME       # перезапустить Pod
kubectl rollout status deployment/NAME        # статус обновления
kubectl rollout undo deployment/NAME          # откатить
kubectl set image deployment/NAME C=IMAGE     # обновить образ
kubectl edit deployment/NAME                  # отредактировать «на лету»
kubectl patch deployment/NAME -p '{"spec":{"replicas":3}}'  # patch

# === Отладка ===
kubectl run debug --rm -it --image=busybox -- sh   # временный Pod для отладки
kubectl debug node/NODE -it --image=busybox         # отладка узла
kubectl debug myapp-pod -it --image=busybox --target=app  # эфемерный контейнер
kubectl auth can-i create pods --as=system:serviceaccount:ns:sa  # проверить права

# === Мониторинг ===
kubectl cluster-info                           # информация о кластере
kubectl top nodes                              # ресурсы узлов
kubectl top pods                               # ресурсы Pod
kubectl api-resources                          # список всех API-ресурсов
kubectl explain pod.spec.containers            # документация по полю

# === Полезные алиасы ===
alias k='kubectl'
alias kg='kubectl get'
alias kgp='kubectl get pods'
alias kgd='kubectl get deployments'
alias kd='kubectl describe'
alias kl='kubectl logs'
alias ke='kubectl exec -it'
```

---

### Лучшие практики Kubernetes

1. **Используйте Namespaces** для изоляции сред (dev/stage/prod) и команд.
2. **Всегда задавайте resource requests и limits** — без них планировщик не может эффективно распределять Pod.
3. **Probes обязательны** — liveness, readiness и startup probes для каждого контейнера.
4. **Readiness проверяет только внутреннее состояние** — не должна зависеть от внешних сервисов.
5. **Не используйте `:latest`** — фиксируйте версии образов.
6. **Graceful shutdown** — приложение должно корректно обрабатывать SIGTERM, использовать `terminationGracePeriodSeconds` и `preStop` хук.
7. **Affinity / Anti-affinity** — распределяйте Pod для отказоустойчивости.
8. **PodDisruptionBudget** — защитите приложения от массовой эвакуации при обслуживании узлов.
9. **ResourceQuotas и LimitRanges** — ограничивайте потребление ресурсов на уровне namespace.
10. **Ingress/Gateway API вместо NodePort** — для внешнего доступа используйте Ingress.
11. **Используйте PriorityClass** — чтобы критичные Pod не вытеснялись некритичными.
12. **Server-side apply** — используйте `kubectl apply --server-side` для избежания конфликтов при работе с большими манифестами.

---

## Часть II. Helm

### Введение: что такое Helm и зачем он нужен

**Helm** — пакетный менеджер для Kubernetes. Он делает для Kubernetes то же, что `apt` для Ubuntu, `brew` для macOS или `pip` для Python. Helm позволяет:

- **Упаковывать** Kubernetes-манифесты в переиспользуемые пакеты — **Chart'ы** (чарты)
- **Параметризовать** развёртывание через файлы `values.yaml`
- **Версионировать** развёртывание (релизы и ревизии)
- **Управлять зависимостями** между чартами
- **Распространять** чарты через репозитории (аналоги Docker Registry)
- **Автоматизировать** установку, обновление и удаление приложений

#### Проблемы, которые решает Helm

| Проблема | Без Helm | С Helm |
|----------|---------|--------|
| Установка приложения | Множество `kubectl apply -f ...` в правильном порядке | `helm install myapp ./chart` |
| Обновление конфигурации | Ручное редактирование YAML-файлов и переприменение | `helm upgrade myapp ./chart --set replicas=5` |
| Переиспользование | Копипаста YAML между проектами | Один Chart, разные values |
| Откат | Сложно: нужно хранить старые версии манифестов | `helm rollback myapp 2` |
| CI/CD интеграция | Скрипты с подстановкой переменных в YAML | `helm upgrade --install` идемпотентно |
| Версионирование | Git + ручная дисциплина | Встроено в Helm (revision) |

---

### История и эволюция

| Версия | Год | Ключевые изменения |
|--------|-----|--------------------|
| **Helm v2** | 2016 | Первая популярная версия. Клиент-серверная архитектура: `helm` (CLI) + `tiller` (внутри кластера). **Проблема:** tiller имел широкие права, был вектором атаки. |
| **Helm v3** | 2019 | **Отказ от tiller**. Helm напрямую использует kubeconfig и RBAC пользователя, запускающего команду. Улучшенная работа с чартами (Library Charts), трёхсторонний стратегический мерж патчей. |

**Текущая актуальная версия — Helm 3.** Helm v2 больше не поддерживается.

---

### Архитектура и основные понятия

#### Chart (чарт)

**Chart** — это набор файлов, описывающий связанный набор Kubernetes-ресурсов. Аналог пакета в apt или образа в Docker.

```bash
mychart/
├── Chart.yaml          # метаданные чарта (имя, версия, описание)
├── values.yaml         # значения по умолчанию для шаблонов
├── values.schema.json  # JSON Schema для валидации values (опционально)
├── charts/             # зависимости (подчарты)
├── templates/          # шаблоны Kubernetes-манифестов
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   ├── _helpers.tpl    # именованные шаблоны (не создают ресурсы)
│   └── NOTES.txt       # сообщение после установки (help)
├── templates/tests/    # тесты чарта
├── .helmignore         # файлы, исключаемые из пакета
├── README.md
└── LICENSE
```

#### Repository (репозиторий)

**Chart Repository** — HTTP-сервер, хранящий упакованные чарты (`.tgz`) и файл `index.yaml`.

```
https://charts.mycompany.com/
├── index.yaml          # список всех чартов и их версий
├── myapp-1.0.0.tgz
├── myapp-1.1.0.tgz
└── postgres-12.0.0.tgz
```

Популярные публичные репозитории:
- **Bitnami**: `https://charts.bitnami.com/bitnami`
- **Prometheus Community**: `https://prometheus-community.github.io/helm-charts`
- **Grafana**: `https://grafana.github.io/helm-charts`
- **Ingress-Nginx**: `https://kubernetes.github.io/ingress-nginx`

**OCI-репозитории** (Helm 3.8+): чарты можно хранить в OCI-совместимых registry (Docker Hub, ECR, GCR, etc.):

```bash
helm push myapp-1.0.0.tgz oci://registry.mycompany.com/charts
helm pull oci://registry.mycompany.com/charts/myapp --version 1.0.0
```

#### Release (релиз)

**Release** — экземпляр чарта, установленный в кластер Kubernetes. Один чарт может быть установлен несколько раз в разные namespace или с разными values — каждый раз создаётся новый release.

```bash
helm install myapp-prod ./mychart --values prod-values.yaml
helm install myapp-staging ./mychart --values staging-values.yaml
# myapp-prod и myapp-staging — разные релизы одного чарта
```

**Release хранит всю историю в Kubernetes Secrets:**

```
$ kubectl get secrets -l owner=helm
NAME                         TYPE     DATA
sh.helm.release.v1.myapp.v1  helm.sh/release.v1  1  # ревизия 1
sh.helm.release.v1.myapp.v2  helm.sh/release.v1  1  # ревизия 2
sh.helm.release.v1.myapp.v3  helm.sh/release.v1  1  # ревизия 3 (текущая)
```

#### Revision (ревизия)

**Revision** — версия релиза. Каждый `helm install`, `helm upgrade` или `helm rollback` создаёт новую ревизию. Ревизии позволяют быстро откатиться:

```bash
helm history myapp                    # список ревизий
helm rollback myapp 2                 # откат на ревизию 2
```

---

### Структура Chart

#### Обязательные файлы

| Файл | Описание |
|------|----------|
| `Chart.yaml` | Метаданные чарта |
| `values.yaml` | Значения по умолчанию |
| `templates/` | Директория с шаблонами (хотя бы один `.yaml` или `.tpl`) |

#### Необязательные файлы и директории

| Файл/директория | Описание |
|-----------------|----------|
| `charts/` | Подчарты (зависимости, скачанные `helm dependency update`) |
| `values.schema.json` | Валидация values |
| `templates/NOTES.txt` | Сообщение при установке (статус, инструкции) |
| `templates/_helpers.tpl` | Именованные шаблоны (partials) |
| `templates/tests/` | Тесты чарта (запускаются `helm test`) |
| `.helmignore` | Аналог `.gitignore` для пакета чарта |
| `README.md` | Документация чарта |
| `LICENSE` | Лицензия |
| `crds/` | Custom Resource Definitions |

#### Chart.yaml подробно

```yaml
apiVersion: v2                          # всегда v2 для Helm 3
name: myapp                             # имя чарта
description: A Helm chart for MyApp     # описание
type: application                       # application или library
version: 1.2.3                          # версия чарта (SemVer)
appVersion: "2.4.1"                     # версия приложения, которое упаковывается
kubeVersion: ">=1.25.0"                # минимальная версия Kubernetes
keywords:
  - web
  - api
home: https://github.com/org/myapp
sources:
  - https://github.com/org/myapp
maintainers:
  - name: DevOps Team
    email: devops@company.com
    url: https://company.com
icon: https://myapp.com/icon.png
annotations:
  category: Application
  licenses: MIT

dependencies:                           # зависимости чарта
  - name: postgresql
    version: "12.x.x"
    repository: "https://charts.bitnami.com/bitnami"
    condition: postgresql.enabled       # условие включения
    tags:
      - database
    import-values:                      # импорт значений из подчарта
      - child: service.port
        parent: db.port
  - name: redis
    version: "18.x.x"
    repository: "https://charts.bitnami.com/bitnami"
    condition: redis.enabled
    alias: cache                        # переименование подчарта
```

**type:**
- `application` — стандартный чарт приложения
- `library` — библиотечный чарт (только `_helpers.tpl`, не создаёт ресурсы)

---

### Шаблонизация: синтаксис Go Templates

Helm использует **Go Templates** с расширениями из пакета **Sprig** (дополнительные функции).

#### Основы синтаксиса

```
{{ ... }}                 — действие (вывод, условие, цикл)
{{- ... }}                — действие + удалить пробелы слева
{{ ... -}}                — действие + удалить пробелы справа
{{- ... -}}               — удалить пробелы с обеих сторон
{{/* комментарий */}}     — комментарий (не попадает в вывод)
```

#### Встроенные объекты (Built-in Objects)

| Объект | Содержит | Пример |
|--------|----------|--------|
| `{{ .Release.Name }}` | Имя релиза | `myapp` |
| `{{ .Release.Namespace }}` | Namespace релиза | `production` |
| `{{ .Release.Service }}` | Сервис, выполнивший релиз | `Helm` |
| `{{ .Release.IsInstall }}` | Первая установка? | `true` |
| `{{ .Release.IsUpgrade }}` | Обновление? | `false` |
| `{{ .Release.Revision }}` | Номер ревизии | `3` |
| `{{ .Chart.Name }}` | Имя чарта (из Chart.yaml) | `myapp` |
| `{{ .Chart.Version }}` | Версия чарта | `1.2.3` |
| `{{ .Chart.AppVersion }}` | Версия приложения | `2.4.1` |
| `{{ .Values }}` | Значения из values.yaml + переопределения | |
| `{{ .Files }}` | Доступ к файлам в чарте (кроме templates/) | |
| `{{ .Template.Name }}` | Путь к текущему шаблону | `mychart/templates/deployment.yaml` |
| `{{ .Capabilities.KubeVersion }}` | Версия Kubernetes-кластера | `v1.28.0` |
| `{{ .Capabilities.APIVersions }}` | Список доступных API-версий | |

#### Values (values.yaml)

**Приоритет values (от низшего к высшему):**

1. `values.yaml` чарта (значения по умолчанию)
2. `values.yaml` родительского чарта (если используется как подчарт)
3. Файл, переданный через `-f` / `--values` (может быть несколько)
4. `--set key=value` (может быть несколько)
5. `--set-string key=string_value` (всегда строка)

```bash
helm install myapp ./mychart \
  -f values/prod.yaml \
  --set replicas=5 \
  --set image.tag=v2.1.0 \
  --set-string appVersion="1.0"
```

#### Функции и pipelines

**Pipeline** (`|`) — передача результата в следующую функцию:

```
{{ .Values.name | upper | quote }}
```

порядок выполнения: `.Values.name` → `upper` → `quote`

**Основные функции:**

```yaml
# Работа со строками
{{ .Values.name | upper }}              # → "MYAPP"
{{ .Values.name | lower }}              # → "myapp"
{{ .Values.name | title }}              # → "Myapp"
{{ .Values.name | quote }}              # → "\"myapp\""
{{ .Values.name | b64enc }}             # → base64
{{ .Values.name | b64dec }}             # → из base64
{{ .Values.name | sha256sum }}          # → хэш
{{ "hello world" | trunc 5 }}           # → "hello"
{{ "hello" | repeat 3 }}                # → "hellohellohello"
{{ .Values.name | default "default" }}  # → "default" если name не задан
{{ .Values.name | empty }}              # → true/false (пусто?)
{{ .Values.name | required "name is required!" }}  # → ошибка при пустом

# Работа с типами
{{ .Values.count | int }}               # → int
{{ .Values.flag | toString }}           # → string
{{ .Values.list | toYaml }}             # → YAML
{{ .Values.list | toJson }}             # → JSON

# Работа со списками
{{ list "a" "b" "c" | first }}          # → "a"
{{ list "a" "b" | join "," }}           # → "a,b"
{{ .Values.items | indent 4 }}          # → отступ 4 пробела
{{ .Values.items | nindent 4 }}         # → новая строка + отступ 4
{{ .Values.list | shuffle }}            # → случайный порядок
{{ .Values.list | uniq }}               # → уникальные значения

# Работа со словарями
{{ $d := dict "key" "value" }}
{{ $d | keys | sortAlpha }}             # → ["key"]
{{ $d | values }}                       # → ["value"]
{{ merge $dict1 $dict2 }}               # → слияние (второй переопределяет первый)
{{ omit $dict "key1" "key2" }}          # → удалить ключи
{{ pick $dict "key1" }}                 # → оставить только указанные ключи

# Дата и время
{{ now | date "2006-01-02" }}           # → текущая дата
{{ now | dateModify "-24h" | date }}    # → 24 часа назад
{{ .Release.Time | date "Jan 2, 2006" }}

# Семантическое версионирование
{{ semverCompare ">=1.2.3" .Capabilities.KubeVersion.Version }}

# Арифметика
{{ add 2 3 }}                           # → 5
{{ sub 10 3 }}                          # → 7
{{ mul 2 3 }}                           # → 6
{{ div 10 2 }}                          # → 5
{{ max 5 10 3 }}                        # → 10
{{ min 5 10 3 }}                        # → 3

# Случайные значения
{{ randAlphaNum 16 }}                   # → случайная строка a-z, 0-9

# Работа с файлами
{{ .Files.Get "configs/app.conf" }}     # → содержимое файла
{{ .Files.GetBytes "data.bin" }}        # → байты файла
{{ .Files.Glob "configs/*.yaml" }}      # → список файлов по маске
{{ .Files.Lines "configs/app.conf" }}   # → содержимое как список строк
{{ (.Files.Glob "configs/*").AsConfig }} # → содержимое как ConfigMap
{{ (.Files.Glob "secrets/*").AsSecrets }}# → содержимое как Secret

# Условные функции
{{ coalesce .Values.x .Values.y "fallback" }}  # → первое непустое
{{ ternary "yes" "no" .Values.enabled }}       # → тернарный оператор

# Работа со строками URL
{{ urlJoin (list "https://example.com" "api" "v1") }}  # → https://example.com/api/v1
{{ urlParse "https://user:pass@example.com:8080/path?q=1#frag" }}
```

#### Условные операторы

```yaml
{{ if .Values.enabled }}
# ...
{{ else if .Values.otherEnabled }}
# ...
{{ else }}
# ...
{{ end }}

{{ if and .Values.enabled (eq .Values.env "production") }}
# ...
{{ end }}

{{ if or .Values.debug .Values.verbose }}
# ...
{{ end }}

{{ if not .Values.disabled }}
# ...
{{ end }}

# Операторы: eq, ne, lt, le, gt, ge
{{ if gt (int .Values.replicas) 3 }}
# ...
{{ end }}

# with — меняет контекст (точку) внутри блока
{{- with .Values.service }}
apiVersion: v1
kind: Service
metadata:
  name: {{ $.Release.Name }}   # $ — корневой контекст
spec:
  type: {{ .type }}            # . = .Values.service
  port: {{ .port }}
{{- end }}
```

#### Циклы и диапазоны

```yaml
# Простой range
{{- range .Values.ports }}
- containerPort: {{ . }}        # . = текущий элемент
{{- end }}

# Range с индексом и значением
{{- range $index, $element := .Values.items }}
- name: item-{{ $index }}
  value: {{ $element }}
{{- end }}

# Range по словарю
{{- range $key, $value := .Values.labels }}
  {{ $key }}: {{ $value }}
{{- end }}

# Range с переменной вне контекста
env:
{{- range .Values.env }}
  - name: {{ .name }}
    value: {{ .value | quote }}
{{- end }}
```

#### Именованные шаблоны (Named Templates / Partials)

Именованные шаблоны хранятся в `templates/_helpers.tpl` (или в любом файле, начинающемся с `_`). Они не создают ресурсы — только переиспользуемый код.

```yaml
# templates/_helpers.tpl
{{/*
Expand the name of the chart.
*/}}
{{- define "mychart.name" -}}
{{- default .Chart.Name .Values.nameOverride | trunc 63 | trimSuffix "-" }}
{{- end }}

{{/*
Create a default fully qualified app name.
*/}}
{{- define "mychart.fullname" -}}
{{- if .Values.fullnameOverride }}
{{- .Values.fullnameOverride | trunc 63 | trimSuffix "-" }}
{{- else }}
{{- $name := default .Chart.Name .Values.nameOverride }}
{{- printf "%s-%s" .Release.Name $name | trunc 63 | trimSuffix "-" }}
{{- end }}
{{- end }}

{{/*
Common labels
*/}}
{{- define "mychart.labels" -}}
helm.sh/chart: {{ include "mychart.chart" . }}
app.kubernetes.io/name: {{ include "mychart.name" . }}
app.kubernetes.io/instance: {{ .Release.Name }}
app.kubernetes.io/version: {{ .Chart.AppVersion | quote }}
app.kubernetes.io/managed-by: {{ .Release.Service }}
{{- end }}

{{/*
Selector labels
*/}}
{{- define "mychart.selectorLabels" -}}
app.kubernetes.io/name: {{ include "mychart.name" . }}
app.kubernetes.io/instance: {{ .Release.Name }}
{{- end }}
```

**Использование в шаблонах:**

```yaml
# templates/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ include "mychart.fullname" . }}
  labels:
    {{- include "mychart.labels" . | nindent 4 }}
spec:
  selector:
    matchLabels:
      {{- include "mychart.selectorLabels" . | nindent 6 }}
  template:
    metadata:
      labels:
        {{- include "mychart.selectorLabels" . | nindent 8 }}
    spec:
      containers:
      - name: {{ .Chart.Name }}
        image: "{{ .Values.image.repository }}:{{ .Values.image.tag | default .Chart.AppVersion }}"
```

---

### Helm Hooks

Хуки позволяют выполнить действия в определённые моменты жизненного цикла релиза.

#### Жизненный цикл и доступные хуки

| Хук | Когда выполняется | Типовой сценарий |
|-----|-------------------|-----------------|
| `pre-install` | После рендеринга шаблонов, до создания ресурсов | Создание Secret, настройка прав |
| `post-install` | После создания всех ресурсов | Создание индексов в БД |
| `pre-delete` | До удаления ресурсов (перед helm uninstall) | Очистка внешних ресурсов |
| `post-delete` | После удаления ресурсов | Удаление записей из внешнего DNS |
| `pre-upgrade` | После рендеринга, до обновления ресурсов | Бэкап БД, создание снепшота |
| `post-upgrade` | После обновления ресурсов | Миграция данных, обновление схемы |
| `pre-rollback` | После рендеринга, до отката | Подготовка данных к откату |
| `post-rollback` | После отката ресурсов | Проверка корректности отката |
| `test` | При вызове `helm test` | Интеграционные тесты |
| `test-success` | При успешном `helm test` | Нотификация об успехе |
| `test-failure` | При неудачном `helm test` | Нотификация об ошибке |

```yaml
# templates/job-db-migrate.yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: {{ include "mychart.fullname" . }}-db-migrate
  annotations:
    "helm.sh/hook": post-install,post-upgrade   # когда выполнять
    "helm.sh/hook-weight": "5"                   # порядок (меньше → раньше)
    "helm.sh/hook-delete-policy": before-hook-creation,hook-succeeded
spec:
  template:
    spec:
      restartPolicy: Never
      containers:
      - name: migrator
        image: myapp-migrator:{{ .Chart.AppVersion }}
```

#### Политики удаления хуков

| Политика | Поведение |
|----------|----------|
| `before-hook-creation` | Удалить предыдущий ресурс хука перед созданием нового |
| `hook-succeeded` | Удалить ресурс после успешного выполнения |
| `hook-failed` | Удалить ресурс после неудачного выполнения |

---

### Управление зависимостями

#### Chart.yaml dependencies

```yaml
dependencies:
  - name: postgresql
    version: "12.x.x"                    # версия подчарта
    repository: "https://charts.bitnami.com/bitnami"
    condition: postgresql.enabled        # условное включение
    tags:
      - database
    alias: db                            # псевдоним (позволяет установить несколько раз)
```

```bash
helm dependency update ./mychart         # скачать зависимости в charts/
helm dependency list ./mychart           # список зависимостей
helm dependency build ./mychart          # то же + пересборка lock-файла
```

#### Chart.lock

Файл `Chart.lock` фиксирует точные версии подчартов (аналог `package-lock.json`). Генерируется командой `helm dependency update`.

#### Library Charts

**Library Chart** (`type: library` в Chart.yaml) — это чарт, который не создаёт ресурсы, а только предоставляет именованные шаблоны для переиспользования другими чартами:

```yaml
# library-chart/templates/_helpers.tpl
{{- define "library.service" -}}
apiVersion: v1
kind: Service
spec:
  type: {{ .Values.service.type }}
  ports:
  - port: {{ .Values.service.port }}
{{- end }}
```

```yaml
# application-chart/Chart.yaml
dependencies:
  - name: library
    version: "1.0.0"
    repository: "file://../library-chart"
```

```yaml
# application-chart/templates/service.yaml
{{ include "library.service" . }}
```

---

### Helm CLI: шпаргалка

```bash
# === Репозитории ===
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo list
helm repo update                     # обновить индексы
helm repo remove bitnami
helm search repo bitnami/nginx       # поиск чарта в репозиториях
helm search hub wordpress            # поиск в Artifact Hub (публичный)

# === Установка и удаление ===
helm install RELEASE CHART [flags]
  --namespace NS                     # namespace
  --create-namespace                 # создать namespace если нет
  -f values.yaml                     # файл с values
  --set key=value                    # переопределить значение
  --set-string key=string            # строковое значение
  --values FILE                      # то же что -f
  --timeout 10m                      # таймаут
  --wait                             # ждать готовности
  --wait-for-jobs                    # ждать завершения Job
  --atomic                           # автоматический rollback при ошибке
  --dry-run                          # не устанавливать, показать манифесты
  --dependency-update                # обновить зависимости перед установкой
  --skip-crds                        # не устанавливать CRDs

helm uninstall RELEASE
  --keep-history                     # не удалять историю (секреты)
  --wait                             # ждать удаления всех ресурсов

# === Обновление ===
helm upgrade RELEASE CHART [flags]   # обновить существующий релиз
  (те же флаги, что и install)

helm upgrade --install RELEASE CHART # установить или обновить (идемпотентно)
helm upgrade --install --force RELEASE CHART  # пересоздать ресурсы

# === Откат ===
helm history RELEASE                 # история релиза
helm rollback RELEASE REVISION       # откатить на ревизию
  --timeout 10m
  --wait
  --cleanup-on-fail                  # удалить новый Pod при ошибке

# === Просмотр ===
helm list                            # список релизов
helm list -A                         # все namespace
helm list --filter myapp             # фильтр по имени
helm list --failed                   # только упавшие
helm status RELEASE                  # статус релиза
helm history RELEASE                 # история
helm get all RELEASE                 # всё: values, манифесты, хуки, заметки
helm get values RELEASE              # текущие values
helm get values RELEASE --revision 2 # values конкретной ревизии
helm get manifest RELEASE            # сгенерированные манифесты
helm get notes RELEASE               # NOTES.txt
helm get hooks RELEASE               # хуки
helm show chart CHART                # Chart.yaml чарта
helm show values CHART               # values.yaml чарта
helm show all CHART                  # всё

# === Работа с чартами ===
helm create NAME                     # создать заготовку чарта
helm package CHART_PATH              # упаковать чарт в .tgz (.helmignore применяется)
helm dependency update CHART_PATH    # скачать подчарты
helm dependency list CHART_PATH      # список зависимостей
helm template RELEASE CHART [flags]  # сгенерировать манифесты (без установки)
  --debug                            # показать отладочную информацию
  --show-only templates/deployment.yaml  # только конкретный шаблон
  -s templates/deployment.yaml       # то же короткий флаг
helm lint CHART_PATH                 # проверить чарт
  --strict                           # строгая проверка (warnings → errors)
helm test RELEASE                    # запустить тесты
  --logs                             # показать логи тестовых Pod

# === Плагины ===
helm plugin install https://github.com/helm-unittest/helm-unittest
helm plugin list
helm plugin update PLUGIN
helm plugin uninstall PLUGIN

# === Переменные окружения ===
export HELM_NAMESPACE=production
export HELM_KUBECONTEXT=prod-cluster
export HELM_DRIVER=secret            # или configmap, sql (где хранить историю)
```

---

### Тестирование чартов

#### helm lint

Проверяет чарт на соответствие best practices, синтаксические ошибки, наличие обязательных полей:

```bash
helm lint ./mychart
# =>
# ==> Linting ./mychart
# [INFO] Chart.yaml: icon is recommended
# 1 chart(s) linted, 0 chart(s) failed

helm lint --strict ./mychart    # warnings → errors
```

#### helm template

Рендерит шаблоны локально (без установки) для проверки вывода:

```bash
helm template RELEASE ./mychart --values ci/values.yaml --debug
```

Можно использовать для CI/CD: проверка, что шаблоны рендерятся без ошибок с разными комбинациями values.

#### helm unittest (плагин)

Плагин `helm-unittest` позволяет писать модульные тесты для шаблонов:

```bash
helm plugin install https://github.com/helm-unittest/helm-unittest
```

```yaml
# tests/deployment_test.yaml
suite: test deployment
templates:
  - deployment.yaml
tests:
  - it: should set correct image
    set:
      image.tag: "1.2.3"
    asserts:
      - equal:
          path: spec.template.spec.containers[0].image
          value: "myapp:1.2.3"

  - it: should set replicas correctly
    set:
      replicas: 5
    asserts:
      - equal:
          path: spec.replicas
          value: 5

  - it: should have liveness probe
    asserts:
      - exists:
          path: spec.template.spec.containers[0].livenessProbe

  - it: should not run as root
    asserts:
      - equal:
          path: spec.template.spec.securityContext.runAsNonRoot
          value: true

  - it: should have resource limits
    asserts:
      - contains:
          path: spec.template.spec.containers[0].resources
          content:
            limits:
              cpu: 500m
              memory: 512Mi
```

---

### Helm vs Kustomize

| Критерий | Helm | Kustomize |
|----------|------|-----------|
| **Подход** | Шаблонизация (Go templates) | Overlay (наложение патчей на базовые манифесты) |
| **Релизы** | Есть (install/upgrade/rollback) | Нет (просто kubectl apply) |
| **Зависимости** | Встроенные (Chart dependencies) | Нет (отдельные инструменты: kpt, helm) |
| **Пакетирование** | Chart-репозитории | Нет |
| **Кривая обучения** | Средняя (Go templates) | Низкая (YAML + patches) |
| **Интеграция с K8s** | Внешний инструмент | Встроен в kubectl (`kubectl apply -k`) |
| **Версионирование** | Встроенное (revisions) | Git |
| **Гибкость** | Высокая (условия, циклы, функции) | Средняя (патчи, strategic merge) |
| **Типовой сценарий** | Распространение приложений, публичные чарты | Настройка одних и тех же манифестов для разных сред |

**Когда что использовать:**
- **Helm**: приложения, которые распространяются как пакеты (базы данных, мониторинг, CI/CD), сложная логика шаблонизации, управление релизами.
- **Kustomize**: настройка одного приложения под разные окружения (dev/stage/prod), когда нужно только переопределить несколько полей без сложной логики.
- **Вместе**: можно использовать Kustomize для пост-обработки Helm-чартов или Helm для управления релизами с Kustomize-патчами через `helm install --post-renderer`.

---

### Лучшие практики Helm

#### Структура и названия

1. **Стандартизируйте `Chart.yaml`**: всегда заполняйте `description`, `appVersion`, `maintainers`.
2. **Используйте `_helpers.tpl`**: выносите повторяющуюся логику в именованные шаблоны.
3. **Документируйте чарт**: `README.md` с описанием параметров, примерами.
4. **`.helmignore`**: исключайте `.git`, `*.tgz`, `README.md`, тестовые файлы.
5. **Семантическое версионирование**: `version` (чарт) и `appVersion` (приложение).

#### Values

6. **Плоские values предпочтительнее глубоко вложенных**:
   ```yaml
   # ХОРОШО
   image: myapp
   imageTag: "1.2.3"
   
   # ПЛОХО (чрезмерная вложенность)
   application:
     container:
       image:
         name: myapp
         tag: "1.2.3"
   ```

7. **Комментируйте values.yaml**: каждый параметр должен быть задокументирован (что это, значения по умолчанию, допустимые значения).
8. **`values.schema.json`**: добавляйте JSON Schema для валидации типов, обязательных полей и допустимых значений.
9. **Используйте `required` для обязательных параметров**:
   ```yaml
   {{ required "image.repository is required!" .Values.image.repository }}
   ```

#### Шаблонизация

10. **Не генерируйте `name` если есть `fullnameOverride`**: используйте стандартный паттерн из `helm create`.
11. **Всегда задавайте labels**:
    ```yaml
    app.kubernetes.io/name: {{ include "mychart.name" . }}
    app.kubernetes.io/instance: {{ .Release.Name }}
    ```
12. **Используйте `nindent` вместо `indent`** в большинстве случаев:
    ```
    {{- include "mychart.labels" . | nindent 4 }}
    ```
13. **Не используйте `lookup` в шаблонах без крайней необходимости**: `lookup` обращается к API-серверу при рендеринге, что замедляет и может приводить к неожиданным результатам.

#### Безопасность

14. **Не храните секреты в values.yaml**: используйте внешние secret-менеджеры (External Secrets Operator, Sealed Secrets, Vault).
15. **Задавайте `securityContext` по умолчанию**: `runAsNonRoot: true`, `readOnlyRootFilesystem: true`, `allowPrivilegeEscalation: false`.
16. **Проверяйте чарты перед установкой**: `helm lint`, `helm template --debug`, сканирование образов.

---

## Часть III. Практические сценарии и референс-архитектуры

### Типовой CI/CD с Docker и Kubernetes

```
┌─────────┐   Push    ┌──────────┐   Build    ┌──────────────┐
│   Git   │──────────▶│  CI (Jen-│───────────▶│  Docker       │
│  (PR)   │           │ kins/GHA)│            │  Registry     │
└─────────┘           └────┬─────┘            └──────┬────────┘
                           │                        │
                           │ Deploy                 │ Pull
                           ▼                        ▼
                    ┌──────────────────────────────────┐
                    │         Kubernetes                │
                    │  ┌────────────────────────────┐  │
                    │  │  ArgoCD / Flux (GitOps)    │  │
                    │  │  или helm upgrade в CI/CD  │  │
                    │  └────────────┬───────────────┘  │
                    │               ▼                   │
                    │  ┌────────────────────────────┐  │
                    │  │  Deployment (RollingUpdate) │  │
                    │  │  ├── Pod v2 (new)          │  │
                    │  │  ├── Pod v2 (new)          │  │
                    │  │  └── Pod v2 (new)          │  │
                    │  └────────────────────────────┘  │
                    └──────────────────────────────────┘
```

**Этапы:**
1. Разработчик пушит код в Git.
2. CI (GitHub Actions / GitLab CI / Jenkins) собирает Docker-образ и пушит в Registry.
3. CI обновляет конфигурацию в Git-репозитории (новый тег образа).
4. GitOps-оператор (ArgoCD / Flux) синхронизирует кластер с Git-репозиторием — происходит развёртывание.

### Локальная разработка: Dev-контур

Инструменты для локальной разработки с Kubernetes:

| Инструмент | Описание | Когда использовать |
|-----------|----------|--------------------|
| **Docker Desktop** | Встроенный Kubernetes | Простой локальный кластер |
| **minikube** | Локальный кластер K8s | Изучение K8s, разработка |
| **kind** | K8s в Docker-контейнерах | CI/CD тестирование |
| **k3s / k3d** | Легковесный K8s (Rancher) | Производственная разработка, IoT |
| **Tilt / Skaffold** | Hot reload для K8s | Быстрая итерация «изменил код — увидел результат» |
| **Telepresence** | Прокси-соединение с удалённым кластером | Разработка локально, зависимости в облачном кластере |
| **DevSpace** | Полный dev-цикл с K8s | Команды, которым нужен полноценный dev-контур |

### Production-grade кластер: чек-лист

- [ ] **Control Plane HA**: минимум 3 узла control plane + внешний etcd или stacked etcd с 3 узлами.
- [ ] **etcd backup**: автоматическое регулярное резервное копирование.
- [ ] **Worker nodes**: минимум 3 узла (для распределения Pod и отказоустойчивости).
- [ ] **CNI plugin**: Calico или Cilium для NetworkPolicy.
- [ ] **Metrics Server**: для HPA и `kubectl top`.
- [ ] **Ingress Controller**: Nginx Ingress или Traefik (или Gateway API).
- [ ] **Storage Class**: динамическое Provisioning томов.
- [ ] **RBAC**: минимальные права для каждого ServiceAccount.
- [ ] **Pod Security Standards**: `restricted` для приложений.
- [ ] **Network Policies**: deny-all + точечные разрешения.
- [ ] **Resource Quotas**: для каждого namespace.
- [ ] **Limit Ranges**: значения по умолчанию и границы для Pod.
- [ ] **Priority Classes**: чтобы критичные Pod имели приоритет.
- [ ] **Pod Disruption Budgets**: для критичных сервисов.
- [ ] **Monitoring**: Prometheus + Grafana + Alertmanager.
- [ ] **Logging**: Fluent Bit + Loki/Elasticsearch + Grafana.
- [ ] **Tracing**: Jaeger или Tempo (OpenTelemetry).
- [ ] **Secret Management**: External Secrets Operator или Sealed Secrets.
- [ ] **Certificate Management**: cert-manager для автоматического Let's Encrypt.
- [ ] **GitOps**: ArgoCD или Flux для синхронизации с Git.
- [ ] **Backup**: Velero для резервного копирования ресурсов и томов.
- [ ] **Registry**: приватный registry (Harbor или облачный).
- [ ] **Image Scanning**: Trivy или Grype в CI/CD.
- [ ] **Policy as Code**: OPA/Gatekeeper или Kyverno.

### Миграция с Docker Compose на Kubernetes

| Docker Compose концепция | Kubernetes эквивалент |
|--------------------------|----------------------|
| Service | Deployment + Service |
| `ports:` | Service (ClusterIP / NodePort / LoadBalancer) |
| `volumes:` | PersistentVolume + PersistentVolumeClaim |
| `environment:` | ConfigMap / Secret + env в Pod spec |
| `depends_on:` | Init Containers (+ startupProbe для синхронизации) |
| `networks:` | Network Namespace + NetworkPolicy |
| `restart: always` | `restartPolicy: Always` (в Pod spec) |
| `healthcheck:` | livenessProbe / readinessProbe |
| `deploy.resources.limits:` | resources.limits |
| `secrets:` | Secret |
| `profiles:` | Отдельные values-файлы для Helm |
| `docker-compose.yml` | Helm Chart / Kustomize / plain manifests |

**Инструменты для миграции:**
- **Kompose**: `kompose convert -f docker-compose.yml` — автоматическая конвертация Compose → K8s манифесты
- **Move2Kube**: более продвинутый инструмент трансформации

---

## Заключение

Контейнеризация и оркестрация — фундамент современной разработки. Docker решил проблему «как упаковать приложение, чтобы оно работало везде одинаково». Kubernetes решил проблему «как управлять всем этим в масштабе». Helm сделал Kubernetes доступным через пакетирование и переиспользование.

Ключевая идея всего этого стека — **декларативность**: вы описываете желаемое состояние (Deployment → 3 реплики → образ `myapp:1.2.3`), а система сама приводит реальность к этому состоянию и поддерживает его. Это фундаментально отличается от императивного подхода («запусти процесс на сервере X, теперь на сервере Y, а теперь обнови сервер X»).

Экосистема продолжает развиваться: Gateway API заменяет Ingress, OpenTelemetry становится стандартом observability, GitOps через ArgoCD и Flux меняет подход к доставке, sidecar-контейнеры становятся нативной функцией Kubernetes — но Docker, Kubernetes и Helm остаются тремя китами, на которых держится контейнеризированная инфраструктура.

---

> **Рекомендуемая литература и ресурсы:**
> - [Docker Documentation](https://docs.docker.com/)
> - [Kubernetes Documentation](https://kubernetes.io/docs/)
> - [Helm Documentation](https://helm.sh/docs/)
> - [CNCF Landscape](https://landscape.cncf.io/)
> - [Kubernetes the Hard Way (Kelsey Hightower)](https://github.com/kelseyhightower/kubernetes-the-hard-way)
> - [12 Factor App](https://12factor.net/)
> - [Artifact Hub](https://artifacthub.io/) — каталог Helm-чартов и других cloud-native артефактов
