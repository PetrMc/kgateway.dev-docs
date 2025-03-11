---
title: DirectResponse
weight: 40
description: API reference for DirectResponse
---

# DirectResponse API Reference

#### DirectResponse



DirectResponse contains configuration for defining direct response routes.



_Appears in:_
- [DirectResponseList](#directresponselist)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `apiVersion` _string_ | `gateway.kgateway.dev/v1alpha1` | | |
| `kind` _string_ | `DirectResponse` | | |
| `kind` _string_ | Kind is a string value representing the REST resource this object represents.<br />Servers may infer this from the endpoint the client submits requests to.<br />Cannot be updated.<br />In CamelCase.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds |  |  |
| `apiVersion` _string_ | APIVersion defines the versioned schema of this representation of an object.<br />Servers should convert recognized schemas to the latest internal value, and<br />may reject unrecognized values.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources |  |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |  |  |
| `spec` _[DirectResponseSpec](#directresponsespec)_ |  |  |  |
| `status` _[DirectResponseStatus](#directresponsestatus)_ |  |  |  |




#### DirectResponseList









| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `apiVersion` _string_ | `gateway.kgateway.dev/v1alpha1` | | |
| `kind` _string_ | `DirectResponseList` | | |
| `kind` _string_ | Kind is a string value representing the REST resource this object represents.<br />Servers may infer this from the endpoint the client submits requests to.<br />Cannot be updated.<br />In CamelCase.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds |  |  |
| `apiVersion` _string_ | APIVersion defines the versioned schema of this representation of an object.<br />Servers should convert recognized schemas to the latest internal value, and<br />may reject unrecognized values.<br />More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources |  |  |
| `metadata` _[ListMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.32/#listmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |  |  |
| `items` _[DirectResponse](#directresponse) array_ |  |  |  |




#### DirectResponseSpec



DirectResponseSpec describes the desired state of a DirectResponse.



_Appears in:_
- [DirectResponse](#directresponse)

| Field | Description | Default | Validation |
| --- | --- | --- | --- |
| `status` _integer_ | StatusCode defines the HTTP status code to return for this route. |  | Maximum: 599 <br />Minimum: 200 <br />Required: \{\} <br /> |
| `body` _string_ | Body defines the content to be returned in the HTTP response body.<br />The maximum length of the body is restricted to prevent excessively large responses. |  | MaxLength: 4096 <br />Optional: \{\} <br /> |




#### DirectResponseStatus



DirectResponseStatus defines the observed state of a DirectResponse.



_Appears in:_
- [DirectResponse](#directresponse)





