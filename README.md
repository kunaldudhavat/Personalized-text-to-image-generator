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

**Running the model:**

In this section, we describe the steps required for setting up the model, fine tuning it on a set of images featuring a novel subject and subsequently utilizing the fine-tuned model to generate creative images of the subject in diverse contexts, guided by textual prompts.

1. Firstly download the zip file containing the repository and extract it. 
2. Download the pretrained stable diffusion model from the link and save it under the folder models/stable-diffusion-v1/.
3. Then setup a conda environment which has all dependencies necessary for the model to run. For setting up the environment, run the below command:<br/>
```bash
conda env create -f environment.yml
```
5. Once the environment is created, you can activate the environment using the command:
conda activate vico
6. Now, that all the dependencies have been installed, we can fine tune the model using the following command: <br/>
```bash
python main.py --base configs/v1-finetune.yaml -t \ 
--actual_resume models/stable-diffusion-v1/sd-v1-4.ckpt \
-n  ""
--gpus GPUS 
--data_root DATA-ROOT 
--init_word INIT-WORD
```
6. In the above command, replace:
	DATA-ROOT with the path to the folder containing a set of reference images
	GPUS with a list of indices of the GPUs you want to train on, separated by commas. For example, we have used a single GPU to train the model, so we provided the variable as –gpus 0,
	INIT-WORD with a word that generally describes the subject. Eg: Toy, Dog
7. The training will run for about 10 minutes depending on the number of GPUs and the type of GPUs you are using. We have used a single A100 GPU, and the training ran for 11 minutes.
Once, the training is complete, we can find the fine tuned checkpoints under a new folder called logs
8. Now that the model is fine tuned on a given set of reference images, we can run inference on the fine tuned model to generate images of the subject under different contexts based on the text prompt given. For generating images using the fine tuned model, run the command below: <br/>
```bash
python scripts/vico_model.py --ddim_eta 0.0  --n_samples 4 \
 --n_iter 2  --scale 7.5  --ddim_steps 50  \
--ckpt_path models/stable-diffusion-v1/sd-v1-4.ckpt  \
--image_path IMAGE-PATH \
--ft_path CHECKPOINTS-PATH \ 
--load_step 399
--prompt TEXT-PROMPT
--outdir OUTPUT-DIR
```

9. In the above command, replace:<br/>
	IMAGE-PATH with the path to a reference image <br/>
	CHECKPOINTS-PATH to a path containing the folder checkpoints <br/>
	TEXT-PROMPT with your desired text prompt <br/>
	OUTPUT-DIR with the path to the folder in which you want the generated images to be saved. <br/>
We ran the model fine tuning and inference on a A100 GPU using Google Colab Pro. We have attached a Colab notebook to run the model on Google Colab. <br/>


You can use the colab file Personalized Text-to-Image Generator for doing the same steps.
