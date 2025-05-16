---
layout: page
title: Automatic Polygon(Mask) Drawing
description: Using the Segment Anything Model for automatic polygon(Mask) drawing.
img: assets/img/sam.gif
importance: 1
category: Other Projects
---

<div style="text-align: justify;">
Implemented a Modified Segment Anything Model to facilitate real-time user interaction (50ms to 200ms latency) for
segmenting large TIFF images, generating precise polygon masks, and improving the efficiency and accuracy of polygon
drawing tools.<br><br>
</div>

<div class="row">
    <div class="col-xl mt-3 mt-md-0">
        <div class="embed-responsive embed-responsive-16by9">

        {% include video.liquid path="https://www.youtube.com/embed/dCxMem8kfn8" class="img-fluid rounded z-depth-1" autoplay=true %}
    </div>
    </div>

    <div class="col-xl mt-3 mt-md-0">
        <div class="embed-responsive embed-responsive-16by9">

        {% include video.liquid path="https://www.youtube.com/embed/CfU6KY6Fgc4" class="img-fluid rounded z-depth-1" autoplay=true %}
    </div>
    </div>

</div>

<div class="caption">
    Automatic Polygon(Mask) drawing with multiple positive prompts and negative prompts in large geo-image.
</div>

<div style="text-align: justify;">
    Segment Anything Model (SAM) is notable for its ability to understand a general notion of objects and generate masks for any object in it.<br><br>
</div>
<div style="text-align: justify;">
    <p>Traditional approaches required either interactive segmentation, which is dependent on human input for refining masks, or automatic segmentation, which is limited to predefined object categories and extensive manual annotation. SAM overcomes these limitations by being a single model capable of performing both interactive and automatic segmentation. Its promptable interface allows for a wide range of segmentation tasks through engineered prompts, like clicks, boxes, text, etc.
    </p>
    <p>
    The model has been optimized to run in real-time on a CPU in a web browser, which is crucial for interactive use. But it was not the case for the larger image. While running the SAM for a larger image size it took an hour which was the challenge.
    </p>
    <p>
    By modifying the architecture(confidential) of the SAM I was able to perform the real-time segmentation in the large geo-image with a size of around 300MB.
    </p>
</div>
