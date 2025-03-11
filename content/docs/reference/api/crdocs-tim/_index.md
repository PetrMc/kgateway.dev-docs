# API Reference

Packages:

- [gateway.kgateway.dev/v1alpha1](#gatewaykgatewaydevv1alpha1)

# gateway.kgateway.dev/v1alpha1

Resource Types:

- [Backend](#backend)

- [DirectResponse](#directresponse)

- [GatewayParameters](#gatewayparameters)

- [HTTPListenerPolicy](#httplistenerpolicy)

- [ListenerPolicy](#listenerpolicy)

- [RoutePolicy](#routepolicy)




## Backend
<sup><sup>[↩ Parent](#gatewaykgatewaydevv1alpha1 )</sup></sup>








<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
      <td><b>apiVersion</b></td>
      <td>string</td>
      <td>gateway.kgateway.dev/v1alpha1</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b>kind</b></td>
      <td>string</td>
      <td>Backend</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b><a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#objectmeta-v1-meta">metadata</a></b></td>
      <td>object</td>
      <td>Refer to the Kubernetes API documentation for the fields of the `metadata` field.</td>
      <td>true</td>
      </tr><tr>
        <td><b><a href="#backendspec">spec</a></b></td>
        <td>object</td>
        <td>
          BackendSpec defines the desired state of Backend.<br/>
          <br/>
            <i>Validations</i>:<li>!(has(self.ai) && self.type != 'ai'): ai backend must be nil if the type is not 'ai'</li><li>!(!has(self.ai) && self.type == 'ai'): ai backend must be specified when type is 'ai'</li><li>!(has(self.aws) && self.type != 'aws'): aws backend must be nil if the type is not 'aws'</li><li>!(!has(self.aws) && self.type == 'aws'): aws backend must be specified when type is 'aws'</li><li>!(has(self.static) && self.type != 'static'): static backend must be nil if the type is not 'static'</li><li>!(!has(self.static) && self.type == 'static'): static backend must be specified when type is 'static'</li>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendstatus">status</a></b></td>
        <td>object</td>
        <td>
          BackendStatus defines the observed state of Backend.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec
<sup><sup>[↩ Parent](#backend)</sup></sup>



BackendSpec defines the desired state of Backend.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>enum</td>
        <td>
          Type indicates the type of the backend to be used.<br/>
          <br/>
            <i>Enum</i>: ai, aws, static<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#backendspecai">ai</a></b></td>
        <td>object</td>
        <td>
          AI is the AI backend configuration.<br/>
          <br/>
            <i>Validations</i>:<li>(has(self.llm) && !has(self.multipool)) || (!has(self.llm) && has(self.multipool)): There must one and only one LLM or MultiPool can be set</li>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaws">aws</a></b></td>
        <td>object</td>
        <td>
          Aws is the AWS backend configuration.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecstatic">static</a></b></td>
        <td>object</td>
        <td>
          Static is the static backend configuration.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai
<sup><sup>[↩ Parent](#backendspec)</sup></sup>



AI is the AI backend configuration.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendspecaillm">llm</a></b></td>
        <td>object</td>
        <td>
          The LLM configures the AI gateway to use a single LLM provider backend.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipool">multipool</a></b></td>
        <td>object</td>
        <td>
          The MultiPool configures the backends for multiple hosts or models from the same provider in one Backend resource.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm
<sup><sup>[↩ Parent](#backendspecai)</sup></sup>



The LLM configures the AI gateway to use a single LLM provider backend.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendspecaillmprovider">provider</a></b></td>
        <td>object</td>
        <td>
          The LLM provider type to configure.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmhostoverride">hostOverride</a></b></td>
        <td>object</td>
        <td>
          Send requests to a custom host and port, such as to proxy the request,
or to use a different backend that is API-compliant with the Backend version.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider
<sup><sup>[↩ Parent](#backendspecaillm)</sup></sup>



The LLM provider type to configure.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendspecaillmprovideranthropic">anthropic</a></b></td>
        <td>object</td>
        <td>
          AnthropicConfig settings for the [Anthropic](https://docs.anthropic.com/en/release-notes/api) LLM provider.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmproviderazureopenai">azureopenai</a></b></td>
        <td>object</td>
        <td>
          AzureOpenAIConfig settings for the [Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/) LLM provider.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmprovidergemini">gemini</a></b></td>
        <td>object</td>
        <td>
          GeminiConfig settings for the [Gemini](https://ai.google.dev/gemini-api/docs) LLM provider.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmprovideropenai">openai</a></b></td>
        <td>object</td>
        <td>
          OpenAIConfig settings for the [OpenAI](https://platform.openai.com/docs/api-reference/streaming) LLM provider.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmprovidervertexai">vertexai</a></b></td>
        <td>object</td>
        <td>
          VertexAIConfig settings for the [Vertex AI](https://cloud.google.com/vertex-ai/docs) LLM provider.
To find the values for the project ID, project location, and publisher, you can check the fields of an API request, such as
`https://{LOCATION}-aiplatform.googleapis.com/{VERSION}/projects/{PROJECT_ID}/locations/{LOCATION}/publishers/{PROVIDER}/<model-path>`.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.anthropic
<sup><sup>[↩ Parent](#backendspecaillmprovider)</sup></sup>



AnthropicConfig settings for the [Anthropic](https://docs.anthropic.com/en/release-notes/api) LLM provider.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendspecaillmprovideranthropicauthtoken">authToken</a></b></td>
        <td>object</td>
        <td>
          The authorization token that the AI gateway uses to access the Anthropic API.
This token is automatically sent in the `x-api-key` header of the request.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>apiVersion</b></td>
        <td>string</td>
        <td>
          Optional: A version header to pass to the Anthropic API.
For more information, see the [Anthropic API versioning docs](https://docs.anthropic.com/en/api/versioning).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>model</b></td>
        <td>string</td>
        <td>
          Optional: Override the model name.
If unset, the model name is taken from the request.
This setting can be useful when testing model failover scenarios.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.anthropic.authToken
<sup><sup>[↩ Parent](#backendspecaillmprovideranthropic)</sup></sup>



The authorization token that the AI gateway uses to access the Anthropic API.
This token is automatically sent in the `x-api-key` header of the request.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>kind</b></td>
        <td>enum</td>
        <td>
          Kind specifies which type of authorization token is being used.
Must be one of: "Inline", "SecretRef", "Passthrough".<br/>
          <br/>
            <i>Enum</i>: Inline, SecretRef, Passthrough<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>inline</b></td>
        <td>string</td>
        <td>
          Provide the token directly in the configuration for the Backend.
This option is the least secure. Only use this option for quick tests such as trying out AI Gateway.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmprovideranthropicauthtokensecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.anthropic.authToken.secretRef
<sup><sup>[↩ Parent](#backendspecaillmprovideranthropicauthtoken)</sup></sup>



Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.azureopenai
<sup><sup>[↩ Parent](#backendspecaillmprovider)</sup></sup>



AzureOpenAIConfig settings for the [Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/) LLM provider.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>apiVersion</b></td>
        <td>string</td>
        <td>
          The version of the Azure OpenAI API to use.
For more information, see the [Azure OpenAI API version reference](https://learn.microsoft.com/en-us/azure/ai-services/openai/reference#api-specs).<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmproviderazureopenaiauthtoken">authToken</a></b></td>
        <td>object</td>
        <td>
          The authorization token that the AI gateway uses to access the Azure OpenAI API.
This token is automatically sent in the `api-key` header of the request.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>deploymentName</b></td>
        <td>string</td>
        <td>
          The name of the Azure OpenAI model deployment to use.
For more information, see the [Azure OpenAI model docs](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models).<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>endpoint</b></td>
        <td>string</td>
        <td>
          The endpoint for the Azure OpenAI API to use, such as `my-endpoint.openai.azure.com`.
If the scheme is included, it is stripped.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.azureopenai.authToken
<sup><sup>[↩ Parent](#backendspecaillmproviderazureopenai)</sup></sup>



The authorization token that the AI gateway uses to access the Azure OpenAI API.
This token is automatically sent in the `api-key` header of the request.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>kind</b></td>
        <td>enum</td>
        <td>
          Kind specifies which type of authorization token is being used.
Must be one of: "Inline", "SecretRef", "Passthrough".<br/>
          <br/>
            <i>Enum</i>: Inline, SecretRef, Passthrough<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>inline</b></td>
        <td>string</td>
        <td>
          Provide the token directly in the configuration for the Backend.
This option is the least secure. Only use this option for quick tests such as trying out AI Gateway.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmproviderazureopenaiauthtokensecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.azureopenai.authToken.secretRef
<sup><sup>[↩ Parent](#backendspecaillmproviderazureopenaiauthtoken)</sup></sup>



Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.gemini
<sup><sup>[↩ Parent](#backendspecaillmprovider)</sup></sup>



GeminiConfig settings for the [Gemini](https://ai.google.dev/gemini-api/docs) LLM provider.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>apiVersion</b></td>
        <td>string</td>
        <td>
          The version of the Gemini API to use.
For more information, see the [Gemini API version docs](https://ai.google.dev/gemini-api/docs/api-versions).<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmprovidergeminiauthtoken">authToken</a></b></td>
        <td>object</td>
        <td>
          The authorization token that the AI gateway uses to access the Gemini API.
This token is automatically sent in the `key` query parameter of the request.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>model</b></td>
        <td>string</td>
        <td>
          The Gemini model to use.
For more information, see the [Gemini models docs](https://ai.google.dev/gemini-api/docs/models/gemini).<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.gemini.authToken
<sup><sup>[↩ Parent](#backendspecaillmprovidergemini)</sup></sup>



The authorization token that the AI gateway uses to access the Gemini API.
This token is automatically sent in the `key` query parameter of the request.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>kind</b></td>
        <td>enum</td>
        <td>
          Kind specifies which type of authorization token is being used.
Must be one of: "Inline", "SecretRef", "Passthrough".<br/>
          <br/>
            <i>Enum</i>: Inline, SecretRef, Passthrough<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>inline</b></td>
        <td>string</td>
        <td>
          Provide the token directly in the configuration for the Backend.
This option is the least secure. Only use this option for quick tests such as trying out AI Gateway.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmprovidergeminiauthtokensecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.gemini.authToken.secretRef
<sup><sup>[↩ Parent](#backendspecaillmprovidergeminiauthtoken)</sup></sup>



Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.openai
<sup><sup>[↩ Parent](#backendspecaillmprovider)</sup></sup>



OpenAIConfig settings for the [OpenAI](https://platform.openai.com/docs/api-reference/streaming) LLM provider.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendspecaillmprovideropenaiauthtoken">authToken</a></b></td>
        <td>object</td>
        <td>
          The authorization token that the AI gateway uses to access the OpenAI API.
This token is automatically sent in the `Authorization` header of the
request and prefixed with `Bearer`.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>model</b></td>
        <td>string</td>
        <td>
          Optional: Override the model name, such as `gpt-4o-mini`.
If unset, the model name is taken from the request.
This setting can be useful when setting up model failover within the same LLM provider.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.openai.authToken
<sup><sup>[↩ Parent](#backendspecaillmprovideropenai)</sup></sup>



The authorization token that the AI gateway uses to access the OpenAI API.
This token is automatically sent in the `Authorization` header of the
request and prefixed with `Bearer`.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>kind</b></td>
        <td>enum</td>
        <td>
          Kind specifies which type of authorization token is being used.
Must be one of: "Inline", "SecretRef", "Passthrough".<br/>
          <br/>
            <i>Enum</i>: Inline, SecretRef, Passthrough<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>inline</b></td>
        <td>string</td>
        <td>
          Provide the token directly in the configuration for the Backend.
This option is the least secure. Only use this option for quick tests such as trying out AI Gateway.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmprovideropenaiauthtokensecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.openai.authToken.secretRef
<sup><sup>[↩ Parent](#backendspecaillmprovideropenaiauthtoken)</sup></sup>



Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.vertexai
<sup><sup>[↩ Parent](#backendspecaillmprovider)</sup></sup>



VertexAIConfig settings for the [Vertex AI](https://cloud.google.com/vertex-ai/docs) LLM provider.
To find the values for the project ID, project location, and publisher, you can check the fields of an API request, such as
`https://{LOCATION}-aiplatform.googleapis.com/{VERSION}/projects/{PROJECT_ID}/locations/{LOCATION}/publishers/{PROVIDER}/<model-path>`.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>apiVersion</b></td>
        <td>string</td>
        <td>
          The version of the Vertex AI API to use.
For more information, see the [Vertex AI API reference](https://cloud.google.com/vertex-ai/docs/reference#versions).<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmprovidervertexaiauthtoken">authToken</a></b></td>
        <td>object</td>
        <td>
          The authorization token that the AI gateway uses to access the Vertex AI API.
This token is automatically sent in the `key` header of the request.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>location</b></td>
        <td>string</td>
        <td>
          The location of the Google Cloud Project that you use for the Vertex AI.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>model</b></td>
        <td>string</td>
        <td>
          The Vertex AI model to use.
For more information, see the [Vertex AI model docs](https://cloud.google.com/vertex-ai/generative-ai/docs/learn/models).<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>projectId</b></td>
        <td>string</td>
        <td>
          The ID of the Google Cloud Project that you use for the Vertex AI.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>publisher</b></td>
        <td>enum</td>
        <td>
          The type of publisher model to use. Currently, only Google is supported.<br/>
          <br/>
            <i>Enum</i>: GOOGLE<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>modelPath</b></td>
        <td>string</td>
        <td>
          Optional: The model path to route to. Defaults to the Gemini model path, `generateContent`.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.vertexai.authToken
<sup><sup>[↩ Parent](#backendspecaillmprovidervertexai)</sup></sup>



The authorization token that the AI gateway uses to access the Vertex AI API.
This token is automatically sent in the `key` header of the request.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>kind</b></td>
        <td>enum</td>
        <td>
          Kind specifies which type of authorization token is being used.
Must be one of: "Inline", "SecretRef", "Passthrough".<br/>
          <br/>
            <i>Enum</i>: Inline, SecretRef, Passthrough<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>inline</b></td>
        <td>string</td>
        <td>
          Provide the token directly in the configuration for the Backend.
This option is the least secure. Only use this option for quick tests such as trying out AI Gateway.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaillmprovidervertexaiauthtokensecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.provider.vertexai.authToken.secretRef
<sup><sup>[↩ Parent](#backendspecaillmprovidervertexaiauthtoken)</sup></sup>



Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.llm.hostOverride
<sup><sup>[↩ Parent](#backendspecaillm)</sup></sup>



Send requests to a custom host and port, such as to proxy the request,
or to use a different backend that is API-compliant with the Backend version.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Host is the host name.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port is the port number.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 1<br/>
            <i>Maximum</i>: 65535<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool
<sup><sup>[↩ Parent](#backendspecai)</sup></sup>



The MultiPool configures the backends for multiple hosts or models from the same provider in one Backend resource.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindex">priorities</a></b></td>
        <td>[]object</td>
        <td>
          The priority list of backend pools. Each entry represents a set of LLM provider backends.
The order defines the priority of the backend endpoints.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index]
<sup><sup>[↩ Parent](#backendspecaimultipool)</sup></sup>



Priority configures the priority of the backend endpoints.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindex">pool</a></b></td>
        <td>[]object</td>
        <td>
          A list of LLM provider backends within a single endpoint pool entry.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index]
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindex)</sup></sup>





<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovider">provider</a></b></td>
        <td>object</td>
        <td>
          The LLM provider type to configure.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexhostoverride">hostOverride</a></b></td>
        <td>object</td>
        <td>
          Send requests to a custom host and port, such as to proxy the request,
or to use a different backend that is API-compliant with the Backend version.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindex)</sup></sup>



The LLM provider type to configure.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovideranthropic">anthropic</a></b></td>
        <td>object</td>
        <td>
          AnthropicConfig settings for the [Anthropic](https://docs.anthropic.com/en/release-notes/api) LLM provider.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexproviderazureopenai">azureopenai</a></b></td>
        <td>object</td>
        <td>
          AzureOpenAIConfig settings for the [Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/) LLM provider.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovidergemini">gemini</a></b></td>
        <td>object</td>
        <td>
          GeminiConfig settings for the [Gemini](https://ai.google.dev/gemini-api/docs) LLM provider.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovideropenai">openai</a></b></td>
        <td>object</td>
        <td>
          OpenAIConfig settings for the [OpenAI](https://platform.openai.com/docs/api-reference/streaming) LLM provider.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovidervertexai">vertexai</a></b></td>
        <td>object</td>
        <td>
          VertexAIConfig settings for the [Vertex AI](https://cloud.google.com/vertex-ai/docs) LLM provider.
To find the values for the project ID, project location, and publisher, you can check the fields of an API request, such as
`https://{LOCATION}-aiplatform.googleapis.com/{VERSION}/projects/{PROJECT_ID}/locations/{LOCATION}/publishers/{PROVIDER}/<model-path>`.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.anthropic
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovider)</sup></sup>



AnthropicConfig settings for the [Anthropic](https://docs.anthropic.com/en/release-notes/api) LLM provider.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovideranthropicauthtoken">authToken</a></b></td>
        <td>object</td>
        <td>
          The authorization token that the AI gateway uses to access the Anthropic API.
This token is automatically sent in the `x-api-key` header of the request.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>apiVersion</b></td>
        <td>string</td>
        <td>
          Optional: A version header to pass to the Anthropic API.
For more information, see the [Anthropic API versioning docs](https://docs.anthropic.com/en/api/versioning).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>model</b></td>
        <td>string</td>
        <td>
          Optional: Override the model name.
If unset, the model name is taken from the request.
This setting can be useful when testing model failover scenarios.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.anthropic.authToken
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovideranthropic)</sup></sup>



The authorization token that the AI gateway uses to access the Anthropic API.
This token is automatically sent in the `x-api-key` header of the request.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>kind</b></td>
        <td>enum</td>
        <td>
          Kind specifies which type of authorization token is being used.
Must be one of: "Inline", "SecretRef", "Passthrough".<br/>
          <br/>
            <i>Enum</i>: Inline, SecretRef, Passthrough<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>inline</b></td>
        <td>string</td>
        <td>
          Provide the token directly in the configuration for the Backend.
This option is the least secure. Only use this option for quick tests such as trying out AI Gateway.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovideranthropicauthtokensecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.anthropic.authToken.secretRef
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovideranthropicauthtoken)</sup></sup>



Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.azureopenai
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovider)</sup></sup>



AzureOpenAIConfig settings for the [Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/) LLM provider.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>apiVersion</b></td>
        <td>string</td>
        <td>
          The version of the Azure OpenAI API to use.
For more information, see the [Azure OpenAI API version reference](https://learn.microsoft.com/en-us/azure/ai-services/openai/reference#api-specs).<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexproviderazureopenaiauthtoken">authToken</a></b></td>
        <td>object</td>
        <td>
          The authorization token that the AI gateway uses to access the Azure OpenAI API.
This token is automatically sent in the `api-key` header of the request.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>deploymentName</b></td>
        <td>string</td>
        <td>
          The name of the Azure OpenAI model deployment to use.
For more information, see the [Azure OpenAI model docs](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/models).<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>endpoint</b></td>
        <td>string</td>
        <td>
          The endpoint for the Azure OpenAI API to use, such as `my-endpoint.openai.azure.com`.
If the scheme is included, it is stripped.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.azureopenai.authToken
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexproviderazureopenai)</sup></sup>



The authorization token that the AI gateway uses to access the Azure OpenAI API.
This token is automatically sent in the `api-key` header of the request.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>kind</b></td>
        <td>enum</td>
        <td>
          Kind specifies which type of authorization token is being used.
Must be one of: "Inline", "SecretRef", "Passthrough".<br/>
          <br/>
            <i>Enum</i>: Inline, SecretRef, Passthrough<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>inline</b></td>
        <td>string</td>
        <td>
          Provide the token directly in the configuration for the Backend.
This option is the least secure. Only use this option for quick tests such as trying out AI Gateway.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexproviderazureopenaiauthtokensecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.azureopenai.authToken.secretRef
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexproviderazureopenaiauthtoken)</sup></sup>



Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.gemini
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovider)</sup></sup>



GeminiConfig settings for the [Gemini](https://ai.google.dev/gemini-api/docs) LLM provider.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>apiVersion</b></td>
        <td>string</td>
        <td>
          The version of the Gemini API to use.
For more information, see the [Gemini API version docs](https://ai.google.dev/gemini-api/docs/api-versions).<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovidergeminiauthtoken">authToken</a></b></td>
        <td>object</td>
        <td>
          The authorization token that the AI gateway uses to access the Gemini API.
This token is automatically sent in the `key` query parameter of the request.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>model</b></td>
        <td>string</td>
        <td>
          The Gemini model to use.
For more information, see the [Gemini models docs](https://ai.google.dev/gemini-api/docs/models/gemini).<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.gemini.authToken
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovidergemini)</sup></sup>



The authorization token that the AI gateway uses to access the Gemini API.
This token is automatically sent in the `key` query parameter of the request.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>kind</b></td>
        <td>enum</td>
        <td>
          Kind specifies which type of authorization token is being used.
Must be one of: "Inline", "SecretRef", "Passthrough".<br/>
          <br/>
            <i>Enum</i>: Inline, SecretRef, Passthrough<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>inline</b></td>
        <td>string</td>
        <td>
          Provide the token directly in the configuration for the Backend.
This option is the least secure. Only use this option for quick tests such as trying out AI Gateway.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovidergeminiauthtokensecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.gemini.authToken.secretRef
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovidergeminiauthtoken)</sup></sup>



Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.openai
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovider)</sup></sup>



OpenAIConfig settings for the [OpenAI](https://platform.openai.com/docs/api-reference/streaming) LLM provider.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovideropenaiauthtoken">authToken</a></b></td>
        <td>object</td>
        <td>
          The authorization token that the AI gateway uses to access the OpenAI API.
This token is automatically sent in the `Authorization` header of the
request and prefixed with `Bearer`.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>model</b></td>
        <td>string</td>
        <td>
          Optional: Override the model name, such as `gpt-4o-mini`.
If unset, the model name is taken from the request.
This setting can be useful when setting up model failover within the same LLM provider.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.openai.authToken
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovideropenai)</sup></sup>



The authorization token that the AI gateway uses to access the OpenAI API.
This token is automatically sent in the `Authorization` header of the
request and prefixed with `Bearer`.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>kind</b></td>
        <td>enum</td>
        <td>
          Kind specifies which type of authorization token is being used.
Must be one of: "Inline", "SecretRef", "Passthrough".<br/>
          <br/>
            <i>Enum</i>: Inline, SecretRef, Passthrough<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>inline</b></td>
        <td>string</td>
        <td>
          Provide the token directly in the configuration for the Backend.
This option is the least secure. Only use this option for quick tests such as trying out AI Gateway.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovideropenaiauthtokensecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.openai.authToken.secretRef
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovideropenaiauthtoken)</sup></sup>



Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.vertexai
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovider)</sup></sup>



VertexAIConfig settings for the [Vertex AI](https://cloud.google.com/vertex-ai/docs) LLM provider.
To find the values for the project ID, project location, and publisher, you can check the fields of an API request, such as
`https://{LOCATION}-aiplatform.googleapis.com/{VERSION}/projects/{PROJECT_ID}/locations/{LOCATION}/publishers/{PROVIDER}/<model-path>`.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>apiVersion</b></td>
        <td>string</td>
        <td>
          The version of the Vertex AI API to use.
For more information, see the [Vertex AI API reference](https://cloud.google.com/vertex-ai/docs/reference#versions).<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovidervertexaiauthtoken">authToken</a></b></td>
        <td>object</td>
        <td>
          The authorization token that the AI gateway uses to access the Vertex AI API.
This token is automatically sent in the `key` header of the request.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>location</b></td>
        <td>string</td>
        <td>
          The location of the Google Cloud Project that you use for the Vertex AI.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>model</b></td>
        <td>string</td>
        <td>
          The Vertex AI model to use.
For more information, see the [Vertex AI model docs](https://cloud.google.com/vertex-ai/generative-ai/docs/learn/models).<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>projectId</b></td>
        <td>string</td>
        <td>
          The ID of the Google Cloud Project that you use for the Vertex AI.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>publisher</b></td>
        <td>enum</td>
        <td>
          The type of publisher model to use. Currently, only Google is supported.<br/>
          <br/>
            <i>Enum</i>: GOOGLE<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>modelPath</b></td>
        <td>string</td>
        <td>
          Optional: The model path to route to. Defaults to the Gemini model path, `generateContent`.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.vertexai.authToken
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovidervertexai)</sup></sup>



The authorization token that the AI gateway uses to access the Vertex AI API.
This token is automatically sent in the `key` header of the request.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>kind</b></td>
        <td>enum</td>
        <td>
          Kind specifies which type of authorization token is being used.
Must be one of: "Inline", "SecretRef", "Passthrough".<br/>
          <br/>
            <i>Enum</i>: Inline, SecretRef, Passthrough<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>inline</b></td>
        <td>string</td>
        <td>
          Provide the token directly in the configuration for the Backend.
This option is the least secure. Only use this option for quick tests such as trying out AI Gateway.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecaimultipoolprioritiesindexpoolindexprovidervertexaiauthtokensecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].provider.vertexai.authToken.secretRef
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindexprovidervertexaiauthtoken)</sup></sup>



Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.ai.multipool.priorities[index].pool[index].hostOverride
<sup><sup>[↩ Parent](#backendspecaimultipoolprioritiesindexpoolindex)</sup></sup>



Send requests to a custom host and port, such as to proxy the request,
or to use a different backend that is API-compliant with the Backend version.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Host is the host name.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port is the port number.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 1<br/>
            <i>Maximum</i>: 65535<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### Backend.spec.aws
<sup><sup>[↩ Parent](#backendspec)</sup></sup>



Aws is the AWS backend configuration.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>region</b></td>
        <td>string</td>
        <td>
          Region is the AWS region.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#backendspecawssecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          SecretRef is the secret reference for the AWS credentials.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.aws.secretRef
<sup><sup>[↩ Parent](#backendspecaws)</sup></sup>



SecretRef is the secret reference for the AWS credentials.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.static
<sup><sup>[↩ Parent](#backendspec)</sup></sup>



Static is the static backend configuration.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendspecstatichostsindex">hosts</a></b></td>
        <td>[]object</td>
        <td>
          Hosts is the list of hosts.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.spec.static.hosts[index]
<sup><sup>[↩ Parent](#backendspecstatic)</sup></sup>



Host is a host and port pair.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Host is the host name.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port is the port number.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 1<br/>
            <i>Maximum</i>: 65535<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### Backend.status
<sup><sup>[↩ Parent](#backend)</sup></sup>



BackendStatus defines the observed state of Backend.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#backendstatusconditionsindex">conditions</a></b></td>
        <td>[]object</td>
        <td>
          Conditions is the list of conditions for the backend.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### Backend.status.conditions[index]
<sup><sup>[↩ Parent](#backendstatus)</sup></sup>



Condition contains details for one aspect of the current state of this API Resource.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>lastTransitionTime</b></td>
        <td>string</td>
        <td>
          lastTransitionTime is the last time the condition transitioned from one status to another.
This should be when the underlying condition changed.  If that is not known, then using the time when the API field changed is acceptable.<br/>
          <br/>
            <i>Format</i>: date-time<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>message</b></td>
        <td>string</td>
        <td>
          message is a human readable message indicating details about the transition.
This may be an empty string.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>reason</b></td>
        <td>string</td>
        <td>
          reason contains a programmatic identifier indicating the reason for the condition's last transition.
Producers of specific condition types may define expected values and meanings for this field,
and whether the values are considered a guaranteed API.
The value should be a CamelCase string.
This field may not be empty.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>status</b></td>
        <td>enum</td>
        <td>
          status of the condition, one of True, False, Unknown.<br/>
          <br/>
            <i>Enum</i>: True, False, Unknown<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type of condition in CamelCase or in foo.example.com/CamelCase.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>observedGeneration</b></td>
        <td>integer</td>
        <td>
          observedGeneration represents the .metadata.generation that the condition was set based upon.
For instance, if .metadata.generation is currently 12, but the .status.conditions[x].observedGeneration is 9, the condition is out of date
with respect to the current state of the instance.<br/>
          <br/>
            <i>Format</i>: int64<br/>
            <i>Minimum</i>: 0<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>

## DirectResponse
<sup><sup>[↩ Parent](#gatewaykgatewaydevv1alpha1 )</sup></sup>






DirectResponse contains configuration for defining direct response routes.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
      <td><b>apiVersion</b></td>
      <td>string</td>
      <td>gateway.kgateway.dev/v1alpha1</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b>kind</b></td>
      <td>string</td>
      <td>DirectResponse</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b><a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#objectmeta-v1-meta">metadata</a></b></td>
      <td>object</td>
      <td>Refer to the Kubernetes API documentation for the fields of the `metadata` field.</td>
      <td>true</td>
      </tr><tr>
        <td><b><a href="#directresponsespec">spec</a></b></td>
        <td>object</td>
        <td>
          DirectResponseSpec describes the desired state of a DirectResponse.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>status</b></td>
        <td>object</td>
        <td>
          DirectResponseStatus defines the observed state of a DirectResponse.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### DirectResponse.spec
<sup><sup>[↩ Parent](#directresponse)</sup></sup>



DirectResponseSpec describes the desired state of a DirectResponse.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>status</b></td>
        <td>integer</td>
        <td>
          StatusCode defines the HTTP status code to return for this route.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 200<br/>
            <i>Maximum</i>: 599<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>body</b></td>
        <td>string</td>
        <td>
          Body defines the content to be returned in the HTTP response body.
The maximum length of the body is restricted to prevent excessively large responses.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>

## GatewayParameters
<sup><sup>[↩ Parent](#gatewaykgatewaydevv1alpha1 )</sup></sup>






A GatewayParameters contains configuration that is used to dynamically
provision kgateway's data plane (Envoy proxy instance), based on a
Kubernetes Gateway.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
      <td><b>apiVersion</b></td>
      <td>string</td>
      <td>gateway.kgateway.dev/v1alpha1</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b>kind</b></td>
      <td>string</td>
      <td>GatewayParameters</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b><a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#objectmeta-v1-meta">metadata</a></b></td>
      <td>object</td>
      <td>Refer to the Kubernetes API documentation for the fields of the `metadata` field.</td>
      <td>true</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspec">spec</a></b></td>
        <td>object</td>
        <td>
          A GatewayParametersSpec describes the type of environment/platform in which
the proxy will be provisioned.<br/>
          <br/>
            <i>Validations</i>:<li>(has(self.kube) && !has(self.selfManaged)) || (!has(self.kube) && has(self.selfManaged)): only one of 'kube' or 'selfManaged' may be set</li>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>status</b></td>
        <td>object</td>
        <td>
          The current conditions of the GatewayParameters. This is not currently implemented.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec
<sup><sup>[↩ Parent](#gatewayparameters)</sup></sup>



A GatewayParametersSpec describes the type of environment/platform in which
the proxy will be provisioned.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckube">kube</a></b></td>
        <td>object</td>
        <td>
          The proxy will be deployed on Kubernetes.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>selfManaged</b></td>
        <td>object</td>
        <td>
          The proxy will be self-managed and not auto-provisioned.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube
<sup><sup>[↩ Parent](#gatewayparametersspec)</sup></sup>



The proxy will be deployed on Kubernetes.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextension">aiExtension</a></b></td>
        <td>object</td>
        <td>
          Configuration for the AI extension.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubedeployment">deployment</a></b></td>
        <td>object</td>
        <td>
          Use a Kubernetes deployment as the proxy workload type. Currently, this is the only
supported workload type.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeenvoycontainer">envoyContainer</a></b></td>
        <td>object</td>
        <td>
          Configuration for the container running Envoy.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>floatingUserId</b></td>
        <td>boolean</td>
        <td>
          Used to unset the `runAsUser` values in security contexts.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistio">istio</a></b></td>
        <td>object</td>
        <td>
          Configuration for the Istio integration.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplate">podTemplate</a></b></td>
        <td>object</td>
        <td>
          Configuration for the pods that will be created.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubesdscontainer">sdsContainer</a></b></td>
        <td>object</td>
        <td>
          Configuration for the container running the Secret Discovery Service (SDS).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeservice">service</a></b></td>
        <td>object</td>
        <td>
          Configuration for the Kubernetes Service that exposes the Envoy proxy over
the network.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeserviceaccount">serviceAccount</a></b></td>
        <td>object</td>
        <td>
          Configuration for the Kubernetes ServiceAccount used by the Envoy pod.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubestats">stats</a></b></td>
        <td>object</td>
        <td>
          Configuration for the stats server.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension
<sup><sup>[↩ Parent](#gatewayparametersspeckube)</sup></sup>



Configuration for the AI extension.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>enabled</b></td>
        <td>boolean</td>
        <td>
          Whether to enable the extension.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionenvindex">env</a></b></td>
        <td>[]object</td>
        <td>
          The extension's container environment variables.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionimage">image</a></b></td>
        <td>object</td>
        <td>
          The extension's container image. See
https://kubernetes.io/docs/concepts/containers/images
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionportsindex">ports</a></b></td>
        <td>[]object</td>
        <td>
          The extension's container ports.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionresources">resources</a></b></td>
        <td>object</td>
        <td>
          The compute resources required by this container. See
https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionsecuritycontext">securityContext</a></b></td>
        <td>object</td>
        <td>
          The security context for this container. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionstats">stats</a></b></td>
        <td>object</td>
        <td>
          Additional stats config for AI Extension.
This config can be useful for adding custom labels to the request metrics.

Example:
```yaml
stats:
  customLabels:
    - name: "subject"
      metadataNamespace: "envoy.filters.http.jwt_authn"
      metadataKey: "principal:sub"
    - name: "issuer"
      metadataNamespace: "envoy.filters.http.jwt_authn"
      metadataKey: "principal:iss"
```<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.env[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextension)</sup></sup>



EnvVar represents an environment variable present in a Container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the environment variable. Must be a C_IDENTIFIER.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          Variable references $(VAR_NAME) are expanded
using the previously defined environment variables in the container and
any service environment variables. If a variable cannot be resolved,
the reference in the input string will be unchanged. Double $$ are reduced
to a single $, which allows for escaping the $(VAR_NAME) syntax: i.e.
"$$(VAR_NAME)" will produce the string literal "$(VAR_NAME)".
Escaped references will never be expanded, regardless of whether the variable
exists or not.
Defaults to "".<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionenvindexvaluefrom">valueFrom</a></b></td>
        <td>object</td>
        <td>
          Source for the environment variable's value. Cannot be used if value is not empty.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.env[index].valueFrom
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextensionenvindex)</sup></sup>



Source for the environment variable's value. Cannot be used if value is not empty.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionenvindexvaluefromconfigmapkeyref">configMapKeyRef</a></b></td>
        <td>object</td>
        <td>
          Selects a key of a ConfigMap.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionenvindexvaluefromfieldref">fieldRef</a></b></td>
        <td>object</td>
        <td>
          Selects a field of the pod: supports metadata.name, metadata.namespace, `metadata.labels['<KEY>']`, `metadata.annotations['<KEY>']`,
spec.nodeName, spec.serviceAccountName, status.hostIP, status.podIP, status.podIPs.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionenvindexvaluefromresourcefieldref">resourceFieldRef</a></b></td>
        <td>object</td>
        <td>
          Selects a resource of the container: only resources limits and requests
(limits.cpu, limits.memory, limits.ephemeral-storage, requests.cpu, requests.memory and requests.ephemeral-storage) are currently supported.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionenvindexvaluefromsecretkeyref">secretKeyRef</a></b></td>
        <td>object</td>
        <td>
          Selects a key of a secret in the pod's namespace<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.env[index].valueFrom.configMapKeyRef
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextensionenvindexvaluefrom)</sup></sup>



Selects a key of a ConfigMap.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          The key to select.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>optional</b></td>
        <td>boolean</td>
        <td>
          Specify whether the ConfigMap or its key must be defined<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.env[index].valueFrom.fieldRef
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextensionenvindexvaluefrom)</sup></sup>



Selects a field of the pod: supports metadata.name, metadata.namespace, `metadata.labels['<KEY>']`, `metadata.annotations['<KEY>']`,
spec.nodeName, spec.serviceAccountName, status.hostIP, status.podIP, status.podIPs.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>fieldPath</b></td>
        <td>string</td>
        <td>
          Path of the field to select in the specified API version.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>apiVersion</b></td>
        <td>string</td>
        <td>
          Version of the schema the FieldPath is written in terms of, defaults to "v1".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.env[index].valueFrom.resourceFieldRef
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextensionenvindexvaluefrom)</sup></sup>



Selects a resource of the container: only resources limits and requests
(limits.cpu, limits.memory, limits.ephemeral-storage, requests.cpu, requests.memory and requests.ephemeral-storage) are currently supported.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>resource</b></td>
        <td>string</td>
        <td>
          Required: resource to select<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>containerName</b></td>
        <td>string</td>
        <td>
          Container name: required for volumes, optional for env vars<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>divisor</b></td>
        <td>int or string</td>
        <td>
          Specifies the output format of the exposed resources, defaults to "1"<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.env[index].valueFrom.secretKeyRef
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextensionenvindexvaluefrom)</sup></sup>



Selects a key of a secret in the pod's namespace

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          The key of the secret to select from.  Must be a valid secret key.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>optional</b></td>
        <td>boolean</td>
        <td>
          Specify whether the Secret or its key must be defined<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.image
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextension)</sup></sup>



The extension's container image. See
https://kubernetes.io/docs/concepts/containers/images
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>digest</b></td>
        <td>string</td>
        <td>
          The hash digest of the image, e.g. `sha256:12345...`<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>pullPolicy</b></td>
        <td>string</td>
        <td>
          The image pull policy for the container. See
https://kubernetes.io/docs/concepts/containers/images/#image-pull-policy
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>registry</b></td>
        <td>string</td>
        <td>
          The image registry.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>repository</b></td>
        <td>string</td>
        <td>
          The image repository (name).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>tag</b></td>
        <td>string</td>
        <td>
          The image tag.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.ports[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextension)</sup></sup>



ContainerPort represents a network port in a single container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>containerPort</b></td>
        <td>integer</td>
        <td>
          Number of port to expose on the pod's IP address.
This must be a valid port number, 0 < x < 65536.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>hostIP</b></td>
        <td>string</td>
        <td>
          What host IP to bind the external port to.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>hostPort</b></td>
        <td>integer</td>
        <td>
          Number of port to expose on the host.
If specified, this must be a valid port number, 0 < x < 65536.
If HostNetwork is specified, this must match ContainerPort.
Most containers do not need this.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          If specified, this must be an IANA_SVC_NAME and unique within the pod. Each
named port in a pod must have a unique name. Name for the port that can be
referred to by services.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>protocol</b></td>
        <td>string</td>
        <td>
          Protocol for port. Must be UDP, TCP, or SCTP.
Defaults to "TCP".<br/>
          <br/>
            <i>Default</i>: TCP<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.resources
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextension)</sup></sup>



The compute resources required by this container. See
https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionresourcesclaimsindex">claims</a></b></td>
        <td>[]object</td>
        <td>
          Claims lists the names of resources, defined in spec.resourceClaims,
that are used by this container.

This is an alpha field and requires enabling the
DynamicResourceAllocation feature gate.

This field is immutable. It can only be set for containers.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>limits</b></td>
        <td>map[string]int or string</td>
        <td>
          Limits describes the maximum amount of compute resources allowed.
More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>requests</b></td>
        <td>map[string]int or string</td>
        <td>
          Requests describes the minimum amount of compute resources required.
If Requests is omitted for a container, it defaults to Limits if that is explicitly specified,
otherwise to an implementation-defined value. Requests cannot exceed Limits.
More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.resources.claims[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextensionresources)</sup></sup>



ResourceClaim references one entry in PodSpec.ResourceClaims.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name must match the name of one entry in pod.spec.resourceClaims of
the Pod where this field is used. It makes that resource available
inside a container.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>request</b></td>
        <td>string</td>
        <td>
          Request is the name chosen for a request in the referenced claim.
If empty, everything from the claim is made available, otherwise
only the result of this request.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.securityContext
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextension)</sup></sup>



The security context for this container. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>allowPrivilegeEscalation</b></td>
        <td>boolean</td>
        <td>
          AllowPrivilegeEscalation controls whether a process can gain more
privileges than its parent process. This bool directly controls if
the no_new_privs flag will be set on the container process.
AllowPrivilegeEscalation is true always when the container is:
1) run as Privileged
2) has CAP_SYS_ADMIN
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionsecuritycontextapparmorprofile">appArmorProfile</a></b></td>
        <td>object</td>
        <td>
          appArmorProfile is the AppArmor options to use by this container. If set, this profile
overrides the pod's appArmorProfile.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionsecuritycontextcapabilities">capabilities</a></b></td>
        <td>object</td>
        <td>
          The capabilities to add/drop when running containers.
Defaults to the default set of capabilities granted by the container runtime.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>privileged</b></td>
        <td>boolean</td>
        <td>
          Run container in privileged mode.
Processes in privileged containers are essentially equivalent to root on the host.
Defaults to false.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>procMount</b></td>
        <td>string</td>
        <td>
          procMount denotes the type of proc mount to use for the containers.
The default value is Default which uses the container runtime defaults for
readonly paths and masked paths.
This requires the ProcMountType feature flag to be enabled.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>readOnlyRootFilesystem</b></td>
        <td>boolean</td>
        <td>
          Whether this container has a read-only root filesystem.
Default is false.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsGroup</b></td>
        <td>integer</td>
        <td>
          The GID to run the entrypoint of the container process.
Uses runtime default if unset.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsNonRoot</b></td>
        <td>boolean</td>
        <td>
          Indicates that the container must run as a non-root user.
If true, the Kubelet will validate the image at runtime to ensure that it
does not run as UID 0 (root) and fail to start the container if it does.
If unset or false, no such validation will be performed.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsUser</b></td>
        <td>integer</td>
        <td>
          The UID to run the entrypoint of the container process.
Defaults to user specified in image metadata if unspecified.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionsecuritycontextselinuxoptions">seLinuxOptions</a></b></td>
        <td>object</td>
        <td>
          The SELinux context to be applied to the container.
If unspecified, the container runtime will allocate a random SELinux context for each
container.  May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionsecuritycontextseccompprofile">seccompProfile</a></b></td>
        <td>object</td>
        <td>
          The seccomp options to use by this container. If seccomp options are
provided at both the pod & container level, the container options
override the pod options.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionsecuritycontextwindowsoptions">windowsOptions</a></b></td>
        <td>object</td>
        <td>
          The Windows specific settings applied to all containers.
If unspecified, the options from the PodSecurityContext will be used.
If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is linux.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.securityContext.appArmorProfile
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextensionsecuritycontext)</sup></sup>



appArmorProfile is the AppArmor options to use by this container. If set, this profile
overrides the pod's appArmorProfile.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type indicates which kind of AppArmor profile will be applied.
Valid options are:
  Localhost - a profile pre-loaded on the node.
  RuntimeDefault - the container runtime's default profile.
  Unconfined - no AppArmor enforcement.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>localhostProfile</b></td>
        <td>string</td>
        <td>
          localhostProfile indicates a profile loaded on the node that should be used.
The profile must be preconfigured on the node to work.
Must match the loaded name of the profile.
Must be set if and only if type is "Localhost".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.securityContext.capabilities
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextensionsecuritycontext)</sup></sup>



The capabilities to add/drop when running containers.
Defaults to the default set of capabilities granted by the container runtime.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>add</b></td>
        <td>[]string</td>
        <td>
          Added capabilities<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>drop</b></td>
        <td>[]string</td>
        <td>
          Removed capabilities<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.securityContext.seLinuxOptions
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextensionsecuritycontext)</sup></sup>



The SELinux context to be applied to the container.
If unspecified, the container runtime will allocate a random SELinux context for each
container.  May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>level</b></td>
        <td>string</td>
        <td>
          Level is SELinux level label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>role</b></td>
        <td>string</td>
        <td>
          Role is a SELinux role label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          Type is a SELinux type label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>user</b></td>
        <td>string</td>
        <td>
          User is a SELinux user label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.securityContext.seccompProfile
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextensionsecuritycontext)</sup></sup>



The seccomp options to use by this container. If seccomp options are
provided at both the pod & container level, the container options
override the pod options.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type indicates which kind of seccomp profile will be applied.
Valid options are:

Localhost - a profile defined in a file on the node should be used.
RuntimeDefault - the container runtime default profile should be used.
Unconfined - no profile should be applied.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>localhostProfile</b></td>
        <td>string</td>
        <td>
          localhostProfile indicates a profile defined in a file on the node should be used.
The profile must be preconfigured on the node to work.
Must be a descending path, relative to the kubelet's configured seccomp profile location.
Must be set if type is "Localhost". Must NOT be set for any other type.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.securityContext.windowsOptions
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextensionsecuritycontext)</sup></sup>



The Windows specific settings applied to all containers.
If unspecified, the options from the PodSecurityContext will be used.
If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is linux.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>gmsaCredentialSpec</b></td>
        <td>string</td>
        <td>
          GMSACredentialSpec is where the GMSA admission webhook
(https://github.com/kubernetes-sigs/windows-gmsa) inlines the contents of the
GMSA credential spec named by the GMSACredentialSpecName field.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>gmsaCredentialSpecName</b></td>
        <td>string</td>
        <td>
          GMSACredentialSpecName is the name of the GMSA credential spec to use.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>hostProcess</b></td>
        <td>boolean</td>
        <td>
          HostProcess determines if a container should be run as a 'Host Process' container.
All of a Pod's containers must have the same effective HostProcess value
(it is not allowed to have a mix of HostProcess containers and non-HostProcess containers).
In addition, if HostProcess is true then HostNetwork must also be set to true.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsUserName</b></td>
        <td>string</td>
        <td>
          The UserName in Windows to run the entrypoint of the container process.
Defaults to the user specified in image metadata if unspecified.
May also be set in PodSecurityContext. If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.stats
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextension)</sup></sup>



Additional stats config for AI Extension.
This config can be useful for adding custom labels to the request metrics.

Example:
```yaml
stats:
  customLabels:
    - name: "subject"
      metadataNamespace: "envoy.filters.http.jwt_authn"
      metadataKey: "principal:sub"
    - name: "issuer"
      metadataNamespace: "envoy.filters.http.jwt_authn"
      metadataKey: "principal:iss"
```

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeaiextensionstatscustomlabelsindex">customLabels</a></b></td>
        <td>[]object</td>
        <td>
          Set of custom labels to be added to the request metrics.
These will be added on each request which goes through the AI Extension.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.aiExtension.stats.customLabels[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeaiextensionstats)</sup></sup>





<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>metadataKey</b></td>
        <td>string</td>
        <td>
          The key to use to get the data from the metadata namespace.
If using a JWT data please see the following envoy docs: https://www.envoyproxy.io/docs/envoy/latest/api-v3/extensions/filters/http/jwt_authn/v3/config.proto#envoy-v3-api-field-extensions-filters-http-jwt-authn-v3-jwtprovider-payload-in-metadata
This key follows the same format as the envoy access logging for dynamic metadata.
Examples can be found here: https://www.envoyproxy.io/docs/envoy/latest/configuration/observability/access_log/usage<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the label to use in the prometheus metrics<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>keyDelimiter</b></td>
        <td>string</td>
        <td>
          The key delimiter to use, by default this is set to `:`.
This allows for keys with `.` in them to be used.
For example, if you have keys in your path with `:` in them, (e.g. `key1:key2:value`)
you can instead set this to `~` to be able to split those keys properly.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>metadataNamespace</b></td>
        <td>enum</td>
        <td>
          The dynamic metadata namespace to get the data from. If not specified, the default namespace will be
the envoy JWT filter namespace.
This can also be used in combination with early_transformations to insert custom data.<br/>
          <br/>
            <i>Enum</i>: envoy.filters.http.jwt_authn, io.solo.transformation<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.deployment
<sup><sup>[↩ Parent](#gatewayparametersspeckube)</sup></sup>



Use a Kubernetes deployment as the proxy workload type. Currently, this is the only
supported workload type.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>replicas</b></td>
        <td>integer</td>
        <td>
          The number of desired pods. Defaults to 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.envoyContainer
<sup><sup>[↩ Parent](#gatewayparametersspeckube)</sup></sup>



Configuration for the container running Envoy.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeenvoycontainerbootstrap">bootstrap</a></b></td>
        <td>object</td>
        <td>
          Initial envoy configuration.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeenvoycontainerimage">image</a></b></td>
        <td>object</td>
        <td>
          The envoy container image. See
https://kubernetes.io/docs/concepts/containers/images
for details.

Default values, which may be overridden individually:

	registry: quay.io/solo-io
	repository: gloo-envoy-wrapper (OSS) / gloo-ee-envoy-wrapper (EE)
	tag: <gloo version> (OSS) / <gloo-ee version> (EE)
	pullPolicy: IfNotPresent<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeenvoycontainerresources">resources</a></b></td>
        <td>object</td>
        <td>
          The compute resources required by this container. See
https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeenvoycontainersecuritycontext">securityContext</a></b></td>
        <td>object</td>
        <td>
          The security context for this container. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core
for details.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.envoyContainer.bootstrap
<sup><sup>[↩ Parent](#gatewayparametersspeckubeenvoycontainer)</sup></sup>



Initial envoy configuration.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>componentLogLevels</b></td>
        <td>map[string]string</td>
        <td>
          Envoy log levels for specific components. The keys are component names and
the values are one of "trace", "debug", "info", "warn", "error",
"critical", or "off", e.g.

	```yaml
	componentLogLevels:
	  upstream: debug
	  connection: trace
	```

These will be converted to the `--component-log-level` Envoy argument
value. See
https://www.envoyproxy.io/docs/envoy/latest/start/quick-start/run-envoy#debugging-envoy
for more information.

Note: the keys and values cannot be empty, but they are not otherwise validated.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>logLevel</b></td>
        <td>string</td>
        <td>
          Envoy log level. Options include "trace", "debug", "info", "warn", "error",
"critical" and "off". Defaults to "info". See
https://www.envoyproxy.io/docs/envoy/latest/start/quick-start/run-envoy#debugging-envoy
for more information.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.envoyContainer.image
<sup><sup>[↩ Parent](#gatewayparametersspeckubeenvoycontainer)</sup></sup>



The envoy container image. See
https://kubernetes.io/docs/concepts/containers/images
for details.

Default values, which may be overridden individually:

	registry: quay.io/solo-io
	repository: gloo-envoy-wrapper (OSS) / gloo-ee-envoy-wrapper (EE)
	tag: <gloo version> (OSS) / <gloo-ee version> (EE)
	pullPolicy: IfNotPresent

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>digest</b></td>
        <td>string</td>
        <td>
          The hash digest of the image, e.g. `sha256:12345...`<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>pullPolicy</b></td>
        <td>string</td>
        <td>
          The image pull policy for the container. See
https://kubernetes.io/docs/concepts/containers/images/#image-pull-policy
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>registry</b></td>
        <td>string</td>
        <td>
          The image registry.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>repository</b></td>
        <td>string</td>
        <td>
          The image repository (name).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>tag</b></td>
        <td>string</td>
        <td>
          The image tag.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.envoyContainer.resources
<sup><sup>[↩ Parent](#gatewayparametersspeckubeenvoycontainer)</sup></sup>



The compute resources required by this container. See
https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeenvoycontainerresourcesclaimsindex">claims</a></b></td>
        <td>[]object</td>
        <td>
          Claims lists the names of resources, defined in spec.resourceClaims,
that are used by this container.

This is an alpha field and requires enabling the
DynamicResourceAllocation feature gate.

This field is immutable. It can only be set for containers.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>limits</b></td>
        <td>map[string]int or string</td>
        <td>
          Limits describes the maximum amount of compute resources allowed.
More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>requests</b></td>
        <td>map[string]int or string</td>
        <td>
          Requests describes the minimum amount of compute resources required.
If Requests is omitted for a container, it defaults to Limits if that is explicitly specified,
otherwise to an implementation-defined value. Requests cannot exceed Limits.
More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.envoyContainer.resources.claims[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeenvoycontainerresources)</sup></sup>



ResourceClaim references one entry in PodSpec.ResourceClaims.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name must match the name of one entry in pod.spec.resourceClaims of
the Pod where this field is used. It makes that resource available
inside a container.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>request</b></td>
        <td>string</td>
        <td>
          Request is the name chosen for a request in the referenced claim.
If empty, everything from the claim is made available, otherwise
only the result of this request.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.envoyContainer.securityContext
<sup><sup>[↩ Parent](#gatewayparametersspeckubeenvoycontainer)</sup></sup>



The security context for this container. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>allowPrivilegeEscalation</b></td>
        <td>boolean</td>
        <td>
          AllowPrivilegeEscalation controls whether a process can gain more
privileges than its parent process. This bool directly controls if
the no_new_privs flag will be set on the container process.
AllowPrivilegeEscalation is true always when the container is:
1) run as Privileged
2) has CAP_SYS_ADMIN
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeenvoycontainersecuritycontextapparmorprofile">appArmorProfile</a></b></td>
        <td>object</td>
        <td>
          appArmorProfile is the AppArmor options to use by this container. If set, this profile
overrides the pod's appArmorProfile.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeenvoycontainersecuritycontextcapabilities">capabilities</a></b></td>
        <td>object</td>
        <td>
          The capabilities to add/drop when running containers.
Defaults to the default set of capabilities granted by the container runtime.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>privileged</b></td>
        <td>boolean</td>
        <td>
          Run container in privileged mode.
Processes in privileged containers are essentially equivalent to root on the host.
Defaults to false.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>procMount</b></td>
        <td>string</td>
        <td>
          procMount denotes the type of proc mount to use for the containers.
The default value is Default which uses the container runtime defaults for
readonly paths and masked paths.
This requires the ProcMountType feature flag to be enabled.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>readOnlyRootFilesystem</b></td>
        <td>boolean</td>
        <td>
          Whether this container has a read-only root filesystem.
Default is false.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsGroup</b></td>
        <td>integer</td>
        <td>
          The GID to run the entrypoint of the container process.
Uses runtime default if unset.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsNonRoot</b></td>
        <td>boolean</td>
        <td>
          Indicates that the container must run as a non-root user.
If true, the Kubelet will validate the image at runtime to ensure that it
does not run as UID 0 (root) and fail to start the container if it does.
If unset or false, no such validation will be performed.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsUser</b></td>
        <td>integer</td>
        <td>
          The UID to run the entrypoint of the container process.
Defaults to user specified in image metadata if unspecified.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeenvoycontainersecuritycontextselinuxoptions">seLinuxOptions</a></b></td>
        <td>object</td>
        <td>
          The SELinux context to be applied to the container.
If unspecified, the container runtime will allocate a random SELinux context for each
container.  May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeenvoycontainersecuritycontextseccompprofile">seccompProfile</a></b></td>
        <td>object</td>
        <td>
          The seccomp options to use by this container. If seccomp options are
provided at both the pod & container level, the container options
override the pod options.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeenvoycontainersecuritycontextwindowsoptions">windowsOptions</a></b></td>
        <td>object</td>
        <td>
          The Windows specific settings applied to all containers.
If unspecified, the options from the PodSecurityContext will be used.
If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is linux.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.envoyContainer.securityContext.appArmorProfile
<sup><sup>[↩ Parent](#gatewayparametersspeckubeenvoycontainersecuritycontext)</sup></sup>



appArmorProfile is the AppArmor options to use by this container. If set, this profile
overrides the pod's appArmorProfile.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type indicates which kind of AppArmor profile will be applied.
Valid options are:
  Localhost - a profile pre-loaded on the node.
  RuntimeDefault - the container runtime's default profile.
  Unconfined - no AppArmor enforcement.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>localhostProfile</b></td>
        <td>string</td>
        <td>
          localhostProfile indicates a profile loaded on the node that should be used.
The profile must be preconfigured on the node to work.
Must match the loaded name of the profile.
Must be set if and only if type is "Localhost".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.envoyContainer.securityContext.capabilities
<sup><sup>[↩ Parent](#gatewayparametersspeckubeenvoycontainersecuritycontext)</sup></sup>



The capabilities to add/drop when running containers.
Defaults to the default set of capabilities granted by the container runtime.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>add</b></td>
        <td>[]string</td>
        <td>
          Added capabilities<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>drop</b></td>
        <td>[]string</td>
        <td>
          Removed capabilities<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.envoyContainer.securityContext.seLinuxOptions
<sup><sup>[↩ Parent](#gatewayparametersspeckubeenvoycontainersecuritycontext)</sup></sup>



The SELinux context to be applied to the container.
If unspecified, the container runtime will allocate a random SELinux context for each
container.  May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>level</b></td>
        <td>string</td>
        <td>
          Level is SELinux level label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>role</b></td>
        <td>string</td>
        <td>
          Role is a SELinux role label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          Type is a SELinux type label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>user</b></td>
        <td>string</td>
        <td>
          User is a SELinux user label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.envoyContainer.securityContext.seccompProfile
<sup><sup>[↩ Parent](#gatewayparametersspeckubeenvoycontainersecuritycontext)</sup></sup>



The seccomp options to use by this container. If seccomp options are
provided at both the pod & container level, the container options
override the pod options.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type indicates which kind of seccomp profile will be applied.
Valid options are:

Localhost - a profile defined in a file on the node should be used.
RuntimeDefault - the container runtime default profile should be used.
Unconfined - no profile should be applied.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>localhostProfile</b></td>
        <td>string</td>
        <td>
          localhostProfile indicates a profile defined in a file on the node should be used.
The profile must be preconfigured on the node to work.
Must be a descending path, relative to the kubelet's configured seccomp profile location.
Must be set if type is "Localhost". Must NOT be set for any other type.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.envoyContainer.securityContext.windowsOptions
<sup><sup>[↩ Parent](#gatewayparametersspeckubeenvoycontainersecuritycontext)</sup></sup>



The Windows specific settings applied to all containers.
If unspecified, the options from the PodSecurityContext will be used.
If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is linux.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>gmsaCredentialSpec</b></td>
        <td>string</td>
        <td>
          GMSACredentialSpec is where the GMSA admission webhook
(https://github.com/kubernetes-sigs/windows-gmsa) inlines the contents of the
GMSA credential spec named by the GMSACredentialSpecName field.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>gmsaCredentialSpecName</b></td>
        <td>string</td>
        <td>
          GMSACredentialSpecName is the name of the GMSA credential spec to use.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>hostProcess</b></td>
        <td>boolean</td>
        <td>
          HostProcess determines if a container should be run as a 'Host Process' container.
All of a Pod's containers must have the same effective HostProcess value
(it is not allowed to have a mix of HostProcess containers and non-HostProcess containers).
In addition, if HostProcess is true then HostNetwork must also be set to true.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsUserName</b></td>
        <td>string</td>
        <td>
          The UserName in Windows to run the entrypoint of the container process.
Defaults to the user specified in image metadata if unspecified.
May also be set in PodSecurityContext. If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio
<sup><sup>[↩ Parent](#gatewayparametersspeckube)</sup></sup>



Configuration for the Istio integration.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindex">customSidecars</a></b></td>
        <td>[]object</td>
        <td>
          do not use slice of pointers: https://github.com/kubernetes/code-generator/issues/166
Override the default Istio sidecar in gateway-proxy with a custom container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistioistioproxycontainer">istioProxyContainer</a></b></td>
        <td>object</td>
        <td>
          Configuration for the container running istio-proxy.
Note that if Istio integration is not enabled, the istio container will not be injected
into the gateway proxy deployment.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistio)</sup></sup>



A single application container that you want to run within a pod.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the container specified as a DNS_LABEL.
Each container in a pod must have a unique name (DNS_LABEL).
Cannot be updated.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>args</b></td>
        <td>[]string</td>
        <td>
          Arguments to the entrypoint.
The container image's CMD is used if this is not provided.
Variable references $(VAR_NAME) are expanded using the container's environment. If a variable
cannot be resolved, the reference in the input string will be unchanged. Double $$ are reduced
to a single $, which allows for escaping the $(VAR_NAME) syntax: i.e. "$$(VAR_NAME)" will
produce the string literal "$(VAR_NAME)". Escaped references will never be expanded, regardless
of whether the variable exists or not. Cannot be updated.
More info: https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/#running-a-command-in-a-shell<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>command</b></td>
        <td>[]string</td>
        <td>
          Entrypoint array. Not executed within a shell.
The container image's ENTRYPOINT is used if this is not provided.
Variable references $(VAR_NAME) are expanded using the container's environment. If a variable
cannot be resolved, the reference in the input string will be unchanged. Double $$ are reduced
to a single $, which allows for escaping the $(VAR_NAME) syntax: i.e. "$$(VAR_NAME)" will
produce the string literal "$(VAR_NAME)". Escaped references will never be expanded, regardless
of whether the variable exists or not. Cannot be updated.
More info: https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/#running-a-command-in-a-shell<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexenvindex">env</a></b></td>
        <td>[]object</td>
        <td>
          List of environment variables to set in the container.
Cannot be updated.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexenvfromindex">envFrom</a></b></td>
        <td>[]object</td>
        <td>
          List of sources to populate environment variables in the container.
The keys defined within a source must be a C_IDENTIFIER. All invalid keys
will be reported as an event when the container is starting. When a key exists in multiple
sources, the value associated with the last source will take precedence.
Values defined by an Env with a duplicate key will take precedence.
Cannot be updated.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>image</b></td>
        <td>string</td>
        <td>
          Container image name.
More info: https://kubernetes.io/docs/concepts/containers/images
This field is optional to allow higher level config management to default or override
container images in workload controllers like Deployments and StatefulSets.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>imagePullPolicy</b></td>
        <td>string</td>
        <td>
          Image pull policy.
One of Always, Never, IfNotPresent.
Defaults to Always if :latest tag is specified, or IfNotPresent otherwise.
Cannot be updated.
More info: https://kubernetes.io/docs/concepts/containers/images#updating-images<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecycle">lifecycle</a></b></td>
        <td>object</td>
        <td>
          Actions that the management system should take in response to container lifecycle events.
Cannot be updated.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlivenessprobe">livenessProbe</a></b></td>
        <td>object</td>
        <td>
          Periodic probe of container liveness.
Container will be restarted if the probe fails.
Cannot be updated.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexportsindex">ports</a></b></td>
        <td>[]object</td>
        <td>
          List of ports to expose from the container. Not specifying a port here
DOES NOT prevent that port from being exposed. Any port which is
listening on the default "0.0.0.0" address inside a container will be
accessible from the network.
Modifying this array with strategic merge patch may corrupt the data.
For more information See https://github.com/kubernetes/kubernetes/issues/108255.
Cannot be updated.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexreadinessprobe">readinessProbe</a></b></td>
        <td>object</td>
        <td>
          Periodic probe of container service readiness.
Container will be removed from service endpoints if the probe fails.
Cannot be updated.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexresizepolicyindex">resizePolicy</a></b></td>
        <td>[]object</td>
        <td>
          Resources resize policy for the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexresources">resources</a></b></td>
        <td>object</td>
        <td>
          Compute Resources required by this container.
Cannot be updated.
More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>restartPolicy</b></td>
        <td>string</td>
        <td>
          RestartPolicy defines the restart behavior of individual containers in a pod.
This field may only be set for init containers, and the only allowed value is "Always".
For non-init containers or when this field is not specified,
the restart behavior is defined by the Pod's restart policy and the container type.
Setting the RestartPolicy as "Always" for the init container will have the following effect:
this init container will be continually restarted on
exit until all regular containers have terminated. Once all regular
containers have completed, all init containers with restartPolicy "Always"
will be shut down. This lifecycle differs from normal init containers and
is often referred to as a "sidecar" container. Although this init
container still starts in the init container sequence, it does not wait
for the container to complete before proceeding to the next init
container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexsecuritycontext">securityContext</a></b></td>
        <td>object</td>
        <td>
          SecurityContext defines the security options the container should be run with.
If set, the fields of SecurityContext override the equivalent fields of PodSecurityContext.
More info: https://kubernetes.io/docs/tasks/configure-pod-container/security-context/<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexstartupprobe">startupProbe</a></b></td>
        <td>object</td>
        <td>
          StartupProbe indicates that the Pod has successfully initialized.
If specified, no other probes are executed until this completes successfully.
If this probe fails, the Pod will be restarted, just as if the livenessProbe failed.
This can be used to provide different probe parameters at the beginning of a Pod's lifecycle,
when it might take a long time to load data or warm a cache, than during steady-state operation.
This cannot be updated.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>stdin</b></td>
        <td>boolean</td>
        <td>
          Whether this container should allocate a buffer for stdin in the container runtime. If this
is not set, reads from stdin in the container will always result in EOF.
Default is false.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>stdinOnce</b></td>
        <td>boolean</td>
        <td>
          Whether the container runtime should close the stdin channel after it has been opened by
a single attach. When stdin is true the stdin stream will remain open across multiple attach
sessions. If stdinOnce is set to true, stdin is opened on container start, is empty until the
first client attaches to stdin, and then remains open and accepts data until the client disconnects,
at which time stdin is closed and remains closed until the container is restarted. If this
flag is false, a container processes that reads from stdin will never receive an EOF.
Default is false<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>terminationMessagePath</b></td>
        <td>string</td>
        <td>
          Optional: Path at which the file to which the container's termination message
will be written is mounted into the container's filesystem.
Message written is intended to be brief final status, such as an assertion failure message.
Will be truncated by the node if greater than 4096 bytes. The total message length across
all containers will be limited to 12kb.
Defaults to /dev/termination-log.
Cannot be updated.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>terminationMessagePolicy</b></td>
        <td>string</td>
        <td>
          Indicate how the termination message should be populated. File will use the contents of
terminationMessagePath to populate the container status message on both success and failure.
FallbackToLogsOnError will use the last chunk of container log output if the termination
message file is empty and the container exited with an error.
The log output is limited to 2048 bytes or 80 lines, whichever is smaller.
Defaults to File.
Cannot be updated.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>tty</b></td>
        <td>boolean</td>
        <td>
          Whether this container should allocate a TTY for itself, also requires 'stdin' to be true.
Default is false.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexvolumedevicesindex">volumeDevices</a></b></td>
        <td>[]object</td>
        <td>
          volumeDevices is the list of block devices to be used by the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexvolumemountsindex">volumeMounts</a></b></td>
        <td>[]object</td>
        <td>
          Pod volumes to mount into the container's filesystem.
Cannot be updated.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>workingDir</b></td>
        <td>string</td>
        <td>
          Container's working directory.
If not specified, the container runtime's default will be used, which
might be configured in the container image.
Cannot be updated.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].env[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindex)</sup></sup>



EnvVar represents an environment variable present in a Container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the environment variable. Must be a C_IDENTIFIER.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          Variable references $(VAR_NAME) are expanded
using the previously defined environment variables in the container and
any service environment variables. If a variable cannot be resolved,
the reference in the input string will be unchanged. Double $$ are reduced
to a single $, which allows for escaping the $(VAR_NAME) syntax: i.e.
"$$(VAR_NAME)" will produce the string literal "$(VAR_NAME)".
Escaped references will never be expanded, regardless of whether the variable
exists or not.
Defaults to "".<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexenvindexvaluefrom">valueFrom</a></b></td>
        <td>object</td>
        <td>
          Source for the environment variable's value. Cannot be used if value is not empty.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].env[index].valueFrom
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexenvindex)</sup></sup>



Source for the environment variable's value. Cannot be used if value is not empty.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexenvindexvaluefromconfigmapkeyref">configMapKeyRef</a></b></td>
        <td>object</td>
        <td>
          Selects a key of a ConfigMap.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexenvindexvaluefromfieldref">fieldRef</a></b></td>
        <td>object</td>
        <td>
          Selects a field of the pod: supports metadata.name, metadata.namespace, `metadata.labels['<KEY>']`, `metadata.annotations['<KEY>']`,
spec.nodeName, spec.serviceAccountName, status.hostIP, status.podIP, status.podIPs.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexenvindexvaluefromresourcefieldref">resourceFieldRef</a></b></td>
        <td>object</td>
        <td>
          Selects a resource of the container: only resources limits and requests
(limits.cpu, limits.memory, limits.ephemeral-storage, requests.cpu, requests.memory and requests.ephemeral-storage) are currently supported.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexenvindexvaluefromsecretkeyref">secretKeyRef</a></b></td>
        <td>object</td>
        <td>
          Selects a key of a secret in the pod's namespace<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].env[index].valueFrom.configMapKeyRef
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexenvindexvaluefrom)</sup></sup>



Selects a key of a ConfigMap.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          The key to select.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>optional</b></td>
        <td>boolean</td>
        <td>
          Specify whether the ConfigMap or its key must be defined<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].env[index].valueFrom.fieldRef
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexenvindexvaluefrom)</sup></sup>



Selects a field of the pod: supports metadata.name, metadata.namespace, `metadata.labels['<KEY>']`, `metadata.annotations['<KEY>']`,
spec.nodeName, spec.serviceAccountName, status.hostIP, status.podIP, status.podIPs.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>fieldPath</b></td>
        <td>string</td>
        <td>
          Path of the field to select in the specified API version.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>apiVersion</b></td>
        <td>string</td>
        <td>
          Version of the schema the FieldPath is written in terms of, defaults to "v1".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].env[index].valueFrom.resourceFieldRef
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexenvindexvaluefrom)</sup></sup>



Selects a resource of the container: only resources limits and requests
(limits.cpu, limits.memory, limits.ephemeral-storage, requests.cpu, requests.memory and requests.ephemeral-storage) are currently supported.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>resource</b></td>
        <td>string</td>
        <td>
          Required: resource to select<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>containerName</b></td>
        <td>string</td>
        <td>
          Container name: required for volumes, optional for env vars<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>divisor</b></td>
        <td>int or string</td>
        <td>
          Specifies the output format of the exposed resources, defaults to "1"<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].env[index].valueFrom.secretKeyRef
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexenvindexvaluefrom)</sup></sup>



Selects a key of a secret in the pod's namespace

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          The key of the secret to select from.  Must be a valid secret key.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>optional</b></td>
        <td>boolean</td>
        <td>
          Specify whether the Secret or its key must be defined<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].envFrom[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindex)</sup></sup>



EnvFromSource represents the source of a set of ConfigMaps

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexenvfromindexconfigmapref">configMapRef</a></b></td>
        <td>object</td>
        <td>
          The ConfigMap to select from<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>prefix</b></td>
        <td>string</td>
        <td>
          An optional identifier to prepend to each key in the ConfigMap. Must be a C_IDENTIFIER.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexenvfromindexsecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          The Secret to select from<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].envFrom[index].configMapRef
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexenvfromindex)</sup></sup>



The ConfigMap to select from

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>optional</b></td>
        <td>boolean</td>
        <td>
          Specify whether the ConfigMap must be defined<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].envFrom[index].secretRef
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexenvfromindex)</sup></sup>



The Secret to select from

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>optional</b></td>
        <td>boolean</td>
        <td>
          Specify whether the Secret must be defined<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindex)</sup></sup>



Actions that the management system should take in response to container lifecycle events.
Cannot be updated.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecyclepoststart">postStart</a></b></td>
        <td>object</td>
        <td>
          PostStart is called immediately after a container is created. If the handler fails,
the container is terminated and restarted according to its restart policy.
Other management of the container blocks until the hook completes.
More info: https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/#container-hooks<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecycleprestop">preStop</a></b></td>
        <td>object</td>
        <td>
          PreStop is called immediately before a container is terminated due to an
API request or management event such as liveness/startup probe failure,
preemption, resource contention, etc. The handler is not called if the
container crashes or exits. The Pod's termination grace period countdown begins before the
PreStop hook is executed. Regardless of the outcome of the handler, the
container will eventually terminate within the Pod's termination grace
period (unless delayed by finalizers). Other management of the container blocks until the hook completes
or until the termination grace period is reached.
More info: https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/#container-hooks<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle.postStart
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlifecycle)</sup></sup>



PostStart is called immediately after a container is created. If the handler fails,
the container is terminated and restarted according to its restart policy.
Other management of the container blocks until the hook completes.
More info: https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/#container-hooks

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecyclepoststartexec">exec</a></b></td>
        <td>object</td>
        <td>
          Exec specifies a command to execute in the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecyclepoststarthttpget">httpGet</a></b></td>
        <td>object</td>
        <td>
          HTTPGet specifies an HTTP GET request to perform.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecyclepoststartsleep">sleep</a></b></td>
        <td>object</td>
        <td>
          Sleep represents a duration that the container should sleep.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecyclepoststarttcpsocket">tcpSocket</a></b></td>
        <td>object</td>
        <td>
          Deprecated. TCPSocket is NOT supported as a LifecycleHandler and kept
for backward compatibility. There is no validation of this field and
lifecycle hooks will fail at runtime when it is specified.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle.postStart.exec
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlifecyclepoststart)</sup></sup>



Exec specifies a command to execute in the container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>command</b></td>
        <td>[]string</td>
        <td>
          Command is the command line to execute inside the container, the working directory for the
command  is root ('/') in the container's filesystem. The command is simply exec'd, it is
not run inside a shell, so traditional shell instructions ('|', etc) won't work. To use
a shell, you need to explicitly call out to that shell.
Exit status of 0 is treated as live/healthy and non-zero is unhealthy.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle.postStart.httpGet
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlifecyclepoststart)</sup></sup>



HTTPGet specifies an HTTP GET request to perform.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Name or number of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Host name to connect to, defaults to the pod IP. You probably want to set
"Host" in httpHeaders instead.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecyclepoststarthttpgethttpheadersindex">httpHeaders</a></b></td>
        <td>[]object</td>
        <td>
          Custom headers to set in the request. HTTP allows repeated headers.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>path</b></td>
        <td>string</td>
        <td>
          Path to access on the HTTP server.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>scheme</b></td>
        <td>string</td>
        <td>
          Scheme to use for connecting to the host.
Defaults to HTTP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle.postStart.httpGet.httpHeaders[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlifecyclepoststarthttpget)</sup></sup>



HTTPHeader describes a custom header to be used in HTTP probes

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          The header field name.
This will be canonicalized upon output, so case-variant names will be understood as the same header.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          The header field value<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle.postStart.sleep
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlifecyclepoststart)</sup></sup>



Sleep represents a duration that the container should sleep.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>seconds</b></td>
        <td>integer</td>
        <td>
          Seconds is the number of seconds to sleep.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle.postStart.tcpSocket
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlifecyclepoststart)</sup></sup>



Deprecated. TCPSocket is NOT supported as a LifecycleHandler and kept
for backward compatibility. There is no validation of this field and
lifecycle hooks will fail at runtime when it is specified.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Number or name of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Optional: Host name to connect to, defaults to the pod IP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle.preStop
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlifecycle)</sup></sup>



PreStop is called immediately before a container is terminated due to an
API request or management event such as liveness/startup probe failure,
preemption, resource contention, etc. The handler is not called if the
container crashes or exits. The Pod's termination grace period countdown begins before the
PreStop hook is executed. Regardless of the outcome of the handler, the
container will eventually terminate within the Pod's termination grace
period (unless delayed by finalizers). Other management of the container blocks until the hook completes
or until the termination grace period is reached.
More info: https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/#container-hooks

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecycleprestopexec">exec</a></b></td>
        <td>object</td>
        <td>
          Exec specifies a command to execute in the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecycleprestophttpget">httpGet</a></b></td>
        <td>object</td>
        <td>
          HTTPGet specifies an HTTP GET request to perform.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecycleprestopsleep">sleep</a></b></td>
        <td>object</td>
        <td>
          Sleep represents a duration that the container should sleep.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecycleprestoptcpsocket">tcpSocket</a></b></td>
        <td>object</td>
        <td>
          Deprecated. TCPSocket is NOT supported as a LifecycleHandler and kept
for backward compatibility. There is no validation of this field and
lifecycle hooks will fail at runtime when it is specified.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle.preStop.exec
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlifecycleprestop)</sup></sup>



Exec specifies a command to execute in the container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>command</b></td>
        <td>[]string</td>
        <td>
          Command is the command line to execute inside the container, the working directory for the
command  is root ('/') in the container's filesystem. The command is simply exec'd, it is
not run inside a shell, so traditional shell instructions ('|', etc) won't work. To use
a shell, you need to explicitly call out to that shell.
Exit status of 0 is treated as live/healthy and non-zero is unhealthy.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle.preStop.httpGet
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlifecycleprestop)</sup></sup>



HTTPGet specifies an HTTP GET request to perform.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Name or number of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Host name to connect to, defaults to the pod IP. You probably want to set
"Host" in httpHeaders instead.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlifecycleprestophttpgethttpheadersindex">httpHeaders</a></b></td>
        <td>[]object</td>
        <td>
          Custom headers to set in the request. HTTP allows repeated headers.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>path</b></td>
        <td>string</td>
        <td>
          Path to access on the HTTP server.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>scheme</b></td>
        <td>string</td>
        <td>
          Scheme to use for connecting to the host.
Defaults to HTTP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle.preStop.httpGet.httpHeaders[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlifecycleprestophttpget)</sup></sup>



HTTPHeader describes a custom header to be used in HTTP probes

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          The header field name.
This will be canonicalized upon output, so case-variant names will be understood as the same header.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          The header field value<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle.preStop.sleep
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlifecycleprestop)</sup></sup>



Sleep represents a duration that the container should sleep.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>seconds</b></td>
        <td>integer</td>
        <td>
          Seconds is the number of seconds to sleep.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].lifecycle.preStop.tcpSocket
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlifecycleprestop)</sup></sup>



Deprecated. TCPSocket is NOT supported as a LifecycleHandler and kept
for backward compatibility. There is no validation of this field and
lifecycle hooks will fail at runtime when it is specified.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Number or name of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Optional: Host name to connect to, defaults to the pod IP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].livenessProbe
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindex)</sup></sup>



Periodic probe of container liveness.
Container will be restarted if the probe fails.
Cannot be updated.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlivenessprobeexec">exec</a></b></td>
        <td>object</td>
        <td>
          Exec specifies a command to execute in the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>failureThreshold</b></td>
        <td>integer</td>
        <td>
          Minimum consecutive failures for the probe to be considered failed after having succeeded.
Defaults to 3. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlivenessprobegrpc">grpc</a></b></td>
        <td>object</td>
        <td>
          GRPC specifies a GRPC HealthCheckRequest.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlivenessprobehttpget">httpGet</a></b></td>
        <td>object</td>
        <td>
          HTTPGet specifies an HTTP GET request to perform.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>initialDelaySeconds</b></td>
        <td>integer</td>
        <td>
          Number of seconds after the container has started before liveness probes are initiated.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>periodSeconds</b></td>
        <td>integer</td>
        <td>
          How often (in seconds) to perform the probe.
Default to 10 seconds. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>successThreshold</b></td>
        <td>integer</td>
        <td>
          Minimum consecutive successes for the probe to be considered successful after having failed.
Defaults to 1. Must be 1 for liveness and startup. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlivenessprobetcpsocket">tcpSocket</a></b></td>
        <td>object</td>
        <td>
          TCPSocket specifies a connection to a TCP port.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>terminationGracePeriodSeconds</b></td>
        <td>integer</td>
        <td>
          Optional duration in seconds the pod needs to terminate gracefully upon probe failure.
The grace period is the duration in seconds after the processes running in the pod are sent
a termination signal and the time when the processes are forcibly halted with a kill signal.
Set this value longer than the expected cleanup time for your process.
If this value is nil, the pod's terminationGracePeriodSeconds will be used. Otherwise, this
value overrides the value provided by the pod spec.
Value must be non-negative integer. The value zero indicates stop immediately via
the kill signal (no opportunity to shut down).
This is a beta field and requires enabling ProbeTerminationGracePeriod feature gate.
Minimum value is 1. spec.terminationGracePeriodSeconds is used if unset.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>timeoutSeconds</b></td>
        <td>integer</td>
        <td>
          Number of seconds after which the probe times out.
Defaults to 1 second. Minimum value is 1.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].livenessProbe.exec
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlivenessprobe)</sup></sup>



Exec specifies a command to execute in the container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>command</b></td>
        <td>[]string</td>
        <td>
          Command is the command line to execute inside the container, the working directory for the
command  is root ('/') in the container's filesystem. The command is simply exec'd, it is
not run inside a shell, so traditional shell instructions ('|', etc) won't work. To use
a shell, you need to explicitly call out to that shell.
Exit status of 0 is treated as live/healthy and non-zero is unhealthy.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].livenessProbe.grpc
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlivenessprobe)</sup></sup>



GRPC specifies a GRPC HealthCheckRequest.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port number of the gRPC service. Number must be in the range 1 to 65535.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>service</b></td>
        <td>string</td>
        <td>
          Service is the name of the service to place in the gRPC HealthCheckRequest
(see https://github.com/grpc/grpc/blob/master/doc/health-checking.md).

If this is not specified, the default behavior is defined by gRPC.<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].livenessProbe.httpGet
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlivenessprobe)</sup></sup>



HTTPGet specifies an HTTP GET request to perform.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Name or number of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Host name to connect to, defaults to the pod IP. You probably want to set
"Host" in httpHeaders instead.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexlivenessprobehttpgethttpheadersindex">httpHeaders</a></b></td>
        <td>[]object</td>
        <td>
          Custom headers to set in the request. HTTP allows repeated headers.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>path</b></td>
        <td>string</td>
        <td>
          Path to access on the HTTP server.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>scheme</b></td>
        <td>string</td>
        <td>
          Scheme to use for connecting to the host.
Defaults to HTTP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].livenessProbe.httpGet.httpHeaders[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlivenessprobehttpget)</sup></sup>



HTTPHeader describes a custom header to be used in HTTP probes

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          The header field name.
This will be canonicalized upon output, so case-variant names will be understood as the same header.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          The header field value<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].livenessProbe.tcpSocket
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexlivenessprobe)</sup></sup>



TCPSocket specifies a connection to a TCP port.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Number or name of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Optional: Host name to connect to, defaults to the pod IP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].ports[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindex)</sup></sup>



ContainerPort represents a network port in a single container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>containerPort</b></td>
        <td>integer</td>
        <td>
          Number of port to expose on the pod's IP address.
This must be a valid port number, 0 < x < 65536.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>hostIP</b></td>
        <td>string</td>
        <td>
          What host IP to bind the external port to.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>hostPort</b></td>
        <td>integer</td>
        <td>
          Number of port to expose on the host.
If specified, this must be a valid port number, 0 < x < 65536.
If HostNetwork is specified, this must match ContainerPort.
Most containers do not need this.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          If specified, this must be an IANA_SVC_NAME and unique within the pod. Each
named port in a pod must have a unique name. Name for the port that can be
referred to by services.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>protocol</b></td>
        <td>string</td>
        <td>
          Protocol for port. Must be UDP, TCP, or SCTP.
Defaults to "TCP".<br/>
          <br/>
            <i>Default</i>: TCP<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].readinessProbe
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindex)</sup></sup>



Periodic probe of container service readiness.
Container will be removed from service endpoints if the probe fails.
Cannot be updated.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexreadinessprobeexec">exec</a></b></td>
        <td>object</td>
        <td>
          Exec specifies a command to execute in the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>failureThreshold</b></td>
        <td>integer</td>
        <td>
          Minimum consecutive failures for the probe to be considered failed after having succeeded.
Defaults to 3. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexreadinessprobegrpc">grpc</a></b></td>
        <td>object</td>
        <td>
          GRPC specifies a GRPC HealthCheckRequest.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexreadinessprobehttpget">httpGet</a></b></td>
        <td>object</td>
        <td>
          HTTPGet specifies an HTTP GET request to perform.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>initialDelaySeconds</b></td>
        <td>integer</td>
        <td>
          Number of seconds after the container has started before liveness probes are initiated.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>periodSeconds</b></td>
        <td>integer</td>
        <td>
          How often (in seconds) to perform the probe.
Default to 10 seconds. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>successThreshold</b></td>
        <td>integer</td>
        <td>
          Minimum consecutive successes for the probe to be considered successful after having failed.
Defaults to 1. Must be 1 for liveness and startup. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexreadinessprobetcpsocket">tcpSocket</a></b></td>
        <td>object</td>
        <td>
          TCPSocket specifies a connection to a TCP port.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>terminationGracePeriodSeconds</b></td>
        <td>integer</td>
        <td>
          Optional duration in seconds the pod needs to terminate gracefully upon probe failure.
The grace period is the duration in seconds after the processes running in the pod are sent
a termination signal and the time when the processes are forcibly halted with a kill signal.
Set this value longer than the expected cleanup time for your process.
If this value is nil, the pod's terminationGracePeriodSeconds will be used. Otherwise, this
value overrides the value provided by the pod spec.
Value must be non-negative integer. The value zero indicates stop immediately via
the kill signal (no opportunity to shut down).
This is a beta field and requires enabling ProbeTerminationGracePeriod feature gate.
Minimum value is 1. spec.terminationGracePeriodSeconds is used if unset.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>timeoutSeconds</b></td>
        <td>integer</td>
        <td>
          Number of seconds after which the probe times out.
Defaults to 1 second. Minimum value is 1.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].readinessProbe.exec
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexreadinessprobe)</sup></sup>



Exec specifies a command to execute in the container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>command</b></td>
        <td>[]string</td>
        <td>
          Command is the command line to execute inside the container, the working directory for the
command  is root ('/') in the container's filesystem. The command is simply exec'd, it is
not run inside a shell, so traditional shell instructions ('|', etc) won't work. To use
a shell, you need to explicitly call out to that shell.
Exit status of 0 is treated as live/healthy and non-zero is unhealthy.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].readinessProbe.grpc
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexreadinessprobe)</sup></sup>



GRPC specifies a GRPC HealthCheckRequest.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port number of the gRPC service. Number must be in the range 1 to 65535.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>service</b></td>
        <td>string</td>
        <td>
          Service is the name of the service to place in the gRPC HealthCheckRequest
(see https://github.com/grpc/grpc/blob/master/doc/health-checking.md).

If this is not specified, the default behavior is defined by gRPC.<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].readinessProbe.httpGet
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexreadinessprobe)</sup></sup>



HTTPGet specifies an HTTP GET request to perform.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Name or number of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Host name to connect to, defaults to the pod IP. You probably want to set
"Host" in httpHeaders instead.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexreadinessprobehttpgethttpheadersindex">httpHeaders</a></b></td>
        <td>[]object</td>
        <td>
          Custom headers to set in the request. HTTP allows repeated headers.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>path</b></td>
        <td>string</td>
        <td>
          Path to access on the HTTP server.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>scheme</b></td>
        <td>string</td>
        <td>
          Scheme to use for connecting to the host.
Defaults to HTTP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].readinessProbe.httpGet.httpHeaders[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexreadinessprobehttpget)</sup></sup>



HTTPHeader describes a custom header to be used in HTTP probes

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          The header field name.
This will be canonicalized upon output, so case-variant names will be understood as the same header.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          The header field value<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].readinessProbe.tcpSocket
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexreadinessprobe)</sup></sup>



