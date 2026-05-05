---
title: "Introducing function-python"
url: "https://blog.crossplane.io/introducing-function-python/"
date: "Wed, 26 Mar 2025 02:26:53 GMT"
author: "Nic Cope"
feed_url: "https://blog.crossplane.io/rss/"
---
<img alt="Introducing function-python" src="https://blog.crossplane.io/content/images/2025/03/python-logo-master-v3-TM-1.png" /><p>We are excited to announce the first release of <a href="https://github.com/crossplane-contrib/function-python">Function Python</a>, a powerful new tool that enables you to write Crossplane compositions using Python. This release opens up new possibilities for platform engineers and developers who prefer Python&apos;s simplicity and readability when configuring Crossplane.</p><p>Function Python was developed by <a href="https://upbound.io">Upbound</a> and has now been contributed to the Crossplane project. This addition strengthens the growing set of tools available for defining compositions with Crossplane.</p><h2 id="what-are-crossplane-composition-functions">What Are Crossplane Composition Functions?</h2><p>In Crossplane, <strong>composition functions</strong> are custom programs that template Crossplane resources. They allow you to define how composite resources (XRs) should be composed from other Kubernetes resources. When you create a composite resource, Crossplane invokes these functions to determine the resources to create, update, or delete. This approach provides flexibility and enables advanced logic, such as loops and conditionals, in your infrastructure definitions.</p><h2 id="why-use-python-for-composition-functions">Why Use Python for Composition Functions?</h2><p>Python is renowned for its ease of use and extensive ecosystem. By writing composition functions in Python, you can leverage:</p><ul><li><strong>Readability</strong>: Python&apos;s clean syntax makes your composition logic easy to understand and maintain.</li><li><strong>Rich Libraries</strong>: Access to a vast array of libraries and frameworks to enhance your compositions.</li><li><strong>Rapid Development</strong>: Quickly prototype and iterate on your infrastructure definitions.</li></ul><p>With Function Python, you can now harness these benefits within the Crossplane ecosystem.</p><h2 id="getting-started-with-function-python">Getting Started with Function Python</h2><p>To start using Function Python in your Crossplane compositions:</p><p><strong>Install the Function</strong>: Apply the following manifest to install Function Python:</p><pre><code class="language-yaml">apiVersion: pkg.crossplane.io/v1
kind: Function
metadata:
  name: function-python
spec:
  package: xpkg.crossplane.io/crossplane-contrib/function-python:v0.1.0
</code></pre><p>This will deploy the Function Python package into your Crossplane environment.</p><p><strong>Define Your Composition</strong>: Create a <code>Composition</code> that references the <code>function-python</code> function. Here&apos;s an example snippet:</p><pre><code class="language-yaml">apiVersion: apiextensions.crossplane.io/v1
kind: Composition
metadata:
  name: example-composition
spec:
  compositeTypeRef:
    apiVersion: example.org/v1alpha1
    kind: XExample
  mode: Pipeline
  pipeline:
    - step: python
      functionRef:
        name: function-python
      input:
        apiVersion: fn.crossplane.io/v1alpha1
        kind: Script
        source: |
          from crossplane.function import v1alpha1 as fn
          def compose(request: fn.RunFunctionRequest) -&gt; fn.RunFunctionResponse:
            rsp.desired.resources[&quot;bucket&quot;].resource.update({
                &quot;apiVersion&quot;: &quot;s3.aws.upbound.io/v1beta2&quot;,
                &quot;kind&quot;: &quot;Bucket&quot;,
                &quot;spec&quot;: {
                    &quot;forProvider&quot;: {
                        &quot;region&quot;: req.observed.composite.resource[&quot;spec&quot;][&quot;region&quot;]
                    }
                },
            })
            rsp.desired.resources[&quot;bucket&quot;].ready = True</code></pre><p>Your script has access to <a href="https://github.com/crossplane/function-sdk-python">function-sdk-python</a>. For example you can <code>import crossplane.function.resource</code>. It also has access to the full Python standard library - use it with care.</p><p>The <a href="https://buf.build/crossplane/crossplane/docs/main:apiextensions.fn.proto.v1" rel="nofollow"><code>RunFunctionRequest</code> and <code>RunFunctionResponse</code> types</a> provided by the SDK are generated from a Protocol Buffers schema. Their fields behave similarly to built-in Python types like lists and dictionaries, but there are some differences. Read the <a href="https://protobuf.dev/reference/python/python-generated/" rel="nofollow">generated code documentation</a> to familiarize yourself with the the differences.</p><p><strong>Create Composite Resources</strong>: With the composition in place, you can now create composite resources that utilize your Python-based composition logic.</p><p>For a comprehensive guide on using composition functions, refer to the <a href="https://docs.crossplane.io/latest/guides/write-a-composition-function-in-python/">Crossplane documentation</a>.</p><h2 id="join-the-community">Join the Community</h2><p>Function Python is an open-source project under the Crossplane Contrib organization. We welcome contributions, feedback, and suggestions from the community. Visit the <a href="https://github.com/crossplane-contrib/function-python">GitHub repository</a> to report issues, submit pull requests, or explore the source code.</p><p>We look forward to seeing how the community leverages Function Python to build their control planes!</p>
