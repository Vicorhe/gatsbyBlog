---
title: Color Quantization w/ KMeans
category: "zombie notes"
cover: colors_thumbnail.jpg
---


Color Quantization — the process of representing an image with a smaller set of colors compared to the original range of colors.

It can be split into two steps: palette design and pixel mapping.

Palette design is the selection of a small set of colors that represent the original image colors.

Pixel mapping is the assignment of each input pixel to one of the palette colors.

One way to decide how an input pixel is assigned a palette color is to assign the palette color closest in distance.

For this situation a useful Python function is:
```
sklearn.metrics.pairwise_distances_argmin
# compute minimum distance between one point and a set of points.
# this function computes for each row in X, the index of the row in Y which is closest
# the minimum distances are returned
```

K-Means clustering is also good for quantization. 
Procedure
1. Apply the K-Means algorithm, specifying the number of centroids parameter to the intended palette size.
2. The resulting centroid will then function as the palette, there’s a good chance the colors on the palette aren’t present in the original image.
3. Each input pixel is them mapped the closest palette color either by using the accompanying K-Means predict method or the pairwise_distance_argmin mentioned above.

If speed is an issue, consider using MiniBatchKMeans. It is substantially faster than normal KMeans at the training stage. This comes at the cost of centroids being instable and sometimes color accuracy.

From my personal testing MiniBatchKMeans.predict is slightly faster than KMeans.predict, both of which run faster than pairwise_distance_argmin in the mapping stage.

##Alternative Color Spaces 
- LAB
    - separates chrominance from luminance
    - two levers, a* and b*, to control color
    - the euclidean distance implies perceptual meaning
- HSV(Hue Saturation Value)
    - separates chrominance from luminance 
    - one lever, Hue, to control color

##Tips
- Treat selecting color space and implementing quantization methods as separate tasks.  Don’t over complicate quantization.

##After Thoughts
- There exists other color quantization techniques I’ve yet to cover, like median split, uniform quantization, popularity quantization, artificial bee colony quantization, and so on.
- I just think KMeans are sufficient for my current needs and I will revisit this topic if that isn’t the case.