TCPSocket specifies a connection to a TCP port.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Number or name of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Optional: Host name to connect to, defaults to the pod IP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].resizePolicy[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindex)</sup></sup>



ContainerResizePolicy represents resource resize policy for the container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>resourceName</b></td>
        <td>string</td>
        <td>
          Name of the resource to which this resource resize policy applies.
Supported values: cpu, memory.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>restartPolicy</b></td>
        <td>string</td>
        <td>
          Restart policy to apply when specified resource is resized.
If not specified, it defaults to NotRequired.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].resources
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindex)</sup></sup>



Compute Resources required by this container.
Cannot be updated.
More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexresourcesclaimsindex">claims</a></b></td>
        <td>[]object</td>
        <td>
          Claims lists the names of resources, defined in spec.resourceClaims,
that are used by this container.

This is an alpha field and requires enabling the
DynamicResourceAllocation feature gate.

This field is immutable. It can only be set for containers.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>limits</b></td>
        <td>map[string]int or string</td>
        <td>
          Limits describes the maximum amount of compute resources allowed.
More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>requests</b></td>
        <td>map[string]int or string</td>
        <td>
          Requests describes the minimum amount of compute resources required.
If Requests is omitted for a container, it defaults to Limits if that is explicitly specified,
otherwise to an implementation-defined value. Requests cannot exceed Limits.
More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].resources.claims[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexresources)</sup></sup>



