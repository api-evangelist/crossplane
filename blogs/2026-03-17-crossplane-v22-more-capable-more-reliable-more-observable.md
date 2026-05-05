---
title: "Crossplane v2.2 — More Capable, More Reliable, More Observable"
url: "https://blog.crossplane.io/crossplane-v2-2-more-capable-more-reliable-more-observable/"
date: "Tue, 17 Mar 2026 15:30:00 GMT"
author: "Adam Wolfe Gordon"
feed_url: "https://blog.crossplane.io/rss/"
---
<figure class="kg-card kg-image-card"><img alt="Crossplane v2.2 &#x2014; More Capable, More Reliable, More Observable" class="kg-image" height="1125" src="https://blog.crossplane.io/content/images/2026/03/Option1_-Crossplane-v2.2---More-Capable--More-Reliable--More-Observable---Crossplane-Blog-Hero.png" width="2000" /></figure><img alt="Crossplane v2.2 &#x2014; More Capable, More Reliable, More Observable" src="https://blog.crossplane.io/content/images/2026/03/Option1_-Crossplane-v2.2---More-Capable--More-Reliable--More-Observable---Crossplane-Blog-Hero-1.png" /><p><br />We are excited to announce that Crossplane <a href="https://github.com/crossplane/crossplane/releases/tag/v2.2.0">v2.2.0</a> has been released and is now available for installation into your control planes. This release is a regular quarterly release focused on maturing key areas of functionality across the project, as Crossplane continues to become more capable, more reliable, and more performant for your production workloads. In this post, we&apos;ll dive into the highlights.</p><hr /><h2 id="debugging-with-the-pipeline-inspector-alpha">Debugging with the Pipeline Inspector (Alpha)</h2><p>Composition functions give platform builders the power to express arbitrarily complex resource generation logic, but debugging that logic inside a running control plane has historically been difficult. You can write tests and use <code>crossplane render</code> locally, but viewing the requests are going into each function step and the responses coming out required updating the pipeline or the functions themselves.</p><p>Crossplane v2.2 introduces a new alpha feature to address this: the <strong>pipeline inspector</strong>. When enabled, the inspector intercepts every function request and response in a composition pipeline and forwards them over gRPC to a user-configured socket path. This opens the door to a range of debugging and observability use cases &#x2014; from a local observer that dumps requests to stdout during development, to a production-grade system that stores pipeline traces for auditing or troubleshooting.</p><p>The pipeline inspector is disabled by default. To enable it, pass the <code>--enable-pipeline-inspector</code> flag to Crossplane. The default socket address is <code>/var/run/pipeline-inspector/socket</code>, which can be overridden by passing the <code>--pipeline-inspector-socket</code> flag. The full Helm values required to enable the inspector and run a basic pipeline logging sidecar are:</p><pre><code class="language-yaml"># Enable the pipeline inspector feature flag
args:
  - --enable-pipeline-inspector
  - --pipeline-inspector-socket=/var/run/pipeline-inspector/socket

# Inject the pipeline inspector sidecar
sidecarsCrossplane:
  - name: pipeline-inspector
    image: xpkg.crossplane.io/crossplane/inspector-sidecar:v0.0.3
    args:
      - --socket-path=/var/run/pipeline-inspector/socket
      - --max-recv-msg-size=8388608  # 8MB
    volumeMounts:
      - name: pipeline-inspector-socket
        mountPath: /var/run/pipeline-inspector
    resources:
      requests:
        cpu: 10m
        memory: 64Mi
      limits:
        cpu: 100m
        memory: 128Mi

# Add the shared volume for Unix socket communication
extraVolumesCrossplane:
  - name: pipeline-inspector-socket
    emptyDir: {}

