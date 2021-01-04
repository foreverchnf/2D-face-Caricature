# 2D-face-Caricature 
**Based on stylegan2 and [Justin Pinkney's Website](https://www.justinpinkney.com)**

## 1.Prepare Dataset
### a.[FERG_DB_256](http://grail.cs.washington.edu/projects/deepexpr/ferg-2d-db.html) 
That's a dataset from Washington University.
I choose 776 photos from those characters which has more than 100 from each one with different expressions.
Use dataset_tool.py to create .tfrecord format.

<img src="photos/reals.jpg" width="750" height="400" alt="dataset"/></div>

### b.yuanshen
To be done. Currently can't get hundreds of faces of yuanshen chracters.

## 2.Transfer Learning
Choose a Pretrained model that matches the size of dataset.
The less FID of the model, the better.
**Gotta to change some parameters in training_loop.py to control the interval between two snapshots**. 
Because after a small amount of training, it will acheive a good results and it's also not suitable to training too long. 
You need to choose and try to find out which snapshot get the best performance.

The pretrained model [ffhq-256-config-e-003810.pkl](https://github.com/justinpinkney/awesome-pretrained-stylegan2#faces-FFHQ-config-e-256x256):

<img src="photos/ffhq-config-e.jpg" width="750" height="400" alt="dataset"/></div>

Transfer learning after 16 kimg:

<img src="photos/fakes_000016.jpg" width="750" height="400" alt="dataset"/></div>

## 3.Blending Models
It's also a process to try and find in which resolution to exchange two models weights is the best.

### Take 256*256 size for example

Blend at 8\16\32:

<img src="photos/blend-256.jpg" width="900" height="300" alt="dataset"/></div>

Blend at 64\128:

<img src="photos/blend-256-2.jpg" width="600" height="300" alt="dataset"/></div>

32 for 256 models and 64 for 1024 models are good choices to make Caricature face with realistic feature of human.

## 4.Projecting and Generating
### a.Aligned photos at first.
### b.Project them to latent space and save as .npy format with project_images.py
### c.Use blended model to regenerate Caricature photos
