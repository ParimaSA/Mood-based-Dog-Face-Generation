# Mood-based-Dog-Face-Generation 🐶
This project focuses on Mood-based Dog Face Generation, aiming to generate dog face images that reflect specific emotional states such as happy, sad, or angry. The task explores how visual features can be associated with emotions and how these emotions can be expressed through synthesized images.

To achieve this, a Conditional Generative Adversarial Network (cGAN) is used to guide the image generation process based on predefined emotion labels. The model is trained on a dataset of dog images with associated mood annotations, allowing it to produce new images that match the desired emotional condition. 

## Motivation
<table>
  <tr>
    <td>
      <p>
        Mood-based Dog Face Generation is an interesting problem because recognizing dog emotions is difficult due to subtle visual cues and limited labeled data. These challenges make it hard to build accurate models. However, advances in generative models, especially GANs, offer a way to generate realistic dog faces based on emotional states.
      </p>
      <p>
        We chose this topic because it combines theory and practice. By exploring conditional GANs, we aim to generate synthetic dog facial expressions to address data scarcity, improve emotion recognition, and support applications that help humans better understand dogs.
      </p>
    </td>
    <td>
      <img src="https://canadiandogs.com/wp-content/uploads/dog-emotions-e1514490676196.jpg" alt="Dog Emotions Guide" width="1000">
    </td>
  </tr>
</table>


## Solution
This project focuses on understanding dog facial expressions and generating realistic synthetic images to address limited data. Dog emotion recognition is challenging due to subtle facial cues, large breed variation, and small labeled datasets.

|Method|Process|Strength|Weakness|
|--|--|--|--|
|Classical Computer Vision | Relies on hand-crafted features like shape, color, and specific facial landmarks. | Highly interpretable and computationally simple. | Struggles with variations in pose, lighting, and subtle expressions. |
|Rule-Based Systems | Depends on human-defined logic and domain expertise to categorize visual data. | Built on clear, expert-driven frameworks. | Limited flexibility and poor generalization to real-world scenarios. |
| Deep Learning (cGANs) | Learns features directly from data; Generator and Discriminator compete to create realistic images. | Capable of generating diverse, labeled data for augmentation. | Suffers from training instability and requires large datasets. |

In summary, deep learning is necessary due to the complex and nonlinear relationship between dog emotions and facial features. cGANs are a strong choice as they can both learn this relationship and generate additional data to overcome dataset limitations.

## Model
### Model Architecture
Conditional GAN (cGAN) consists of two main components: a generator and a discriminator. The generator creates synthetic dog face images based on a given emotion label, while the discriminator evaluates whether an image is real or generated and checks if it matches the specified emotion. Together, they are trained in a competitive process that improves the realism and correctness of the generated images.

<div align="center">

| **Discriminator** | **Generator** |
| :---: | :---: |
| <img src="https://github.com/ParimaSA/Mood-based-Dog-Face-Generation/blob/main/images/Discriminator.png?raw=true" alt="Discriminator Diagram" width="400"> | <img src="https://github.com/ParimaSA/Mood-based-Dog-Face-Generation/blob/main/images/Generator.png?raw=true" alt="Generator Diagram" width="400"> |

</div>

### Training Method
The model is trained using labeled dog face images to learn the relationship between visual features and emotional states. A conditional GAN (cGAN) is used, which includes a generator and a discriminator.

The generator takes random noise and a mood label to create synthetic dog face images, while the discriminator evaluates whether the images are real or fake and whether they match the given emotion. Both networks are trained together in an adversarial process: the generator tries to fool the discriminator, and the discriminator tries to correctly identify real and fake images.

This process is guided by a loss function that helps both networks improve over time, resulting in more realistic and accurate mood-based image generation.