extraVolumeMountsCrossplane:
  - name: pipeline-inspector-socket
    mountPath: /var/run/pipeline-inspector</code></pre><p>With this configured, Crossplane will forward a copy of each <code>RunFunctionRequest</code> and <code>RunFunctionResponse</code> to the inspector sidecar as the pipeline runs, giving you full visibility into the data flowing through your function pipeline. This feature remains <a href="https://docs.crossplane.io/v2.2/learn/feature-lifecycle/#alpha-features" rel="nofollow">Alpha</a> in v2.2 and will continue to be matured in future releases.</p><hr /><h2 id="runtime-configuration-for-package-dependencies">Runtime Configuration for Package Dependencies</h2><p>Previously, if you needed to configure a package&apos;s runtime you had to set a <code>runtimeConfigRef</code> directly on each package resource. This worked for explicitly installed packages, but had no effect on packages installed as dependencies. This made it difficult to leverage <code>Configuration</code> packages as a top-level construct.</p><p><code>ImageConfig</code>, introduced in Crossplane v1.18, has grown into a powerful centralized mechanism for configuring package installation. New in v2.2, <code>ImageConfig</code> can configure the <code>DeploymentRuntimeConfig</code> used by packages matching a given image prefix, including packages installed as dependencies. The new <code>spec.runtime.configRef</code> field lets you specify a runtime configuration and it applies to all matching packages regardless of how they are installed.</p><p>Consider a scenario where you&apos;re running on Azure and need your provider pods to use Azure Workload Identity. Previously, you might have disabled dependency resolution to install the provider manually. Now you can express this intent once, declaratively:</p><pre><code class="language-yaml">---
apiVersion: pkg.crossplane.io/v1beta1
kind: ImageConfig
metadata:
  name: azure-workload-identity
spec:
  matchImages:
    - prefix: xpkg.crossplane.io/crossplane-contrib/provider-azure-
    - prefix: xpkg.crossplane.io/crossplane-contrib/provider-family-azure
  runtime:
    configRef:
      name: azure-workload-identity

---
apiVersion: pkg.crossplane.io/v1beta1
kind: DeploymentRuntimeConfig
metadata:
  name: azure-workload-identity
spec:
  serviceAccountTemplate:
    metadata:
      annotations:
        azure.workload.identity/client-id: &quot;12345678-1234-1234-1234-123456789012&quot;
  deploymentTemplate:
    metadata:
      labels:
        azure.workload.identity/use: &quot;true&quot;
    spec:
      selector: {}
      template:
        metadata:
          labels:
            azure.workload.identity/use: &quot;true&quot;
        spec:
          containers:
            - name: package-runtime
              args: []</code></pre><p>With this <code>ImageConfig</code> in place, all Azure family providers &#x2014; whether installed explicitly or as dependencies &#x2014; will get the <code>azure-workload-identity</code> runtime configuration applied, and therefore have Workload Identity configured on their service accounts. Note that a matching <code>ImageConfig</code> runtime takes precedence over any <code>runtimeConfigRef</code> specified directly on a package&apos;s spec.</p><p>To confirm the configuration was applied, check the <code>appliedImageConfigRefs</code> field in the package revision&apos;s status:</p><pre><code class="language-shell">$ kubectl get providerrevision crossplane-contrib-provider-family-azure-e57d1e7b1ce7 -o yaml
# ...
status:
  appliedImageConfigRefs:
  - name: azure-workload-identity
    reason: ConfigureRuntime
# ...
</code></pre><hr /><h2 id="xrd-validation-beyond-the-spec">XRD Validation Beyond the Spec</h2><p>Crossplane XRDs let you define rich OpenAPI schemas for the resources your platform users create. Until now, <code>x-kubernetes-validations</code> (CEL validation rules) could only be used to validate fields within the <code>spec</code> of a composite resource. This left a real gap for platform builders who wanted to enforce naming conventions, require specific labels, or validate other metadata properties at admission time.</p><p>Crossplane v2.2 closes this gap by allowing XRDs to configure <code>x-kubernetes-validations</code> outside of <code>spec</code>. This lets you write CEL rules that validate things like the resource&apos;s name format or required label values and provide a more complete API contract for your composite resources.</p><p>For example, suppose your platform requires all XR names to follow a specific pattern. You can now enforce this directly in the XRD:</p><pre><code class="language-yaml">apiVersion: apiextensions.crossplane.io/v1
kind: CompositeResourceDefinition
metadata:
  name: databases.platform.example.org
