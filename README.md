# Personalized Text-to-Image Generator

In the landscape of AI advancements, large text-to-image generation models have significantly
progressed, enabling the synthesis of high-quality, diverse images from textual prompts.
However, a notable gap remains in their capability to accurately replicate and creatively adapt
the appearance of novel subjects across various contexts. Recent studies have shown that we can
address these challenges, using models implemented by fine tuning the pre-trained diffusion
model. But these models are computationally expensive as they might require partial or complete
fine tuning of the pre-trained diffusion model. Our project is inspired from an innovative
approach which injects visual condition of the novel subject into the pretrained Stable Diffusion
model denoising process (based on the recent paper: ‘ViCo: Plug-and-Play Visual Condition for
Personalized Text-to-Image Generation’). This diffusion-based architecture uniquely embeds
visual conditions into the image generation diffusion process, facilitating dynamic,
context-sensitive synthesis from text inputs. Given a handful of images (4-7) showing a novel
object concept, the model can generate high quality images of this unique object following some
text guidance. This approach eliminates the need for any fine-tuning of the original diffusion
model parameters, thereby facilitating more flexible and scalable model deployment. This key
advantage distinguishes ViCo from most existing models that necessitate partial or full diffusion
fine-tuning. In this project, we plan to implement a personalized text-to-image generation model
based on the methodology described in the paper.


![teaser](https://github.com/kunaldudhavat/Personalized-text-to-image-generator/assets/54941117/96598ddc-8094-4e89-b12b-a3619c2c983f)

![image](https://github.com/kunaldudhavat/Personalized-text-to-image-generator/assets/78093389/23d7aceb-b62b-41c9-8f14-e3acdc35af38)
![image](https://github.com/kunaldudhavat/Personalized-text-to-image-generator/assets/78093389/bce6f3a0-fd84-4a3f-a292-2776616e980e)

