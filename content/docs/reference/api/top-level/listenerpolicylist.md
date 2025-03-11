---
title: ListenerPolicyList
weight: 110
description: API reference for ListenerPolicyList
---

# ListenerPolicyList API Reference

#### ListenerPolicyList









| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `apiVersion` _string_ | `gateway.kgateway.dev/v1alpha1` | | |
| `kind` _string_ | `ListenerPolicyList` | | |
| `kind` _string_ | Kind is a string value representing the REST resource this object represents.<br />Servers may infer this from the endpoint the client submits requests to.<br />Cannot be updated.<br />In CamelCase.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds |  |  |
| `apiVersion` _string_ | APIVersion defines the versioned schema of this representation of an object.<br />Servers should convert recognized schemas to the latest internal value, and<br />may reject unrecognized values.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources |  |  |
| `metadata` _[ListMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#listmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |  |  |
| `items` _[ListenerPolicy](#listenerpolicy) array_ |  |  |  |




#### AIBackend





_Validation:_
- MaxProperties: 1
- MinProperties: 1

_Appears in:_
- [BackendSpec](#backendspec)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `llm` _[LLMProvider](#llmprovider)_ | The LLM configures the AI gateway to use a single LLM provider backend. |  |  |
| `multipool` _[MultiPoolConfig](#multipoolconfig)_ | The MultiPool configures the backends for multiple hosts or models from the same provider in one Backend resource. |  |  |




#### AIPromptEnrichment



AIPromptEnrichment defines the config to enrich requests sent to the LLM provider by appending and prepending system prompts.
This can be configured only for LLM providers that use the `CHAT` or `CHAT_STREAMING` API type.


Prompt enrichment allows you to add additional context to the prompt before sending it to the model.
Unlike RAG or other dynamic context methods, prompt enrichment is static and is applied to every request.


**Note**: Some providers, including Anthropic, do not support SYSTEM role messages, and instead have a dedicated
system field in the input JSON. In this case, use the [`defaults` setting](#fielddefault) to set the system field.


The following example prepends a system prompt of `Answer all questions in French.`
and appends `Describe the painting as if you were a famous art critic from the 17th century.`
to each request that is sent to the `openai` HTTPRoute.
```yaml


	name: openai-opt
	namespace: kgateway-system


spec:


	targetRefs:
	- group: gateway.networking.k8s.io
	  kind: HTTPRoute
	  name: openai
	aiRoutePolicy:
	    promptEnrichment:
	      prepend:
	      - role: SYSTEM
	        content: "Answer all questions in French."
	      append:
	      - role: USER
	        content: "Describe the painting as if you were a famous art critic from the 17th century."


```



_Appears in:_
- [AIRoutePolicy](#airoutepolicy)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `prepend` _[Message](#message) array_ | A list of messages to be prepended to the prompt sent by the client. |  |  |
| `append` _[Message](#message) array_ | A list of messages to be appended to the prompt sent by the client. |  |  |




#### AIPromptGuard



AIPromptGuard configures a prompt guards to block unwanted requests to the LLM provider and mask sensitive data.
Prompt guards can be used to reject requests based on the content of the prompt, as well as
mask responses based on the content of the response.


This example rejects any request prompts that contain
the string "credit card", and masks any credit card numbers in the response.
```yaml
promptGuard:


	request:
	  customResponse:
	    message: "Rejected due to inappropriate content"
	  regex:
	    action: REJECT
	    matches:
	    - pattern: "credit card"
	      name: "CC"
	response:
	  regex:
	    builtins:
	    - CREDIT_CARD
	    action: MASK


```



_Appears in:_
- [AIRoutePolicy](#airoutepolicy)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `request` _[PromptguardRequest](#promptguardrequest)_ | Prompt guards to apply to requests sent by the client. |  |  |
| `response` _[PromptguardResponse](#promptguardresponse)_ | Prompt guards to apply to responses returned by the LLM provider. |  |  |




#### AIRoutePolicy



AIRoutePolicy config is used to configure the behavior of the LLM provider
on the level of individual routes. These route settings, such as prompt enrichment,
retrieval augmented generation (RAG), and semantic caching, are applicable only
for routes that send requests to an LLM provider backend.



_Appears in:_
- [RoutePolicySpec](#routepolicyspec)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `promptEnrichment` _[AIPromptEnrichment](#aipromptenrichment)_ | Enrich requests sent to the LLM provider by appending and prepending system prompts.<br />This can be configured only for LLM providers that use the `CHAT` or `CHAT_STREAMING` API route type. |  |  |
| `promptGuard` _[AIPromptGuard](#aipromptguard)_ | Set up prompt guards to block unwanted requests to the LLM provider and mask sensitive data.<br />Prompt guards can be used to reject requests based on the content of the prompt, as well as<br />mask responses based on the content of the response. |  |  |
| `defaults` _[FieldDefault](#fielddefault) array_ | Provide defaults to merge with user input fields.<br />Defaults do _not_ override the user input fields, unless you explicitly set `override` to `true`. |  |  |
| `routeType` _[RouteType](#routetype)_ | The type of route to the LLM provider API. Currently, `CHAT` and `CHAT_STREAMING` are supported. |  | Enum: [CHAT CHAT_STREAMING] <br /> |




#### AccessLog



AccessLog represents the top-level access log configuration.



_Appears in:_
- [HTTPListenerPolicySpec](#httplistenerpolicyspec)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `fileSink` _[FileSink](#filesink)_ | Output access logs to local file |  |  |
| `grpcService` _[GrpcService](#grpcservice)_ | Send access logs to gRPC service |  |  |
| `filter` _[AccessLogFilter](#accesslogfilter)_ | Filter access logs configuration |  | MaxProperties: 1 <br />MinProperties: 1 <br /> |




#### AccessLogFilter



AccessLogFilter represents the top-level filter structure.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-accesslogfilter

_Validation:_
- MaxProperties: 1
- MinProperties: 1

_Appears in:_
- [AccessLog](#accesslog)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `andFilter` _[FilterType](#filtertype) array_ | Performs a logical "and" operation on the result of each individual filter.<br />Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-andfilter |  | MaxProperties: 1 <br />MinItems: 2 <br />MinProperties: 1 <br /> |
| `orFilter` _[FilterType](#filtertype) array_ | Performs a logical "or" operation on the result of each individual filter.<br />Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-orfilter |  | MaxProperties: 1 <br />MinItems: 2 <br />MinProperties: 1 <br /> |




#### Action

_Underlying type:_ _string_

Action to take if a regex pattern is matched in a request or response.
This setting applies only to request matches. PromptguardResponse matches are always masked by default.



_Appears in:_
- [Regex](#regex)

| Field | Description |
| --- | --- |
| `MASK` | Mask the matched data in the request.<br /> |
| `REJECT` | Reject the request if the regex matches content in the request.<br /> |




#### AnthropicConfig



AnthropicConfig settings for the [Anthropic](https://docs.anthropic.com/en/release-notes/api) LLM provider.



_Appears in:_
- [SupportedLLMProvider](#supportedllmprovider)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `authToken` _[SingleAuthToken](#singleauthtoken)_ | The authorization token that the AI gateway uses to access the Anthropic API.<br />This token is automatically sent in the `x-api-key` header of the request. |  | Required: \{\} <br /> |
| `apiVersion` _string_ | Optional: A version header to pass to the Anthropic API.<br />For more information, see the [Anthropic API versioning docs](https://docs.anthropic.com/en/api/versioning). |  |  |
| `model` _string_ | Optional: Override the model name.<br />If unset, the model name is taken from the request.<br />This setting can be useful when testing model failover scenarios. |  |  |




#### AwsBackend



AwsBackend is the AWS backend configuration.



_Appears in:_
- [BackendSpec](#backendspec)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `region` _string_ | Region is the AWS region. |  |  |
| `secretRef` _[LocalObjectReference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#localobjectreference-v1-core)_ | SecretRef is the secret reference for the AWS credentials. |  |  |




#### AzureOpenAIConfig



AzureOpenAIConfig settings for the [Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/) LLM provider.



_Appears in:_
- [SupportedLLMProvider](#supportedllmprovider)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `authToken` _[SingleAuthToken](#singleauthtoken)_ | The authorization token that the AI gateway uses to access the Azure OpenAI API.<br />This token is automatically sent in the `api-key` header of the request. |  | Required: \{\} <br /> |
| `endpoint` _string_ | The endpoint for the Azure OpenAI API to use, such as `my-endpoint.openai.azure.com`.<br />If the scheme is included, it is stripped. |  | MinLength: 1 <br />Required: \{\} <br /> |
| `deploymentName` _string_ | The name of the Azure OpenAI model deployment to use.<br />For more information, see the [Azure OpenAI model docs](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models). |  | MinLength: 1 <br />Required: \{\} <br /> |
| `apiVersion` _string_ | The version of the Azure OpenAI API to use.<br />For more information, see the [Azure OpenAI API version reference](https://learn.microsoft.com/en-us/azure/ai-services/openai/reference#api-specs). |  | MinLength: 1 <br />Required: \{\} <br /> |




#### Backend







_Appears in:_
- [BackendList](#backendlist)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `apiVersion` _string_ | `gateway.kgateway.dev/v1alpha1` | | |
| `kind` _string_ | `Backend` | | |
| `kind` _string_ | Kind is a string value representing the REST resource this object represents.<br />Servers may infer this from the endpoint the client submits requests to.<br />Cannot be updated.<br />In CamelCase.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds |  |  |
| `apiVersion` _string_ | APIVersion defines the versioned schema of this representation of an object.<br />Servers should convert recognized schemas to the latest internal value, and<br />may reject unrecognized values.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources |  |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |  |  |
| `spec` _[BackendSpec](#backendspec)_ |  |  |  |
| `status` _[BackendStatus](#backendstatus)_ |  |  |  |




#### BackendList









| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `apiVersion` _string_ | `gateway.kgateway.dev/v1alpha1` | | |
| `kind` _string_ | `BackendList` | | |
| `kind` _string_ | Kind is a string value representing the REST resource this object represents.<br />Servers may infer this from the endpoint the client submits requests to.<br />Cannot be updated.<br />In CamelCase.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds |  |  |
| `apiVersion` _string_ | APIVersion defines the versioned schema of this representation of an object.<br />Servers should convert recognized schemas to the latest internal value, and<br />may reject unrecognized values.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources |  |  |
| `metadata` _[ListMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#listmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |  |  |
| `items` _[Backend](#backend) array_ |  |  |  |




#### BackendSpec



BackendSpec defines the desired state of Backend.



_Appears in:_
- [Backend](#backend)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `type` _[BackendType](#backendtype)_ | Type indicates the type of the backend to be used. |  | Enum: [ai aws static] <br />Required: \{\} <br /> |
| `ai` _[AIBackend](#aibackend)_ | AI is the AI backend configuration. |  | MaxProperties: 1 <br />MinProperties: 1 <br /> |
| `aws` _[AwsBackend](#awsbackend)_ | Aws is the AWS backend configuration. |  |  |
| `static` _[StaticBackend](#staticbackend)_ | Static is the static backend configuration. |  |  |




#### BackendStatus



BackendStatus defines the observed state of Backend.



_Appears in:_
- [Backend](#backend)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `conditions` _[Condition](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#condition-v1-meta) array_ | Conditions is the list of conditions for the backend. |  | MaxItems: 8 <br /> |




#### BackendType

_Underlying type:_ _string_

BackendType indicates the type of the backend.



_Appears in:_
- [BackendSpec](#backendspec)

| Field | Description |
| --- | --- |
| `ai` | BackendTypeAI is the type for AI backends.<br /> |
| `aws` | BackendTypeAWS is the type for AWS backends.<br /> |
| `static` | BackendTypeStatic is the type for static backends.<br /> |




#### BuiltIn

_Underlying type:_ _string_

BuiltIn regex patterns for specific types of strings in prompts.
For example, if you specify `CREDIT_CARD`, any credit card numbers
in the request or response are matched.

_Validation:_
- Enum: [SSN CREDIT_CARD PHONE_NUMBER EMAIL]

_Appears in:_
- [Regex](#regex)

| Field | Description |
| --- | --- |
| `SSN` | Default regex matching for Social Security numbers.<br /> |
| `CREDIT_CARD` | Default regex matching for credit card numbers.<br /> |
| `PHONE_NUMBER` | Default regex matching for phone numbers.<br /> |
| `EMAIL` | Default regex matching for email addresses.<br /> |




#### CELFilter



CELFilter filters requests based on Common Expression Language (CEL).



_Appears in:_
- [FilterType](#filtertype)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `match` _string_ | The CEL expressions to evaluate. AccessLogs are only emitted when the CEL expressions evaluates to true.<br />see: https://www.envoyproxy.io/docs/envoy/v1.33.0/xds/type/v3/cel.proto.html#common-expression-language-cel-proto |  |  |




#### ComparisonFilter

_Underlying type:_ _[struct{Op Op "json:\"op,omitempty\""; Value uint32 "json:\"value,omitempty\""}](#struct{op-op-"json:\"op,omitempty\"";-value-uint32-"json:\"value,omitempty\""})_

ComparisonFilter represents a filter based on a comparison.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-comparisonfilter



_Appears in:_
- [DurationFilter](#durationfilter)
- [StatusCodeFilter](#statuscodefilter)





#### CustomResponse



CustomResponse configures a response to return to the client if request content
is matched against a regex pattern and the action is `REJECT`.



_Appears in:_
- [PromptguardRequest](#promptguardrequest)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `message` _string_ | A custom response message to return to the client. If not specified, defaults to<br />"The request was rejected due to inappropriate content". | The request was rejected due to inappropriate content |  |
| `statusCode` _integer_ | The status code to return to the client. Defaults to 403. | 403 | Maximum: 599 <br />Minimum: 200 <br /> |






#### DurationFilter

_Underlying type:_ _[ComparisonFilter](#comparisonfilter)_

DurationFilter filters based on request duration.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-durationfilter



_Appears in:_
- [FilterType](#filtertype)





#### FieldDefault



FieldDefault provides default values for specific fields in the JSON request body sent to the LLM provider.
These defaults are merged with the user-provided request to ensure missing fields are populated.


User input fields here refer to the fields in the JSON request body that a client sends when making a request to the LLM provider.
Defaults set here do _not_ override those user-provided values unless you explicitly set `override` to `true`.


Example: Setting a default system field for Anthropic, which does not support system role messages:
```yaml
defaults:
  - field: "system"
    value: "answer all questions in French"


```


Example: Setting a default temperature and overriding `max_tokens`:
```yaml
defaults:
  - field: "temperature"
    value: "0.5"
  - field: "max_tokens"
    value: "100"
    override: true


```


Example: Overriding a custom list field:
```yaml
defaults:
  - field: "custom_list"
    value: "[a,b,c]"


```


Note: The `field` values correspond to keys in the JSON request body, not fields in this CRD.



_Appears in:_
- [AIRoutePolicy](#airoutepolicy)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `field` _string_ | The name of the field. |  | MinLength: 1 <br />Required: \{\} <br /> |
| `value` _string_ | The field default value, which can be any JSON Data Type. |  | MinLength: 1 <br />Required: \{\} <br /> |
| `override` _boolean_ | Whether to override the field's value if it already exists.<br />Defaults to false. | false |  |




#### FileSink



FileSink represents the file sink configuration for access logs.



_Appears in:_
- [AccessLog](#accesslog)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `path` _string_ | the file path to which the file access logging service will sink |  | Required: \{\} <br /> |
| `stringFormat` _string_ | the format string by which envoy will format the log lines<br />https://www.envoyproxy.io/docs/envoy/v1.33.0/configuration/observability/access_log/usage#format-strings |  |  |
| `jsonFormat` _[RawExtension](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#rawextension-runtime-pkg)_ | the format object by which to envoy will emit the logs in a structured way.<br />https://www.envoyproxy.io/docs/envoy/v1.33.0/configuration/observability/access_log/usage#format-dictionaries |  |  |




#### FilterType



FilterType represents the type of filter to apply (only one of these should be set).
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#envoy-v3-api-msg-config-accesslog-v3-accesslogfilter

_Validation:_
- MaxProperties: 1
- MinProperties: 1

_Appears in:_
- [AccessLogFilter](#accesslogfilter)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `statusCodeFilter` _[StatusCodeFilter](#statuscodefilter)_ |  |  |  |
| `durationFilter` _[DurationFilter](#durationfilter)_ |  |  |  |
| `notHealthCheckFilter` _boolean_ | Filters for requests that are not health check requests.<br />Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-nothealthcheckfilter |  |  |
| `traceableFilter` _boolean_ | Filters for requests that are traceable.<br />Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-traceablefilter |  |  |
| `headerFilter` _[HeaderFilter](#headerfilter)_ |  |  |  |
| `responseFlagFilter` _[ResponseFlagFilter](#responseflagfilter)_ |  |  |  |
| `grpcStatusFilter` _[GrpcStatusFilter](#grpcstatusfilter)_ |  |  |  |
| `celFilter` _[CELFilter](#celfilter)_ |  |  |  |




#### GeminiConfig



GeminiConfig settings for the [Gemini](https://ai.google.dev/gemini-api/docs) LLM provider.



_Appears in:_
- [SupportedLLMProvider](#supportedllmprovider)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `authToken` _[SingleAuthToken](#singleauthtoken)_ | The authorization token that the AI gateway uses to access the Gemini API.<br />This token is automatically sent in the `key` query parameter of the request. |  | Required: \{\} <br /> |
| `model` _string_ | The Gemini model to use.<br />For more information, see the [Gemini models docs](https://ai.google.dev/gemini-api/docs/models/gemini). |  | Required: \{\} <br /> |
| `apiVersion` _string_ | The version of the Gemini API to use.<br />For more information, see the [Gemini API version docs](https://ai.google.dev/gemini-api/docs/api-versions). |  | Required: \{\} <br /> |




#### GrpcService



GrpcService represents the gRPC service configuration for access logs.



_Appears in:_
- [AccessLog](#accesslog)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `logName` _string_ | name of log stream |  | Required: \{\} <br /> |
| `backendRef` _[BackendRef](#backendref)_ | The backend gRPC service. Can be any type of supported backed (Kubernetes Service, kgateway Backend, etc..) |  | Required: \{\} <br /> |
| `additionalRequestHeadersToLog` _string array_ | Additional request headers to log in the access log |  |  |
| `additionalResponseHeadersToLog` _string array_ | Additional response headers to log in the access log |  |  |
| `additionalResponseTrailersToLog` _string array_ | Additional response trailers to log in the access log |  |  |






#### GrpcStatusFilter



GrpcStatusFilter filters gRPC requests based on their response status.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#enum-config-accesslog-v3-grpcstatusfilter-status



_Appears in:_
- [FilterType](#filtertype)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `statuses` _[GrpcStatus](#grpcstatus) array_ |  |  | Enum: [OK CANCELED UNKNOWN INVALID_ARGUMENT DEADLINE_EXCEEDED NOT_FOUND ALREADY_EXISTS PERMISSION_DENIED RESOURCE_EXHAUSTED FAILED_PRECONDITION ABORTED OUT_OF_RANGE UNIMPLEMENTED INTERNAL UNAVAILABLE DATA_LOSS UNAUTHENTICATED] <br />MinItems: 1 <br /> |
| `exclude` _boolean_ |  |  |  |




#### HTTPListenerPolicy







_Appears in:_
- [HTTPListenerPolicyList](#httplistenerpolicylist)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `apiVersion` _string_ | `gateway.kgateway.dev/v1alpha1` | | |
| `kind` _string_ | `HTTPListenerPolicy` | | |
| `kind` _string_ | Kind is a string value representing the REST resource this object represents.<br />Servers may infer this from the endpoint the client submits requests to.<br />Cannot be updated.<br />In CamelCase.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds |  |  |
| `apiVersion` _string_ | APIVersion defines the versioned schema of this representation of an object.<br />Servers should convert recognized schemas to the latest internal value, and<br />may reject unrecognized values.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources |  |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |  |  |
| `spec` _[HTTPListenerPolicySpec](#httplistenerpolicyspec)_ |  |  |  |
| `status` _[PolicyStatus](#policystatus)_ |  |  |  |




#### HTTPListenerPolicyList









| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `apiVersion` _string_ | `gateway.kgateway.dev/v1alpha1` | | |
| `kind` _string_ | `HTTPListenerPolicyList` | | |
| `kind` _string_ | Kind is a string value representing the REST resource this object represents.<br />Servers may infer this from the endpoint the client submits requests to.<br />Cannot be updated.<br />In CamelCase.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds |  |  |
| `apiVersion` _string_ | APIVersion defines the versioned schema of this representation of an object.<br />Servers should convert recognized schemas to the latest internal value, and<br />may reject unrecognized values.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources |  |  |
| `metadata` _[ListMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#listmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |  |  |
| `items` _[HTTPListenerPolicy](#httplistenerpolicy) array_ |  |  |  |




#### HTTPListenerPolicySpec







_Appears in:_
- [HTTPListenerPolicy](#httplistenerpolicy)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `targetRef` _[LocalPolicyTargetReference](#localpolicytargetreference)_ |  |  |  |
| `compress` _boolean_ |  |  |  |
| `accessLog` _[AccessLog](#accesslog) array_ | AccessLoggingConfig contains various settings for Envoy's access logging service.<br />See here for more information: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto |  |  |




#### HeaderFilter



HeaderFilter filters requests based on headers.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-headerfilter



_Appears in:_
- [FilterType](#filtertype)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `header` _[HTTPHeaderMatch](#httpheadermatch)_ |  |  | Required: \{\} <br /> |




#### Host



Host is a host and port pair.



_Appears in:_
- [LLMProvider](#llmprovider)
- [StaticBackend](#staticbackend)
- [Webhook](#webhook)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `host` _string_ | Host is the host name. |  | MaxLength: 253 <br />MinLength: 1 <br /> |
| `port` _[PortNumber](#portnumber)_ | Port is the port number. |  |  |




#### LLMProvider







_Appears in:_
- [AIBackend](#aibackend)
- [Priority](#priority)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `provider` _[SupportedLLMProvider](#supportedllmprovider)_ | The LLM provider type to configure. |  | MaxProperties: 1 <br />MinProperties: 1 <br /> |
| `hostOverride` _[Host](#host)_ | Send requests to a custom host and port, such as to proxy the request,<br />or to use a different backend that is API-compliant with the Backend version. |  |  |




#### ListenerPolicy







_Appears in:_
- [ListenerPolicyList](#listenerpolicylist)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `apiVersion` _string_ | `gateway.kgateway.dev/v1alpha1` | | |
| `kind` _string_ | `ListenerPolicy` | | |
| `kind` _string_ | Kind is a string value representing the REST resource this object represents.<br />Servers may infer this from the endpoint the client submits requests to.<br />Cannot be updated.<br />In CamelCase.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds |  |  |
| `apiVersion` _string_ | APIVersion defines the versioned schema of this representation of an object.<br />Servers should convert recognized schemas to the latest internal value, and<br />may reject unrecognized values.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources |  |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |  |  |
| `spec` _[ListenerPolicySpec](#listenerpolicyspec)_ |  |  |  |
| `status` _[PolicyStatus](#policystatus)_ |  |  |  |




#### ListenerPolicySpec







_Appears in:_
- [ListenerPolicy](#listenerpolicy)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `targetRef` _[LocalPolicyTargetReference](#localpolicytargetreference)_ |  |  |  |
| `perConnectionBufferLimitBytes` _integer_ |  |  |  |




#### LocalPolicyTargetReference



not sure why i need to copy this; codegen fails if i dont



_Appears in:_
- [HTTPListenerPolicySpec](#httplistenerpolicyspec)
- [ListenerPolicySpec](#listenerpolicyspec)
- [RoutePolicySpec](#routepolicyspec)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `group` _[Group](#group)_ | Group is the group of the target resource. |  |  |
| `kind` _[Kind](#kind)_ | Kind is kind of the target resource. |  |  |
| `name` _[ObjectName](#objectname)_ | Name is the name of the target resource. |  |  |




#### Message



An entry for a message to prepend or append to each prompt.



_Appears in:_
- [AIPromptEnrichment](#aipromptenrichment)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `role` _string_ | Role of the message. The available roles depend on the backend<br />LLM provider model, such as `SYSTEM` or `USER` in the OpenAI API. |  |  |
| `content` _string_ | String content of the message. |  |  |




#### Moderation



Moderation configures an external moderation model endpoint. This endpoint evaluates
request prompt data against predefined content rules to determine if the content
adheres to those rules.


Any requests routed through the AI Gateway are processed by the specified
moderation model. If the model identifies the content as harmful based on its rules,
the request is automatically rejected.


You can configure a moderation endpoint either as a standalone prompt guard setting
or alongside other request and response guard settings.



_Appears in:_
- [PromptguardRequest](#promptguardrequest)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `openAIModeration` _[OpenAIConfig](#openaiconfig)_ | Pass prompt data through an external moderation model endpoint,<br />which compares the request prompt input to predefined content rules.<br />Configure an OpenAI moderation endpoint. |  |  |




#### MultiPoolConfig



MultiPoolConfig configures the backends for multiple hosts or models from the same provider in one Backend resource.
This method can be useful for creating one logical endpoint that is backed
by multiple hosts or models.


In the `priorities` section, the order of `pool` entries defines the priority of the backend endpoints.
The `pool` entries can either define a list of backends or a single backend.
Note: Only two levels of nesting are permitted. Any nested entries after the second level are ignored.


```yaml
multi:


	priorities:
	- pool:
	  - azureOpenai:
	      deploymentName: gpt-4o-mini
	      apiVersion: 2024-02-15-preview
	      endpoint: ai-gateway.openai.azure.com
	      authToken:
	        secretRef:
	          name: azure-secret
	          namespace: kgateway-system
	- pool:
	  - azureOpenai:
	      deploymentName: gpt-4o-mini-2
	      apiVersion: 2024-02-15-preview
	      endpoint: ai-gateway-2.openai.azure.com
	      authToken:
	        secretRef:
	          name: azure-secret-2
	          namespace: kgateway-system


```



_Appears in:_
- [AIBackend](#aibackend)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `priorities` _[Priority](#priority) array_ | The priority list of backend pools. Each entry represents a set of LLM provider backends.<br />The order defines the priority of the backend endpoints. |  | MaxItems: 20 <br />MinItems: 1 <br />Required: \{\} <br /> |






#### OpenAIConfig



OpenAIConfig settings for the [OpenAI](https://platform.openai.com/docs/api-reference/streaming) LLM provider.



_Appears in:_
- [Moderation](#moderation)
- [SupportedLLMProvider](#supportedllmprovider)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `authToken` _[SingleAuthToken](#singleauthtoken)_ | The authorization token that the AI gateway uses to access the OpenAI API.<br />This token is automatically sent in the `Authorization` header of the<br />request and prefixed with `Bearer`. |  | Required: \{\} <br /> |
| `model` _string_ | Optional: Override the model name, such as `gpt-4o-mini`.<br />If unset, the model name is taken from the request.<br />This setting can be useful when setting up model failover within the same LLM provider. |  |  |




#### PolicyAncestorStatus







_Appears in:_
- [PolicyStatus](#policystatus)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `ancestorRef` _[ParentReference](#parentreference)_ | AncestorRef corresponds with a ParentRef in the spec that this<br />PolicyAncestorStatus struct describes the status of. |  |  |
| `controllerName` _string_ | ControllerName is a domain/path string that indicates the name of the<br />controller that wrote this status. This corresponds with the<br />controllerName field on GatewayClass.<br /><br />Example: "example.net/gateway-controller".<br /><br />The format of this field is DOMAIN "/" PATH, where DOMAIN and PATH are<br />valid Kubernetes names<br />(https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names).<br /><br />Controllers MUST populate this field when writing status. Controllers should ensure that<br />entries to status populated with their ControllerName are cleaned up when they are no<br />longer necessary. |  |  |
| `conditions` _[Condition](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#condition-v1-meta) array_ | Conditions describes the status of the Policy with respect to the given Ancestor. |  | MaxItems: 8 <br />MinItems: 1 <br /> |




#### PolicyStatus







_Appears in:_
- [HTTPListenerPolicy](#httplistenerpolicy)
- [ListenerPolicy](#listenerpolicy)
- [RoutePolicy](#routepolicy)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `conditions` _[Condition](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#condition-v1-meta) array_ |  |  | MaxItems: 8 <br /> |
| `ancestors` _[PolicyAncestorStatus](#policyancestorstatus) array_ |  |  | MaxItems: 16 <br /> |




#### Priority



Priority configures the priority of the backend endpoints.



_Appears in:_
- [MultiPoolConfig](#multipoolconfig)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `pool` _[LLMProvider](#llmprovider) array_ | A list of LLM provider backends within a single endpoint pool entry. |  | MaxItems: 20 <br />MinItems: 1 <br /> |




#### PromptguardRequest



PromptguardRequest defines the prompt guards to apply to requests sent by the client.
Multiple prompt guard configurations can be set, and they will be executed in the following order:
webhook → regex → moderation for requests, where each step can reject the request and stop further processing.



_Appears in:_
- [AIPromptGuard](#aipromptguard)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `customResponse` _[CustomResponse](#customresponse)_ | A custom response message to return to the client. If not specified, defaults to<br />"The request was rejected due to inappropriate content". |  |  |
| `regex` _[Regex](#regex)_ | Regular expression (regex) matching for prompt guards and data masking. |  |  |
| `webhook` _[Webhook](#webhook)_ | Configure a webhook to forward requests to for prompt guarding. |  |  |
| `moderation` _[Moderation](#moderation)_ | Pass prompt data through an external moderation model endpoint,<br />which compares the request prompt input to predefined content rules. |  |  |




#### PromptguardResponse



PromptguardResponse configures the response that the prompt guard applies to responses returned by the LLM provider.
Both webhook and regex can be set, they will be executed in the following order: webhook → regex, where each step
can reject the request and stop further processing.



_Appears in:_
- [AIPromptGuard](#aipromptguard)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `regex` _[Regex](#regex)_ | Regular expression (regex) matching for prompt guards and data masking. |  |  |
| `webhook` _[Webhook](#webhook)_ | Configure a webhook to forward responses to for prompt guarding. |  |  |




#### Publisher

_Underlying type:_ _string_

Publisher configures the type of publisher model to use for VertexAI. Currently, only Google is supported.



_Appears in:_
- [VertexAIConfig](#vertexaiconfig)

| Field | Description |
| --- | --- |
| `GOOGLE` |  |




#### Regex



Regex configures the regular expression (regex) matching for prompt guards and data masking.



_Appears in:_
- [PromptguardRequest](#promptguardrequest)
- [PromptguardResponse](#promptguardresponse)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `matches` _[RegexMatch](#regexmatch) array_ | A list of regex patterns to match against the request or response.<br />Matches and built-ins are additive. |  |  |
| `builtins` _[BuiltIn](#builtin) array_ | A list of built-in regex patterns to match against the request or response.<br />Matches and built-ins are additive. |  | Enum: [SSN CREDIT_CARD PHONE_NUMBER EMAIL] <br /> |
| `action` _[Action](#action)_ | The action to take if a regex pattern is matched in a request or response.<br />This setting applies only to request matches. PromptguardResponse matches are always masked by default.<br />Defaults to `MASK`. | MASK |  |




#### RegexMatch



RegexMatch configures the regular expression (regex) matching for prompt guards and data masking.



_Appears in:_
- [Regex](#regex)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `pattern` _string_ | The regex pattern to match against the request or response. |  |  |
| `name` _string_ | An optional name for this match, which can be used for debugging purposes. |  |  |




#### ResponseFlagFilter



ResponseFlagFilter filters based on response flags.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-responseflagfilter



_Appears in:_
- [FilterType](#filtertype)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `flags` _string array_ |  |  | MinItems: 1 <br /> |




#### RoutePolicy







_Appears in:_
- [RoutePolicyList](#routepolicylist)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `apiVersion` _string_ | `gateway.kgateway.dev/v1alpha1` | | |
| `kind` _string_ | `RoutePolicy` | | |
| `kind` _string_ | Kind is a string value representing the REST resource this object represents.<br />Servers may infer this from the endpoint the client submits requests to.<br />Cannot be updated.<br />In CamelCase.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds |  |  |
| `apiVersion` _string_ | APIVersion defines the versioned schema of this representation of an object.<br />Servers should convert recognized schemas to the latest internal value, and<br />may reject unrecognized values.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources |  |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |  |  |
| `spec` _[RoutePolicySpec](#routepolicyspec)_ |  |  |  |
| `status` _[PolicyStatus](#policystatus)_ |  |  |  |




#### RoutePolicyList









| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `apiVersion` _string_ | `gateway.kgateway.dev/v1alpha1` | | |
| `kind` _string_ | `RoutePolicyList` | | |
| `kind` _string_ | Kind is a string value representing the REST resource this object represents.<br />Servers may infer this from the endpoint the client submits requests to.<br />Cannot be updated.<br />In CamelCase.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds |  |  |
| `apiVersion` _string_ | APIVersion defines the versioned schema of this representation of an object.<br />Servers should convert recognized schemas to the latest internal value, and<br />may reject unrecognized values.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources |  |  |
| `metadata` _[ListMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#listmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |  |  |
| `items` _[RoutePolicy](#routepolicy) array_ |  |  |  |




#### RoutePolicySpec







_Appears in:_
- [RoutePolicy](#routepolicy)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `targetRef` _[LocalPolicyTargetReference](#localpolicytargetreference)_ |  |  |  |
| `timeout` _integer_ |  |  | Minimum: 1 <br /> |
| `ai` _[AIRoutePolicy](#airoutepolicy)_ |  |  |  |




#### RouteType

_Underlying type:_ _string_

RouteType is the type of route to the LLM provider API.



_Appears in:_
- [AIRoutePolicy](#airoutepolicy)

| Field | Description |
| --- | --- |
| `CHAT` | The LLM generates the full response before responding to a client.<br /> |
| `CHAT_STREAMING` | Stream responses to a client, which allows the LLM to stream out tokens as they are generated.<br /> |




#### SingleAuthToken



SingleAuthToken configures the authorization token that the AI gateway uses to access the LLM provider API.
This token is automatically sent in a request header, depending on the LLM provider.



_Appears in:_
- [AnthropicConfig](#anthropicconfig)
- [AzureOpenAIConfig](#azureopenaiconfig)
- [GeminiConfig](#geminiconfig)
- [OpenAIConfig](#openaiconfig)
- [VertexAIConfig](#vertexaiconfig)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `kind` _[SingleAuthTokenKind](#singleauthtokenkind)_ | Kind specifies which type of authorization token is being used.<br />Must be one of: "Inline", "SecretRef", "Passthrough". |  | Enum: [Inline SecretRef Passthrough] <br /> |
| `inline` _string_ | Provide the token directly in the configuration for the Backend.<br />This option is the least secure. Only use this option for quick tests such as trying out AI Gateway. |  |  |
| `secretRef` _[LocalObjectReference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#localobjectreference-v1-core)_ | Store the API key in a Kubernetes secret in the same namespace as the Backend.<br />Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,<br />because the API key is encoded and you can restrict access to secrets through RBAC rules.<br />You might use this option in proofs of concept, controlled development and staging environments,<br />or well-controlled prod environments that use secrets. |  |  |




#### SingleAuthTokenKind

_Underlying type:_ _string_





_Appears in:_
- [SingleAuthToken](#singleauthtoken)

| Field | Description |
| --- | --- |
| `Inline` | Inline provides the token directly in the configuration for the Backend.<br /> |
| `SecretRef` | SecretRef provides the token directly in the configuration for the Backend.<br /> |
| `Passthrough` | Passthrough the existing token. This token can either<br />come directly from the client, or be generated by an OIDC flow<br />early in the request lifecycle. This option is useful for<br />backends which have federated identity setup and can re-use<br />the token from the client.<br />Currently, this token must exist in the `Authorization` header.<br /> |




#### StaticBackend



StaticBackend is the static backend configuration.



_Appears in:_
- [BackendSpec](#backendspec)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `hosts` _[Host](#host) array_ | Hosts is the list of hosts. |  | MinItems: 1 <br /> |




#### StatusCodeFilter

_Underlying type:_ _[ComparisonFilter](#comparisonfilter)_

StatusCodeFilter filters based on HTTP status code.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#envoy-v3-api-msg-config-accesslog-v3-statuscodefilter



_Appears in:_
- [FilterType](#filtertype)





#### SupportedLLMProvider



SupportedLLMProvider configures the AI gateway to use a single LLM provider backend.

_Validation:_
- MaxProperties: 1
- MinProperties: 1

_Appears in:_
- [LLMProvider](#llmprovider)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `openai` _[OpenAIConfig](#openaiconfig)_ |  |  |  |
| `azureopenai` _[AzureOpenAIConfig](#azureopenaiconfig)_ |  |  |  |
| `anthropic` _[AnthropicConfig](#anthropicconfig)_ |  |  |  |
| `gemini` _[GeminiConfig](#geminiconfig)_ |  |  |  |
| `vertexai` _[VertexAIConfig](#vertexaiconfig)_ |  |  |  |




#### VertexAIConfig



VertexAIConfig settings for the [Vertex AI](https://cloud.google.com/vertex-ai/docs) LLM provider.
To find the values for the project ID, project location, and publisher, you can check the fields of an API request, such as
`https://{LOCATION}-aiplatform.googleapis.com/{VERSION}/projects/{PROJECT_ID}/locations/{LOCATION}/publishers/{PROVIDER}/<model-path>`.



_Appears in:_
- [SupportedLLMProvider](#supportedllmprovider)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `authToken` _[SingleAuthToken](#singleauthtoken)_ | The authorization token that the AI gateway uses to access the Vertex AI API.<br />This token is automatically sent in the `key` header of the request. |  | Required: \{\} <br /> |
| `model` _string_ | The Vertex AI model to use.<br />For more information, see the [Vertex AI model docs](https://cloud.google.com/vertex-ai/generative-ai/docs/learn/models). |  | MinLength: 1 <br />Required: \{\} <br /> |
| `apiVersion` _string_ | The version of the Vertex AI API to use.<br />For more information, see the [Vertex AI API reference](https://cloud.google.com/vertex-ai/docs/reference#versions). |  | MinLength: 1 <br />Required: \{\} <br /> |
| `projectId` _string_ | The ID of the Google Cloud Project that you use for the Vertex AI. |  | MinLength: 1 <br />Required: \{\} <br /> |
| `location` _string_ | The location of the Google Cloud Project that you use for the Vertex AI. |  | MinLength: 1 <br />Required: \{\} <br /> |
| `modelPath` _string_ | Optional: The model path to route to. Defaults to the Gemini model path, `generateContent`. |  |  |
| `publisher` _[Publisher](#publisher)_ | The type of publisher model to use. Currently, only Google is supported. |  | Enum: [GOOGLE] <br /> |




#### Webhook



Webhook configures a webhook to forward requests or responses to for prompt guarding.



_Appears in:_
- [PromptguardRequest](#promptguardrequest)
- [PromptguardResponse](#promptguardresponse)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `host` _[Host](#host)_ | Host to send the traffic to. |  | Required: \{\} <br /> |
| `forwardHeaders` _[HTTPHeaderMatch](#httpheadermatch) array_ | ForwardHeaders define headers to forward with the request to the webhook. |  |  |





