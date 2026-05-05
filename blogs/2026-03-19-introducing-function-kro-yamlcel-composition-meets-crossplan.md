---
title: "Introducing function-kro: YAML+CEL Composition Meets Crossplane"
url: "https://blog.crossplane.io/function-kro-yaml-cel/"
date: "Thu, 19 Mar 2026 10:59:28 GMT"
author: "Jared Watts"
feed_url: "https://blog.crossplane.io/rss/"
---
<figure class="kg-card kg-image-card"><img alt="Introducing function-kro: YAML+CEL Composition Meets Crossplane" class="kg-image" height="1125" src="https://blog.crossplane.io/content/images/2026/03/function-kro-blog-hero.png" width="2000" /></figure><!--kg-card-begin: markdown--><img alt="Introducing function-kro: YAML+CEL Composition Meets Crossplane" src="https://blog.crossplane.io/content/images/2026/03/function-kro-blog-hero-1.png" /><p>The combination of YAML+<a href="https://cel.dev/">CEL</a> provides a simple experience to define Kubernetes resources &#x2014; declare what you want, wire dependencies with CEL expressions, and let the system figure out the order. It&apos;s an intuitive model, and we&apos;ve been hearing from our community that they want this authoring experience inside Crossplane, alongside the many existing languages, functions, and experiences that Crossplane already supports.</p>
<p>We&apos;re excited to announce <strong>function-kro</strong> &#x2014; a Crossplane composition function that brings the YAML+CEL authoring model of <a href="https://kro.run/">kro</a> into Crossplane&apos;s pipeline architecture. Your kro-style resource definitions drop straight into a Composition pipeline step &#x2014; same syntax, same CEL expressions, unchanged and now running inside Crossplane. function-kro embeds kro&apos;s graph builder, CEL evaluator, and runtime engine to offer full feature parity with the latest kro release.</p>
<p>function-kro has been donated to the Crossplane community as a community extension project at <a href="https://github.com/crossplane-contrib/function-kro">crossplane-contrib/function-kro</a>. We&apos;ve shared it with the kro community and we welcome collaboration and contributions from anyone interested in this experience!</p>
<h2 id="the-function-pipeline">The Function Pipeline</h2>
<p>Below is a Crossplane <code>Composition</code> that uses function-kro to define a <code>NetworkingStack</code> platform API &#x2014; a VPC, Subnet, and SecurityGroup, all wired together with CEL expressions:</p>
<pre><code>apiVersion: apiextensions.crossplane.io/v1
kind: Composition
metadata:
  name: networkingstack
spec:
  compositeTypeRef:
    apiVersion: example.crossplane.io/v1
    kind: NetworkingStack
  mode: Pipeline
  pipeline:
  - step: kro-run
    functionRef:
      name: function-kro
    input:
      apiVersion: kro.fn.crossplane.io/v1beta1
      kind: ResourceGraph
      status:
        networkingInfo:
          vpcID: ${vpc.status.atProvider.id}
          subnetID: ${subnet.status.atProvider.id}
          securityGroupID: ${securityGroup.status.atProvider.id}
      resources:
      - id: vpc
        template:
          apiVersion: ec2.aws.m.upbound.io/v1beta1
          kind: VPC
          metadata: {}
          spec:
            forProvider:
              region: ${schema.spec.region}
              cidrBlock: 192.168.0.0/16
              enableDnsHostnames: false
              enableDnsSupport: true
      - id: subnet
        template:
          apiVersion: ec2.aws.m.upbound.io/v1beta1
          kind: Subnet
          metadata: {}
          spec:
            forProvider:
              region: ${schema.spec.region}
              cidrBlock: 192.168.0.0/18
              vpcId: ${vpc.status.atProvider.id}
      - id: securityGroup
        template:
          apiVersion: ec2.aws.m.upbound.io/v1beta1
          kind: SecurityGroup
          metadata: {}
          spec:
            forProvider:
              name: my-sg-${schema.metadata.name}
              region: ${schema.spec.region}
              description: Default security group for NetworkingStack
              vpcId: ${vpc.status.atProvider.id}
  - step: auto-ready
    functionRef:
      name: function-auto-ready