ResourceClaim references one entry in PodSpec.ResourceClaims.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name must match the name of one entry in pod.spec.resourceClaims of
the Pod where this field is used. It makes that resource available
inside a container.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>request</b></td>
        <td>string</td>
        <td>
          Request is the name chosen for a request in the referenced claim.
If empty, everything from the claim is made available, otherwise
only the result of this request.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].securityContext
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindex)</sup></sup>



SecurityContext defines the security options the container should be run with.
If set, the fields of SecurityContext override the equivalent fields of PodSecurityContext.
More info: https://kubernetes.io/docs/tasks/configure-pod-container/security-context/

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>allowPrivilegeEscalation</b></td>
        <td>boolean</td>
        <td>
          AllowPrivilegeEscalation controls whether a process can gain more
privileges than its parent process. This bool directly controls if
the no_new_privs flag will be set on the container process.
AllowPrivilegeEscalation is true always when the container is:
1) run as Privileged
2) has CAP_SYS_ADMIN
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexsecuritycontextapparmorprofile">appArmorProfile</a></b></td>
        <td>object</td>
        <td>
          appArmorProfile is the AppArmor options to use by this container. If set, this profile
overrides the pod's appArmorProfile.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexsecuritycontextcapabilities">capabilities</a></b></td>
        <td>object</td>
        <td>
          The capabilities to add/drop when running containers.
Defaults to the default set of capabilities granted by the container runtime.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>privileged</b></td>
        <td>boolean</td>
        <td>
          Run container in privileged mode.
Processes in privileged containers are essentially equivalent to root on the host.
Defaults to false.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>procMount</b></td>
        <td>string</td>
        <td>
          procMount denotes the type of proc mount to use for the containers.
The default value is Default which uses the container runtime defaults for
readonly paths and masked paths.
This requires the ProcMountType feature flag to be enabled.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>readOnlyRootFilesystem</b></td>
        <td>boolean</td>
        <td>
          Whether this container has a read-only root filesystem.
