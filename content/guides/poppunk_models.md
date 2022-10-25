---
title: "A beginner's guide to fitting PopPUNK models"
description: "A complement to the documentation"
date: 2022-10-18T12:12:42+01:00
type: "post"
draft: false
author: "John Lees"
featured_image: '/images/header2.jpg'
---

[PopPUNK](https://www.poppunk.net/) now has a lot of different models available,
which can make it hard to know where to start, or to tell if you've done the right
thing when fitting one to your data.

Some questions I'll address:

{{< toc >}}

## Do you need to fit a new model?

If there is an existing one you can download
from [databases](https://www.poppunk.net/databases) then you can usually forgo this
step entirely. As well as avoiding extra work and validation, you'll also get consistent
cluster names with other studies, which is a big advantage.

If your species isn't listed, then you are going to need to fit a model. If you're happy
with your fit, we'd encourage you to share it with us (no need to share genome data) so we
can add it to the database list. Others will be able to benefit from it, and it will
build momentum for your nomenclature.

The other case is where the given model isn't exactly the resolution you want (too many,
or not enough clusters). In this case you probably want to try something like
`--multi-boundary` to get a few alternatives to compare.

A bad time to fit a new model is if you have a different dataset but the same species
as an existing model -- it's always worth trying the existing model first.

## Which model should I use?

The ideal model to use is one with a 2D boundary

### Refine/threshold

### Iterative PopPUNK

### BGMM

### DBSCAN


## Are my clusters correct?

## My clusters don't match MLST.