#### Relevant Dataset
We trained our model using the Dog Emotion dataset from Kaggle: [Dog Emotion Dataset](https://www.kaggle.com/datasets/danielshanbalico/dog-emotion). 
This dataset contains 4,000 dog face images in total, with 1,000 images for each emotion class including angry, happy, relaxed, and sad.
<div align="center">
<img src="https://github.com/ParimaSA/Mood-based-Dog-Face-Generation/blob/main/images/SampleData.png?raw=true" alt="Sample Data" width="800">
</div>

### Evaluation Method
During training, generator and discriminator losses were monitored to track learning progress. The discriminator loss reflects how well it distinguishes real from fake images, while the generator loss shows how effectively it can fool the discriminator.

To evaluate results, we used both visual inspection and Fréchet Inception Distance (FID). Sample images were generated at different epochs to observe improvements in realism and consistency with mood labels. FID was used as a quantitative metric to measure similarity between generated and real images, where a lower score indicates better quality and diversity.

## Result
<table>
  <tr>
    <td>
      <p>The model was trained for 100 epochs and then fine-tuned for another 100 with lower learning rates. In the first 100 epochs, the generator loss started unstable but gradually stabilized, while the discriminator stayed relatively steady, indicating balanced training. Toward the end of this phase, the discriminator gained an edge, prompting the decision to fine‑tune with smaller learning rates.>
      </p>
    </td>
    <td>
      <div align="center">
      <img src="https://github.com/ParimaSA/Mood-based-Dog-Face-Generation/blob/main/images/TrainingLoss.png?raw=true" alt="Sample Data" width="2000">
      </div>
    </td>
  </tr>
</table>
<table>
  <tr>
    <td width="61%">
      <p>
        Fréchet Inception Distance (FID) was used to evaluate image quality. FID slightly improved from 193.20 at epoch 100 to 186.88 at epoch 200, with minor fluctuations in between. 
      </p>
      <p>
        Although this shows modest improvement, the scores remain relatively high, indicating that generated images are still noticeably different from real ones.
      </p>
    </td>
    <td width="39%">
      <table align="center">
        <thead>
          <tr>
            <th>Checkpoint</th>
            <th>FID Score</th>
          </tr>
        </thead>
        <tbody>
          <tr><td>Epoch 100</td><td>193.20</td></tr>
          <tr><td>Epoch 120 (↘)</td><td>189.53</td></tr>
          <tr><td>Epoch 150 (↗)</td><td>191.04</td></tr>
          <tr><td>Epoch 180 (↘)</td><td>187.47</td></tr>
          <tr><td>Epoch 200 (↘)</td><td>186.88</td></tr>
        </tbody>
      </table>
    </td>
  </tr>
</table>




Visually, the model produces dog‑like shapes, colors, and textures, but outputs are often blurry and emotional differences between classes are not clearly visible.
<div align="center">
<img src="https://github.com/ParimaSA/Mood-based-Dog-Face-Generation/blob/main/images/GeneratedImage.png?raw=true" alt="Sample Data" width="800">
</div>

## Conclusion
The final cGAN learned rough dog‑like structures, colors, and textures, but the generated images remain blurry and emotional differences between classes are often unclear. This is expected because the dataset is small, the images are low‑resolution (64×64), dog emotions are visually subtle, and GAN training is inherently unstable, sometimes allowing the discriminator to dominate.

The best checkpoint was selected based on FID, with epoch 200 achieving the lowest score of 186.88. Although this score is still high, it shows improvement over earlier checkpoints and indicates that the final preprocessing and training strategy helped align the generated distribution closer to the real data.

Future improvements could include using a larger dog face dataset, applying face detection and cropping, training at higher resolution, or adopting stronger generative models such as StyleGAN2 or diffusion models.

## Member
| Member | Responsibility |
|--------|----------------|
|Natcha Ranchan 6610545260| Responsible for the practical implementation of the project, including setting up the training environment in Google Colab, building and training the cGAN model, running experiments, and recording results. Also responsible for answering key questions in the report by providing findings and observations from the training process.|
|Parima Sangsirakoup 6610545367|Responsible for compiling the final report by organizing the findings and answers from Natcha into a structured format, and enriching the content with additional references and background information for deeper context. Additionally responsible for creating the GitHub repository, uploading the code, and converting the report into a README file.|