Default is false.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsGroup</b></td>
        <td>integer</td>
        <td>
          The GID to run the entrypoint of the container process.
Uses runtime default if unset.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsNonRoot</b></td>
        <td>boolean</td>
        <td>
          Indicates that the container must run as a non-root user.
If true, the Kubelet will validate the image at runtime to ensure that it
does not run as UID 0 (root) and fail to start the container if it does.
If unset or false, no such validation will be performed.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsUser</b></td>
        <td>integer</td>
        <td>
          The UID to run the entrypoint of the container process.
Defaults to user specified in image metadata if unspecified.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexsecuritycontextselinuxoptions">seLinuxOptions</a></b></td>
        <td>object</td>
        <td>
          The SELinux context to be applied to the container.
If unspecified, the container runtime will allocate a random SELinux context for each
container.  May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexsecuritycontextseccompprofile">seccompProfile</a></b></td>
        <td>object</td>
        <td>
          The seccomp options to use by this container. If seccomp options are
provided at both the pod & container level, the container options
override the pod options.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexsecuritycontextwindowsoptions">windowsOptions</a></b></td>
        <td>object</td>
        <td>
          The Windows specific settings applied to all containers.
If unspecified, the options from the PodSecurityContext will be used.
If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is linux.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].securityContext.appArmorProfile
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexsecuritycontext)</sup></sup>



appArmorProfile is the AppArmor options to use by this container. If set, this profile
overrides the pod's appArmorProfile.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type indicates which kind of AppArmor profile will be applied.
Valid options are:
  Localhost - a profile pre-loaded on the node.
  RuntimeDefault - the container runtime's default profile.
  Unconfined - no AppArmor enforcement.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>localhostProfile</b></td>
        <td>string</td>
        <td>
          localhostProfile indicates a profile loaded on the node that should be used.
The profile must be preconfigured on the node to work.
Must match the loaded name of the profile.
Must be set if and only if type is "Localhost".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].securityContext.capabilities
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexsecuritycontext)</sup></sup>



The capabilities to add/drop when running containers.
Defaults to the default set of capabilities granted by the container runtime.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>add</b></td>
        <td>[]string</td>
        <td>
          Added capabilities<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>drop</b></td>
        <td>[]string</td>
        <td>
          Removed capabilities<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].securityContext.seLinuxOptions
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexsecuritycontext)</sup></sup>



The SELinux context to be applied to the container.
If unspecified, the container runtime will allocate a random SELinux context for each
container.  May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>level</b></td>
        <td>string</td>
        <td>
          Level is SELinux level label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>role</b></td>
        <td>string</td>
        <td>
          Role is a SELinux role label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          Type is a SELinux type label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>user</b></td>
        <td>string</td>
        <td>
          User is a SELinux user label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].securityContext.seccompProfile
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexsecuritycontext)</sup></sup>



The seccomp options to use by this container. If seccomp options are
provided at both the pod & container level, the container options
override the pod options.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type indicates which kind of seccomp profile will be applied.
Valid options are:

Localhost - a profile defined in a file on the node should be used.
RuntimeDefault - the container runtime default profile should be used.
Unconfined - no profile should be applied.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>localhostProfile</b></td>
        <td>string</td>
        <td>
          localhostProfile indicates a profile defined in a file on the node should be used.
The profile must be preconfigured on the node to work.
Must be a descending path, relative to the kubelet's configured seccomp profile location.
Must be set if type is "Localhost". Must NOT be set for any other type.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].securityContext.windowsOptions
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexsecuritycontext)</sup></sup>



The Windows specific settings applied to all containers.
If unspecified, the options from the PodSecurityContext will be used.
If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is linux.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>gmsaCredentialSpec</b></td>
        <td>string</td>
        <td>
          GMSACredentialSpec is where the GMSA admission webhook
(https://github.com/kubernetes-sigs/windows-gmsa) inlines the contents of the
GMSA credential spec named by the GMSACredentialSpecName field.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>gmsaCredentialSpecName</b></td>
        <td>string</td>
        <td>
          GMSACredentialSpecName is the name of the GMSA credential spec to use.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>hostProcess</b></td>
        <td>boolean</td>
        <td>
          HostProcess determines if a container should be run as a 'Host Process' container.
All of a Pod's containers must have the same effective HostProcess value
(it is not allowed to have a mix of HostProcess containers and non-HostProcess containers).
In addition, if HostProcess is true then HostNetwork must also be set to true.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsUserName</b></td>
        <td>string</td>
        <td>
          The UserName in Windows to run the entrypoint of the container process.
Defaults to the user specified in image metadata if unspecified.
May also be set in PodSecurityContext. If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].startupProbe
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindex)</sup></sup>



StartupProbe indicates that the Pod has successfully initialized.
If specified, no other probes are executed until this completes successfully.
If this probe fails, the Pod will be restarted, just as if the livenessProbe failed.
This can be used to provide different probe parameters at the beginning of a Pod's lifecycle,
when it might take a long time to load data or warm a cache, than during steady-state operation.
This cannot be updated.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexstartupprobeexec">exec</a></b></td>
        <td>object</td>
        <td>
          Exec specifies a command to execute in the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>failureThreshold</b></td>
        <td>integer</td>
        <td>
          Minimum consecutive failures for the probe to be considered failed after having succeeded.
Defaults to 3. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexstartupprobegrpc">grpc</a></b></td>
        <td>object</td>
        <td>
          GRPC specifies a GRPC HealthCheckRequest.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexstartupprobehttpget">httpGet</a></b></td>
        <td>object</td>
        <td>
          HTTPGet specifies an HTTP GET request to perform.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>initialDelaySeconds</b></td>
        <td>integer</td>
        <td>
          Number of seconds after the container has started before liveness probes are initiated.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>periodSeconds</b></td>
        <td>integer</td>
        <td>
          How often (in seconds) to perform the probe.
Default to 10 seconds. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>successThreshold</b></td>
        <td>integer</td>
        <td>
          Minimum consecutive successes for the probe to be considered successful after having failed.
Defaults to 1. Must be 1 for liveness and startup. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexstartupprobetcpsocket">tcpSocket</a></b></td>
        <td>object</td>
        <td>
          TCPSocket specifies a connection to a TCP port.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>terminationGracePeriodSeconds</b></td>
        <td>integer</td>
        <td>
          Optional duration in seconds the pod needs to terminate gracefully upon probe failure.
The grace period is the duration in seconds after the processes running in the pod are sent
a termination signal and the time when the processes are forcibly halted with a kill signal.
Set this value longer than the expected cleanup time for your process.
If this value is nil, the pod's terminationGracePeriodSeconds will be used. Otherwise, this
value overrides the value provided by the pod spec.
Value must be non-negative integer. The value zero indicates stop immediately via
the kill signal (no opportunity to shut down).
This is a beta field and requires enabling ProbeTerminationGracePeriod feature gate.
Minimum value is 1. spec.terminationGracePeriodSeconds is used if unset.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>timeoutSeconds</b></td>
        <td>integer</td>
        <td>
          Number of seconds after which the probe times out.
Defaults to 1 second. Minimum value is 1.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].startupProbe.exec
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexstartupprobe)</sup></sup>



Exec specifies a command to execute in the container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>command</b></td>
        <td>[]string</td>
        <td>
          Command is the command line to execute inside the container, the working directory for the
command  is root ('/') in the container's filesystem. The command is simply exec'd, it is
not run inside a shell, so traditional shell instructions ('|', etc) won't work. To use
a shell, you need to explicitly call out to that shell.
Exit status of 0 is treated as live/healthy and non-zero is unhealthy.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].startupProbe.grpc
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexstartupprobe)</sup></sup>



GRPC specifies a GRPC HealthCheckRequest.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port number of the gRPC service. Number must be in the range 1 to 65535.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>service</b></td>
        <td>string</td>
        <td>
          Service is the name of the service to place in the gRPC HealthCheckRequest
(see https://github.com/grpc/grpc/blob/master/doc/health-checking.md).

If this is not specified, the default behavior is defined by gRPC.<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].startupProbe.httpGet
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexstartupprobe)</sup></sup>



HTTPGet specifies an HTTP GET request to perform.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Name or number of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Host name to connect to, defaults to the pod IP. You probably want to set
"Host" in httpHeaders instead.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistiocustomsidecarsindexstartupprobehttpgethttpheadersindex">httpHeaders</a></b></td>
        <td>[]object</td>
        <td>
          Custom headers to set in the request. HTTP allows repeated headers.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>path</b></td>
        <td>string</td>
        <td>
          Path to access on the HTTP server.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>scheme</b></td>
        <td>string</td>
        <td>
          Scheme to use for connecting to the host.
Defaults to HTTP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].startupProbe.httpGet.httpHeaders[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexstartupprobehttpget)</sup></sup>



HTTPHeader describes a custom header to be used in HTTP probes

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          The header field name.
This will be canonicalized upon output, so case-variant names will be understood as the same header.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          The header field value<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].startupProbe.tcpSocket
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindexstartupprobe)</sup></sup>



TCPSocket specifies a connection to a TCP port.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Number or name of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Optional: Host name to connect to, defaults to the pod IP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].volumeDevices[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindex)</sup></sup>



volumeDevice describes a mapping of a raw block device within a container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>devicePath</b></td>
        <td>string</td>
        <td>
          devicePath is the path inside of the container that the device will be mapped to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          name must match the name of a persistentVolumeClaim in the pod<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.customSidecars[index].volumeMounts[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistiocustomsidecarsindex)</sup></sup>



VolumeMount describes a mounting of a Volume within a container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>mountPath</b></td>
        <td>string</td>
        <td>
          Path within the container at which the volume should be mounted.  Must
not contain ':'.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          This must match the Name of a Volume.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>mountPropagation</b></td>
        <td>string</td>
        <td>
          mountPropagation determines how mounts are propagated from the host
to container and the other way around.
When not set, MountPropagationNone is used.
This field is beta in 1.10.
When RecursiveReadOnly is set to IfPossible or to Enabled, MountPropagation must be None or unspecified
(which defaults to None).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>readOnly</b></td>
        <td>boolean</td>
        <td>
          Mounted read-only if true, read-write otherwise (false or unspecified).
Defaults to false.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>recursiveReadOnly</b></td>
        <td>string</td>
        <td>
          RecursiveReadOnly specifies whether read-only mounts should be handled
recursively.

If ReadOnly is false, this field has no meaning and must be unspecified.

If ReadOnly is true, and this field is set to Disabled, the mount is not made
recursively read-only.  If this field is set to IfPossible, the mount is made
recursively read-only, if it is supported by the container runtime.  If this
field is set to Enabled, the mount is made recursively read-only if it is
supported by the container runtime, otherwise the pod will not be started and
an error will be generated to indicate the reason.

If this field is set to IfPossible or Enabled, MountPropagation must be set to
None (or be unspecified, which defaults to None).

If this field is not specified, it is treated as an equivalent of Disabled.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>subPath</b></td>
        <td>string</td>
        <td>
          Path within the volume from which the container's volume should be mounted.
Defaults to "" (volume's root).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>subPathExpr</b></td>
        <td>string</td>
        <td>
          Expanded path within the volume from which the container's volume should be mounted.
Behaves similarly to SubPath but environment variable references $(VAR_NAME) are expanded using the container's environment.
Defaults to "" (volume's root).
SubPathExpr and SubPath are mutually exclusive.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.istioProxyContainer
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistio)</sup></sup>



Configuration for the container running istio-proxy.
Note that if Istio integration is not enabled, the istio container will not be injected
into the gateway proxy deployment.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeistioistioproxycontainerimage">image</a></b></td>
        <td>object</td>
        <td>
          The envoy container image. See
https://kubernetes.io/docs/concepts/containers/images
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>istioDiscoveryAddress</b></td>
        <td>string</td>
        <td>
          The address of the istio discovery service. Defaults to "istiod.istio-system.svc:15012".<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>istioMetaClusterId</b></td>
        <td>string</td>
        <td>
          The cluster id of the istio cluster. Defaults to "Kubernetes".<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>istioMetaMeshId</b></td>
        <td>string</td>
        <td>
          The mesh id of the istio mesh. Defaults to "cluster.local".<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>logLevel</b></td>
        <td>string</td>
        <td>
          Log level for istio-proxy. Options include "info", "debug", "warning", and "error".
Default level is info Default is "warning".<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistioistioproxycontainerresources">resources</a></b></td>
        <td>object</td>
        <td>
          The compute resources required by this container. See
https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistioistioproxycontainersecuritycontext">securityContext</a></b></td>
        <td>object</td>
        <td>
          The security context for this container. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core
for details.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.istioProxyContainer.image
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistioistioproxycontainer)</sup></sup>



The envoy container image. See
https://kubernetes.io/docs/concepts/containers/images
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>digest</b></td>
        <td>string</td>
        <td>
          The hash digest of the image, e.g. `sha256:12345...`<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>pullPolicy</b></td>
        <td>string</td>
        <td>
          The image pull policy for the container. See
https://kubernetes.io/docs/concepts/containers/images/#image-pull-policy
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>registry</b></td>
        <td>string</td>
        <td>
          The image registry.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>repository</b></td>
        <td>string</td>
        <td>
          The image repository (name).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>tag</b></td>
        <td>string</td>
        <td>
          The image tag.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.istioProxyContainer.resources
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistioistioproxycontainer)</sup></sup>



The compute resources required by this container. See
https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubeistioistioproxycontainerresourcesclaimsindex">claims</a></b></td>
        <td>[]object</td>
        <td>
          Claims lists the names of resources, defined in spec.resourceClaims,
that are used by this container.

This is an alpha field and requires enabling the
DynamicResourceAllocation feature gate.

This field is immutable. It can only be set for containers.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>limits</b></td>
        <td>map[string]int or string</td>
        <td>
          Limits describes the maximum amount of compute resources allowed.
More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>requests</b></td>
        <td>map[string]int or string</td>
        <td>
          Requests describes the minimum amount of compute resources required.
If Requests is omitted for a container, it defaults to Limits if that is explicitly specified,
otherwise to an implementation-defined value. Requests cannot exceed Limits.
More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.istioProxyContainer.resources.claims[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistioistioproxycontainerresources)</sup></sup>



ResourceClaim references one entry in PodSpec.ResourceClaims.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name must match the name of one entry in pod.spec.resourceClaims of
the Pod where this field is used. It makes that resource available
inside a container.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>request</b></td>
        <td>string</td>
        <td>
          Request is the name chosen for a request in the referenced claim.
If empty, everything from the claim is made available, otherwise
only the result of this request.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.istioProxyContainer.securityContext
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistioistioproxycontainer)</sup></sup>



The security context for this container. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>allowPrivilegeEscalation</b></td>
        <td>boolean</td>
        <td>
          AllowPrivilegeEscalation controls whether a process can gain more
privileges than its parent process. This bool directly controls if
the no_new_privs flag will be set on the container process.
AllowPrivilegeEscalation is true always when the container is:
1) run as Privileged
2) has CAP_SYS_ADMIN
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistioistioproxycontainersecuritycontextapparmorprofile">appArmorProfile</a></b></td>
        <td>object</td>
        <td>
          appArmorProfile is the AppArmor options to use by this container. If set, this profile
overrides the pod's appArmorProfile.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistioistioproxycontainersecuritycontextcapabilities">capabilities</a></b></td>
        <td>object</td>
        <td>
          The capabilities to add/drop when running containers.
Defaults to the default set of capabilities granted by the container runtime.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>privileged</b></td>
        <td>boolean</td>
        <td>
          Run container in privileged mode.
Processes in privileged containers are essentially equivalent to root on the host.
Defaults to false.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>procMount</b></td>
        <td>string</td>
        <td>
          procMount denotes the type of proc mount to use for the containers.
The default value is Default which uses the container runtime defaults for
readonly paths and masked paths.
This requires the ProcMountType feature flag to be enabled.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>readOnlyRootFilesystem</b></td>
        <td>boolean</td>
        <td>
          Whether this container has a read-only root filesystem.
Default is false.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsGroup</b></td>
        <td>integer</td>
        <td>
          The GID to run the entrypoint of the container process.
Uses runtime default if unset.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsNonRoot</b></td>
        <td>boolean</td>
        <td>
          Indicates that the container must run as a non-root user.
If true, the Kubelet will validate the image at runtime to ensure that it
does not run as UID 0 (root) and fail to start the container if it does.
If unset or false, no such validation will be performed.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsUser</b></td>
        <td>integer</td>
        <td>
          The UID to run the entrypoint of the container process.
Defaults to user specified in image metadata if unspecified.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistioistioproxycontainersecuritycontextselinuxoptions">seLinuxOptions</a></b></td>
        <td>object</td>
        <td>
          The SELinux context to be applied to the container.
If unspecified, the container runtime will allocate a random SELinux context for each
container.  May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistioistioproxycontainersecuritycontextseccompprofile">seccompProfile</a></b></td>
        <td>object</td>
        <td>
          The seccomp options to use by this container. If seccomp options are
provided at both the pod & container level, the container options
override the pod options.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubeistioistioproxycontainersecuritycontextwindowsoptions">windowsOptions</a></b></td>
        <td>object</td>
        <td>
          The Windows specific settings applied to all containers.
If unspecified, the options from the PodSecurityContext will be used.
If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is linux.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.istioProxyContainer.securityContext.appArmorProfile
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistioistioproxycontainersecuritycontext)</sup></sup>



appArmorProfile is the AppArmor options to use by this container. If set, this profile
overrides the pod's appArmorProfile.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type indicates which kind of AppArmor profile will be applied.
Valid options are:
  Localhost - a profile pre-loaded on the node.
  RuntimeDefault - the container runtime's default profile.
  Unconfined - no AppArmor enforcement.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>localhostProfile</b></td>
        <td>string</td>
        <td>
          localhostProfile indicates a profile loaded on the node that should be used.
The profile must be preconfigured on the node to work.
Must match the loaded name of the profile.
Must be set if and only if type is "Localhost".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.istioProxyContainer.securityContext.capabilities
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistioistioproxycontainersecuritycontext)</sup></sup>



The capabilities to add/drop when running containers.
Defaults to the default set of capabilities granted by the container runtime.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>add</b></td>
        <td>[]string</td>
        <td>
          Added capabilities<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>drop</b></td>
        <td>[]string</td>
        <td>
          Removed capabilities<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.istioProxyContainer.securityContext.seLinuxOptions
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistioistioproxycontainersecuritycontext)</sup></sup>



The SELinux context to be applied to the container.
If unspecified, the container runtime will allocate a random SELinux context for each
container.  May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>level</b></td>
        <td>string</td>
        <td>
          Level is SELinux level label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>role</b></td>
        <td>string</td>
        <td>
          Role is a SELinux role label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          Type is a SELinux type label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>user</b></td>
        <td>string</td>
        <td>
          User is a SELinux user label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.istioProxyContainer.securityContext.seccompProfile
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistioistioproxycontainersecuritycontext)</sup></sup>



The seccomp options to use by this container. If seccomp options are
provided at both the pod & container level, the container options
override the pod options.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type indicates which kind of seccomp profile will be applied.
Valid options are:

Localhost - a profile defined in a file on the node should be used.
RuntimeDefault - the container runtime default profile should be used.
Unconfined - no profile should be applied.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>localhostProfile</b></td>
        <td>string</td>
        <td>
          localhostProfile indicates a profile defined in a file on the node should be used.
The profile must be preconfigured on the node to work.
Must be a descending path, relative to the kubelet's configured seccomp profile location.
Must be set if type is "Localhost". Must NOT be set for any other type.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.istio.istioProxyContainer.securityContext.windowsOptions
<sup><sup>[↩ Parent](#gatewayparametersspeckubeistioistioproxycontainersecuritycontext)</sup></sup>



The Windows specific settings applied to all containers.
If unspecified, the options from the PodSecurityContext will be used.
If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is linux.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>gmsaCredentialSpec</b></td>
        <td>string</td>
        <td>
          GMSACredentialSpec is where the GMSA admission webhook
(https://github.com/kubernetes-sigs/windows-gmsa) inlines the contents of the
GMSA credential spec named by the GMSACredentialSpecName field.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>gmsaCredentialSpecName</b></td>
        <td>string</td>
        <td>
          GMSACredentialSpecName is the name of the GMSA credential spec to use.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>hostProcess</b></td>
        <td>boolean</td>
        <td>
          HostProcess determines if a container should be run as a 'Host Process' container.
All of a Pod's containers must have the same effective HostProcess value
(it is not allowed to have a mix of HostProcess containers and non-HostProcess containers).
In addition, if HostProcess is true then HostNetwork must also be set to true.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsUserName</b></td>
        <td>string</td>
        <td>
          The UserName in Windows to run the entrypoint of the container process.
Defaults to the user specified in image metadata if unspecified.
May also be set in PodSecurityContext. If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate
<sup><sup>[↩ Parent](#gatewayparametersspeckube)</sup></sup>



Configuration for the pods that will be created.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinity">affinity</a></b></td>
        <td>object</td>
        <td>
          If specified, the pod's scheduling constraints. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#affinity-v1-core
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>extraAnnotations</b></td>
        <td>map[string]string</td>
        <td>
          Additional annotations to add to the Pod object metadata.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>extraLabels</b></td>
        <td>map[string]string</td>
        <td>
          Additional labels to add to the Pod object metadata.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplategracefulshutdown">gracefulShutdown</a></b></td>
        <td>object</td>
        <td>
          If specified, the pod's graceful shutdown spec.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateimagepullsecretsindex">imagePullSecrets</a></b></td>
        <td>[]object</td>
        <td>
          An optional list of references to secrets in the same namespace to use for
pulling any of the images used by this Pod spec. See
https://kubernetes.io/docs/concepts/containers/images/#specifying-imagepullsecrets-on-a-pod
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatelivenessprobe">livenessProbe</a></b></td>
        <td>object</td>
        <td>
          If specified, the pod's liveness probe. Periodic probe of container service readiness.
Container will be restarted if the probe fails. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#probe-v1-core
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>nodeSelector</b></td>
        <td>map[string]string</td>
        <td>
          A selector which must be true for the pod to fit on a node. See
https://kubernetes.io/docs/concepts/configuration/assign-pod-node/ for
details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatereadinessprobe">readinessProbe</a></b></td>
        <td>object</td>
        <td>
          If specified, the pod's readiness probe. Periodic probe of container service readiness.
Container will be removed from service endpoints if the probe fails. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#probe-v1-core
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatesecuritycontext">securityContext</a></b></td>
        <td>object</td>
        <td>
          The pod security context. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#podsecuritycontext-v1-core
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>terminationGracePeriodSeconds</b></td>
        <td>integer</td>
        <td>
          If specified, the pod's termination grace period in seconds. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#pod-v1-core
for details<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatetolerationsindex">tolerations</a></b></td>
        <td>[]object</td>
        <td>
          do not use slice of pointers: https://github.com/kubernetes/code-generator/issues/166
If specified, the pod's tolerations. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#toleration-v1-core
for details.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplate)</sup></sup>



If specified, the pod's scheduling constraints. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#affinity-v1-core
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitynodeaffinity">nodeAffinity</a></b></td>
        <td>object</td>
        <td>
          Describes node affinity scheduling rules for the pod.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodaffinity">podAffinity</a></b></td>
        <td>object</td>
        <td>
          Describes pod affinity scheduling rules (e.g. co-locate this pod in the same node, zone, etc. as some other pod(s)).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodantiaffinity">podAntiAffinity</a></b></td>
        <td>object</td>
        <td>
          Describes pod anti-affinity scheduling rules (e.g. avoid putting this pod in the same node, zone, etc. as some other pod(s)).<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.nodeAffinity
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinity)</sup></sup>



Describes node affinity scheduling rules for the pod.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitynodeaffinitypreferredduringschedulingignoredduringexecutionindex">preferredDuringSchedulingIgnoredDuringExecution</a></b></td>
        <td>[]object</td>
        <td>
          The scheduler will prefer to schedule pods to nodes that satisfy
the affinity expressions specified by this field, but it may choose
a node that violates one or more of the expressions. The node that is
most preferred is the one with the greatest sum of weights, i.e.
for each node that meets all of the scheduling requirements (resource
request, requiredDuringScheduling affinity expressions, etc.),
compute a sum by iterating through the elements of this field and adding
"weight" to the sum if the node matches the corresponding matchExpressions; the
node(s) with the highest sum are the most preferred.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitynodeaffinityrequiredduringschedulingignoredduringexecution">requiredDuringSchedulingIgnoredDuringExecution</a></b></td>
        <td>object</td>
        <td>
          If the affinity requirements specified by this field are not met at
scheduling time, the pod will not be scheduled onto the node.
If the affinity requirements specified by this field cease to be met
at some point during pod execution (e.g. due to an update), the system
may or may not try to eventually evict the pod from its node.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.nodeAffinity.preferredDuringSchedulingIgnoredDuringExecution[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitynodeaffinity)</sup></sup>



An empty preferred scheduling term matches all objects with implicit weight 0
(i.e. it's a no-op). A null preferred scheduling term matches no objects (i.e. is also a no-op).

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitynodeaffinitypreferredduringschedulingignoredduringexecutionindexpreference">preference</a></b></td>
        <td>object</td>
        <td>
          A node selector term, associated with the corresponding weight.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>weight</b></td>
        <td>integer</td>
        <td>
          Weight associated with matching the corresponding nodeSelectorTerm, in the range 1-100.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.nodeAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].preference
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitynodeaffinitypreferredduringschedulingignoredduringexecutionindex)</sup></sup>



A node selector term, associated with the corresponding weight.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitynodeaffinitypreferredduringschedulingignoredduringexecutionindexpreferencematchexpressionsindex">matchExpressions</a></b></td>
        <td>[]object</td>
        <td>
          A list of node selector requirements by node's labels.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitynodeaffinitypreferredduringschedulingignoredduringexecutionindexpreferencematchfieldsindex">matchFields</a></b></td>
        <td>[]object</td>
        <td>
          A list of node selector requirements by node's fields.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.nodeAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].preference.matchExpressions[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitynodeaffinitypreferredduringschedulingignoredduringexecutionindexpreference)</sup></sup>



A node selector requirement is a selector that contains values, a key, and an operator
that relates the key and values.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          The label key that the selector applies to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          Represents a key's relationship to a set of values.
Valid operators are In, NotIn, Exists, DoesNotExist. Gt, and Lt.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>values</b></td>
        <td>[]string</td>
        <td>
          An array of string values. If the operator is In or NotIn,
the values array must be non-empty. If the operator is Exists or DoesNotExist,
the values array must be empty. If the operator is Gt or Lt, the values
array must have a single element, which will be interpreted as an integer.
This array is replaced during a strategic merge patch.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.nodeAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].preference.matchFields[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitynodeaffinitypreferredduringschedulingignoredduringexecutionindexpreference)</sup></sup>



A node selector requirement is a selector that contains values, a key, and an operator
that relates the key and values.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          The label key that the selector applies to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          Represents a key's relationship to a set of values.
Valid operators are In, NotIn, Exists, DoesNotExist. Gt, and Lt.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>values</b></td>
        <td>[]string</td>
        <td>
          An array of string values. If the operator is In or NotIn,
the values array must be non-empty. If the operator is Exists or DoesNotExist,
the values array must be empty. If the operator is Gt or Lt, the values
array must have a single element, which will be interpreted as an integer.
This array is replaced during a strategic merge patch.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitynodeaffinity)</sup></sup>



If the affinity requirements specified by this field are not met at
scheduling time, the pod will not be scheduled onto the node.
If the affinity requirements specified by this field cease to be met
at some point during pod execution (e.g. due to an update), the system
may or may not try to eventually evict the pod from its node.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitynodeaffinityrequiredduringschedulingignoredduringexecutionnodeselectortermsindex">nodeSelectorTerms</a></b></td>
        <td>[]object</td>
        <td>
          Required. A list of node selector terms. The terms are ORed.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitynodeaffinityrequiredduringschedulingignoredduringexecution)</sup></sup>



A null or empty node selector term matches no objects. The requirements of
them are ANDed.
The TopologySelectorTerm type implements a subset of the NodeSelectorTerm.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitynodeaffinityrequiredduringschedulingignoredduringexecutionnodeselectortermsindexmatchexpressionsindex">matchExpressions</a></b></td>
        <td>[]object</td>
        <td>
          A list of node selector requirements by node's labels.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitynodeaffinityrequiredduringschedulingignoredduringexecutionnodeselectortermsindexmatchfieldsindex">matchFields</a></b></td>
        <td>[]object</td>
        <td>
          A list of node selector requirements by node's fields.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[index].matchExpressions[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitynodeaffinityrequiredduringschedulingignoredduringexecutionnodeselectortermsindex)</sup></sup>



A node selector requirement is a selector that contains values, a key, and an operator
that relates the key and values.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          The label key that the selector applies to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          Represents a key's relationship to a set of values.
Valid operators are In, NotIn, Exists, DoesNotExist. Gt, and Lt.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>values</b></td>
        <td>[]string</td>
        <td>
          An array of string values. If the operator is In or NotIn,
the values array must be non-empty. If the operator is Exists or DoesNotExist,
the values array must be empty. If the operator is Gt or Lt, the values
array must have a single element, which will be interpreted as an integer.
This array is replaced during a strategic merge patch.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[index].matchFields[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitynodeaffinityrequiredduringschedulingignoredduringexecutionnodeselectortermsindex)</sup></sup>



A node selector requirement is a selector that contains values, a key, and an operator
that relates the key and values.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          The label key that the selector applies to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          Represents a key's relationship to a set of values.
Valid operators are In, NotIn, Exists, DoesNotExist. Gt, and Lt.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>values</b></td>
        <td>[]string</td>
        <td>
          An array of string values. If the operator is In or NotIn,
the values array must be non-empty. If the operator is Exists or DoesNotExist,
the values array must be empty. If the operator is Gt or Lt, the values
array must have a single element, which will be interpreted as an integer.
This array is replaced during a strategic merge patch.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAffinity
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinity)</sup></sup>



Describes pod affinity scheduling rules (e.g. co-locate this pod in the same node, zone, etc. as some other pod(s)).

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodaffinitypreferredduringschedulingignoredduringexecutionindex">preferredDuringSchedulingIgnoredDuringExecution</a></b></td>
        <td>[]object</td>
        <td>
          The scheduler will prefer to schedule pods to nodes that satisfy
