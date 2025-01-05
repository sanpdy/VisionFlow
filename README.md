# VisionFlow
VisionFlow is an innovative project aimed at learning a shared latent space between visual stimuli (images) and brain activity (fMRI responses). By leveraging Variational Autoencoders (VAEs) and Vision Transformers (ViT), VisionFlow enables image reconstruction from predicted fMRI signals.

## Objective

- Learn a shared latent space between paired images and human brain fMRI responses.
- Enable image reconstruction from predicted fMRI signals by aligning image-derived latent codes with fMRI-derived latent codes.

## Background

Brain imaging using fMRI illustrates how the human brain encodes visual information. VisionFlow employs VAEs and pretrained ViT models to map image features to corresponding fMRI signal representations, creating a bidirectional framework for image and fMRI interaction.

## Methodology

### Training Data
- Paired image and fMRI response datasets from human subjects.

### Model Architecture
1. **Encoder**: Pretrained Vision Transformer (ViT-16).
   - Extracts image features and outputs parameters for a latent distribution.
2. **Latent Space**: Represents both image and fMRI data.
   - `z_img`: Latent vector from images.
   - `z_fmri`: Latent vector from fMRI signals.
3. **fMRI Integration**: 
   - MLP for fMRI-to-latent mapping.
   - Another MLP for latent-to-fMRI reconstruction.
4. **Decoder**: Stack of `ConvTranspose2D` layers reconstructs images from latent vectors.

### Training Procedure
- **VAE Training**:
  - Image → ViT Encoder → Latent Vector (`z_img`) → Decoder → Reconstructed Image.
  - fMRI → MLP → Latent Vector (`z_fmri`).
- **Joint Objective**:
  - **Image Reconstruction Loss**: Ensures fidelity of reconstructed images.
  - **KL Divergence**: Regularizes latent space.
  - **Latent Alignment Loss**: Aligns `z_img` and `z_fmri`.
  - **fMRI Reconstruction Loss**: Ensures predicted fMRI signals match ground truth.

### Inference Procedure
1. **Image → fMRI Prediction**:
   - Encode image to latent vector (`z_img`).
   - Predict fMRI from latent vector using `latent_to_fmri` mapping.
2. **fMRI → Image Reconstruction**:
   - Convert predicted fMRI to latent vector via `fmri_to_latent`.
   - Decode latent vector to reconstruct the image.


## Results

- Trained for 5 epochs (can train longer for better results, however training is costly, and there are diminishing returns).
- Evaluation focused on latent alignment and image reconstruction fidelity.


## Files and Structure

- **Notebook**: `VAE_Testing.ipynb`
  - Contains model implementation, training loop, and evaluation results.
- **Presentation**: `Mapping Visual Stimuli to Brain Activity via VAE and ViT.pptx`
  - Detailed methodology, results, and architecture visuals.



## Requirements

- Python 3.7
- PyTorch
- Transformers (Hugging Face)
- h5py
- pandas
- Matplotlib


## Running the Code

1. Clone the repository.
2. Open `VAE_Testing.ipynb` in Jupyter Notebook and follow the instructions for preprocessing, training, and evaluation.


## Future Work

- Fine-tune model parameters for improved alignment and reconstruction.
- Extend training to additional datasets for robustness.
- Explore alternative architectures for better performance.


## Acknowledgments

This project builds on cutting-edge research in computational neuroscience and vision, leveraging tools like VAEs and ViTs to bridge the gap between visual stimuli and brain activity.

---

Feel free to contribute or raise issues for further development!
