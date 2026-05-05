---
title: "Strengthening Crossplane's Community-Driven Ecosystem"
url: "https://blog.crossplane.io/community-ecosystem/"
date: "Tue, 25 Feb 2025 18:51:37 GMT"
author: "Bassam Tabbara"
feed_url: "https://blog.crossplane.io/rss/"
---
<!--kg-card-begin: markdown--><img alt="Strengthening Crossplane&apos;s Community-Driven Ecosystem" src="https://blog.crossplane.io/content/images/2025/02/Greencity.svg" /><p>The Crossplane community has always thrived on collaboration, innovation, and openness. Today, we&apos;re excited to announce key updates aimed at fostering the growth of community-contributed Crossplane extensions (providers and functions) while reinforcing our commitment to vendor neutrality&#x2014;just like all CNCF projects.</p>
<p>We recognize the importance of ensuring that all community-driven contributions remain accessible, well-maintained, and free from vendor lock-in. These updates provide clear expectations and a neutral foundation to support the entire Crossplane ecosystem.</p>
<h2 id="what%E2%80%99s-changing">What&#x2019;s Changing?</h2>
<h3 id="clear-expectations-for-community-contributed-extensions">Clear Expectations for Community-Contributed Extensions</h3>
<p>We are introducing operational guidelines for maintaining extensions contributed under the <code>github.com/crossplane-contrib</code> organization. These policies ensure that community extensions are properly maintained, fostering long-term sustainability and reliability.</p>
<h3 id="a-vendor-neutral-community-driven-home-for-extensions">A Vendor-Neutral, Community-Driven Home for Extensions</h3>
<p>To enhance accessibility and neutrality, all community-contributed extensions will now be published, at a minimum, to <code>ghcr.io/crossplane-contrib</code>. Project documentation will reference this location, providing a consistent and independent source that the entire community can trust&#x2014;regardless of vendor affiliations.</p>
<p>By reinforcing vendor neutrality, we align with the broader CNCF ecosystem&#x2019;s principles, ensuring that Crossplane remains an open, community-first project. These changes support our shared goal of making Crossplane the best choice for building cloud-native control planes while improving transparency, accessibility, and long-term adoption.</p>
<p>Your contributions and feedback fuel Crossplane&#x2019;s success. We appreciate your continued support and look forward to building a strong, open, and vendor-neutral ecosystem together!</p>
<h2 id="the-crossplane-ecosystem">The Crossplane Ecosystem</h2>
<!--kg-card-end: markdown--><figure class="kg-card kg-image-card"><img alt="Strengthening Crossplane&apos;s Community-Driven Ecosystem" class="kg-image" height="960" src="https://blog.crossplane.io/content/images/2025/02/ecosystem-diagram.png" width="1346" /></figure><!--kg-card-begin: markdown--><p>Crossplane has a large and thriving ecosystem of providers and functions&#x2014;collectively referred to as extensions. These extensions can be public or private and maintained by individuals, end-user organizations, or vendors.</p>
<p>A subset of these extensions has been donated to the Crossplane project and resides in the <code>crossplane-contrib</code> GitHub organization. With today&apos;s governance updates, these projects will follow the same requirements as the Crossplane core project.</p>
<h2 id="the-goals-of-crossplane-contrib">The Goals of <code>crossplane-contrib</code></h2>
<p>From its inception, <code>crossplane-contrib</code> was created to provide a collaborative home for community-driven Crossplane extensions. With today&#x2019;s changes, we are introducing a clear health criteria for these projects, aligned with the CNCF&#x2019;s standards. These criteria include:</p>
<ul>
<li>Regular builds</li>
<li>A vendor-neutral home for released OCI images</li>
</ul>
<p>However, it is not a requirement for all Crossplane extensions to reside in <code>crossplane-contrib</code>. To ensure the ecosystem thrives, there must be opportunities for differentiation through commercial offerings and services around these extensions.</p>
<h2 id="regular-builds-for-community-extensions">Regular Builds for Community Extensions</h2>
<p>A key governance update requires that all extensions donated to <code>github.com/crossplane-contrib</code> provide regular builds, ensuring the community has reliable access to up-to-date extensions. This change will help maintain a curated and well-maintained catalog of community extensions.</p>
<h2 id="introducing-xpkgcrossplaneio">Introducing <code>xpkg.crossplane.io</code></h2>
<p>All Crossplane packages&#x2014;including Crossplane itself and community-contributed extensions&#x2014;will be hosted on GitHub Container Registry (GHCR) at <code>ghcr.io/crossplane-contrib</code> and proxied via <code>xpkg.crossplane.io</code>.</p>
<p>Previously, much of the community content was served from <code>xpkg.upbound.io</code>. To ensure vendor neutrality, Crossplane and community content will now be published to <code>xpkg.crossplane.io</code>. Additionally, content can be published to other registries such as Upbound and Docker Hub.</p>
<h2 id="api-groups-for-extensions">API Groups for Extensions</h2>
<p>Crossplane providers define managed resources using Kubernetes API conventions. Moving forward:</p>
<ul>
<li>All new extension projects in <code>crossplane-contrib</code> must use a <code>crossplane.io</code> API group.</li>
<li>Existing projects that are later donated to Crossplane will not be required to change their API group, as this would introduce breaking changes for existing compositions.</li>
</ul>
<h2 id="updates-to-crossplane-documentation-and-website">Updates to Crossplane Documentation and Website</h2>
<p>To maintain vendor neutrality, the Crossplane documentation and website will only reference community extensions. Commercial offerings related to Crossplane will be listed separately on a dedicated Enterprise page.</p>
<h2 id="implementing-the-new-policies">Implementing the New Policies</h2>
<p>Over the coming weeks, we will work with community maintainers to bring their Crossplane extensions into compliance with these new policies. Additionally, project documentation will be updated to refer to images from GHCR.</p>
<h2 id="looking-ahead">Looking Ahead</h2>
<p>We&#x2019;re excited about the future of Crossplane and the continued growth of community contributions. We look forward to discussing these updates and other new features at this year&#x2019;s KubeCon in London&#x2014;be sure to stop by our booth!</p>
<p>The Crossplane community is at the heart of this project&#x2019;s success. Whether you&apos;re a developer, user, or just interested in what we&apos;re building, we&#x2019;d love to hear from you! Connect with us through the following channels:</p>
<ul>
<li><a href="https://crossplane.io"><strong>Crossplane Website</strong></a></li>
<li><a href="https://github.com/crossplane/crossplane"><strong>GitHub</strong></a></li>
<li><a href="https://slack.crossplane.io"><strong>Slack</strong></a></li>
</ul>
<p>Let&#x2019;s continue building a strong, open, and vendor-neutral ecosystem together!</p>
<!--kg-card-end: markdown-->