</code></pre>
<p>This is a two-step pipeline. Step one &#x2014; function-kro &#x2014; handles resource composition using kro&apos;s YAML+CEL model. Each resource is defined as a template with <code>${...}</code> CEL expressions that wire dependencies between them. <code>${schema.spec.region}</code> pulls from the Composite Resource (XR) spec, while <code>${vpc.status.atProvider.id}</code> creates a dependency on the VPC&apos;s output &#x2014; the subnets and security group won&apos;t be created until the VPC is ready and its ID is available. The <code>status</code> block aggregates data from composed resources back to the XR, so consumers of the <code>NetworkingStack</code> API can read the IDs of each resource directly from their XR&#x2019;s status.</p>
<p>Step two &#x2014; <code>function-auto-ready</code> &#x2014; handles automatic readiness detection. But the pipeline could have ten steps. Need to enforce policy on all resources? Add a step. Need to inject cost-allocation tags? Add a step. Need to pull secrets from an external API? Add a step. Each step is independent &#x2014; you can add the capabilities you need to support your simple resource definitions.</p>
<p>Again, the <code>resources</code> block in that Composition is identical to what you&apos;d write in a standalone kro ResourceGraphDefinition (RGD). If you already have kro resource definitions, they drop into the pipeline input without changes. And when you need more &#x2014; multi-cloud implementations, safe rollouts, operational controls &#x2014; you add pipeline steps without rewriting what you already have. Same composition language, with a growth path when you need more.</p>
<h2 id="simpleschema-for-crossplane">SimpleSchema for Crossplane</h2>
<p>kro bundles schema definition into the RGD using SimpleSchema &#x2014; a compact shorthand (e.g., <code>region: string | default=us-west-2</code>) that avoids writing full OpenAPIv3. This is a straightforward experience to define a schema, so we&#x2019;re making it available in Crossplane&#x2019;s developer tooling as well.</p>
<p>Given a kro-style RGD that includes SimpleSchema:</p>
<pre><code>apiVersion: kro.run/v1alpha1
kind: ResourceGraphDefinition
metadata:
  name: networkingstack
spec:
  schema:
    apiVersion: v1
    kind: NetworkingStack
    spec:
      region: string
    status:
      vpcID: ${vpc.status.atProvider.id}
      subnetID: ${subnet.status.atProvider.id}
      securityGroupID: ${securityGroup.status.atProvider.id}
  resources:
  - id: vpc
    template:
      # ... same resource templates as above
