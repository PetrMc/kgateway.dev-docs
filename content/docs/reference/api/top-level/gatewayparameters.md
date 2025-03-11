---
title: GatewayParameters
weight: 30
description: API reference for GatewayParameters
---

# GatewayParameters

#### GatewayParameters



A GatewayParameters contains configuration that is used to dynamically
provision kgateway's data plane (Envoy proxy instance), based on a
Kubernetes Gateway.



_Appears in:_
- [GatewayParametersList](#gatewayparameterslist)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `apiVersion` _string_ | `gateway.kgateway.dev/v1alpha1` | | |
| `kind` _string_ | `GatewayParameters` | | |
| `kind` _string_ | Kind is a string value representing the REST resource this object represents.<br />Servers may infer this from the endpoint the client submits requests to.<br />Cannot be updated.<br />In CamelCase.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds |  |  |
| `apiVersion` _string_ | APIVersion defines the versioned schema of this representation of an object.<br />Servers should convert recognized schemas to the latest internal value, and<br />may reject unrecognized values.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources |  |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |  |  |
| `spec` _[GatewayParametersSpec](#gatewayparametersspec)_ |  |  |  |
| `status` _[GatewayParametersStatus](#gatewayparametersstatus)_ |  |  |  |




# GatewayParametersList

#### GatewayParametersList









| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `apiVersion` _string_ | `gateway.kgateway.dev/v1alpha1` | | |
| `kind` _string_ | `GatewayParametersList` | | |
| `kind` _string_ | Kind is a string value representing the REST resource this object represents.<br />Servers may infer this from the endpoint the client submits requests to.<br />Cannot be updated.<br />In CamelCase.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds |  |  |
| `apiVersion` _string_ | APIVersion defines the versioned schema of this representation of an object.<br />Servers should convert recognized schemas to the latest internal value, and<br />may reject unrecognized values.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources |  |  |
| `metadata` _[ListMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#listmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |  |  |
| `items` _[GatewayParameters](#gatewayparameters) array_ |  |  |  |




# GatewayParametersSpec

#### GatewayParametersSpec



A GatewayParametersSpec describes the type of environment/platform in which
the proxy will be provisioned.



_Appears in:_
- [GatewayParameters](#gatewayparameters)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `kube` _[KubernetesProxyConfig](#kubernetesproxyconfig)_ | The proxy will be deployed on Kubernetes. |  | Optional: \{\} <br /> |
| `selfManaged` _[SelfManagedGateway](#selfmanagedgateway)_ | The proxy will be self-managed and not auto-provisioned. |  | Optional: \{\} <br /> |




# KubernetesProxyConfig

#### KubernetesProxyConfig



Configuration for the set of Kubernetes resources that will be provisioned
for a given Gateway.



_Appears in:_
- [GatewayParametersSpec](#gatewayparametersspec)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `deployment` _[ProxyDeployment](#proxydeployment)_ | Use a Kubernetes deployment as the proxy workload type. Currently, this is the only<br />supported workload type. |  | Optional: \{\} <br /> |
| `envoyContainer` _[EnvoyContainer](#envoycontainer)_ | Configuration for the container running Envoy. |  | Optional: \{\} <br /> |
| `sdsContainer` _[SdsContainer](#sdscontainer)_ | Configuration for the container running the Secret Discovery Service (SDS). |  | Optional: \{\} <br /> |
| `podTemplate` _[Pod](#pod)_ | Configuration for the pods that will be created. |  | Optional: \{\} <br /> |
| `service` _[Service](#service)_ | Configuration for the Kubernetes Service that exposes the Envoy proxy over<br />the network. |  | Optional: \{\} <br /> |
| `serviceAccount` _[ServiceAccount](#serviceaccount)_ | Configuration for the Kubernetes ServiceAccount used by the Envoy pod. |  | Optional: \{\} <br /> |
| `istio` _[IstioIntegration](#istiointegration)_ | Configuration for the Istio integration. |  | Optional: \{\} <br /> |
| `stats` _[StatsConfig](#statsconfig)_ | Configuration for the stats server. |  | Optional: \{\} <br /> |
| `aiExtension` _[AiExtension](#aiextension)_ | Configuration for the AI extension. |  | Optional: \{\} <br /> |
| `floatingUserId` _boolean_ | Used to unset the `runAsUser` values in security contexts. |  |  |




# ProxyDeployment

#### ProxyDeployment



Configuration for the Proxy deployment in Kubernetes.



_Appears in:_
- [KubernetesProxyConfig](#kubernetesproxyconfig)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `replicas` _integer_ | The number of desired pods. Defaults to 1. |  | Optional: \{\} <br /> |




# EnvoyContainer

#### EnvoyContainer



Configuration for the container running Envoy.



_Appears in:_
- [KubernetesProxyConfig](#kubernetesproxyconfig)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `bootstrap` _[EnvoyBootstrap](#envoybootstrap)_ | Initial envoy configuration. |  | Optional: \{\} <br /> |
| `image` _[Image](#image)_ | The envoy container image. See<br />https://kubernetes.io/docs/concepts/containers/images<br />for details.<br /><br />Default values, which may be overridden individually:<br /><br />	registry: quay.io/solo-io<br />	repository: gloo-envoy-wrapper (OSS) / gloo-ee-envoy-wrapper (EE)<br />	tag: <gloo version> (OSS) / <gloo-ee version> (EE)<br />	pullPolicy: IfNotPresent |  | Optional: \{\} <br /> |
| `securityContext` _[SecurityContext](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#securitycontext-v1-core)_ | The security context for this container. See<br />https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core<br />for details. |  | Optional: \{\} <br /> |
| `resources` _[ResourceRequirements](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#resourcerequirements-v1-core)_ | The compute resources required by this container. See<br />https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br />for details. |  | Optional: \{\} <br /> |




# EnvoyBootstrap

#### EnvoyBootstrap



Configuration for the Envoy proxy instance that is provisioned from a
Kubernetes Gateway.



_Appears in:_
- [EnvoyContainer](#envoycontainer)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `logLevel` _string_ | Envoy log level. Options include "trace", "debug", "info", "warn", "error",<br />"critical" and "off". Defaults to "info". See<br />https://www.envoyproxy.io/docs/envoy/latest/start/quick-start/run-envoy#debugging-envoy<br />for more information. |  | Optional: \{\} <br /> |
| `componentLogLevels` _object (keys:string, values:string)_ | Envoy log levels for specific components. The keys are component names and<br />the values are one of "trace", "debug", "info", "warn", "error",<br />"critical", or "off", e.g.<br /><br />	```yaml<br />	componentLogLevels:<br />	  upstream: debug<br />	  connection: trace<br />	```<br /><br />These will be converted to the `--component-log-level` Envoy argument<br />value. See<br />https://www.envoyproxy.io/docs/envoy/latest/start/quick-start/run-envoy#debugging-envoy<br />for more information.<br /><br />Note: the keys and values cannot be empty, but they are not otherwise validated. |  | Optional: \{\} <br /> |




# Image

#### Image



A container image. See https://kubernetes.io/docs/concepts/containers/images
for details.



_Appears in:_
- [AiExtension](#aiextension)
- [EnvoyContainer](#envoycontainer)
- [IstioContainer](#istiocontainer)
- [SdsContainer](#sdscontainer)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `registry` _string_ | The image registry. |  | Optional: \{\} <br /> |
| `repository` _string_ | The image repository (name). |  | Optional: \{\} <br /> |
| `tag` _string_ | The image tag. |  | Optional: \{\} <br /> |
| `digest` _string_ | The hash digest of the image, e.g. `sha256:12345...` |  | Optional: \{\} <br /> |
| `pullPolicy` _[PullPolicy](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#pullpolicy-v1-core)_ | The image pull policy for the container. See<br />https://kubernetes.io/docs/concepts/containers/images/#image-pull-policy<br />for details. |  | Optional: \{\} <br /> |




# AiExtension

#### AiExtension



Configuration for the AI extension.



_Appears in:_
- [KubernetesProxyConfig](#kubernetesproxyconfig)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `enabled` _boolean_ | Whether to enable the extension. |  | Optional: \{\} <br /> |
| `image` _[Image](#image)_ | The extension's container image. See<br />https://kubernetes.io/docs/concepts/containers/images<br />for details. |  | Optional: \{\} <br /> |
| `securityContext` _[SecurityContext](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#securitycontext-v1-core)_ | The security context for this container. See<br />https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core<br />for details. |  | Optional: \{\} <br /> |
| `resources` _[ResourceRequirements](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#resourcerequirements-v1-core)_ | The compute resources required by this container. See<br />https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br />for details. |  | Optional: \{\} <br /> |
| `env` _[EnvVar](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#envvar-v1-core) array_ | The extension's container environment variables. |  | Optional: \{\} <br /> |
| `ports` _[ContainerPort](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#containerport-v1-core) array_ | The extension's container ports. |  | Optional: \{\} <br /> |
| `stats` _[AiExtensionStats](#aiextensionstats)_ | Additional stats config for AI Extension.<br />This config can be useful for adding custom labels to the request metrics.<br /><br />Example:<br />```yaml<br />stats:<br />  customLabels:<br />    - name: "subject"<br />      metadataNamespace: "envoy.filters.http.jwt_authn"<br />      metadataKey: "principal:sub"<br />    - name: "issuer"<br />      metadataNamespace: "envoy.filters.http.jwt_authn"<br />      metadataKey: "principal:iss"<br />``` |  |  |




# AiExtensionStats

#### AiExtensionStats







_Appears in:_
- [AiExtension](#aiextension)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `customLabels` _[CustomLabel](#customlabel) array_ | Set of custom labels to be added to the request metrics.<br />These will be added on each request which goes through the AI Extension. |  |  |




# CustomLabel

#### CustomLabel

_Underlying type:_ _[struct{Name string "json:\"name\""; MetadataNamespace *string "json:\"metadataNamespace,omitempty\""; MetdataKey string "json:\"metadataKey\""; KeyDelimiter *string "json:\"keyDelimiter,omitempty\""}](#struct{name-string-"json:\"name\"";-metadatanamespace-*string-"json:\"metadatanamespace,omitempty\"";-metdatakey-string-"json:\"metadatakey\"";-keydelimiter-*string-"json:\"keydelimiter,omitempty\""})_





_Appears in:_
- [AiExtensionStats](#aiextensionstats)





# IstioContainer

#### IstioContainer



Configuration for the container running the istio-proxy.



_Appears in:_
- [IstioIntegration](#istiointegration)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `image` _[Image](#image)_ | The envoy container image. See<br />https://kubernetes.io/docs/concepts/containers/images<br />for details. |  | Optional: \{\} <br /> |
| `securityContext` _[SecurityContext](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#securitycontext-v1-core)_ | The security context for this container. See<br />https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core<br />for details. |  | Optional: \{\} <br /> |
| `resources` _[ResourceRequirements](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#resourcerequirements-v1-core)_ | The compute resources required by this container. See<br />https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br />for details. |  | Optional: \{\} <br /> |
| `logLevel` _string_ | Log level for istio-proxy. Options include "info", "debug", "warning", and "error".<br />Default level is info Default is "warning". |  | Optional: \{\} <br /> |
| `istioDiscoveryAddress` _string_ | The address of the istio discovery service. Defaults to "istiod.istio-system.svc:15012". |  | Optional: \{\} <br /> |
| `istioMetaMeshId` _string_ | The mesh id of the istio mesh. Defaults to "cluster.local". |  | Optional: \{\} <br /> |
| `istioMetaClusterId` _string_ | The cluster id of the istio cluster. Defaults to "Kubernetes". |  | Optional: \{\} <br /> |




# IstioIntegration

#### IstioIntegration



Configuration for the Istio integration settings used by a Gloo Gateway's data plane (Envoy proxy instance)



_Appears in:_
- [KubernetesProxyConfig](#kubernetesproxyconfig)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `istioProxyContainer` _[IstioContainer](#istiocontainer)_ | Configuration for the container running istio-proxy.<br />Note that if Istio integration is not enabled, the istio container will not be injected<br />into the gateway proxy deployment. |  | Optional: \{\} <br /> |
| `customSidecars` _[Container](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#container-v1-core) array_ | do not use slice of pointers: https://github.com/kubernetes/code-generator/issues/166<br />Override the default Istio sidecar in gateway-proxy with a custom container. |  | Optional: \{\} <br /> |




# SdsContainer

#### SdsContainer



Configuration for the container running Gloo SDS.



_Appears in:_
- [KubernetesProxyConfig](#kubernetesproxyconfig)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `image` _[Image](#image)_ | The SDS container image. See<br />https://kubernetes.io/docs/concepts/containers/images<br />for details. |  | Optional: \{\} <br /> |
| `securityContext` _[SecurityContext](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#securitycontext-v1-core)_ | The security context for this container. See<br />https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core<br />for details. |  | Optional: \{\} <br /> |
| `resources` _[ResourceRequirements](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#resourcerequirements-v1-core)_ | The compute resources required by this container. See<br />https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br />for details. |  | Optional: \{\} <br /> |
| `bootstrap` _[SdsBootstrap](#sdsbootstrap)_ | Initial SDS container configuration. |  | Optional: \{\} <br /> |




# SdsBootstrap

#### SdsBootstrap



Configuration for the SDS instance that is provisioned from a Kubernetes Gateway.



_Appears in:_
- [SdsContainer](#sdscontainer)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `logLevel` _string_ | Log level for SDS. Options include "info", "debug", "warn", "error", "panic" and "fatal".<br />Default level is "info". |  | Optional: \{\} <br /> |




# Pod

#### Pod



Configuration for a Kubernetes Pod template.



_Appears in:_
- [KubernetesProxyConfig](#kubernetesproxyconfig)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `extraLabels` _object (keys:string, values:string)_ | Additional labels to add to the Pod object metadata. |  | Optional: \{\} <br /> |
| `extraAnnotations` _object (keys:string, values:string)_ | Additional annotations to add to the Pod object metadata. |  | Optional: \{\} <br /> |
| `securityContext` _[PodSecurityContext](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#podsecuritycontext-v1-core)_ | The pod security context. See<br />https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#podsecuritycontext-v1-core<br />for details. |  | Optional: \{\} <br /> |
| `imagePullSecrets` _[LocalObjectReference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#localobjectreference-v1-core) array_ | An optional list of references to secrets in the same namespace to use for<br />pulling any of the images used by this Pod spec. See<br />https://kubernetes.io/docs/concepts/containers/images/#specifying-imagepullsecrets-on-a-pod<br />for details. |  | Optional: \{\} <br /> |
| `nodeSelector` _object (keys:string, values:string)_ | A selector which must be true for the pod to fit on a node. See<br />https://kubernetes.io/docs/concepts/configuration/assign-pod-node/ for<br />details. |  | Optional: \{\} <br /> |
| `affinity` _[Affinity](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#affinity-v1-core)_ | If specified, the pod's scheduling constraints. See<br />https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#affinity-v1-core<br />for details. |  | Optional: \{\} <br /> |
| `tolerations` _[Toleration](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#toleration-v1-core) array_ | do not use slice of pointers: https://github.com/kubernetes/code-generator/issues/166<br />If specified, the pod's tolerations. See<br />https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#toleration-v1-core<br />for details. |  | Optional: \{\} <br /> |
| `gracefulShutdown` _[GracefulShutdownSpec](#gracefulshutdownspec)_ | If specified, the pod's graceful shutdown spec. |  | Optional: \{\} <br /> |
| `terminationGracePeriodSeconds` _integer_ | If specified, the pod's termination grace period in seconds. See<br />https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#pod-v1-core<br />for details |  | Optional: \{\} <br /> |
| `readinessProbe` _[Probe](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#probe-v1-core)_ | If specified, the pod's readiness probe. Periodic probe of container service readiness.<br />Container will be removed from service endpoints if the probe fails. See<br />https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#probe-v1-core<br />for details. |  | Optional: \{\} <br /> |
| `livenessProbe` _[Probe](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#probe-v1-core)_ | If specified, the pod's liveness probe. Periodic probe of container service readiness.<br />Container will be restarted if the probe fails. See<br />https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#probe-v1-core<br />for details. |  | Optional: \{\} <br /> |




# GracefulShutdownSpec

#### GracefulShutdownSpec







_Appears in:_
- [Pod](#pod)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `enabled` _boolean_ | Enable grace period before shutdown to finish current requests while Envoy health checks fail to e.g. notify external load balancers. *NOTE:* This will not have any effect if you have not defined health checks via the health check filter |  | Optional: \{\} <br /> |
| `sleepTimeSeconds` _integer_ | Time (in seconds) for the preStop hook to wait before allowing Envoy to terminate |  | Optional: \{\} <br /> |




# Service

#### Service



Configuration for a Kubernetes Service.



_Appears in:_
- [KubernetesProxyConfig](#kubernetesproxyconfig)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `type` _[ServiceType](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#servicetype-v1-core)_ | The Kubernetes Service type. |  | Optional: \{\} <br /> |
| `clusterIP` _string_ | The manually specified IP address of the service, if a randomly assigned<br />IP is not desired. See<br />https://kubernetes.io/docs/concepts/services-networking/service/#choosing-your-own-ip-address<br />and<br />https://kubernetes.io/docs/concepts/services-networking/service/#headless-services<br />on the implications of setting `clusterIP`. |  | Optional: \{\} <br /> |
| `extraLabels` _object (keys:string, values:string)_ | Additional labels to add to the Service object metadata. |  | Optional: \{\} <br /> |
| `extraAnnotations` _object (keys:string, values:string)_ | Additional annotations to add to the Service object metadata. |  | Optional: \{\} <br /> |




# ServiceAccount

#### ServiceAccount







_Appears in:_
- [KubernetesProxyConfig](#kubernetesproxyconfig)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `extraLabels` _object (keys:string, values:string)_ | Additional labels to add to the ServiceAccount object metadata. |  | Optional: \{\} <br /> |
| `extraAnnotations` _object (keys:string, values:string)_ | Additional annotations to add to the ServiceAccount object metadata. |  | Optional: \{\} <br /> |




# StatsConfig

#### StatsConfig



Configuration for the stats server.



_Appears in:_
- [KubernetesProxyConfig](#kubernetesproxyconfig)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `enabled` _boolean_ | Whether to expose metrics annotations and ports for scraping metrics. |  | Optional: \{\} <br /> |
| `routePrefixRewrite` _string_ | The Envoy stats endpoint to which the metrics are written |  | Optional: \{\} <br /> |
| `enableStatsRoute` _boolean_ | Enables an additional route to the stats cluster defaulting to /stats |  | Optional: \{\} <br /> |
| `statsRoutePrefixRewrite` _string_ | The Envoy stats endpoint with general metrics for the additional stats route |  | Optional: \{\} <br /> |




# SelfManagedGateway

#### SelfManagedGateway







_Appears in:_
- [GatewayParametersSpec](#gatewayparametersspec)





# GatewayParametersStatus

#### GatewayParametersStatus



The current conditions of the GatewayParameters. This is not currently implemented.



_Appears in:_
- [GatewayParameters](#gatewayparameters)





