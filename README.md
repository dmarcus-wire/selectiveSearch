# Object Detection using Selective Search

Selective Search is meant to replace the computationally expensive, highly inefficient method of exhaustively using image pyramids and sliding windows to examine locations of an image for a potential object.

By using Selective Search, we can more efficiently examine regions of an image that likely contain an object and then pass those regions on to a SVM, CNN, etc. for final classification.

If you are using Selective Search, just keep in mind that the Selective Search algorithm will not give you class label predictions — it is assumed that your downstream classifier will do that for you

Select Search over-segments an image using superpixel alg. and measures similarity:
1. color (25-bin histogram)
1. texture (Gaussian derivatives)
1. size (Hierarchical Agglomerative Clustering (HAC))
1. shape (fitness)
1. meta (linear combo of the above)

Benefits:
1. faster and more efficient than sliding windows and image pyramids
1. accurate detecting regions of an image containing the object
1. passes candidates downstream

Running the fast method on the drone image: .47s generated 327 proposals. Most could be filtered out via pipeline.
[INFO] using *fast* selective search
[INFO] selective search took 0.4779 seconds
[INFO] 327 total region proposals

(selectiveSearch) davidmarcus@MacBook-Pro selectiveSearch % python selective_search.py --image drone.jpeg --method quality
Rinning the quality method on the drone image: 1.1s generated 950 proposals. More regions + more time on CPU/GPU = more expensive. worth it?
[INFO] using *quality* selective search
[INFO] selective search took 1.1471 seconds
[INFO] 950 total region proposals