the affinity expressions specified by this field, but it may choose
a node that violates one or more of the expressions. The node that is
most preferred is the one with the greatest sum of weights, i.e.
for each node that meets all of the scheduling requirements (resource
request, requiredDuringScheduling affinity expressions, etc.),
compute a sum by iterating through the elements of this field and adding
"weight" to the sum if the node has pods which matches the corresponding podAffinityTerm; the
node(s) with the highest sum are the most preferred.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodaffinityrequiredduringschedulingignoredduringexecutionindex">requiredDuringSchedulingIgnoredDuringExecution</a></b></td>
        <td>[]object</td>
        <td>
          If the affinity requirements specified by this field are not met at
scheduling time, the pod will not be scheduled onto the node.
If the affinity requirements specified by this field cease to be met
at some point during pod execution (e.g. due to a pod label update), the
system may or may not try to eventually evict the pod from its node.
When there are multiple elements, the lists of nodes corresponding to each
podAffinityTerm are intersected, i.e. all terms must be satisfied.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAffinity.preferredDuringSchedulingIgnoredDuringExecution[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodaffinity)</sup></sup>



The weights of all of the matched WeightedPodAffinityTerm fields are added per-node to find the most preferred node(s)

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinityterm">podAffinityTerm</a></b></td>
        <td>object</td>
        <td>
          Required. A pod affinity term, associated with the corresponding weight.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>weight</b></td>
        <td>integer</td>
        <td>
          weight associated with matching the corresponding podAffinityTerm,
in the range 1-100.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].podAffinityTerm
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodaffinitypreferredduringschedulingignoredduringexecutionindex)</sup></sup>



Required. A pod affinity term, associated with the corresponding weight.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>topologyKey</b></td>
        <td>string</td>
        <td>
          This pod should be co-located (affinity) or not co-located (anti-affinity) with the pods matching
the labelSelector in the specified namespaces, where co-located is defined as running on a node
whose value of the label with key topologyKey matches that of any node on which any of the
selected pods is running.
Empty topologyKey is not allowed.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinitytermlabelselector">labelSelector</a></b></td>
        <td>object</td>
        <td>
          A label query over a set of resources, in this case pods.
If it's null, this PodAffinityTerm matches with no Pods.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>matchLabelKeys</b></td>
        <td>[]string</td>
        <td>
          MatchLabelKeys is a set of pod label keys to select which pods will
be taken into consideration. The keys are used to lookup values from the
incoming pod labels, those key-value labels are merged with `labelSelector` as `key in (value)`
to select the group of existing pods which pods will be taken into consideration
for the incoming pod's pod (anti) affinity. Keys that don't exist in the incoming
pod labels will be ignored. The default value is empty.
The same key is forbidden to exist in both matchLabelKeys and labelSelector.
Also, matchLabelKeys cannot be set when labelSelector isn't set.
This is a beta field and requires enabling MatchLabelKeysInPodAffinity feature gate (enabled by default).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>mismatchLabelKeys</b></td>
        <td>[]string</td>
        <td>
          MismatchLabelKeys is a set of pod label keys to select which pods will
be taken into consideration. The keys are used to lookup values from the
incoming pod labels, those key-value labels are merged with `labelSelector` as `key notin (value)`
to select the group of existing pods which pods will be taken into consideration
for the incoming pod's pod (anti) affinity. Keys that don't exist in the incoming
pod labels will be ignored. The default value is empty.
The same key is forbidden to exist in both mismatchLabelKeys and labelSelector.
Also, mismatchLabelKeys cannot be set when labelSelector isn't set.
This is a beta field and requires enabling MatchLabelKeysInPodAffinity feature gate (enabled by default).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinitytermnamespaceselector">namespaceSelector</a></b></td>
        <td>object</td>
        <td>
          A label query over the set of namespaces that the term applies to.
The term is applied to the union of the namespaces selected by this field
and the ones listed in the namespaces field.
null selector and null or empty namespaces list means "this pod's namespace".
An empty selector ({}) matches all namespaces.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>namespaces</b></td>
        <td>[]string</td>
        <td>
          namespaces specifies a static list of namespace names that the term applies to.
The term is applied to the union of the namespaces listed in this field
and the ones selected by namespaceSelector.
null or empty namespaces list and null namespaceSelector means "this pod's namespace".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].podAffinityTerm.labelSelector
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinityterm)</sup></sup>



A label query over a set of resources, in this case pods.
If it's null, this PodAffinityTerm matches with no Pods.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinitytermlabelselectormatchexpressionsindex">matchExpressions</a></b></td>
        <td>[]object</td>
        <td>
          matchExpressions is a list of label selector requirements. The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>matchLabels</b></td>
        <td>map[string]string</td>
        <td>
          matchLabels is a map of {key,value} pairs. A single {key,value} in the matchLabels
map is equivalent to an element of matchExpressions, whose key field is "key", the
operator is "In", and the values array contains only "value". The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].podAffinityTerm.labelSelector.matchExpressions[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinitytermlabelselector)</sup></sup>



A label selector requirement is a selector that contains values, a key, and an operator that
relates the key and values.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          key is the label key that the selector applies to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          operator represents a key's relationship to a set of values.
Valid operators are In, NotIn, Exists and DoesNotExist.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>values</b></td>
        <td>[]string</td>
        <td>
          values is an array of string values. If the operator is In or NotIn,
the values array must be non-empty. If the operator is Exists or DoesNotExist,
the values array must be empty. This array is replaced during a strategic
merge patch.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].podAffinityTerm.namespaceSelector
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinityterm)</sup></sup>



A label query over the set of namespaces that the term applies to.
The term is applied to the union of the namespaces selected by this field
and the ones listed in the namespaces field.
null selector and null or empty namespaces list means "this pod's namespace".
An empty selector ({}) matches all namespaces.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinitytermnamespaceselectormatchexpressionsindex">matchExpressions</a></b></td>
        <td>[]object</td>
        <td>
          matchExpressions is a list of label selector requirements. The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>matchLabels</b></td>
        <td>map[string]string</td>
        <td>
          matchLabels is a map of {key,value} pairs. A single {key,value} in the matchLabels
map is equivalent to an element of matchExpressions, whose key field is "key", the
operator is "In", and the values array contains only "value". The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].podAffinityTerm.namespaceSelector.matchExpressions[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinitytermnamespaceselector)</sup></sup>



A label selector requirement is a selector that contains values, a key, and an operator that
relates the key and values.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          key is the label key that the selector applies to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          operator represents a key's relationship to a set of values.
Valid operators are In, NotIn, Exists and DoesNotExist.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>values</b></td>
        <td>[]string</td>
        <td>
          values is an array of string values. If the operator is In or NotIn,
the values array must be non-empty. If the operator is Exists or DoesNotExist,
the values array must be empty. This array is replaced during a strategic
merge patch.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAffinity.requiredDuringSchedulingIgnoredDuringExecution[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodaffinity)</sup></sup>



Defines a set of pods (namely those matching the labelSelector
relative to the given namespace(s)) that this pod should be
co-located (affinity) or not co-located (anti-affinity) with,
where co-located is defined as running on a node whose value of
the label with key <topologyKey> matches that of any node on which
a pod of the set of pods is running

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>topologyKey</b></td>
        <td>string</td>
        <td>
          This pod should be co-located (affinity) or not co-located (anti-affinity) with the pods matching
the labelSelector in the specified namespaces, where co-located is defined as running on a node
whose value of the label with key topologyKey matches that of any node on which any of the
selected pods is running.
Empty topologyKey is not allowed.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodaffinityrequiredduringschedulingignoredduringexecutionindexlabelselector">labelSelector</a></b></td>
        <td>object</td>
        <td>
          A label query over a set of resources, in this case pods.
If it's null, this PodAffinityTerm matches with no Pods.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>matchLabelKeys</b></td>
        <td>[]string</td>
        <td>
          MatchLabelKeys is a set of pod label keys to select which pods will
be taken into consideration. The keys are used to lookup values from the
incoming pod labels, those key-value labels are merged with `labelSelector` as `key in (value)`
to select the group of existing pods which pods will be taken into consideration
for the incoming pod's pod (anti) affinity. Keys that don't exist in the incoming
pod labels will be ignored. The default value is empty.
The same key is forbidden to exist in both matchLabelKeys and labelSelector.
Also, matchLabelKeys cannot be set when labelSelector isn't set.
This is a beta field and requires enabling MatchLabelKeysInPodAffinity feature gate (enabled by default).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>mismatchLabelKeys</b></td>
        <td>[]string</td>
        <td>
          MismatchLabelKeys is a set of pod label keys to select which pods will
be taken into consideration. The keys are used to lookup values from the
incoming pod labels, those key-value labels are merged with `labelSelector` as `key notin (value)`
to select the group of existing pods which pods will be taken into consideration
for the incoming pod's pod (anti) affinity. Keys that don't exist in the incoming
pod labels will be ignored. The default value is empty.
The same key is forbidden to exist in both mismatchLabelKeys and labelSelector.
Also, mismatchLabelKeys cannot be set when labelSelector isn't set.
This is a beta field and requires enabling MatchLabelKeysInPodAffinity feature gate (enabled by default).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodaffinityrequiredduringschedulingignoredduringexecutionindexnamespaceselector">namespaceSelector</a></b></td>
        <td>object</td>
        <td>
          A label query over the set of namespaces that the term applies to.
The term is applied to the union of the namespaces selected by this field
and the ones listed in the namespaces field.
null selector and null or empty namespaces list means "this pod's namespace".
An empty selector ({}) matches all namespaces.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>namespaces</b></td>
        <td>[]string</td>
        <td>
          namespaces specifies a static list of namespace names that the term applies to.
The term is applied to the union of the namespaces listed in this field
and the ones selected by namespaceSelector.
null or empty namespaces list and null namespaceSelector means "this pod's namespace".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAffinity.requiredDuringSchedulingIgnoredDuringExecution[index].labelSelector
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodaffinityrequiredduringschedulingignoredduringexecutionindex)</sup></sup>



A label query over a set of resources, in this case pods.
If it's null, this PodAffinityTerm matches with no Pods.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodaffinityrequiredduringschedulingignoredduringexecutionindexlabelselectormatchexpressionsindex">matchExpressions</a></b></td>
        <td>[]object</td>
        <td>
          matchExpressions is a list of label selector requirements. The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>matchLabels</b></td>
        <td>map[string]string</td>
        <td>
          matchLabels is a map of {key,value} pairs. A single {key,value} in the matchLabels
map is equivalent to an element of matchExpressions, whose key field is "key", the
operator is "In", and the values array contains only "value". The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAffinity.requiredDuringSchedulingIgnoredDuringExecution[index].labelSelector.matchExpressions[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodaffinityrequiredduringschedulingignoredduringexecutionindexlabelselector)</sup></sup>



A label selector requirement is a selector that contains values, a key, and an operator that
relates the key and values.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          key is the label key that the selector applies to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          operator represents a key's relationship to a set of values.
Valid operators are In, NotIn, Exists and DoesNotExist.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>values</b></td>
        <td>[]string</td>
        <td>
          values is an array of string values. If the operator is In or NotIn,
the values array must be non-empty. If the operator is Exists or DoesNotExist,
the values array must be empty. This array is replaced during a strategic
merge patch.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAffinity.requiredDuringSchedulingIgnoredDuringExecution[index].namespaceSelector
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodaffinityrequiredduringschedulingignoredduringexecutionindex)</sup></sup>



A label query over the set of namespaces that the term applies to.
The term is applied to the union of the namespaces selected by this field
and the ones listed in the namespaces field.
null selector and null or empty namespaces list means "this pod's namespace".
An empty selector ({}) matches all namespaces.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodaffinityrequiredduringschedulingignoredduringexecutionindexnamespaceselectormatchexpressionsindex">matchExpressions</a></b></td>
        <td>[]object</td>
        <td>
          matchExpressions is a list of label selector requirements. The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>matchLabels</b></td>
        <td>map[string]string</td>
        <td>
          matchLabels is a map of {key,value} pairs. A single {key,value} in the matchLabels
map is equivalent to an element of matchExpressions, whose key field is "key", the
operator is "In", and the values array contains only "value". The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAffinity.requiredDuringSchedulingIgnoredDuringExecution[index].namespaceSelector.matchExpressions[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodaffinityrequiredduringschedulingignoredduringexecutionindexnamespaceselector)</sup></sup>



A label selector requirement is a selector that contains values, a key, and an operator that
relates the key and values.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          key is the label key that the selector applies to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          operator represents a key's relationship to a set of values.
Valid operators are In, NotIn, Exists and DoesNotExist.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>values</b></td>
        <td>[]string</td>
        <td>
          values is an array of string values. If the operator is In or NotIn,
the values array must be non-empty. If the operator is Exists or DoesNotExist,
the values array must be empty. This array is replaced during a strategic
merge patch.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAntiAffinity
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinity)</sup></sup>



Describes pod anti-affinity scheduling rules (e.g. avoid putting this pod in the same node, zone, etc. as some other pod(s)).

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodantiaffinitypreferredduringschedulingignoredduringexecutionindex">preferredDuringSchedulingIgnoredDuringExecution</a></b></td>
        <td>[]object</td>
        <td>
          The scheduler will prefer to schedule pods to nodes that satisfy
the anti-affinity expressions specified by this field, but it may choose
a node that violates one or more of the expressions. The node that is
most preferred is the one with the greatest sum of weights, i.e.
for each node that meets all of the scheduling requirements (resource
request, requiredDuringScheduling anti-affinity expressions, etc.),
compute a sum by iterating through the elements of this field and adding
"weight" to the sum if the node has pods which matches the corresponding podAffinityTerm; the
node(s) with the highest sum are the most preferred.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodantiaffinityrequiredduringschedulingignoredduringexecutionindex">requiredDuringSchedulingIgnoredDuringExecution</a></b></td>
        <td>[]object</td>
        <td>
          If the anti-affinity requirements specified by this field are not met at
scheduling time, the pod will not be scheduled onto the node.
If the anti-affinity requirements specified by this field cease to be met
at some point during pod execution (e.g. due to a pod label update), the
system may or may not try to eventually evict the pod from its node.
When there are multiple elements, the lists of nodes corresponding to each
podAffinityTerm are intersected, i.e. all terms must be satisfied.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAntiAffinity.preferredDuringSchedulingIgnoredDuringExecution[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodantiaffinity)</sup></sup>



The weights of all of the matched WeightedPodAffinityTerm fields are added per-node to find the most preferred node(s)

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodantiaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinityterm">podAffinityTerm</a></b></td>
        <td>object</td>
        <td>
          Required. A pod affinity term, associated with the corresponding weight.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>weight</b></td>
        <td>integer</td>
        <td>
          weight associated with matching the corresponding podAffinityTerm,
in the range 1-100.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAntiAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].podAffinityTerm
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodantiaffinitypreferredduringschedulingignoredduringexecutionindex)</sup></sup>



Required. A pod affinity term, associated with the corresponding weight.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>topologyKey</b></td>
        <td>string</td>
        <td>
          This pod should be co-located (affinity) or not co-located (anti-affinity) with the pods matching
the labelSelector in the specified namespaces, where co-located is defined as running on a node
whose value of the label with key topologyKey matches that of any node on which any of the
selected pods is running.
Empty topologyKey is not allowed.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodantiaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinitytermlabelselector">labelSelector</a></b></td>
        <td>object</td>
        <td>
          A label query over a set of resources, in this case pods.
If it's null, this PodAffinityTerm matches with no Pods.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>matchLabelKeys</b></td>
        <td>[]string</td>
        <td>
          MatchLabelKeys is a set of pod label keys to select which pods will
be taken into consideration. The keys are used to lookup values from the
incoming pod labels, those key-value labels are merged with `labelSelector` as `key in (value)`
to select the group of existing pods which pods will be taken into consideration
for the incoming pod's pod (anti) affinity. Keys that don't exist in the incoming
pod labels will be ignored. The default value is empty.
The same key is forbidden to exist in both matchLabelKeys and labelSelector.
Also, matchLabelKeys cannot be set when labelSelector isn't set.
This is a beta field and requires enabling MatchLabelKeysInPodAffinity feature gate (enabled by default).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>mismatchLabelKeys</b></td>
        <td>[]string</td>
        <td>
          MismatchLabelKeys is a set of pod label keys to select which pods will
be taken into consideration. The keys are used to lookup values from the
incoming pod labels, those key-value labels are merged with `labelSelector` as `key notin (value)`
to select the group of existing pods which pods will be taken into consideration
for the incoming pod's pod (anti) affinity. Keys that don't exist in the incoming
pod labels will be ignored. The default value is empty.
The same key is forbidden to exist in both mismatchLabelKeys and labelSelector.
Also, mismatchLabelKeys cannot be set when labelSelector isn't set.
This is a beta field and requires enabling MatchLabelKeysInPodAffinity feature gate (enabled by default).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodantiaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinitytermnamespaceselector">namespaceSelector</a></b></td>
        <td>object</td>
        <td>
          A label query over the set of namespaces that the term applies to.
The term is applied to the union of the namespaces selected by this field
and the ones listed in the namespaces field.
null selector and null or empty namespaces list means "this pod's namespace".
An empty selector ({}) matches all namespaces.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>namespaces</b></td>
        <td>[]string</td>
        <td>
          namespaces specifies a static list of namespace names that the term applies to.
The term is applied to the union of the namespaces listed in this field
and the ones selected by namespaceSelector.
null or empty namespaces list and null namespaceSelector means "this pod's namespace".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAntiAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].podAffinityTerm.labelSelector
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodantiaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinityterm)</sup></sup>



A label query over a set of resources, in this case pods.
If it's null, this PodAffinityTerm matches with no Pods.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodantiaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinitytermlabelselectormatchexpressionsindex">matchExpressions</a></b></td>
        <td>[]object</td>
        <td>
          matchExpressions is a list of label selector requirements. The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>matchLabels</b></td>
        <td>map[string]string</td>
        <td>
          matchLabels is a map of {key,value} pairs. A single {key,value} in the matchLabels
map is equivalent to an element of matchExpressions, whose key field is "key", the
operator is "In", and the values array contains only "value". The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAntiAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].podAffinityTerm.labelSelector.matchExpressions[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodantiaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinitytermlabelselector)</sup></sup>



A label selector requirement is a selector that contains values, a key, and an operator that
relates the key and values.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          key is the label key that the selector applies to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          operator represents a key's relationship to a set of values.
Valid operators are In, NotIn, Exists and DoesNotExist.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>values</b></td>
        <td>[]string</td>
        <td>
          values is an array of string values. If the operator is In or NotIn,
the values array must be non-empty. If the operator is Exists or DoesNotExist,
the values array must be empty. This array is replaced during a strategic
merge patch.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAntiAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].podAffinityTerm.namespaceSelector
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodantiaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinityterm)</sup></sup>



A label query over the set of namespaces that the term applies to.
The term is applied to the union of the namespaces selected by this field
and the ones listed in the namespaces field.
null selector and null or empty namespaces list means "this pod's namespace".
An empty selector ({}) matches all namespaces.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodantiaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinitytermnamespaceselectormatchexpressionsindex">matchExpressions</a></b></td>
        <td>[]object</td>
        <td>
          matchExpressions is a list of label selector requirements. The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>matchLabels</b></td>
        <td>map[string]string</td>
        <td>
          matchLabels is a map of {key,value} pairs. A single {key,value} in the matchLabels
map is equivalent to an element of matchExpressions, whose key field is "key", the
operator is "In", and the values array contains only "value". The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAntiAffinity.preferredDuringSchedulingIgnoredDuringExecution[index].podAffinityTerm.namespaceSelector.matchExpressions[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodantiaffinitypreferredduringschedulingignoredduringexecutionindexpodaffinitytermnamespaceselector)</sup></sup>



A label selector requirement is a selector that contains values, a key, and an operator that
relates the key and values.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          key is the label key that the selector applies to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          operator represents a key's relationship to a set of values.
Valid operators are In, NotIn, Exists and DoesNotExist.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>values</b></td>
        <td>[]string</td>
        <td>
          values is an array of string values. If the operator is In or NotIn,
the values array must be non-empty. If the operator is Exists or DoesNotExist,
the values array must be empty. This array is replaced during a strategic
merge patch.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodantiaffinity)</sup></sup>



Defines a set of pods (namely those matching the labelSelector
relative to the given namespace(s)) that this pod should be
co-located (affinity) or not co-located (anti-affinity) with,
where co-located is defined as running on a node whose value of
the label with key <topologyKey> matches that of any node on which
a pod of the set of pods is running

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>topologyKey</b></td>
        <td>string</td>
        <td>
          This pod should be co-located (affinity) or not co-located (anti-affinity) with the pods matching
the labelSelector in the specified namespaces, where co-located is defined as running on a node
whose value of the label with key topologyKey matches that of any node on which any of the
selected pods is running.
Empty topologyKey is not allowed.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodantiaffinityrequiredduringschedulingignoredduringexecutionindexlabelselector">labelSelector</a></b></td>
        <td>object</td>
        <td>
          A label query over a set of resources, in this case pods.
If it's null, this PodAffinityTerm matches with no Pods.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>matchLabelKeys</b></td>
        <td>[]string</td>
        <td>
          MatchLabelKeys is a set of pod label keys to select which pods will
be taken into consideration. The keys are used to lookup values from the
incoming pod labels, those key-value labels are merged with `labelSelector` as `key in (value)`
to select the group of existing pods which pods will be taken into consideration
for the incoming pod's pod (anti) affinity. Keys that don't exist in the incoming
pod labels will be ignored. The default value is empty.
The same key is forbidden to exist in both matchLabelKeys and labelSelector.
Also, matchLabelKeys cannot be set when labelSelector isn't set.
This is a beta field and requires enabling MatchLabelKeysInPodAffinity feature gate (enabled by default).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>mismatchLabelKeys</b></td>
        <td>[]string</td>
        <td>
          MismatchLabelKeys is a set of pod label keys to select which pods will
be taken into consideration. The keys are used to lookup values from the
incoming pod labels, those key-value labels are merged with `labelSelector` as `key notin (value)`
to select the group of existing pods which pods will be taken into consideration
for the incoming pod's pod (anti) affinity. Keys that don't exist in the incoming
pod labels will be ignored. The default value is empty.
The same key is forbidden to exist in both mismatchLabelKeys and labelSelector.
Also, mismatchLabelKeys cannot be set when labelSelector isn't set.
This is a beta field and requires enabling MatchLabelKeysInPodAffinity feature gate (enabled by default).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodantiaffinityrequiredduringschedulingignoredduringexecutionindexnamespaceselector">namespaceSelector</a></b></td>
        <td>object</td>
        <td>
          A label query over the set of namespaces that the term applies to.
The term is applied to the union of the namespaces selected by this field
and the ones listed in the namespaces field.
null selector and null or empty namespaces list means "this pod's namespace".
An empty selector ({}) matches all namespaces.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>namespaces</b></td>
        <td>[]string</td>
        <td>
          namespaces specifies a static list of namespace names that the term applies to.
The term is applied to the union of the namespaces listed in this field
and the ones selected by namespaceSelector.
null or empty namespaces list and null namespaceSelector means "this pod's namespace".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution[index].labelSelector
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodantiaffinityrequiredduringschedulingignoredduringexecutionindex)</sup></sup>



A label query over a set of resources, in this case pods.
If it's null, this PodAffinityTerm matches with no Pods.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodantiaffinityrequiredduringschedulingignoredduringexecutionindexlabelselectormatchexpressionsindex">matchExpressions</a></b></td>
        <td>[]object</td>
        <td>
          matchExpressions is a list of label selector requirements. The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>matchLabels</b></td>
        <td>map[string]string</td>
        <td>
          matchLabels is a map of {key,value} pairs. A single {key,value} in the matchLabels
map is equivalent to an element of matchExpressions, whose key field is "key", the
operator is "In", and the values array contains only "value". The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution[index].labelSelector.matchExpressions[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodantiaffinityrequiredduringschedulingignoredduringexecutionindexlabelselector)</sup></sup>



A label selector requirement is a selector that contains values, a key, and an operator that
relates the key and values.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          key is the label key that the selector applies to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          operator represents a key's relationship to a set of values.
Valid operators are In, NotIn, Exists and DoesNotExist.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>values</b></td>
        <td>[]string</td>
        <td>
          values is an array of string values. If the operator is In or NotIn,
the values array must be non-empty. If the operator is Exists or DoesNotExist,
the values array must be empty. This array is replaced during a strategic
merge patch.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution[index].namespaceSelector
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodantiaffinityrequiredduringschedulingignoredduringexecutionindex)</sup></sup>



A label query over the set of namespaces that the term applies to.
The term is applied to the union of the namespaces selected by this field
and the ones listed in the namespaces field.
null selector and null or empty namespaces list means "this pod's namespace".
An empty selector ({}) matches all namespaces.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplateaffinitypodantiaffinityrequiredduringschedulingignoredduringexecutionindexnamespaceselectormatchexpressionsindex">matchExpressions</a></b></td>
        <td>[]object</td>
        <td>
          matchExpressions is a list of label selector requirements. The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>matchLabels</b></td>
        <td>map[string]string</td>
        <td>
          matchLabels is a map of {key,value} pairs. A single {key,value} in the matchLabels
map is equivalent to an element of matchExpressions, whose key field is "key", the
operator is "In", and the values array contains only "value". The requirements are ANDed.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution[index].namespaceSelector.matchExpressions[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplateaffinitypodantiaffinityrequiredduringschedulingignoredduringexecutionindexnamespaceselector)</sup></sup>



A label selector requirement is a selector that contains values, a key, and an operator that
relates the key and values.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          key is the label key that the selector applies to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          operator represents a key's relationship to a set of values.
Valid operators are In, NotIn, Exists and DoesNotExist.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>values</b></td>
        <td>[]string</td>
        <td>
          values is an array of string values. If the operator is In or NotIn,
the values array must be non-empty. If the operator is Exists or DoesNotExist,
the values array must be empty. This array is replaced during a strategic
merge patch.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.gracefulShutdown
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplate)</sup></sup>



If specified, the pod's graceful shutdown spec.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>enabled</b></td>
        <td>boolean</td>
        <td>
          Enable grace period before shutdown to finish current requests while Envoy health checks fail to e.g. notify external load balancers. *NOTE:* This will not have any effect if you have not defined health checks via the health check filter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>sleepTimeSeconds</b></td>
        <td>integer</td>
        <td>
          Time (in seconds) for the preStop hook to wait before allowing Envoy to terminate<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.imagePullSecrets[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplate)</sup></sup>



LocalObjectReference contains enough information to let you locate the
referenced object inside the same namespace.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.livenessProbe
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplate)</sup></sup>



If specified, the pod's liveness probe. Periodic probe of container service readiness.
Container will be restarted if the probe fails. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#probe-v1-core
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatelivenessprobeexec">exec</a></b></td>
        <td>object</td>
        <td>
          Exec specifies a command to execute in the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>failureThreshold</b></td>
        <td>integer</td>
        <td>
          Minimum consecutive failures for the probe to be considered failed after having succeeded.
Defaults to 3. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatelivenessprobegrpc">grpc</a></b></td>
        <td>object</td>
        <td>
          GRPC specifies a GRPC HealthCheckRequest.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatelivenessprobehttpget">httpGet</a></b></td>
        <td>object</td>
        <td>
          HTTPGet specifies an HTTP GET request to perform.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>initialDelaySeconds</b></td>
        <td>integer</td>
        <td>
          Number of seconds after the container has started before liveness probes are initiated.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>periodSeconds</b></td>
        <td>integer</td>
        <td>
          How often (in seconds) to perform the probe.
Default to 10 seconds. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>successThreshold</b></td>
        <td>integer</td>
        <td>
          Minimum consecutive successes for the probe to be considered successful after having failed.
Defaults to 1. Must be 1 for liveness and startup. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatelivenessprobetcpsocket">tcpSocket</a></b></td>
        <td>object</td>
        <td>
          TCPSocket specifies a connection to a TCP port.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>terminationGracePeriodSeconds</b></td>
        <td>integer</td>
        <td>
          Optional duration in seconds the pod needs to terminate gracefully upon probe failure.
The grace period is the duration in seconds after the processes running in the pod are sent
a termination signal and the time when the processes are forcibly halted with a kill signal.
Set this value longer than the expected cleanup time for your process.
If this value is nil, the pod's terminationGracePeriodSeconds will be used. Otherwise, this
value overrides the value provided by the pod spec.
Value must be non-negative integer. The value zero indicates stop immediately via
the kill signal (no opportunity to shut down).
This is a beta field and requires enabling ProbeTerminationGracePeriod feature gate.
Minimum value is 1. spec.terminationGracePeriodSeconds is used if unset.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>timeoutSeconds</b></td>
        <td>integer</td>
        <td>
          Number of seconds after which the probe times out.
Defaults to 1 second. Minimum value is 1.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.livenessProbe.exec
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatelivenessprobe)</sup></sup>



Exec specifies a command to execute in the container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>command</b></td>
        <td>[]string</td>
        <td>
          Command is the command line to execute inside the container, the working directory for the
command  is root ('/') in the container's filesystem. The command is simply exec'd, it is
not run inside a shell, so traditional shell instructions ('|', etc) won't work. To use
a shell, you need to explicitly call out to that shell.
Exit status of 0 is treated as live/healthy and non-zero is unhealthy.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.livenessProbe.grpc
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatelivenessprobe)</sup></sup>



GRPC specifies a GRPC HealthCheckRequest.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port number of the gRPC service. Number must be in the range 1 to 65535.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>service</b></td>
        <td>string</td>
        <td>
          Service is the name of the service to place in the gRPC HealthCheckRequest
(see https://github.com/grpc/grpc/blob/master/doc/health-checking.md).

If this is not specified, the default behavior is defined by gRPC.<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.livenessProbe.httpGet
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatelivenessprobe)</sup></sup>



