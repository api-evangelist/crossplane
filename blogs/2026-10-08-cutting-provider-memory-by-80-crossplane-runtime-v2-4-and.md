---
title: "Cutting Provider Memory by 80%: crossplane-runtime v2.4 and Client Caching"
url: "https://blog.crossplane.io/cutting-provider-memory-by-80-crossplane-runtime-v2-4-and-client-caching/"
date: "2026-10-08"
author: "Jonasz Małecki"
feed_url: "https://blog.crossplane.io/feed/"
---
Crossplane providers have always paid a memory tax that grows with the size of the cluster they run in, not with the number of resources they manage. A provider watching ten managed resources on a cluster with two thousand CRDs and a few thousand Secrets could sit at well over
