# V2X-UniPool

## Data Formatting

The final data format should align with the reuqirements as the following:

```
{"query": "eeeee<image>eeeee<image>eeeee", "response": "fffff", "images": ["image_path1", "image_path2"]}
```

For openemma, it should contains the prevous **10** ego **front images**, **curvature**, **speed**, and **trajectory** (driving scenes and status of the past 5 seconds).

And after obtaining the above data, it then should be structured like:

```
query = f"""These are frames from a video taken by a camera mounted in the front of a car. The images are taken at a 0.5 second interval. 
        The 5 second historical velocities and curvatures of the ego car are {speed_curvature_str}. 
        Infer the association between these numbers and the image sequence. Generate the predicted future speeds and curvatures in the format [speed_1, curvature_1], [speed_2, curvature_2],..., [speed_10, curvature_10]. Write the raw text not markdown or latex. Future speeds and curvatures:"""
```
*The trajectory is also required because it will be used to compute the error and can serve as an alternative input for fine-tuning.*

Thus, the response shuold be 
```
[speed_1, curvature_1], [speed_2, curvature_2],..., [speed_10, curvature_10]
```

And the images should be the dirs of the previous 10 frames of the ego front camera.