HTTPGet specifies an HTTP GET request to perform.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Name or number of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Host name to connect to, defaults to the pod IP. You probably want to set
"Host" in httpHeaders instead.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatelivenessprobehttpgethttpheadersindex">httpHeaders</a></b></td>
        <td>[]object</td>
        <td>
          Custom headers to set in the request. HTTP allows repeated headers.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>path</b></td>
        <td>string</td>
        <td>
          Path to access on the HTTP server.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>scheme</b></td>
        <td>string</td>
        <td>
          Scheme to use for connecting to the host.
Defaults to HTTP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.livenessProbe.httpGet.httpHeaders[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatelivenessprobehttpget)</sup></sup>



HTTPHeader describes a custom header to be used in HTTP probes

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          The header field name.
This will be canonicalized upon output, so case-variant names will be understood as the same header.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          The header field value<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.livenessProbe.tcpSocket
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatelivenessprobe)</sup></sup>



TCPSocket specifies a connection to a TCP port.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Number or name of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Optional: Host name to connect to, defaults to the pod IP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.readinessProbe
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplate)</sup></sup>



If specified, the pod's readiness probe. Periodic probe of container service readiness.
Container will be removed from service endpoints if the probe fails. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#probe-v1-core
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatereadinessprobeexec">exec</a></b></td>
        <td>object</td>
        <td>
          Exec specifies a command to execute in the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>failureThreshold</b></td>
        <td>integer</td>
        <td>
          Minimum consecutive failures for the probe to be considered failed after having succeeded.
Defaults to 3. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatereadinessprobegrpc">grpc</a></b></td>
        <td>object</td>
        <td>
          GRPC specifies a GRPC HealthCheckRequest.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatereadinessprobehttpget">httpGet</a></b></td>
        <td>object</td>
        <td>
          HTTPGet specifies an HTTP GET request to perform.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>initialDelaySeconds</b></td>
        <td>integer</td>
        <td>
          Number of seconds after the container has started before liveness probes are initiated.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>periodSeconds</b></td>
        <td>integer</td>
        <td>
          How often (in seconds) to perform the probe.
Default to 10 seconds. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>successThreshold</b></td>
        <td>integer</td>
        <td>
          Minimum consecutive successes for the probe to be considered successful after having failed.
Defaults to 1. Must be 1 for liveness and startup. Minimum value is 1.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatereadinessprobetcpsocket">tcpSocket</a></b></td>
        <td>object</td>
        <td>
          TCPSocket specifies a connection to a TCP port.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>terminationGracePeriodSeconds</b></td>
        <td>integer</td>
        <td>
          Optional duration in seconds the pod needs to terminate gracefully upon probe failure.
The grace period is the duration in seconds after the processes running in the pod are sent
a termination signal and the time when the processes are forcibly halted with a kill signal.
Set this value longer than the expected cleanup time for your process.
If this value is nil, the pod's terminationGracePeriodSeconds will be used. Otherwise, this
value overrides the value provided by the pod spec.
Value must be non-negative integer. The value zero indicates stop immediately via
the kill signal (no opportunity to shut down).
This is a beta field and requires enabling ProbeTerminationGracePeriod feature gate.
Minimum value is 1. spec.terminationGracePeriodSeconds is used if unset.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>timeoutSeconds</b></td>
        <td>integer</td>
        <td>
          Number of seconds after which the probe times out.
Defaults to 1 second. Minimum value is 1.
More info: https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle#container-probes<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.readinessProbe.exec
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatereadinessprobe)</sup></sup>



Exec specifies a command to execute in the container.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>command</b></td>
        <td>[]string</td>
        <td>
          Command is the command line to execute inside the container, the working directory for the
command  is root ('/') in the container's filesystem. The command is simply exec'd, it is
not run inside a shell, so traditional shell instructions ('|', etc) won't work. To use
a shell, you need to explicitly call out to that shell.
Exit status of 0 is treated as live/healthy and non-zero is unhealthy.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.readinessProbe.grpc
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatereadinessprobe)</sup></sup>



GRPC specifies a GRPC HealthCheckRequest.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port number of the gRPC service. Number must be in the range 1 to 65535.<br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>service</b></td>
        <td>string</td>
        <td>
          Service is the name of the service to place in the gRPC HealthCheckRequest
(see https://github.com/grpc/grpc/blob/master/doc/health-checking.md).

If this is not specified, the default behavior is defined by gRPC.<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.readinessProbe.httpGet
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatereadinessprobe)</sup></sup>



HTTPGet specifies an HTTP GET request to perform.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Name or number of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Host name to connect to, defaults to the pod IP. You probably want to set
"Host" in httpHeaders instead.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatereadinessprobehttpgethttpheadersindex">httpHeaders</a></b></td>
        <td>[]object</td>
        <td>
          Custom headers to set in the request. HTTP allows repeated headers.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>path</b></td>
        <td>string</td>
        <td>
          Path to access on the HTTP server.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>scheme</b></td>
        <td>string</td>
        <td>
          Scheme to use for connecting to the host.
Defaults to HTTP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.readinessProbe.httpGet.httpHeaders[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatereadinessprobehttpget)</sup></sup>



HTTPHeader describes a custom header to be used in HTTP probes

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          The header field name.
This will be canonicalized upon output, so case-variant names will be understood as the same header.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          The header field value<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.readinessProbe.tcpSocket
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatereadinessprobe)</sup></sup>



TCPSocket specifies a connection to a TCP port.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>port</b></td>
        <td>int or string</td>
        <td>
          Number or name of the port to access on the container.
Number must be in the range 1 to 65535.
Name must be an IANA_SVC_NAME.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Optional: Host name to connect to, defaults to the pod IP.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.securityContext
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplate)</sup></sup>



The pod security context. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#podsecuritycontext-v1-core
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatesecuritycontextapparmorprofile">appArmorProfile</a></b></td>
        <td>object</td>
        <td>
          appArmorProfile is the AppArmor options to use by the containers in this pod.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>fsGroup</b></td>
        <td>integer</td>
        <td>
          A special supplemental group that applies to all containers in a pod.
Some volume types allow the Kubelet to change the ownership of that volume
to be owned by the pod:

1. The owning GID will be the FSGroup
2. The setgid bit is set (new files created in the volume will be owned by FSGroup)
3. The permission bits are OR'd with rw-rw----

If unset, the Kubelet will not modify the ownership and permissions of any volume.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>fsGroupChangePolicy</b></td>
        <td>string</td>
        <td>
          fsGroupChangePolicy defines behavior of changing ownership and permission of the volume
before being exposed inside Pod. This field will only apply to
volume types which support fsGroup based ownership(and permissions).
It will have no effect on ephemeral volume types such as: secret, configmaps
and emptydir.
Valid values are "OnRootMismatch" and "Always". If not specified, "Always" is used.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsGroup</b></td>
        <td>integer</td>
        <td>
          The GID to run the entrypoint of the container process.
Uses runtime default if unset.
May also be set in SecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence
for that container.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsNonRoot</b></td>
        <td>boolean</td>
        <td>
          Indicates that the container must run as a non-root user.
If true, the Kubelet will validate the image at runtime to ensure that it
does not run as UID 0 (root) and fail to start the container if it does.
If unset or false, no such validation will be performed.
May also be set in SecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsUser</b></td>
        <td>integer</td>
        <td>
          The UID to run the entrypoint of the container process.
Defaults to user specified in image metadata if unspecified.
May also be set in SecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence
for that container.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>seLinuxChangePolicy</b></td>
        <td>string</td>
        <td>
          seLinuxChangePolicy defines how the container's SELinux label is applied to all volumes used by the Pod.
It has no effect on nodes that do not support SELinux or to volumes does not support SELinux.
Valid values are "MountOption" and "Recursive".

"Recursive" means relabeling of all files on all Pod volumes by the container runtime.
This may be slow for large volumes, but allows mixing privileged and unprivileged Pods sharing the same volume on the same node.

"MountOption" mounts all eligible Pod volumes with `-o context` mount option.
This requires all Pods that share the same volume to use the same SELinux label.
It is not possible to share the same volume among privileged and unprivileged Pods.
Eligible volumes are in-tree FibreChannel and iSCSI volumes, and all CSI volumes
whose CSI driver announces SELinux support by setting spec.seLinuxMount: true in their
CSIDriver instance. Other volumes are always re-labelled recursively.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatesecuritycontextselinuxoptions">seLinuxOptions</a></b></td>
        <td>object</td>
        <td>
          The SELinux context to be applied to all containers.
If unspecified, the container runtime will allocate a random SELinux context for each
container.  May also be set in SecurityContext.  If set in
both SecurityContext and PodSecurityContext, the value specified in SecurityContext
takes precedence for that container.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatesecuritycontextseccompprofile">seccompProfile</a></b></td>
        <td>object</td>
        <td>
          The seccomp options to use by the containers in this pod.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>supplementalGroups</b></td>
        <td>[]integer</td>
        <td>
          A list of groups applied to the first process run in each container, in
addition to the container's primary GID and fsGroup (if specified).  If
the SupplementalGroupsPolicy feature is enabled, the
supplementalGroupsPolicy field determines whether these are in addition
to or instead of any group memberships defined in the container image.
If unspecified, no additional groups are added, though group memberships
defined in the container image may still be used, depending on the
supplementalGroupsPolicy field.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>supplementalGroupsPolicy</b></td>
        <td>string</td>
        <td>
          Defines how supplemental groups of the first container processes are calculated.
Valid values are "Merge" and "Strict". If not specified, "Merge" is used.
(Alpha) Using the field requires the SupplementalGroupsPolicy feature gate to be enabled
and the container runtime must implement support for this feature.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatesecuritycontextsysctlsindex">sysctls</a></b></td>
        <td>[]object</td>
        <td>
          Sysctls hold a list of namespaced sysctls used for the pod. Pods with unsupported
sysctls (by the container runtime) might fail to launch.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubepodtemplatesecuritycontextwindowsoptions">windowsOptions</a></b></td>
        <td>object</td>
        <td>
          The Windows specific settings applied to all containers.
If unspecified, the options within a container's SecurityContext will be used.
If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is linux.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.securityContext.appArmorProfile
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatesecuritycontext)</sup></sup>



appArmorProfile is the AppArmor options to use by the containers in this pod.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type indicates which kind of AppArmor profile will be applied.
Valid options are:
  Localhost - a profile pre-loaded on the node.
  RuntimeDefault - the container runtime's default profile.
  Unconfined - no AppArmor enforcement.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>localhostProfile</b></td>
        <td>string</td>
        <td>
          localhostProfile indicates a profile loaded on the node that should be used.
The profile must be preconfigured on the node to work.
Must match the loaded name of the profile.
Must be set if and only if type is "Localhost".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.securityContext.seLinuxOptions
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatesecuritycontext)</sup></sup>



The SELinux context to be applied to all containers.
If unspecified, the container runtime will allocate a random SELinux context for each
container.  May also be set in SecurityContext.  If set in
both SecurityContext and PodSecurityContext, the value specified in SecurityContext
takes precedence for that container.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>level</b></td>
        <td>string</td>
        <td>
          Level is SELinux level label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>role</b></td>
        <td>string</td>
        <td>
          Role is a SELinux role label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          Type is a SELinux type label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>user</b></td>
        <td>string</td>
        <td>
          User is a SELinux user label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.securityContext.seccompProfile
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatesecuritycontext)</sup></sup>



The seccomp options to use by the containers in this pod.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type indicates which kind of seccomp profile will be applied.
Valid options are:

Localhost - a profile defined in a file on the node should be used.
RuntimeDefault - the container runtime default profile should be used.
Unconfined - no profile should be applied.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>localhostProfile</b></td>
        <td>string</td>
        <td>
          localhostProfile indicates a profile defined in a file on the node should be used.
The profile must be preconfigured on the node to work.
Must be a descending path, relative to the kubelet's configured seccomp profile location.
Must be set if type is "Localhost". Must NOT be set for any other type.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.securityContext.sysctls[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatesecuritycontext)</sup></sup>



Sysctl defines a kernel parameter to be set

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of a property to set<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          Value of a property to set<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.securityContext.windowsOptions
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplatesecuritycontext)</sup></sup>



The Windows specific settings applied to all containers.
If unspecified, the options within a container's SecurityContext will be used.
If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is linux.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>gmsaCredentialSpec</b></td>
        <td>string</td>
        <td>
          GMSACredentialSpec is where the GMSA admission webhook
(https://github.com/kubernetes-sigs/windows-gmsa) inlines the contents of the
GMSA credential spec named by the GMSACredentialSpecName field.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>gmsaCredentialSpecName</b></td>
        <td>string</td>
        <td>
          GMSACredentialSpecName is the name of the GMSA credential spec to use.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>hostProcess</b></td>
        <td>boolean</td>
        <td>
          HostProcess determines if a container should be run as a 'Host Process' container.
All of a Pod's containers must have the same effective HostProcess value
(it is not allowed to have a mix of HostProcess containers and non-HostProcess containers).
In addition, if HostProcess is true then HostNetwork must also be set to true.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsUserName</b></td>
        <td>string</td>
        <td>
          The UserName in Windows to run the entrypoint of the container process.
Defaults to the user specified in image metadata if unspecified.
May also be set in PodSecurityContext. If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.podTemplate.tolerations[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubepodtemplate)</sup></sup>



The pod this Toleration is attached to tolerates any taint that matches
the triple <key,value,effect> using the matching operator <operator>.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>effect</b></td>
        <td>string</td>
        <td>
          Effect indicates the taint effect to match. Empty means match all taint effects.
When specified, allowed values are NoSchedule, PreferNoSchedule and NoExecute.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>key</b></td>
        <td>string</td>
        <td>
          Key is the taint key that the toleration applies to. Empty means match all taint keys.
If the key is empty, operator must be Exists; this combination means to match all values and all keys.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>operator</b></td>
        <td>string</td>
        <td>
          Operator represents a key's relationship to the value.
Valid operators are Exists and Equal. Defaults to Equal.
Exists is equivalent to wildcard for value, so that a pod can
tolerate all taints of a particular category.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>tolerationSeconds</b></td>
        <td>integer</td>
        <td>
          TolerationSeconds represents the period of time the toleration (which must be
of effect NoExecute, otherwise this field is ignored) tolerates the taint. By default,
it is not set, which means tolerate the taint forever (do not evict). Zero and
negative values will be treated as 0 (evict immediately) by the system.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          Value is the taint value the toleration matches to.
If the operator is Exists, the value should be empty, otherwise just a regular string.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.sdsContainer
<sup><sup>[↩ Parent](#gatewayparametersspeckube)</sup></sup>



Configuration for the container running the Secret Discovery Service (SDS).

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubesdscontainerbootstrap">bootstrap</a></b></td>
        <td>object</td>
        <td>
          Initial SDS container configuration.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubesdscontainerimage">image</a></b></td>
        <td>object</td>
        <td>
          The SDS container image. See
https://kubernetes.io/docs/concepts/containers/images
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubesdscontainerresources">resources</a></b></td>
        <td>object</td>
        <td>
          The compute resources required by this container. See
https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubesdscontainersecuritycontext">securityContext</a></b></td>
        <td>object</td>
        <td>
          The security context for this container. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core
for details.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.sdsContainer.bootstrap
<sup><sup>[↩ Parent](#gatewayparametersspeckubesdscontainer)</sup></sup>



Initial SDS container configuration.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>logLevel</b></td>
        <td>string</td>
        <td>
          Log level for SDS. Options include "info", "debug", "warn", "error", "panic" and "fatal".
Default level is "info".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.sdsContainer.image
<sup><sup>[↩ Parent](#gatewayparametersspeckubesdscontainer)</sup></sup>



The SDS container image. See
https://kubernetes.io/docs/concepts/containers/images
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>digest</b></td>
        <td>string</td>
        <td>
          The hash digest of the image, e.g. `sha256:12345...`<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>pullPolicy</b></td>
        <td>string</td>
        <td>
          The image pull policy for the container. See
https://kubernetes.io/docs/concepts/containers/images/#image-pull-policy
for details.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>registry</b></td>
        <td>string</td>
        <td>
          The image registry.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>repository</b></td>
        <td>string</td>
        <td>
          The image repository (name).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>tag</b></td>
        <td>string</td>
        <td>
          The image tag.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.sdsContainer.resources
<sup><sup>[↩ Parent](#gatewayparametersspeckubesdscontainer)</sup></sup>



The compute resources required by this container. See
https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#gatewayparametersspeckubesdscontainerresourcesclaimsindex">claims</a></b></td>
        <td>[]object</td>
        <td>
          Claims lists the names of resources, defined in spec.resourceClaims,
that are used by this container.

This is an alpha field and requires enabling the
DynamicResourceAllocation feature gate.

This field is immutable. It can only be set for containers.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>limits</b></td>
        <td>map[string]int or string</td>
        <td>
          Limits describes the maximum amount of compute resources allowed.
More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>requests</b></td>
        <td>map[string]int or string</td>
        <td>
          Requests describes the minimum amount of compute resources required.
If Requests is omitted for a container, it defaults to Limits if that is explicitly specified,
otherwise to an implementation-defined value. Requests cannot exceed Limits.
More info: https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.sdsContainer.resources.claims[index]
<sup><sup>[↩ Parent](#gatewayparametersspeckubesdscontainerresources)</sup></sup>



ResourceClaim references one entry in PodSpec.ResourceClaims.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name must match the name of one entry in pod.spec.resourceClaims of
the Pod where this field is used. It makes that resource available
inside a container.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>request</b></td>
        <td>string</td>
        <td>
          Request is the name chosen for a request in the referenced claim.
If empty, everything from the claim is made available, otherwise
only the result of this request.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.sdsContainer.securityContext
<sup><sup>[↩ Parent](#gatewayparametersspeckubesdscontainer)</sup></sup>



The security context for this container. See
https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.26/#securitycontext-v1-core
for details.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>allowPrivilegeEscalation</b></td>
        <td>boolean</td>
        <td>
          AllowPrivilegeEscalation controls whether a process can gain more
privileges than its parent process. This bool directly controls if
the no_new_privs flag will be set on the container process.
AllowPrivilegeEscalation is true always when the container is:
1) run as Privileged
2) has CAP_SYS_ADMIN
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubesdscontainersecuritycontextapparmorprofile">appArmorProfile</a></b></td>
        <td>object</td>
        <td>
          appArmorProfile is the AppArmor options to use by this container. If set, this profile
overrides the pod's appArmorProfile.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubesdscontainersecuritycontextcapabilities">capabilities</a></b></td>
        <td>object</td>
        <td>
          The capabilities to add/drop when running containers.
Defaults to the default set of capabilities granted by the container runtime.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>privileged</b></td>
        <td>boolean</td>
        <td>
          Run container in privileged mode.
Processes in privileged containers are essentially equivalent to root on the host.
Defaults to false.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>procMount</b></td>
        <td>string</td>
        <td>
          procMount denotes the type of proc mount to use for the containers.
The default value is Default which uses the container runtime defaults for
readonly paths and masked paths.
This requires the ProcMountType feature flag to be enabled.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>readOnlyRootFilesystem</b></td>
        <td>boolean</td>
        <td>
          Whether this container has a read-only root filesystem.
Default is false.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsGroup</b></td>
        <td>integer</td>
        <td>
          The GID to run the entrypoint of the container process.
Uses runtime default if unset.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsNonRoot</b></td>
        <td>boolean</td>
        <td>
          Indicates that the container must run as a non-root user.
If true, the Kubelet will validate the image at runtime to ensure that it
does not run as UID 0 (root) and fail to start the container if it does.
If unset or false, no such validation will be performed.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsUser</b></td>
        <td>integer</td>
        <td>
          The UID to run the entrypoint of the container process.
Defaults to user specified in image metadata if unspecified.
May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
          <br/>
            <i>Format</i>: int64<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubesdscontainersecuritycontextselinuxoptions">seLinuxOptions</a></b></td>
        <td>object</td>
        <td>
          The SELinux context to be applied to the container.
If unspecified, the container runtime will allocate a random SELinux context for each
container.  May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubesdscontainersecuritycontextseccompprofile">seccompProfile</a></b></td>
        <td>object</td>
        <td>
          The seccomp options to use by this container. If seccomp options are
provided at both the pod & container level, the container options
override the pod options.
Note that this field cannot be set when spec.os.name is windows.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#gatewayparametersspeckubesdscontainersecuritycontextwindowsoptions">windowsOptions</a></b></td>
        <td>object</td>
        <td>
          The Windows specific settings applied to all containers.
If unspecified, the options from the PodSecurityContext will be used.
If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is linux.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.sdsContainer.securityContext.appArmorProfile
<sup><sup>[↩ Parent](#gatewayparametersspeckubesdscontainersecuritycontext)</sup></sup>



appArmorProfile is the AppArmor options to use by this container. If set, this profile
overrides the pod's appArmorProfile.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type indicates which kind of AppArmor profile will be applied.
Valid options are:
  Localhost - a profile pre-loaded on the node.
  RuntimeDefault - the container runtime's default profile.
  Unconfined - no AppArmor enforcement.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>localhostProfile</b></td>
        <td>string</td>
        <td>
          localhostProfile indicates a profile loaded on the node that should be used.
The profile must be preconfigured on the node to work.
Must match the loaded name of the profile.
Must be set if and only if type is "Localhost".<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.sdsContainer.securityContext.capabilities
<sup><sup>[↩ Parent](#gatewayparametersspeckubesdscontainersecuritycontext)</sup></sup>



The capabilities to add/drop when running containers.
Defaults to the default set of capabilities granted by the container runtime.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>add</b></td>
        <td>[]string</td>
        <td>
          Added capabilities<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>drop</b></td>
        <td>[]string</td>
        <td>
          Removed capabilities<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.sdsContainer.securityContext.seLinuxOptions
<sup><sup>[↩ Parent](#gatewayparametersspeckubesdscontainersecuritycontext)</sup></sup>



The SELinux context to be applied to the container.
If unspecified, the container runtime will allocate a random SELinux context for each
container.  May also be set in PodSecurityContext.  If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>level</b></td>
        <td>string</td>
        <td>
          Level is SELinux level label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>role</b></td>
        <td>string</td>
        <td>
          Role is a SELinux role label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          Type is a SELinux type label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>user</b></td>
        <td>string</td>
        <td>
          User is a SELinux user label that applies to the container.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.sdsContainer.securityContext.seccompProfile
<sup><sup>[↩ Parent](#gatewayparametersspeckubesdscontainersecuritycontext)</sup></sup>



The seccomp options to use by this container. If seccomp options are
provided at both the pod & container level, the container options
override the pod options.
Note that this field cannot be set when spec.os.name is windows.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type indicates which kind of seccomp profile will be applied.
Valid options are:

Localhost - a profile defined in a file on the node should be used.
RuntimeDefault - the container runtime default profile should be used.
Unconfined - no profile should be applied.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>localhostProfile</b></td>
        <td>string</td>
        <td>
          localhostProfile indicates a profile defined in a file on the node should be used.
The profile must be preconfigured on the node to work.
Must be a descending path, relative to the kubelet's configured seccomp profile location.
Must be set if type is "Localhost". Must NOT be set for any other type.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.sdsContainer.securityContext.windowsOptions
<sup><sup>[↩ Parent](#gatewayparametersspeckubesdscontainersecuritycontext)</sup></sup>



The Windows specific settings applied to all containers.
If unspecified, the options from the PodSecurityContext will be used.
If set in both SecurityContext and PodSecurityContext, the value specified in SecurityContext takes precedence.
Note that this field cannot be set when spec.os.name is linux.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>gmsaCredentialSpec</b></td>
        <td>string</td>
        <td>
          GMSACredentialSpec is where the GMSA admission webhook
(https://github.com/kubernetes-sigs/windows-gmsa) inlines the contents of the
GMSA credential spec named by the GMSACredentialSpecName field.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>gmsaCredentialSpecName</b></td>
        <td>string</td>
        <td>
          GMSACredentialSpecName is the name of the GMSA credential spec to use.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>hostProcess</b></td>
        <td>boolean</td>
        <td>
          HostProcess determines if a container should be run as a 'Host Process' container.
All of a Pod's containers must have the same effective HostProcess value
(it is not allowed to have a mix of HostProcess containers and non-HostProcess containers).
In addition, if HostProcess is true then HostNetwork must also be set to true.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>runAsUserName</b></td>
        <td>string</td>
        <td>
          The UserName in Windows to run the entrypoint of the container process.
Defaults to the user specified in image metadata if unspecified.
May also be set in PodSecurityContext. If set in both SecurityContext and
PodSecurityContext, the value specified in SecurityContext takes precedence.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.service
<sup><sup>[↩ Parent](#gatewayparametersspeckube)</sup></sup>



Configuration for the Kubernetes Service that exposes the Envoy proxy over
the network.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>clusterIP</b></td>
        <td>string</td>
        <td>
          The manually specified IP address of the service, if a randomly assigned
IP is not desired. See
https://kubernetes.io/docs/concepts/services-networking/service/#choosing-your-own-ip-address
and
https://kubernetes.io/docs/concepts/services-networking/service/#headless-services
on the implications of setting `clusterIP`.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>extraAnnotations</b></td>
        <td>map[string]string</td>
        <td>
          Additional annotations to add to the Service object metadata.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>extraLabels</b></td>
        <td>map[string]string</td>
        <td>
          Additional labels to add to the Service object metadata.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          The Kubernetes Service type.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.serviceAccount
<sup><sup>[↩ Parent](#gatewayparametersspeckube)</sup></sup>



Configuration for the Kubernetes ServiceAccount used by the Envoy pod.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>extraAnnotations</b></td>
        <td>map[string]string</td>
        <td>
          Additional annotations to add to the ServiceAccount object metadata.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>extraLabels</b></td>
        <td>map[string]string</td>
        <td>
          Additional labels to add to the ServiceAccount object metadata.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### GatewayParameters.spec.kube.stats
<sup><sup>[↩ Parent](#gatewayparametersspeckube)</sup></sup>



Configuration for the stats server.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>enableStatsRoute</b></td>
        <td>boolean</td>
        <td>
          Enables an additional route to the stats cluster defaulting to /stats<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>enabled</b></td>
        <td>boolean</td>
        <td>
          Whether to expose metrics annotations and ports for scraping metrics.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>routePrefixRewrite</b></td>
        <td>string</td>
        <td>
          The Envoy stats endpoint to which the metrics are written<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>statsRoutePrefixRewrite</b></td>
        <td>string</td>
        <td>
          The Envoy stats endpoint with general metrics for the additional stats route<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>

## HTTPListenerPolicy
<sup><sup>[↩ Parent](#gatewaykgatewaydevv1alpha1 )</sup></sup>








<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
      <td><b>apiVersion</b></td>
      <td>string</td>
      <td>gateway.kgateway.dev/v1alpha1</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b>kind</b></td>
      <td>string</td>
      <td>HTTPListenerPolicy</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b><a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#objectmeta-v1-meta">metadata</a></b></td>
      <td>object</td>
      <td>Refer to the Kubernetes API documentation for the fields of the `metadata` field.</td>
      <td>true</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspec">spec</a></b></td>
        <td>object</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicystatus">status</a></b></td>
        <td>object</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec
<sup><sup>[↩ Parent](#httplistenerpolicy)</sup></sup>





<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindex">accessLog</a></b></td>
        <td>[]object</td>
        <td>
          AccessLoggingConfig contains various settings for Envoy's access logging service.
See here for more information: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>compress</b></td>
        <td>boolean</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspectargetref">targetRef</a></b></td>
        <td>object</td>
        <td>
          not sure why i need to copy this; codegen fails if i dont<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index]
<sup><sup>[↩ Parent](#httplistenerpolicyspec)</sup></sup>



AccessLog represents the top-level access log configuration.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilesink">fileSink</a></b></td>
        <td>object</td>
        <td>
          Output access logs to local file<br/>
          <br/>
            <i>Validations</i>:<li>(has(self.stringFormat) && !has(self.jsonFormat)) || (!has(self.stringFormat) && has(self.jsonFormat)): only one of 'StringFormat' or 'JsonFormat' may be set</li>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilter">filter</a></b></td>
        <td>object</td>
        <td>
          Filter access logs configuration<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexgrpcservice">grpcService</a></b></td>
        <td>object</td>
        <td>
          Send access logs to gRPC service<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].fileSink
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindex)</sup></sup>



Output access logs to local file

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>path</b></td>
        <td>string</td>
        <td>
          the file path to which the file access logging service will sink<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>jsonFormat</b></td>
        <td>object</td>
        <td>
          the format object by which to envoy will emit the logs in a structured way.
https://www.envoyproxy.io/docs/envoy/v1.33.0/configuration/observability/access_log/usage#format-dictionaries<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>stringFormat</b></td>
        <td>string</td>
        <td>
          the format string by which envoy will format the log lines
https://www.envoyproxy.io/docs/envoy/v1.33.0/configuration/observability/access_log/usage#format-strings<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindex)</sup></sup>



Filter access logs configuration

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterandfilterindex">andFilter</a></b></td>
        <td>[]object</td>
        <td>
          Performs a logical "and" operation on the result of each individual filter.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-andfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfiltercelfilter">celFilter</a></b></td>
        <td>object</td>
        <td>
          CELFilter filters requests based on Common Expression Language (CEL).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterdurationfilter">durationFilter</a></b></td>
        <td>object</td>
        <td>
          DurationFilter filters based on request duration.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-durationfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfiltergrpcstatusfilter">grpcStatusFilter</a></b></td>
        <td>object</td>
        <td>
          GrpcStatusFilter filters gRPC requests based on their response status.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#enum-config-accesslog-v3-grpcstatusfilter-status<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterheaderfilter">headerFilter</a></b></td>
        <td>object</td>
        <td>
          HeaderFilter filters requests based on headers.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-headerfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>notHealthCheckFilter</b></td>
        <td>boolean</td>
        <td>
          Filters for requests that are not health check requests.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-nothealthcheckfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterorfilterindex">orFilter</a></b></td>
        <td>[]object</td>
        <td>
          Performs a logical "or" operation on the result of each individual filter.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-orfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterresponseflagfilter">responseFlagFilter</a></b></td>
        <td>object</td>
        <td>
          ResponseFlagFilter filters based on response flags.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-responseflagfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterstatuscodefilter">statusCodeFilter</a></b></td>
        <td>object</td>
        <td>
          StatusCodeFilter filters based on HTTP status code.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#envoy-v3-api-msg-config-accesslog-v3-statuscodefilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>traceableFilter</b></td>
        <td>boolean</td>
        <td>
          Filters for requests that are traceable.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-traceablefilter<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.andFilter[index]
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilter)</sup></sup>



FilterType represents the type of filter to apply (only one of these should be set).
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#envoy-v3-api-msg-config-accesslog-v3-accesslogfilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterandfilterindexcelfilter">celFilter</a></b></td>
        <td>object</td>
        <td>
          CELFilter filters requests based on Common Expression Language (CEL).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterandfilterindexdurationfilter">durationFilter</a></b></td>
        <td>object</td>
        <td>
          DurationFilter filters based on request duration.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-durationfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterandfilterindexgrpcstatusfilter">grpcStatusFilter</a></b></td>
        <td>object</td>
        <td>
          GrpcStatusFilter filters gRPC requests based on their response status.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#enum-config-accesslog-v3-grpcstatusfilter-status<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterandfilterindexheaderfilter">headerFilter</a></b></td>
        <td>object</td>
        <td>
          HeaderFilter filters requests based on headers.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-headerfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>notHealthCheckFilter</b></td>
        <td>boolean</td>
        <td>
          Filters for requests that are not health check requests.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-nothealthcheckfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterandfilterindexresponseflagfilter">responseFlagFilter</a></b></td>
        <td>object</td>
        <td>
          ResponseFlagFilter filters based on response flags.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-responseflagfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterandfilterindexstatuscodefilter">statusCodeFilter</a></b></td>
        <td>object</td>
        <td>
          StatusCodeFilter filters based on HTTP status code.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#envoy-v3-api-msg-config-accesslog-v3-statuscodefilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>traceableFilter</b></td>
        <td>boolean</td>
        <td>
          Filters for requests that are traceable.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-traceablefilter<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.andFilter[index].celFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterandfilterindex)</sup></sup>



CELFilter filters requests based on Common Expression Language (CEL).

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>match</b></td>
        <td>string</td>
        <td>
          The CEL expressions to evaluate. AccessLogs are only emitted when the CEL expressions evaluates to true.
see: https://www.envoyproxy.io/docs/envoy/v1.33.0/xds/type/v3/cel.proto.html#common-expression-language-cel-proto<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.andFilter[index].durationFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterandfilterindex)</sup></sup>



DurationFilter filters based on request duration.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-durationfilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>op</b></td>
        <td>enum</td>
        <td>
          Op represents comparison operators.<br/>
          <br/>
            <i>Enum</i>: EQ, GE, LE<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>integer</td>
        <td>
          Value to compare against.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 0<br/>
            <i>Maximum</i>: 4.294967295e+09<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.andFilter[index].grpcStatusFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterandfilterindex)</sup></sup>



GrpcStatusFilter filters gRPC requests based on their response status.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#enum-config-accesslog-v3-grpcstatusfilter-status

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>exclude</b></td>
        <td>boolean</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>statuses</b></td>
        <td>[]enum</td>
        <td>
          <br/>
          <br/>
            <i>Enum</i>: OK, CANCELED, UNKNOWN, INVALID_ARGUMENT, DEADLINE_EXCEEDED, NOT_FOUND, ALREADY_EXISTS, PERMISSION_DENIED, RESOURCE_EXHAUSTED, FAILED_PRECONDITION, ABORTED, OUT_OF_RANGE, UNIMPLEMENTED, INTERNAL, UNAVAILABLE, DATA_LOSS, UNAUTHENTICATED<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.andFilter[index].headerFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterandfilterindex)</sup></sup>



HeaderFilter filters requests based on headers.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-headerfilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterandfilterindexheaderfilterheader">header</a></b></td>
        <td>object</td>
        <td>
          HTTPHeaderMatch describes how to select a HTTP route by matching HTTP request
headers.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.andFilter[index].headerFilter.header
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterandfilterindexheaderfilter)</sup></sup>



HTTPHeaderMatch describes how to select a HTTP route by matching HTTP request
headers.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is the name of the HTTP Header to be matched. Name matching MUST be
case insensitive. (See https://tools.ietf.org/html/rfc7230#section-3.2).

If multiple entries specify equivalent header names, only the first
entry with an equivalent name MUST be considered for a match. Subsequent
entries with an equivalent header name MUST be ignored. Due to the
case-insensitivity of header names, "foo" and "Foo" are considered
equivalent.

When a header is repeated in an HTTP request, it is
implementation-specific behavior as to how this is represented.
Generally, proxies should follow the guidance from the RFC:
https://www.rfc-editor.org/rfc/rfc7230.html#section-3.2.2 regarding
processing a repeated header, with special handling for "Set-Cookie".<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          Value is the value of HTTP Header to be matched.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>enum</td>
        <td>
          Type specifies how to match against the value of the header.

Support: Core (Exact)

Support: Implementation-specific (RegularExpression)

Since RegularExpression HeaderMatchType has implementation-specific
conformance, implementations can support POSIX, PCRE or any other dialects
of regular expressions. Please read the implementation's documentation to
determine the supported dialect.<br/>
          <br/>
            <i>Enum</i>: Exact, RegularExpression<br/>
            <i>Default</i>: Exact<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.andFilter[index].responseFlagFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterandfilterindex)</sup></sup>



ResponseFlagFilter filters based on response flags.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-responseflagfilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>flags</b></td>
        <td>[]string</td>
        <td>
          <br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.andFilter[index].statusCodeFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterandfilterindex)</sup></sup>



StatusCodeFilter filters based on HTTP status code.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#envoy-v3-api-msg-config-accesslog-v3-statuscodefilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>op</b></td>
        <td>enum</td>
        <td>
          Op represents comparison operators.<br/>
          <br/>
            <i>Enum</i>: EQ, GE, LE<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>integer</td>
        <td>
          Value to compare against.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 0<br/>
            <i>Maximum</i>: 4.294967295e+09<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.celFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilter)</sup></sup>



CELFilter filters requests based on Common Expression Language (CEL).

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>match</b></td>
        <td>string</td>
        <td>
          The CEL expressions to evaluate. AccessLogs are only emitted when the CEL expressions evaluates to true.
see: https://www.envoyproxy.io/docs/envoy/v1.33.0/xds/type/v3/cel.proto.html#common-expression-language-cel-proto<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.durationFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilter)</sup></sup>



DurationFilter filters based on request duration.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-durationfilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>op</b></td>
        <td>enum</td>
        <td>
          Op represents comparison operators.<br/>
          <br/>
            <i>Enum</i>: EQ, GE, LE<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>integer</td>
        <td>
          Value to compare against.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 0<br/>
            <i>Maximum</i>: 4.294967295e+09<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.grpcStatusFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilter)</sup></sup>



GrpcStatusFilter filters gRPC requests based on their response status.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#enum-config-accesslog-v3-grpcstatusfilter-status

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>exclude</b></td>
        <td>boolean</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>statuses</b></td>
        <td>[]enum</td>
        <td>
          <br/>
          <br/>
            <i>Enum</i>: OK, CANCELED, UNKNOWN, INVALID_ARGUMENT, DEADLINE_EXCEEDED, NOT_FOUND, ALREADY_EXISTS, PERMISSION_DENIED, RESOURCE_EXHAUSTED, FAILED_PRECONDITION, ABORTED, OUT_OF_RANGE, UNIMPLEMENTED, INTERNAL, UNAVAILABLE, DATA_LOSS, UNAUTHENTICATED<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.headerFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilter)</sup></sup>



HeaderFilter filters requests based on headers.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-headerfilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterheaderfilterheader">header</a></b></td>
        <td>object</td>
        <td>
          HTTPHeaderMatch describes how to select a HTTP route by matching HTTP request
headers.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.headerFilter.header
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterheaderfilter)</sup></sup>



HTTPHeaderMatch describes how to select a HTTP route by matching HTTP request
headers.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is the name of the HTTP Header to be matched. Name matching MUST be
case insensitive. (See https://tools.ietf.org/html/rfc7230#section-3.2).

If multiple entries specify equivalent header names, only the first
entry with an equivalent name MUST be considered for a match. Subsequent
entries with an equivalent header name MUST be ignored. Due to the
case-insensitivity of header names, "foo" and "Foo" are considered
equivalent.

When a header is repeated in an HTTP request, it is
implementation-specific behavior as to how this is represented.
Generally, proxies should follow the guidance from the RFC:
https://www.rfc-editor.org/rfc/rfc7230.html#section-3.2.2 regarding
processing a repeated header, with special handling for "Set-Cookie".<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          Value is the value of HTTP Header to be matched.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>enum</td>
        <td>
          Type specifies how to match against the value of the header.

Support: Core (Exact)

Support: Implementation-specific (RegularExpression)

Since RegularExpression HeaderMatchType has implementation-specific
conformance, implementations can support POSIX, PCRE or any other dialects
of regular expressions. Please read the implementation's documentation to
determine the supported dialect.<br/>
          <br/>
            <i>Enum</i>: Exact, RegularExpression<br/>
            <i>Default</i>: Exact<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.orFilter[index]
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilter)</sup></sup>



FilterType represents the type of filter to apply (only one of these should be set).
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#envoy-v3-api-msg-config-accesslog-v3-accesslogfilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterorfilterindexcelfilter">celFilter</a></b></td>
        <td>object</td>
        <td>
          CELFilter filters requests based on Common Expression Language (CEL).<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterorfilterindexdurationfilter">durationFilter</a></b></td>
        <td>object</td>
        <td>
          DurationFilter filters based on request duration.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-durationfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterorfilterindexgrpcstatusfilter">grpcStatusFilter</a></b></td>
        <td>object</td>
        <td>
          GrpcStatusFilter filters gRPC requests based on their response status.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#enum-config-accesslog-v3-grpcstatusfilter-status<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterorfilterindexheaderfilter">headerFilter</a></b></td>
        <td>object</td>
        <td>
          HeaderFilter filters requests based on headers.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-headerfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>notHealthCheckFilter</b></td>
        <td>boolean</td>
        <td>
          Filters for requests that are not health check requests.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-nothealthcheckfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterorfilterindexresponseflagfilter">responseFlagFilter</a></b></td>
        <td>object</td>
        <td>
          ResponseFlagFilter filters based on response flags.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-responseflagfilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterorfilterindexstatuscodefilter">statusCodeFilter</a></b></td>
        <td>object</td>
        <td>
          StatusCodeFilter filters based on HTTP status code.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#envoy-v3-api-msg-config-accesslog-v3-statuscodefilter<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>traceableFilter</b></td>
        <td>boolean</td>
        <td>
          Filters for requests that are traceable.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-traceablefilter<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.orFilter[index].celFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterorfilterindex)</sup></sup>



CELFilter filters requests based on Common Expression Language (CEL).

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>match</b></td>
        <td>string</td>
        <td>
          The CEL expressions to evaluate. AccessLogs are only emitted when the CEL expressions evaluates to true.
see: https://www.envoyproxy.io/docs/envoy/v1.33.0/xds/type/v3/cel.proto.html#common-expression-language-cel-proto<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.orFilter[index].durationFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterorfilterindex)</sup></sup>



DurationFilter filters based on request duration.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-durationfilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>op</b></td>
        <td>enum</td>
        <td>
          Op represents comparison operators.<br/>
          <br/>
            <i>Enum</i>: EQ, GE, LE<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>integer</td>
        <td>
          Value to compare against.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 0<br/>
            <i>Maximum</i>: 4.294967295e+09<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.orFilter[index].grpcStatusFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterorfilterindex)</sup></sup>



GrpcStatusFilter filters gRPC requests based on their response status.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#enum-config-accesslog-v3-grpcstatusfilter-status

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>exclude</b></td>
        <td>boolean</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>statuses</b></td>
        <td>[]enum</td>
        <td>
          <br/>
          <br/>
            <i>Enum</i>: OK, CANCELED, UNKNOWN, INVALID_ARGUMENT, DEADLINE_EXCEEDED, NOT_FOUND, ALREADY_EXISTS, PERMISSION_DENIED, RESOURCE_EXHAUSTED, FAILED_PRECONDITION, ABORTED, OUT_OF_RANGE, UNIMPLEMENTED, INTERNAL, UNAVAILABLE, DATA_LOSS, UNAUTHENTICATED<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.orFilter[index].headerFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterorfilterindex)</sup></sup>



HeaderFilter filters requests based on headers.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-headerfilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexfilterorfilterindexheaderfilterheader">header</a></b></td>
        <td>object</td>
        <td>
          HTTPHeaderMatch describes how to select a HTTP route by matching HTTP request
headers.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.orFilter[index].headerFilter.header
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterorfilterindexheaderfilter)</sup></sup>



