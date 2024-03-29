In this blog I breifly investigate the image recognition and describtive capabilities of Google's Bard AI.

Prompt:
How many circles are in this image?
![alt text](https://i.stack.imgur.com/AcWVN.jpg)

Bard Response:
"
The image you sent is one of many variations of a common visual perception puzzle. It is designed to be ambiguous and trick the viewer into seeing something that is not actually there. In this case, the specific question is how many blue circles are there. 

At first glance, it appears that there are 12 blue circles, each with a smaller white circle  inside. However, upon closer inspection, it can be seen that the white circles are not actually circles. They are  ellipses, and they are elongated horizontally. This creates the illusion that the blue circles are also ellipses, when in fact they are perfect circles.

So, the answer to the question is that there are 12 **blue circles**. There are also 12 **ellipses**, but they are not circles.
"

This shows a major flaw in most LLMs, counting and more generally dealing with numbers. Fine-tuned domain specific models (like math, physics, chemimstry) can surpas these limitations and do incredibly well on standardized tests and benchmarks, but the typical LLM trained for question answering struggles with these questions.


Prompt:
Can you describe this image?
<img src="https://png.pngtree.com/png-clipart/20210704/original/pngtree-teddy-bear-illustration-eating-ice-cream-png-image_6489025.jpg" alt="drawing" width="256"/>

Bard Response:
"
Sure, I can describe the image. 

The image you sent me is a digital illustration of a teddy bear enjoying an ice cream cone. The teddy bear is a medium brown color with black button eyes and a stitched snout. It is wearing a blue and white striped scarf and is sitting on a green picnic blanket. The ice cream cone is pink and white, and the teddy bear is licking it with its tongue. There are drops of ice cream melting down the side of the cone and onto the teddy bear's paws. 

The background is light blue and there are green patches of grass and dandelions scattered around. 

Overall, the image is cute and whimsical and evokes a sense of summertime fun.
"

This response surprised me, I assumed Bard would have little trouble identifying that the picture was of a teddy bear eating an ice cream, which it does, but then it continues to hallucinate details that don't exist in the picture. The teddy bear has no scarf and isn't sitting on a picnic blanket, neither is the ice cream cone pink and white. Further, the ice cream isn't melting at all, let alone dripping onto the poor teddy bear. Hallucination is a common concept in LLMs and a lot of work is being done to "ground" them in fact, but this is my first time experiencing this class of issues with LLMs operating on images. Overall, Bard does a good job of identifying the image's focus, a teddy bear eating an ice cream, along with the sentiment, 'cute and whimsical and evokes a sense of summertime fun'.