spec:
  group: platform.example.org
  names:
    kind: Database
    plural: databases
  versions:
    - name: v1alpha1
      served: true
      referenceable: true
      schema:
        openAPIV3Schema:
          type: object
          x-kubernetes-validations:
            - rule: &quot;self.metadata.name.startsWith(&apos;db-&apos;)&quot;
              message: &quot;Database names must start with &apos;db-&apos;&quot;
          properties:
            spec:
              type: object
              properties:
                region:
                  type: string</code></pre><p>Any attempt to create an <code>Database</code> with a name that doesn&apos;t start with <code>db-</code> will now be rejected at the Kubernetes API server level, giving your users clear, immediate feedback rather than a confusing reconciliation error later.</p><hr /><h2 id="using-openapi-schemas-in-functions">Using OpenAPI Schemas in Functions</h2><p>Composition and operation functions may wish to know the OpenAPI schemas for the resources they&apos;re working with, for example to make schema-aware decisions, validate resources, or dynamically generate resources. Previously a function could indirectly get the OpenAPI schema for a CRD by requesting the CRD as a <code>RequiredResource</code> (or <code>ExtraResource</code> in Crossplane 1.x). However, schemas were not available for built-in Kubernetes kinds and some manipulation was necessary to extract the OpenAPI schema from the CRD.</p><p>Crossplane v2.2 introduces <code>RequiredSchemas</code> in the <code>RunFunctionResponse</code>, allowing functions to request schemas. Analogous to <code>RequiredResources</code>, a function can populate the new field with the API group/version/kind of any resources whose OpenAPI schema it needs and on the next reconciliation Crossplane will include the requested schemas in the function request.</p><p>With this expansion of the function gRPC API, Crossplane v2.2 also introduces capability advertisement. The <code>RunFunctionRequest</code> now includes a <code>Capabilities</code> field that tells the function what the running version of Crossplane supports. For example, a function that can optionally use OpenAPI schemas may check whether <code>Capabilities</code> contains <code>CAPABILITY_REQUIRED_SCHEMAS</code> to determine whether schemas are available.</p><hr /><h2 id="improvements-to-crossplane-beta-trace">Improvements to <code>crossplane beta trace</code></h2><p>Many platform engineers use the <code>crossplane beta trace</code> command is a to understand the state of resources in a Crossplane control plane. v2.2 ships two significant enhancements to make it even more useful.</p><p><strong>Trace all resources of a given kind.</strong> Previously, <code>crossplane beta trace</code> could take only a single resource instance. Now you can pass a kind (and optionally a namespace) to trace all resources of that type at once. This is helpful when you want to quickly understand the health of every <code>Database</code> or every <code>Provider</code> in your cluster:</p><pre><code class="language-shell"># Trace all Database resources in the platform namespace
crossplane beta trace databases.platform.example.org -n platform

# Trace all Providers
crossplane beta trace providers</code></pre><p><strong>Watch mode.</strong> The trace command now supports a <code>--watch</code> flag (shorthand <code>-w</code>), which keeps the trace output live and refreshes it as resources change, similar to <code>kubectl get --watch</code>. This is especially useful during debugging sessions when you&apos;re waiting for a resource to reconcile and want to see the dependency tree update in real time:</p><pre><code class="language-shell">crossplane beta trace databases.platform.example.org db-production --watch</code></pre><hr /><h2 id="notable-breaking-changes">Notable Breaking Changes</h2><p>Before upgrading, be aware of two breaking changes in v2.2:</p><p><strong>Function input CRDs are no longer installed.</strong> Input CRDs included in <code>Function</code> packages are no longer installed by the package manager, following the xpkg specification. Additionally, unknown or disallowed resource types within a package are now silently ignored instead of causing package installation to fail.</p><p><strong>Package cache on-disk structure has changed.</strong> The internal structure of the package cache has been updated. This breaks an undocumented behavior that allowed packages to be &quot;side-loaded&quot; directly into Crossplane, which was sometimes used for testing. If you relied on this behavior, please see <a href="https://github.com/crossplane/crossplane/pull/6981">#6981</a> and <a href="https://github.com/crossplane/crossplane/issues/7147">#7147</a> for details on the necessary changes.</p><hr /><h2 id="get-involved">Get Involved</h2><p>We love contributions from the community in any form: code contributions, issues, questions, feedback on proposals, and many more. Whether you are a developer, user, or just interested in what we&apos;re up to, feel free to join us via one of the following methods:</p><ul><li><a href="https://www.crossplane.io/" rel="nofollow">Crossplane website</a></li><li><a href="https://github.com/crossplane/crossplane">GitHub</a></li><li><a href="https://slack.crossplane.io/" rel="nofollow">Slack</a></li><li><a href="https://www.linkedin.com/company/crossplane/" rel="nofollow">LinkedIn</a></li><li><a href="https://www.youtube.com/@Crossplane" rel="nofollow">YouTube</a></li><li><a href="https://www.reddit.com/r/crossplane/" rel="nofollow">Reddit</a></li><li><a href="mailto:crossplane-info@lists.cncf.io">Email</a></li><li><a href="https://zoom-lfx.platform.linuxfoundation.org/meeting/98901510164?password=c60c41ae-1e1e-42d0-9a74-16de2fbb66f9&amp;invite=true" rel="nofollow">Attend a community meeting</a></li></ul>
