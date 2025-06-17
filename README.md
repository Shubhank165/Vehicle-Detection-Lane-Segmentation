Real-Time Lane Segmentation for Autonomous Pathfinding
This repository documents the development of a deep learning model for real-time lane segmentation. The ultimate goal of this project is to create a system that can identify lane boundaries from a video feed, enabling vehicle density calculation for each lane and providing optimal pathfinding recommendations for emergency vehicles.
This README outlines the progress so far, detailing the model architecture, training process, and key achievements.
Project Status: High-Performance Baseline Model Complete
We have successfully developed and validated a powerful lane segmentation model. The current status is:
A robust, fine-tuned U-Net model has been trained and has demonstrated high accuracy on its primary training domain.
The model is capable of cleanly segmenting lane markings from complex, driver-perspective road images.
A clear path forward has been identified to adapt this model for new, more challenging visual domains (e.g., high-angle CCTV footage).
Key Achievements
The project progressed through several key stages, each building upon the last to create a progressively better model.
1. Foundational Model Training
Architecture: A classic U-Net architecture was implemented using PyTorch. This model is renowned for its effectiveness in biomedical and, more recently, autonomous driving segmentation tasks due to its powerful encoder-decoder structure and use of skip connections to preserve spatial information.
Initial Training: The model was first trained on the TuSimple Lane Detection dataset, using a 256x512 resolution. This phase involved significant debugging and established a proof-of-concept, but performance was limited by a standard BCEWithLogitsLoss function.
2. Advanced Training and Fine-Tuning
Improved Training Objective: The training process was upgraded to use DiceLoss, a loss function far better suited for imbalanced segmentation tasks. This directly optimized the model to maximize the overlap (Dice Score) between its predictions and the ground truth.
High-Resolution Fine-Tuning: The best model from the initial phase was then fine-tuned on a higher 640x640 resolution. This stage was critical for enabling the model to learn more precise features from more detailed images.
Robustness through Augmentation: To prepare the model for real-world conditions, aggressive data augmentations were introduced during training. Techniques like RandomShadow, CLAHE (for contrast), and GaussNoise were used to create a model more resilient to varied lighting and weather.
3. Achieved Performance
The final fine-tuned model achieved a peak validation Dice Score of 0.74 on the TuSimple dataset.
Visual inference tests show that this model produces clean, confident, and accurate segmentation masks on "in-domain" images (i.e., those from a driver's perspective), successfully handling curves and occlusion by other vehicles.
<p align="center">
<img src="[URL_TO_YOUR_GOOD_RESULT_IMAGE.jpg](https://ibb.co/5XnYZZJd)" alt="Successful Lane Detection" width="700"/>
<br>
<em>Example of the fine-tuned model successfully segmenting lanes on a test image.</em>
</p>
The Domain Adaptation Challenge
When tested on a high-angle CCTV video, the model's performance dropped significantly. This is a classic "domain gap" problem: the model is an expert on the data it was trained on (low-angle, driver-view) but is a novice on the new perspective.
This is not a failure but a planned-for, advanced challenge in the project lifecycle. The strong performance of the fine-tuned model provides an excellent foundation to solve this problem.
Next Steps
The project is now poised for its final and most important phase: Domain-Specific Adaptation.
Custom Dataset Creation: Extract a small (50-100 frames) but representative dataset from the target CCTV video.
Manual Annotation: Manually create high-quality segmentation masks for these frames, teaching the model what "lanes" look like from this new perspective.
Final Fine-Tuning: Use the current high-performance model as a starting point and fine-tune it on this new, custom-annotated dataset. This will adapt its knowledge to the target domain.
Full Pipeline Integration: Once the segmentation is robust, integrate the output with a vehicle detection model and a post-processing script to calculate lane density and fulfill the project's primary objective.
