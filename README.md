
# What is pHash?

<div align="center">
  <img src="https://www.researchgate.net/profile/Jianfei-Yang-2/publication/300415034/figure/fig1/AS:370337138135040@1465306662353/Framework-of-the-proposed-Perceptual-Hashing-Tracking.png"
 width="600" height="300"/>
</div>

#### pHash is an open source software library released under the GPLv3 license that implements several perceptual hashing algorithms, and provides a C-like API to use those functions in your own programs.pHash itself is written in C++.

## Relevance of Perceptual Hashing
#### Perceptual hashes must be robust enough to take into account transformations or "attacks" on a given input and yet be flexible enough to distinguish between dissimilar files. Such attacks can include rotation, skew, contrast adjustment and different compression/formats. All of these challenges make perceptual hashing an interesting field of study and at the forefront of computer science research.

##### I see an improvement point here. Let’s say we have a component and the view model of the component have 8 different property to configure the view. It can be assumed that a fixed value or a nil value is assigned to a property. This ends up with 256 different variations. The number of variations is likely to be increased if projects supports dark mode or RTL languages. If any onf the mis supported, the total number of test cases become 512. If we assume that each image file is 10KB, the total size required to test for a simple view is around 5MB.
Apparently, this is not a big deal, otherwise there should already be an alternative. As i said, i see this as an improvement point and i propose that this redundant space requirement can be removed by using perceptual hashing.
Perceptual hash is similar to cryptographic hashes in terms of the idea of creating a fingerprint from a data. While cryptographic hash functions have avalanche effect which means the output of the hash function is being effected drastically even just for one bit of changes. However, output of perceptual hash functions are kept same or changed slightly with the small changes in the input data. This property of perceptual hashes make the reverse media search easier like Google Image Search or Shazam.
There are a couple of image hash functions available such as average hash, blockhash, perceptual hash, etc.. Many of them are compared in this article here and perceptual hash seems performing better. I will not go into the details of this algorithm but i recommend you to check how those algorithms work.
The output size of perceptual hashes are just 64bits. The outputs of them are not randomly distributed by design but it is possible to say two images are most probably similar images if their hash values are same. In the use cases of these algorithms, a threshold value is determined since having same values as a requirement for similarity can be too strict for just a search. The threshold value is simply calculated by Hamming distance of two hashes which is basically the number of different bits in two hashes.
Usage of a perceptual hash in testing is a new use case and same hash result should be expected from output of the tests. This is possible if it is guaranteed that the same simulator will be used for tests. When this is guaranteed, even a cryptographic hash may be possible to use. However, this condition is not feasible and different device simulators simulate different screens with different scale values. Basically, the output of two different simulators can produce scaled version of each other and since the data is different the hashes would also be different.
It is obvious that, even if scaled images represent different data, they are similar images. This can conclude that the perceptual hashes of them should be close to each other. Using a very small threshold can make the use of perceptual hashes possible in testing and it ends up with 64bits of space requirements for each snapshot which ends up with 4KB instead of 5MB in the previous example above.


[Info for perceptual hash](http://www.phash.org/)