HTTPHeaderMatch describes how to select a HTTP route by matching HTTP request
headers.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is the name of the HTTP Header to be matched. Name matching MUST be
case insensitive. (See https://tools.ietf.org/html/rfc7230#section-3.2).

If multiple entries specify equivalent header names, only the first
entry with an equivalent name MUST be considered for a match. Subsequent
entries with an equivalent header name MUST be ignored. Due to the
case-insensitivity of header names, "foo" and "Foo" are considered
equivalent.

When a header is repeated in an HTTP request, it is
implementation-specific behavior as to how this is represented.
Generally, proxies should follow the guidance from the RFC:
https://www.rfc-editor.org/rfc/rfc7230.html#section-3.2.2 regarding
processing a repeated header, with special handling for "Set-Cookie".<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          Value is the value of HTTP Header to be matched.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>enum</td>
        <td>
          Type specifies how to match against the value of the header.

Support: Core (Exact)

Support: Implementation-specific (RegularExpression)

Since RegularExpression HeaderMatchType has implementation-specific
conformance, implementations can support POSIX, PCRE or any other dialects
of regular expressions. Please read the implementation's documentation to
determine the supported dialect.<br/>
          <br/>
            <i>Enum</i>: Exact, RegularExpression<br/>
            <i>Default</i>: Exact<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.orFilter[index].responseFlagFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterorfilterindex)</sup></sup>



ResponseFlagFilter filters based on response flags.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-responseflagfilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>flags</b></td>
        <td>[]string</td>
        <td>
          <br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.orFilter[index].statusCodeFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilterorfilterindex)</sup></sup>



StatusCodeFilter filters based on HTTP status code.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#envoy-v3-api-msg-config-accesslog-v3-statuscodefilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>op</b></td>
        <td>enum</td>
        <td>
          Op represents comparison operators.<br/>
          <br/>
            <i>Enum</i>: EQ, GE, LE<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>integer</td>
        <td>
          Value to compare against.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 0<br/>
            <i>Maximum</i>: 4.294967295e+09<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.responseFlagFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilter)</sup></sup>



ResponseFlagFilter filters based on response flags.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#config-accesslog-v3-responseflagfilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>flags</b></td>
        <td>[]string</td>
        <td>
          <br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].filter.statusCodeFilter
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexfilter)</sup></sup>



StatusCodeFilter filters based on HTTP status code.
Based on: https://www.envoyproxy.io/docs/envoy/v1.33.0/api-v3/config/accesslog/v3/accesslog.proto#envoy-v3-api-msg-config-accesslog-v3-statuscodefilter

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>op</b></td>
        <td>enum</td>
        <td>
          Op represents comparison operators.<br/>
          <br/>
            <i>Enum</i>: EQ, GE, LE<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>integer</td>
        <td>
          Value to compare against.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 0<br/>
            <i>Maximum</i>: 4.294967295e+09<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].grpcService
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindex)</sup></sup>



Send access logs to gRPC service

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#httplistenerpolicyspecaccesslogindexgrpcservicebackendref">backendRef</a></b></td>
        <td>object</td>
        <td>
          The backend gRPC service. Can be any type of supported backed (Kubernetes Service, kgateway Backend, etc..)<br/>
          <br/>
            <i>Validations</i>:<li>(size(self.group) == 0 && self.kind == 'Service') ? has(self.port) : true: Must have port for Service reference</li>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>logName</b></td>
        <td>string</td>
        <td>
          name of log stream<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>additionalRequestHeadersToLog</b></td>
        <td>[]string</td>
        <td>
          Additional request headers to log in the access log<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>additionalResponseHeadersToLog</b></td>
        <td>[]string</td>
        <td>
          Additional response headers to log in the access log<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>additionalResponseTrailersToLog</b></td>
        <td>[]string</td>
        <td>
          Additional response trailers to log in the access log<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.accessLog[index].grpcService.backendRef