</code></pre>
<p>You&#x2019;d be able to generate the full Crossplane XRD with OpenAPIv3 schema automatically:</p>
<pre><code class="language-shell">crossplane xrd generate --input=rgd rgd.yaml
</code></pre>
<p>In other words, SimpleSchema becomes just another schema authoring option in Crossplane, similar to how function-kro is just another composition logic option. Write your schema and logic the way you prefer, and Crossplane handles the rest.</p>
<h2 id="running-inside-crossplanes-architecture">Running Inside Crossplane&apos;s Architecture</h2>
<p>Now that we&apos;ve seen the syntax, let&apos;s look at how these resource definitions fit into the broader Crossplane platform. Because function-kro is a function pipeline step, your YAML+CEL definitions automatically participate in the capabilities that Crossplane provides to all compositions. Crossplane does add some structure beyond a standalone RGD &#x2014; it separates your API schema from its implementation &#x2014; but that structure is what makes the following possible.</p>
<p><strong>Safe rollouts.</strong> CompositionRevisions let you pin existing instances to a known-good revision, roll forward team-by-team, and roll back without a rewrite. When you update your composition logic, it doesn&apos;t immediately affect every running instance. You control the blast radius.</p>
<p><strong>Pipeline composability.</strong> Add functions from a vast ecosystem of pipeline steps alongside your YAML+CEL definitions. Need to call an external API, query a cloud provider, connect to a secret store, or enforce policy? Add a pipeline step &#x2014; your resource definitions stay untouched. For cross-cutting concerns that push beyond what CEL can express, general-purpose languages like Go and Python are available as pipeline steps in the same Composition.</p>
<p><strong>Multi-implementation APIs.</strong> Define one API backed by multiple Compositions. The same NetworkingStack API can be backed by AWS, GCP, and Azure. One schema, many implementations. Platform teams define the API once and provide region or cloud-specific implementations behind it.</p>
<p><strong>Operational controls.</strong> Pausing reconciliation, management policies, and resource lifecycle control. When something goes wrong at 2 AM, you can stop reconciling a specific instance with a single annotation without touching the Composition or affecting other instances.</p>
<p><strong>Developer experience.</strong> Shift-left your testing and validation with <code>crossplane render</code>, unit tests, and integration tests. Run a Composition locally against a sample XR before deploying and see the same outputs that would surface at runtime. Diff your logic against a live environment with <a href="https://github.com/crossplane-contrib/crossplane-diff">crossplane-diff</a>. Develop your logic in a modular fashion with Crossplane&#x2019;s DevEx tooling.</p>
<h2 id="extensibility-offers-choice">Extensibility Offers Choice</h2>
<p>Crossplane&apos;s composition function architecture was designed around a simple idea: the platform team should pick the authoring model that fits their needs and skills. function-kro adds YAML+CEL to that already expansive menu.</p>
<p>Today, Crossplane supports <a href="https://github.com/crossplane-contrib/function-kcl/">KCL</a> for streamlined expressiveness, <a href="https://github.com/crossplane/function-sdk-go/">Go</a> and <a href="https://github.com/crossplane/function-sdk-python">Python</a> for teams that want full programming languages, <a href="https://github.com/crossplane-contrib/function-go-templating">YAML templating</a> for those familiar with Helm, <a href="https://github.com/crossplane-contrib/function-hcl">HCL</a> for those coming from Terraform, and many others. Now <a href="https://github.com/crossplane-contrib/function-kro">YAML+CEL</a> can be added to that list for teams that like declarative resource definitions with simple expressions to wire them all up.</p>
<p>You don&apos;t have to choose one approach for everything - different Compositions can use different functions, and a single pipeline can mix multiple languages across steps.</p>
<h2 id="get-involved">Get Involved</h2>
<p>We&apos;re continuing to track upstream kro releases and will keep function-kro current as the kro project evolves. We&apos;re also expanding our library of working examples &#x2014; YAML+CEL has been added to the <a href="https://docs.crossplane.io/latest/get-started/get-started-with-composition/">getting started with composition</a> guide in the Crossplane docs and the function repo includes <a href="https://github.com/crossplane-contrib/function-kro/tree/main/example">multiple examples</a> for basic composition, conditionals, readiness checks, collections, and external references to help you get started.</p>
<p>We welcome the kro community to start using and contributing to this new function! We love to hear from all users, as they are exactly what makes this project great. Whether you are a developer, user, or just interested in what we&apos;re up to, feel free to reach out via any of the following:</p>
<ul>
<li><a href="https://github.com/crossplane-contrib/function-kro">GitHub &#x2014; function-kro</a></li>
<li><a href="https://www.crossplane.io/">Crossplane website</a></li>
<li><a href="https://docs.crossplane.io/">Crossplane docs</a></li>
<li><a href="https://slack.crossplane.io/">Slack</a></li>
<li><a href="https://www.linkedin.com/company/crossplane/">LinkedIn</a></li>
<li><a href="https://www.youtube.com/@Crossplane">YouTube</a></li>
<li><a href="https://zoom-lfx.platform.linuxfoundation.org/meetings/crossplane?view=month%20">Community meetings</a></li>
</ul>
<!--kg-card-end: markdown-->