<sup><sup>[↩ Parent](#httplistenerpolicyspecaccesslogindexgrpcservice)</sup></sup>



The backend gRPC service. Can be any type of supported backed (Kubernetes Service, kgateway Backend, etc..)

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is the name of the referent.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>group</b></td>
        <td>string</td>
        <td>
          Group is the group of the referent. For example, "gateway.networking.k8s.io".
When unspecified or empty string, core API group is inferred.<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>kind</b></td>
        <td>string</td>
        <td>
          Kind is the Kubernetes resource kind of the referent. For example
"Service".

Defaults to "Service" when not specified.

ExternalName services can refer to CNAME DNS records that may live
outside of the cluster and as such are difficult to reason about in
terms of conformance. They also may not be safe to forward to (see
CVE-2021-25740 for more information). Implementations SHOULD NOT
support ExternalName Services.

Support: Core (Services with a type other than ExternalName)

Support: Implementation-specific (Services with type ExternalName)<br/>
          <br/>
            <i>Default</i>: Service<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>namespace</b></td>
        <td>string</td>
        <td>
          Namespace is the namespace of the backend. When unspecified, the local
namespace is inferred.

Note that when a namespace different than the local namespace is specified,
a ReferenceGrant object is required in the referent namespace to allow that
namespace's owner to accept the reference. See the ReferenceGrant
documentation for details.

Support: Core<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port specifies the destination port number to use for this resource.
Port is required when the referent is a Kubernetes Service. In this
case, the port number is the service port number, not the target port.
For other resources, destination port might be derived from the referent
resource or this field.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 1<br/>
            <i>Maximum</i>: 65535<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>weight</b></td>
        <td>integer</td>
        <td>
          Weight specifies the proportion of requests forwarded to the referenced
backend. This is computed as weight/(sum of all weights in this
BackendRefs list). For non-zero values, there may be some epsilon from
the exact proportion defined here depending on the precision an
implementation supports. Weight is not a percentage and the sum of
weights does not need to equal 100.

If only one backend is specified and it has a weight greater than 0, 100%
of the traffic is forwarded to that backend. If weight is set to 0, no
traffic should be forwarded for this entry. If unspecified, weight
defaults to 1.

Support for this field varies based on the context where used.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Default</i>: 1<br/>
            <i>Minimum</i>: 0<br/>
            <i>Maximum</i>: 1e+06<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.spec.targetRef
<sup><sup>[↩ Parent](#httplistenerpolicyspec)</sup></sup>



not sure why i need to copy this; codegen fails if i dont

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>group</b></td>
        <td>string</td>
        <td>
          Group is the group of the target resource.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>kind</b></td>
        <td>string</td>
        <td>
          Kind is kind of the target resource.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is the name of the target resource.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.status
<sup><sup>[↩ Parent](#httplistenerpolicy)</sup></sup>





<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#httplistenerpolicystatusancestorsindex">ancestors</a></b></td>
        <td>[]object</td>
        <td>
          <br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicystatusconditionsindex">conditions</a></b></td>
        <td>[]object</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.status.ancestors[index]
<sup><sup>[↩ Parent](#httplistenerpolicystatus)</sup></sup>





<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#httplistenerpolicystatusancestorsindexancestorref">ancestorRef</a></b></td>
        <td>object</td>
        <td>
          AncestorRef corresponds with a ParentRef in the spec that this
PolicyAncestorStatus struct describes the status of.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>controllerName</b></td>
        <td>string</td>
        <td>
          ControllerName is a domain/path string that indicates the name of the
controller that wrote this status. This corresponds with the
controllerName field on GatewayClass.

Example: "example.net/gateway-controller".

The format of this field is DOMAIN "/" PATH, where DOMAIN and PATH are
valid Kubernetes names
(https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names).

Controllers MUST populate this field when writing status. Controllers should ensure that
entries to status populated with their ControllerName are cleaned up when they are no
longer necessary.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#httplistenerpolicystatusancestorsindexconditionsindex">conditions</a></b></td>
        <td>[]object</td>
        <td>
          Conditions describes the status of the Policy with respect to the given Ancestor.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.status.ancestors[index].ancestorRef
<sup><sup>[↩ Parent](#httplistenerpolicystatusancestorsindex)</sup></sup>



AncestorRef corresponds with a ParentRef in the spec that this
PolicyAncestorStatus struct describes the status of.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is the name of the referent.

Support: Core<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>group</b></td>
        <td>string</td>
        <td>
          Group is the group of the referent.
When unspecified, "gateway.networking.k8s.io" is inferred.
To set the core API group (such as for a "Service" kind referent),
Group must be explicitly set to "" (empty string).

Support: Core<br/>
          <br/>
            <i>Default</i>: gateway.networking.k8s.io<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>kind</b></td>
        <td>string</td>
        <td>
          Kind is kind of the referent.

There are two kinds of parent resources with "Core" support:

* Gateway (Gateway conformance profile)
* Service (Mesh conformance profile, ClusterIP Services only)

Support for other resources is Implementation-Specific.<br/>
          <br/>
            <i>Default</i>: Gateway<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>namespace</b></td>
        <td>string</td>
        <td>
          Namespace is the namespace of the referent. When unspecified, this refers
to the local namespace of the Route.

Note that there are specific rules for ParentRefs which cross namespace
boundaries. Cross-namespace references are only valid if they are explicitly
allowed by something in the namespace they are referring to. For example:
Gateway has the AllowedRoutes field, and ReferenceGrant provides a
generic way to enable any other kind of cross-namespace reference.

<gateway:experimental:description>
ParentRefs from a Route to a Service in the same namespace are "producer"
routes, which apply default routing rules to inbound connections from
any namespace to the Service.

ParentRefs from a Route to a Service in a different namespace are
"consumer" routes, and these routing rules are only applied to outbound
connections originating from the same namespace as the Route, for which
the intended destination of the connections are a Service targeted as a
ParentRef of the Route.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port is the network port this Route targets. It can be interpreted
differently based on the type of parent resource.

When the parent resource is a Gateway, this targets all listeners
listening on the specified port that also support this kind of Route(and
select this Route). It's not recommended to set `Port` unless the
networking behaviors specified in a Route must apply to a specific port
as opposed to a listener(s) whose port(s) may be changed. When both Port
and SectionName are specified, the name and port of the selected listener
must match both specified values.

<gateway:experimental:description>
When the parent resource is a Service, this targets a specific port in the
Service spec. When both Port (experimental) and SectionName are specified,
the name and port of the selected port must match both specified values.
</gateway:experimental:description>

Implementations MAY choose to support other parent resources.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 1<br/>
            <i>Maximum</i>: 65535<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>sectionName</b></td>
        <td>string</td>
        <td>
          SectionName is the name of a section within the target resource. In the
following resources, SectionName is interpreted as the following:

* Gateway: Listener name. When both Port (experimental) and SectionName
are specified, the name and port of the selected listener must match
both specified values.
* Service: Port name. When both Port (experimental) and SectionName
are specified, the name and port of the selected listener must match
both specified values.

Implementations MAY choose to support attaching Routes to other resources.
If that is the case, they MUST clearly document how SectionName is
interpreted.

When unspecified (empty string), this will reference the entire resource.
For the purpose of status, an attachment is considered successful if at
least one section in the parent resource accepts it. For example, Gateway
listeners can restrict which Routes can attach to them by Route kind,
namespace, or hostname.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.status.ancestors[index].conditions[index]
<sup><sup>[↩ Parent](#httplistenerpolicystatusancestorsindex)</sup></sup>



Condition contains details for one aspect of the current state of this API Resource.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>lastTransitionTime</b></td>
        <td>string</td>
        <td>
          lastTransitionTime is the last time the condition transitioned from one status to another.
This should be when the underlying condition changed.  If that is not known, then using the time when the API field changed is acceptable.<br/>
          <br/>
            <i>Format</i>: date-time<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>message</b></td>
        <td>string</td>
        <td>
          message is a human readable message indicating details about the transition.
This may be an empty string.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>reason</b></td>
        <td>string</td>
        <td>
          reason contains a programmatic identifier indicating the reason for the condition's last transition.
Producers of specific condition types may define expected values and meanings for this field,
and whether the values are considered a guaranteed API.
The value should be a CamelCase string.
This field may not be empty.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>status</b></td>
        <td>enum</td>
        <td>
          status of the condition, one of True, False, Unknown.<br/>
          <br/>
            <i>Enum</i>: True, False, Unknown<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type of condition in CamelCase or in foo.example.com/CamelCase.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>observedGeneration</b></td>
        <td>integer</td>
        <td>
          observedGeneration represents the .metadata.generation that the condition was set based upon.
For instance, if .metadata.generation is currently 12, but the .status.conditions[x].observedGeneration is 9, the condition is out of date
with respect to the current state of the instance.<br/>
          <br/>
            <i>Format</i>: int64<br/>
            <i>Minimum</i>: 0<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### HTTPListenerPolicy.status.conditions[index]
<sup><sup>[↩ Parent](#httplistenerpolicystatus)</sup></sup>



Condition contains details for one aspect of the current state of this API Resource.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>lastTransitionTime</b></td>
        <td>string</td>
        <td>
          lastTransitionTime is the last time the condition transitioned from one status to another.
This should be when the underlying condition changed.  If that is not known, then using the time when the API field changed is acceptable.<br/>
          <br/>
            <i>Format</i>: date-time<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>message</b></td>
        <td>string</td>
        <td>
          message is a human readable message indicating details about the transition.
This may be an empty string.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>reason</b></td>
        <td>string</td>
        <td>
          reason contains a programmatic identifier indicating the reason for the condition's last transition.
Producers of specific condition types may define expected values and meanings for this field,
and whether the values are considered a guaranteed API.
The value should be a CamelCase string.
This field may not be empty.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>status</b></td>
        <td>enum</td>
        <td>
          status of the condition, one of True, False, Unknown.<br/>
          <br/>
            <i>Enum</i>: True, False, Unknown<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type of condition in CamelCase or in foo.example.com/CamelCase.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>observedGeneration</b></td>
        <td>integer</td>
        <td>
          observedGeneration represents the .metadata.generation that the condition was set based upon.
For instance, if .metadata.generation is currently 12, but the .status.conditions[x].observedGeneration is 9, the condition is out of date
with respect to the current state of the instance.<br/>
          <br/>
            <i>Format</i>: int64<br/>
            <i>Minimum</i>: 0<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>

## ListenerPolicy
<sup><sup>[↩ Parent](#gatewaykgatewaydevv1alpha1 )</sup></sup>








<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
      <td><b>apiVersion</b></td>
      <td>string</td>
      <td>gateway.kgateway.dev/v1alpha1</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b>kind</b></td>
      <td>string</td>
      <td>ListenerPolicy</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b><a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#objectmeta-v1-meta">metadata</a></b></td>
      <td>object</td>
      <td>Refer to the Kubernetes API documentation for the fields of the `metadata` field.</td>
      <td>true</td>
      </tr><tr>
        <td><b><a href="#listenerpolicyspec">spec</a></b></td>
        <td>object</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#listenerpolicystatus">status</a></b></td>
        <td>object</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### ListenerPolicy.spec
<sup><sup>[↩ Parent](#listenerpolicy)</sup></sup>





<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>perConnectionBufferLimitBytes</b></td>
        <td>integer</td>
        <td>
          <br/>
          <br/>
            <i>Format</i>: int32<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#listenerpolicyspectargetref">targetRef</a></b></td>
        <td>object</td>
        <td>
          not sure why i need to copy this; codegen fails if i dont<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### ListenerPolicy.spec.targetRef
<sup><sup>[↩ Parent](#listenerpolicyspec)</sup></sup>



not sure why i need to copy this; codegen fails if i dont

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>group</b></td>
        <td>string</td>
        <td>
          Group is the group of the target resource.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>kind</b></td>
        <td>string</td>
        <td>
          Kind is kind of the target resource.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is the name of the target resource.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### ListenerPolicy.status
<sup><sup>[↩ Parent](#listenerpolicy)</sup></sup>





<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#listenerpolicystatusancestorsindex">ancestors</a></b></td>
        <td>[]object</td>
        <td>
          <br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#listenerpolicystatusconditionsindex">conditions</a></b></td>
        <td>[]object</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### ListenerPolicy.status.ancestors[index]
<sup><sup>[↩ Parent](#listenerpolicystatus)</sup></sup>





<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#listenerpolicystatusancestorsindexancestorref">ancestorRef</a></b></td>
        <td>object</td>
        <td>
          AncestorRef corresponds with a ParentRef in the spec that this
PolicyAncestorStatus struct describes the status of.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>controllerName</b></td>
        <td>string</td>
        <td>
          ControllerName is a domain/path string that indicates the name of the
controller that wrote this status. This corresponds with the
controllerName field on GatewayClass.

Example: "example.net/gateway-controller".

The format of this field is DOMAIN "/" PATH, where DOMAIN and PATH are
valid Kubernetes names
(https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names).

Controllers MUST populate this field when writing status. Controllers should ensure that
entries to status populated with their ControllerName are cleaned up when they are no
longer necessary.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#listenerpolicystatusancestorsindexconditionsindex">conditions</a></b></td>
        <td>[]object</td>
        <td>
          Conditions describes the status of the Policy with respect to the given Ancestor.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### ListenerPolicy.status.ancestors[index].ancestorRef
<sup><sup>[↩ Parent](#listenerpolicystatusancestorsindex)</sup></sup>



AncestorRef corresponds with a ParentRef in the spec that this
PolicyAncestorStatus struct describes the status of.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is the name of the referent.

Support: Core<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>group</b></td>
        <td>string</td>
        <td>
          Group is the group of the referent.
When unspecified, "gateway.networking.k8s.io" is inferred.
To set the core API group (such as for a "Service" kind referent),
Group must be explicitly set to "" (empty string).

Support: Core<br/>
          <br/>
            <i>Default</i>: gateway.networking.k8s.io<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>kind</b></td>
        <td>string</td>
        <td>
          Kind is kind of the referent.

There are two kinds of parent resources with "Core" support:

* Gateway (Gateway conformance profile)
* Service (Mesh conformance profile, ClusterIP Services only)

Support for other resources is Implementation-Specific.<br/>
          <br/>
            <i>Default</i>: Gateway<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>namespace</b></td>
        <td>string</td>
        <td>
          Namespace is the namespace of the referent. When unspecified, this refers
to the local namespace of the Route.

Note that there are specific rules for ParentRefs which cross namespace
boundaries. Cross-namespace references are only valid if they are explicitly
allowed by something in the namespace they are referring to. For example:
Gateway has the AllowedRoutes field, and ReferenceGrant provides a
generic way to enable any other kind of cross-namespace reference.

<gateway:experimental:description>
ParentRefs from a Route to a Service in the same namespace are "producer"
routes, which apply default routing rules to inbound connections from
any namespace to the Service.

ParentRefs from a Route to a Service in a different namespace are
"consumer" routes, and these routing rules are only applied to outbound
connections originating from the same namespace as the Route, for which
the intended destination of the connections are a Service targeted as a
ParentRef of the Route.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port is the network port this Route targets. It can be interpreted
differently based on the type of parent resource.

When the parent resource is a Gateway, this targets all listeners
listening on the specified port that also support this kind of Route(and
select this Route). It's not recommended to set `Port` unless the
networking behaviors specified in a Route must apply to a specific port
as opposed to a listener(s) whose port(s) may be changed. When both Port
and SectionName are specified, the name and port of the selected listener
must match both specified values.

<gateway:experimental:description>
When the parent resource is a Service, this targets a specific port in the
Service spec. When both Port (experimental) and SectionName are specified,
the name and port of the selected port must match both specified values.
</gateway:experimental:description>

Implementations MAY choose to support other parent resources.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 1<br/>
            <i>Maximum</i>: 65535<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>sectionName</b></td>
        <td>string</td>
        <td>
          SectionName is the name of a section within the target resource. In the
following resources, SectionName is interpreted as the following:

* Gateway: Listener name. When both Port (experimental) and SectionName
are specified, the name and port of the selected listener must match
both specified values.
* Service: Port name. When both Port (experimental) and SectionName
are specified, the name and port of the selected listener must match
both specified values.

Implementations MAY choose to support attaching Routes to other resources.
If that is the case, they MUST clearly document how SectionName is
interpreted.

When unspecified (empty string), this will reference the entire resource.
For the purpose of status, an attachment is considered successful if at
least one section in the parent resource accepts it. For example, Gateway
listeners can restrict which Routes can attach to them by Route kind,
namespace, or hostname.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### ListenerPolicy.status.ancestors[index].conditions[index]
<sup><sup>[↩ Parent](#listenerpolicystatusancestorsindex)</sup></sup>



Condition contains details for one aspect of the current state of this API Resource.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>lastTransitionTime</b></td>
        <td>string</td>
        <td>
          lastTransitionTime is the last time the condition transitioned from one status to another.
This should be when the underlying condition changed.  If that is not known, then using the time when the API field changed is acceptable.<br/>
          <br/>
            <i>Format</i>: date-time<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>message</b></td>
        <td>string</td>
        <td>
          message is a human readable message indicating details about the transition.
This may be an empty string.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>reason</b></td>
        <td>string</td>
        <td>
          reason contains a programmatic identifier indicating the reason for the condition's last transition.
Producers of specific condition types may define expected values and meanings for this field,
and whether the values are considered a guaranteed API.
The value should be a CamelCase string.
This field may not be empty.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>status</b></td>
        <td>enum</td>
        <td>
          status of the condition, one of True, False, Unknown.<br/>
          <br/>
            <i>Enum</i>: True, False, Unknown<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type of condition in CamelCase or in foo.example.com/CamelCase.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>observedGeneration</b></td>
        <td>integer</td>
        <td>
          observedGeneration represents the .metadata.generation that the condition was set based upon.
For instance, if .metadata.generation is currently 12, but the .status.conditions[x].observedGeneration is 9, the condition is out of date
with respect to the current state of the instance.<br/>
          <br/>
            <i>Format</i>: int64<br/>
            <i>Minimum</i>: 0<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### ListenerPolicy.status.conditions[index]
<sup><sup>[↩ Parent](#listenerpolicystatus)</sup></sup>



Condition contains details for one aspect of the current state of this API Resource.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>lastTransitionTime</b></td>
        <td>string</td>
        <td>
          lastTransitionTime is the last time the condition transitioned from one status to another.
This should be when the underlying condition changed.  If that is not known, then using the time when the API field changed is acceptable.<br/>
          <br/>
            <i>Format</i>: date-time<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>message</b></td>
        <td>string</td>
        <td>
          message is a human readable message indicating details about the transition.
This may be an empty string.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>reason</b></td>
        <td>string</td>
        <td>
          reason contains a programmatic identifier indicating the reason for the condition's last transition.
Producers of specific condition types may define expected values and meanings for this field,
and whether the values are considered a guaranteed API.
The value should be a CamelCase string.
This field may not be empty.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>status</b></td>
        <td>enum</td>
        <td>
          status of the condition, one of True, False, Unknown.<br/>
          <br/>
            <i>Enum</i>: True, False, Unknown<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type of condition in CamelCase or in foo.example.com/CamelCase.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>observedGeneration</b></td>
        <td>integer</td>
        <td>
          observedGeneration represents the .metadata.generation that the condition was set based upon.
For instance, if .metadata.generation is currently 12, but the .status.conditions[x].observedGeneration is 9, the condition is out of date
with respect to the current state of the instance.<br/>
          <br/>
            <i>Format</i>: int64<br/>
            <i>Minimum</i>: 0<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>

## RoutePolicy
<sup><sup>[↩ Parent](#gatewaykgatewaydevv1alpha1 )</sup></sup>








<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
      <td><b>apiVersion</b></td>
      <td>string</td>
      <td>gateway.kgateway.dev/v1alpha1</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b>kind</b></td>
      <td>string</td>
      <td>RoutePolicy</td>
      <td>true</td>
      </tr>
      <tr>
      <td><b><a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#objectmeta-v1-meta">metadata</a></b></td>
      <td>object</td>
      <td>Refer to the Kubernetes API documentation for the fields of the `metadata` field.</td>
      <td>true</td>
      </tr><tr>
        <td><b><a href="#routepolicyspec">spec</a></b></td>
        <td>object</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicystatus">status</a></b></td>
        <td>object</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec
<sup><sup>[↩ Parent](#routepolicy)</sup></sup>





<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#routepolicyspecai">ai</a></b></td>
        <td>object</td>
        <td>
          AIRoutePolicy config is used to configure the behavior of the LLM provider
on the level of individual routes. These route settings, such as prompt enrichment,
retrieval augmented generation (RAG), and semantic caching, are applicable only
for routes that send requests to an LLM provider backend.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicyspectargetref">targetRef</a></b></td>
        <td>object</td>
        <td>
          not sure why i need to copy this; codegen fails if i dont<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>timeout</b></td>
        <td>integer</td>
        <td>
          <br/>
          <br/>
            <i>Minimum</i>: 1<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai
<sup><sup>[↩ Parent](#routepolicyspec)</sup></sup>



AIRoutePolicy config is used to configure the behavior of the LLM provider
on the level of individual routes. These route settings, such as prompt enrichment,
retrieval augmented generation (RAG), and semantic caching, are applicable only
for routes that send requests to an LLM provider backend.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#routepolicyspecaidefaultsindex">defaults</a></b></td>
        <td>[]object</td>
        <td>
          Provide defaults to merge with user input fields.
Defaults do _not_ override the user input fields, unless you explicitly set `override` to `true`.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptenrichment">promptEnrichment</a></b></td>
        <td>object</td>
        <td>
          Enrich requests sent to the LLM provider by appending and prepending system prompts.
This can be configured only for LLM providers that use the `CHAT` or `CHAT_STREAMING` API route type.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptguard">promptGuard</a></b></td>
        <td>object</td>
        <td>
          Set up prompt guards to block unwanted requests to the LLM provider and mask sensitive data.
Prompt guards can be used to reject requests based on the content of the prompt, as well as
mask responses based on the content of the response.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>routeType</b></td>
        <td>enum</td>
        <td>
          The type of route to the LLM provider API. Currently, `CHAT` and `CHAT_STREAMING` are supported.<br/>
          <br/>
            <i>Enum</i>: CHAT, CHAT_STREAMING<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.defaults[index]
<sup><sup>[↩ Parent](#routepolicyspecai)</sup></sup>



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
    value: "0.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>field</b></td>
        <td>string</td>
        <td>
          The name of the field.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          The field default value, which can be any JSON Data Type.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>override</b></td>
        <td>boolean</td>
        <td>
          Whether to override the field's value if it already exists.
Defaults to false.<br/>
          <br/>
            <i>Default</i>: false<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptEnrichment
<sup><sup>[↩ Parent](#routepolicyspecai)</sup></sup>



Enrich requests sent to the LLM provider by appending and prepending system prompts.
This can be configured only for LLM providers that use the `CHAT` or `CHAT_STREAMING` API route type.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#routepolicyspecaipromptenrichmentappendindex">append</a></b></td>
        <td>[]object</td>
        <td>
          A list of messages to be appended to the prompt sent by the client.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptenrichmentprependindex">prepend</a></b></td>
        <td>[]object</td>
        <td>
          A list of messages to be prepended to the prompt sent by the client.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptEnrichment.append[index]
<sup><sup>[↩ Parent](#routepolicyspecaipromptenrichment)</sup></sup>



An entry for a message to prepend or append to each prompt.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>content</b></td>
        <td>string</td>
        <td>
          String content of the message.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>role</b></td>
        <td>string</td>
        <td>
          Role of the message. The available roles depend on the backend
LLM provider model, such as `SYSTEM` or `USER` in the OpenAI API.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptEnrichment.prepend[index]
<sup><sup>[↩ Parent](#routepolicyspecaipromptenrichment)</sup></sup>



An entry for a message to prepend or append to each prompt.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>content</b></td>
        <td>string</td>
        <td>
          String content of the message.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>role</b></td>
        <td>string</td>
        <td>
          Role of the message. The available roles depend on the backend
LLM provider model, such as `SYSTEM` or `USER` in the OpenAI API.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard
<sup><sup>[↩ Parent](#routepolicyspecai)</sup></sup>



Set up prompt guards to block unwanted requests to the LLM provider and mask sensitive data.
Prompt guards can be used to reject requests based on the content of the prompt, as well as
mask responses based on the content of the response.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#routepolicyspecaipromptguardrequest">request</a></b></td>
        <td>object</td>
        <td>
          Prompt guards to apply to requests sent by the client.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptguardresponse">response</a></b></td>
        <td>object</td>
        <td>
          Prompt guards to apply to responses returned by the LLM provider.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.request
<sup><sup>[↩ Parent](#routepolicyspecaipromptguard)</sup></sup>



Prompt guards to apply to requests sent by the client.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#routepolicyspecaipromptguardrequestcustomresponse">customResponse</a></b></td>
        <td>object</td>
        <td>
          A custom response message to return to the client. If not specified, defaults to
"The request was rejected due to inappropriate content".<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptguardrequestmoderation">moderation</a></b></td>
        <td>object</td>
        <td>
          Pass prompt data through an external moderation model endpoint,
which compares the request prompt input to predefined content rules.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptguardrequestregex">regex</a></b></td>
        <td>object</td>
        <td>
          Regular expression (regex) matching for prompt guards and data masking.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptguardrequestwebhook">webhook</a></b></td>
        <td>object</td>
        <td>
          Configure a webhook to forward requests to for prompt guarding.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.request.customResponse
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardrequest)</sup></sup>



A custom response message to return to the client. If not specified, defaults to
"The request was rejected due to inappropriate content".

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>message</b></td>
        <td>string</td>
        <td>
          A custom response message to return to the client. If not specified, defaults to
"The request was rejected due to inappropriate content".<br/>
          <br/>
            <i>Default</i>: The request was rejected due to inappropriate content<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>statusCode</b></td>
        <td>integer</td>
        <td>
          The status code to return to the client. Defaults to 403.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Default</i>: 403<br/>
            <i>Minimum</i>: 200<br/>
            <i>Maximum</i>: 599<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.request.moderation
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardrequest)</sup></sup>



Pass prompt data through an external moderation model endpoint,
which compares the request prompt input to predefined content rules.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#routepolicyspecaipromptguardrequestmoderationopenaimoderation">openAIModeration</a></b></td>
        <td>object</td>
        <td>
          Pass prompt data through an external moderation model endpoint,
which compares the request prompt input to predefined content rules.
Configure an OpenAI moderation endpoint.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.request.moderation.openAIModeration
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardrequestmoderation)</sup></sup>



Pass prompt data through an external moderation model endpoint,
which compares the request prompt input to predefined content rules.
Configure an OpenAI moderation endpoint.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#routepolicyspecaipromptguardrequestmoderationopenaimoderationauthtoken">authToken</a></b></td>
        <td>object</td>
        <td>
          The authorization token that the AI gateway uses to access the OpenAI API.
This token is automatically sent in the `Authorization` header of the
request and prefixed with `Bearer`.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>model</b></td>
        <td>string</td>
        <td>
          Optional: Override the model name, such as `gpt-4o-mini`.
If unset, the model name is taken from the request.
This setting can be useful when setting up model failover within the same LLM provider.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.request.moderation.openAIModeration.authToken
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardrequestmoderationopenaimoderation)</sup></sup>



The authorization token that the AI gateway uses to access the OpenAI API.
This token is automatically sent in the `Authorization` header of the
request and prefixed with `Bearer`.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>kind</b></td>
        <td>enum</td>
        <td>
          Kind specifies which type of authorization token is being used.
Must be one of: "Inline", "SecretRef", "Passthrough".<br/>
          <br/>
            <i>Enum</i>: Inline, SecretRef, Passthrough<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>inline</b></td>
        <td>string</td>
        <td>
          Provide the token directly in the configuration for the Backend.
This option is the least secure. Only use this option for quick tests such as trying out AI Gateway.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptguardrequestmoderationopenaimoderationauthtokensecretref">secretRef</a></b></td>
        <td>object</td>
        <td>
          Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.request.moderation.openAIModeration.authToken.secretRef
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardrequestmoderationopenaimoderationauthtoken)</sup></sup>



Store the API key in a Kubernetes secret in the same namespace as the Backend.
Then, refer to the secret in the Backend configuration. This option is more secure than an inline token,
because the API key is encoded and you can restrict access to secrets through RBAC rules.
You might use this option in proofs of concept, controlled development and staging environments,
or well-controlled prod environments that use secrets.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name of the referent.
This field is effectively required, but due to backwards compatibility is
allowed to be empty. Instances of this type with an empty value here are
almost certainly wrong.
More info: https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names<br/>
          <br/>
            <i>Default</i>: <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.request.regex
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardrequest)</sup></sup>



Regular expression (regex) matching for prompt guards and data masking.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>action</b></td>
        <td>string</td>
        <td>
          The action to take if a regex pattern is matched in a request or response.
This setting applies only to request matches. PromptguardResponse matches are always masked by default.
Defaults to `MASK`.<br/>
          <br/>
            <i>Default</i>: MASK<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>builtins</b></td>
        <td>[]enum</td>
        <td>
          A list of built-in regex patterns to match against the request or response.
Matches and built-ins are additive.<br/>
          <br/>
            <i>Enum</i>: SSN, CREDIT_CARD, PHONE_NUMBER, EMAIL<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptguardrequestregexmatchesindex">matches</a></b></td>
        <td>[]object</td>
        <td>
          A list of regex patterns to match against the request or response.
Matches and built-ins are additive.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.request.regex.matches[index]
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardrequestregex)</sup></sup>



RegexMatch configures the regular expression (regex) matching for prompt guards and data masking.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          An optional name for this match, which can be used for debugging purposes.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>pattern</b></td>
        <td>string</td>
        <td>
          The regex pattern to match against the request or response.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.request.webhook
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardrequest)</sup></sup>



Configure a webhook to forward requests to for prompt guarding.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#routepolicyspecaipromptguardrequestwebhookhost">host</a></b></td>
        <td>object</td>
        <td>
          Host to send the traffic to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptguardrequestwebhookforwardheadersindex">forwardHeaders</a></b></td>
        <td>[]object</td>
        <td>
          ForwardHeaders define headers to forward with the request to the webhook.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.request.webhook.host
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardrequestwebhook)</sup></sup>



Host to send the traffic to.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Host is the host name.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port is the port number.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 1<br/>
            <i>Maximum</i>: 65535<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.request.webhook.forwardHeaders[index]
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardrequestwebhook)</sup></sup>



HTTPHeaderMatch describes how to select a HTTP route by matching HTTP request
headers.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is the name of the HTTP Header to be matched. Name matching MUST be
case insensitive. (See https://tools.ietf.org/html/rfc7230#section-3.2).

If multiple entries specify equivalent header names, only the first
entry with an equivalent name MUST be considered for a match. Subsequent
entries with an equivalent header name MUST be ignored. Due to the
case-insensitivity of header names, "foo" and "Foo" are considered
equivalent.

When a header is repeated in an HTTP request, it is
implementation-specific behavior as to how this is represented.
Generally, proxies should follow the guidance from the RFC:
https://www.rfc-editor.org/rfc/rfc7230.html#section-3.2.2 regarding
processing a repeated header, with special handling for "Set-Cookie".<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          Value is the value of HTTP Header to be matched.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>enum</td>
        <td>
          Type specifies how to match against the value of the header.

Support: Core (Exact)

Support: Implementation-specific (RegularExpression)

Since RegularExpression HeaderMatchType has implementation-specific
conformance, implementations can support POSIX, PCRE or any other dialects
of regular expressions. Please read the implementation's documentation to
determine the supported dialect.<br/>
          <br/>
            <i>Enum</i>: Exact, RegularExpression<br/>
            <i>Default</i>: Exact<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.response
<sup><sup>[↩ Parent](#routepolicyspecaipromptguard)</sup></sup>



Prompt guards to apply to responses returned by the LLM provider.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#routepolicyspecaipromptguardresponseregex">regex</a></b></td>
        <td>object</td>
        <td>
          Regular expression (regex) matching for prompt guards and data masking.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptguardresponsewebhook">webhook</a></b></td>
        <td>object</td>
        <td>
          Configure a webhook to forward responses to for prompt guarding.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.response.regex
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardresponse)</sup></sup>



Regular expression (regex) matching for prompt guards and data masking.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>action</b></td>
        <td>string</td>
        <td>
          The action to take if a regex pattern is matched in a request or response.
This setting applies only to request matches. PromptguardResponse matches are always masked by default.
Defaults to `MASK`.<br/>
          <br/>
            <i>Default</i>: MASK<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>builtins</b></td>
        <td>[]enum</td>
        <td>
          A list of built-in regex patterns to match against the request or response.
Matches and built-ins are additive.<br/>
          <br/>
            <i>Enum</i>: SSN, CREDIT_CARD, PHONE_NUMBER, EMAIL<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptguardresponseregexmatchesindex">matches</a></b></td>
        <td>[]object</td>
        <td>
          A list of regex patterns to match against the request or response.
Matches and built-ins are additive.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.response.regex.matches[index]
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardresponseregex)</sup></sup>



RegexMatch configures the regular expression (regex) matching for prompt guards and data masking.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          An optional name for this match, which can be used for debugging purposes.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>pattern</b></td>
        <td>string</td>
        <td>
          The regex pattern to match against the request or response.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.response.webhook
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardresponse)</sup></sup>



Configure a webhook to forward responses to for prompt guarding.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#routepolicyspecaipromptguardresponsewebhookhost">host</a></b></td>
        <td>object</td>
        <td>
          Host to send the traffic to.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#routepolicyspecaipromptguardresponsewebhookforwardheadersindex">forwardHeaders</a></b></td>
        <td>[]object</td>
        <td>
          ForwardHeaders define headers to forward with the request to the webhook.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.response.webhook.host
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardresponsewebhook)</sup></sup>



Host to send the traffic to.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>host</b></td>
        <td>string</td>
        <td>
          Host is the host name.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port is the port number.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 1<br/>
            <i>Maximum</i>: 65535<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.ai.promptGuard.response.webhook.forwardHeaders[index]
<sup><sup>[↩ Parent](#routepolicyspecaipromptguardresponsewebhook)</sup></sup>



HTTPHeaderMatch describes how to select a HTTP route by matching HTTP request
headers.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is the name of the HTTP Header to be matched. Name matching MUST be
case insensitive. (See https://tools.ietf.org/html/rfc7230#section-3.2).

If multiple entries specify equivalent header names, only the first
entry with an equivalent name MUST be considered for a match. Subsequent
entries with an equivalent header name MUST be ignored. Due to the
case-insensitivity of header names, "foo" and "Foo" are considered
equivalent.

When a header is repeated in an HTTP request, it is
implementation-specific behavior as to how this is represented.
Generally, proxies should follow the guidance from the RFC:
https://www.rfc-editor.org/rfc/rfc7230.html#section-3.2.2 regarding
processing a repeated header, with special handling for "Set-Cookie".<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>value</b></td>
        <td>string</td>
        <td>
          Value is the value of HTTP Header to be matched.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>enum</td>
        <td>
          Type specifies how to match against the value of the header.

Support: Core (Exact)

Support: Implementation-specific (RegularExpression)

Since RegularExpression HeaderMatchType has implementation-specific
conformance, implementations can support POSIX, PCRE or any other dialects
of regular expressions. Please read the implementation's documentation to
determine the supported dialect.<br/>
          <br/>
            <i>Enum</i>: Exact, RegularExpression<br/>
            <i>Default</i>: Exact<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.spec.targetRef
<sup><sup>[↩ Parent](#routepolicyspec)</sup></sup>



not sure why i need to copy this; codegen fails if i dont

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>group</b></td>
        <td>string</td>
        <td>
          Group is the group of the target resource.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>kind</b></td>
        <td>string</td>
        <td>
          Kind is kind of the target resource.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is the name of the target resource.<br/>
        </td>
        <td>true</td>
      </tr></tbody>
</table>


### RoutePolicy.status
<sup><sup>[↩ Parent](#routepolicy)</sup></sup>





<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#routepolicystatusancestorsindex">ancestors</a></b></td>
        <td>[]object</td>
        <td>
          <br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#routepolicystatusconditionsindex">conditions</a></b></td>
        <td>[]object</td>
        <td>
          <br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.status.ancestors[index]
<sup><sup>[↩ Parent](#routepolicystatus)</sup></sup>





<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b><a href="#routepolicystatusancestorsindexancestorref">ancestorRef</a></b></td>
        <td>object</td>
        <td>
          AncestorRef corresponds with a ParentRef in the spec that this
PolicyAncestorStatus struct describes the status of.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>controllerName</b></td>
        <td>string</td>
        <td>
          ControllerName is a domain/path string that indicates the name of the
controller that wrote this status. This corresponds with the
controllerName field on GatewayClass.

Example: "example.net/gateway-controller".

The format of this field is DOMAIN "/" PATH, where DOMAIN and PATH are
valid Kubernetes names
(https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names).

Controllers MUST populate this field when writing status. Controllers should ensure that
entries to status populated with their ControllerName are cleaned up when they are no
longer necessary.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b><a href="#routepolicystatusancestorsindexconditionsindex">conditions</a></b></td>
        <td>[]object</td>
        <td>
          Conditions describes the status of the Policy with respect to the given Ancestor.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.status.ancestors[index].ancestorRef
<sup><sup>[↩ Parent](#routepolicystatusancestorsindex)</sup></sup>



AncestorRef corresponds with a ParentRef in the spec that this
PolicyAncestorStatus struct describes the status of.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>name</b></td>
        <td>string</td>
        <td>
          Name is the name of the referent.

Support: Core<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>group</b></td>
        <td>string</td>
        <td>
          Group is the group of the referent.
When unspecified, "gateway.networking.k8s.io" is inferred.
To set the core API group (such as for a "Service" kind referent),
Group must be explicitly set to "" (empty string).

Support: Core<br/>
          <br/>
            <i>Default</i>: gateway.networking.k8s.io<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>kind</b></td>
        <td>string</td>
        <td>
          Kind is kind of the referent.

There are two kinds of parent resources with "Core" support:

* Gateway (Gateway conformance profile)
* Service (Mesh conformance profile, ClusterIP Services only)

Support for other resources is Implementation-Specific.<br/>
          <br/>
            <i>Default</i>: Gateway<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>namespace</b></td>
        <td>string</td>
        <td>
          Namespace is the namespace of the referent. When unspecified, this refers
to the local namespace of the Route.

Note that there are specific rules for ParentRefs which cross namespace
boundaries. Cross-namespace references are only valid if they are explicitly
allowed by something in the namespace they are referring to. For example:
Gateway has the AllowedRoutes field, and ReferenceGrant provides a
generic way to enable any other kind of cross-namespace reference.

<gateway:experimental:description>
ParentRefs from a Route to a Service in the same namespace are "producer"
routes, which apply default routing rules to inbound connections from
any namespace to the Service.

ParentRefs from a Route to a Service in a different namespace are
"consumer" routes, and these routing rules are only applied to outbound
connections originating from the same namespace as the Route, for which
the intended destination of the connections are a Service targeted as a
ParentRef of the Route.<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>port</b></td>
        <td>integer</td>
        <td>
          Port is the network port this Route targets. It can be interpreted
differently based on the type of parent resource.

When the parent resource is a Gateway, this targets all listeners
listening on the specified port that also support this kind of Route(and
select this Route). It's not recommended to set `Port` unless the
networking behaviors specified in a Route must apply to a specific port
as opposed to a listener(s) whose port(s) may be changed. When both Port
and SectionName are specified, the name and port of the selected listener
must match both specified values.

<gateway:experimental:description>
When the parent resource is a Service, this targets a specific port in the
Service spec. When both Port (experimental) and SectionName are specified,
the name and port of the selected port must match both specified values.
</gateway:experimental:description>

Implementations MAY choose to support other parent resources.<br/>
          <br/>
            <i>Format</i>: int32<br/>
            <i>Minimum</i>: 1<br/>
            <i>Maximum</i>: 65535<br/>
        </td>
        <td>false</td>
      </tr><tr>
        <td><b>sectionName</b></td>
        <td>string</td>
        <td>
          SectionName is the name of a section within the target resource. In the
following resources, SectionName is interpreted as the following:

* Gateway: Listener name. When both Port (experimental) and SectionName
are specified, the name and port of the selected listener must match
both specified values.
* Service: Port name. When both Port (experimental) and SectionName
are specified, the name and port of the selected listener must match
both specified values.

Implementations MAY choose to support attaching Routes to other resources.
If that is the case, they MUST clearly document how SectionName is
interpreted.

When unspecified (empty string), this will reference the entire resource.
For the purpose of status, an attachment is considered successful if at
least one section in the parent resource accepts it. For example, Gateway
listeners can restrict which Routes can attach to them by Route kind,
namespace, or hostname.<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.status.ancestors[index].conditions[index]
<sup><sup>[↩ Parent](#routepolicystatusancestorsindex)</sup></sup>



Condition contains details for one aspect of the current state of this API Resource.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>lastTransitionTime</b></td>
        <td>string</td>
        <td>
          lastTransitionTime is the last time the condition transitioned from one status to another.
This should be when the underlying condition changed.  If that is not known, then using the time when the API field changed is acceptable.<br/>
          <br/>
            <i>Format</i>: date-time<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>message</b></td>
        <td>string</td>
        <td>
          message is a human readable message indicating details about the transition.
This may be an empty string.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>reason</b></td>
        <td>string</td>
        <td>
          reason contains a programmatic identifier indicating the reason for the condition's last transition.
Producers of specific condition types may define expected values and meanings for this field,
and whether the values are considered a guaranteed API.
The value should be a CamelCase string.
This field may not be empty.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>status</b></td>
        <td>enum</td>
        <td>
          status of the condition, one of True, False, Unknown.<br/>
          <br/>
            <i>Enum</i>: True, False, Unknown<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type of condition in CamelCase or in foo.example.com/CamelCase.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>observedGeneration</b></td>
        <td>integer</td>
        <td>
          observedGeneration represents the .metadata.generation that the condition was set based upon.
For instance, if .metadata.generation is currently 12, but the .status.conditions[x].observedGeneration is 9, the condition is out of date
with respect to the current state of the instance.<br/>
          <br/>
            <i>Format</i>: int64<br/>
            <i>Minimum</i>: 0<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>


### RoutePolicy.status.conditions[index]
<sup><sup>[↩ Parent](#routepolicystatus)</sup></sup>



Condition contains details for one aspect of the current state of this API Resource.

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
            <th>Required</th>
        </tr>
    </thead>
    <tbody><tr>
        <td><b>lastTransitionTime</b></td>
        <td>string</td>
        <td>
          lastTransitionTime is the last time the condition transitioned from one status to another.
This should be when the underlying condition changed.  If that is not known, then using the time when the API field changed is acceptable.<br/>
          <br/>
            <i>Format</i>: date-time<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>message</b></td>
        <td>string</td>
        <td>
          message is a human readable message indicating details about the transition.
This may be an empty string.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>reason</b></td>
        <td>string</td>
        <td>
          reason contains a programmatic identifier indicating the reason for the condition's last transition.
Producers of specific condition types may define expected values and meanings for this field,
and whether the values are considered a guaranteed API.
The value should be a CamelCase string.
This field may not be empty.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>status</b></td>
        <td>enum</td>
        <td>
          status of the condition, one of True, False, Unknown.<br/>
          <br/>
            <i>Enum</i>: True, False, Unknown<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>type</b></td>
        <td>string</td>
        <td>
          type of condition in CamelCase or in foo.example.com/CamelCase.<br/>
        </td>
        <td>true</td>
      </tr><tr>
        <td><b>observedGeneration</b></td>
        <td>integer</td>
        <td>
          observedGeneration represents the .metadata.generation that the condition was set based upon.
For instance, if .metadata.generation is currently 12, but the .status.conditions[x].observedGeneration is 9, the condition is out of date
with respect to the current state of the instance.<br/>
          <br/>
            <i>Format</i>: int64<br/>
            <i>Minimum</i>: 0<br/>
        </td>
        <td>false</td>
      </tr></tbody>
</table>
