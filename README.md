# CSI-Channel Spatial Decomposition for WiFi-Based Human Pose Estimation in Rescue Scenarios

A deep-learning framework for estimating human body poses from WiFi Channel State Information (CSI) in visually degraded rescue environments. The project processes multi-antenna and multi-subcarrier CSI measurements to identify human-induced channel variations and estimate 2D or 3D body keypoints. It is designed for research involving smoke-filled rooms, darkness, visual obstruction, indoor disasters, and non-line-of-sight conditions.

> **Research status:** This repository contains an experimental prototype. It is not certified for emergency-response, medical, or other safety-critical applications.

---

## Overview

Camera-based pose-estimation systems may fail when illumination is poor or when smoke, dust, debris, or physical obstacles block the camera view. WiFi signals can continue propagating under some of these conditions and are affected by human movement through reflection, diffraction, scattering, and multipath propagation. Channel State Information provides measurements of the amplitude and phase response of individual OFDM subcarriers and antenna links. The proposed framework uses these measurements to extract spatial and temporal features associated with human posture and movement.

The main processing pipeline is:
![](https://github.com/1Px-Vision/WiFi-CSI-SAR/blob/main/WIFI_CSI_SAR.png)

WiFi CSI-based human pose estimation pipeline for rescue scenarios. Multi-receiver WiFi probing captures human-induced channel variations, which are preprocessed, spatially decomposed, and fused across packets and receivers. A deep-learning model then reconstructs 3D rescue-relevant poses, including standing, kneeling, crawling, and fallen postures, to support victim localization, fallen-person detection, search-and-rescue monitoring, and responder assistance.
---

## Objectives

* Process CSI measurements from multiple antennas and OFDM subcarriers.
* Suppress static environmental components and hardware noise.
* Extract human-induced spatial and temporal channel variations.
* Estimate 2D or 3D human body keypoints.
* Recognize rescue-relevant postures such as crawling, lying, kneeling, and falling.
* Evaluate performance under line-of-sight and non-line-of-sight conditions.
* Support multimodal systems combining CSI with thermal, RGB, radar, LiDAR, or inertial sensing.

---

## Potential Applications

* Human detection in smoke-filled or dark environments.
* Fallen-person and motionless-person detection.
* Monitoring trapped victims behind lightweight obstacles.
* Post-earthquake and collapsed-building assessment.
* Indoor search-and-rescue support.
* Human–robot and human–UAV rescue coordination.
* Privacy-preserving posture and occupancy sensing.

WiFi sensing should be used as a complementary modality rather than the sole source of information for rescue decisions.

---
### Human Pose

![](https://github.com/1Px-Vision/WiFi-CSI-SAR/blob/main/WIFI_CSI_Pose.jpg)

### Breathing 
![](https://github.com/1Px-Vision/WiFi-CSI-SAR/blob/main/WIFI_CSI_Breathing.jpg)

## Main Features

* Multi-antenna WiFi CSI processing.
* CSI amplitude and phase calibration.
* Missing-packet detection and interpolation.
* Static-channel suppression.
* Antenna-link spatial decomposition.
* OFDM subcarrier feature decomposition.
* Sliding temporal-window generation.
* Spatial and temporal attention.
* CNN, LSTM, GRU, TCN, and Transformer support.
* Direct coordinate- or heatmap-based pose estimation.
* Joint-confidence prediction.
* Rescue-posture classification.
* LOS and NLOS evaluation.
* CSI and skeleton visualization.
* Configurable training and evaluation pipelines.

---

## CSI Representation

A CSI measurement can be represented as:

$$
\mathbf{H}(t) \in
\mathbb{C}^{N_{\mathrm{rx}} \times N_{\mathrm{tx}} \times N_{\mathrm{sc}}}
$$

where:

* ($N_{\mathrm{rx}}$) is the number of receiving antennas.
* ($N_{\mathrm{tx}}$) is the number of transmitting antennas.
* ($N_{\mathrm{sc}}$) is the number of OFDM subcarriers.
* (t) is the packet or time index.

For a temporal sequence of (T) packets, the model input may be arranged as:

```text
[batch, channels, time, antenna_links, subcarriers]
```

Input channels can include:

* CSI amplitude.
* Calibrated phase.
* Real and imaginary components.
* Inter-antenna phase differences.
* Temporal CSI differences.
* Doppler or time-frequency features.

---

## CSI-Channel Spatial Decomposition

The measured CSI is modeled as:

$$
\mathbf{X}=
\mathbf{X}*{\mathrm{static}}
+
\mathbf{X}*{\mathrm{dynamic}}
+
\mathbf{N},
$$

where:

* ($\mathbf{X}_{\mathrm{static}}$) represents static propagation paths.
* ($\mathbf{X}_{\mathrm{dynamic}}$) represents human-induced channel changes.
* ($\mathbf{N}$) represents noise, interference, and hardware distortion.

The decomposition module may perform:

* Antenna-link separation.
* Subcarrier grouping.
* Static and dynamic component separation.
* Amplitude and phase feature extraction.
* Low-rank and residual decomposition.
* Spatial-channel attention.
* Temporal-frequency analysis.

---

## Model Architecture

The reference framework consists of four main components.

### 1. CSI Input Encoder

Processes amplitude, phase, and antenna-difference features using convolutional or embedding layers.

### 2. Spatial Decomposition Module

Learns relationships among antenna links, subcarriers, and propagation components.

Possible implementations include:

* 2D or 3D convolution.
* Depthwise-separable convolution.
* Principal-component analysis.
* Singular-value decomposition.
* Low-rank decomposition.
* Channel attention.
* Graph neural networks.
* Transformer-based spatial attention.

### 3. Temporal Encoder

Models human movement across consecutive CSI packets using:

* Temporal convolutional networks.
* LSTM or bidirectional LSTM.
* GRU.
* Transformer encoders.
* Convolution–Transformer models.

### 4. Pose Decoder

Produces:

* 2D body-joint coordinates.
* 3D body-joint coordinates.
* Pose heatmaps.
* Joint-confidence values.
* Rescue-posture classes.

---

## Repository Structure

```text
CSI-Channel-Spatial-Decomposition/
├── acquisition/
│   ├── collect_csi.py
│   └── receiver_config.py
├── configs/
│   ├── dataset.yaml
│   ├── train.yaml
│   └── evaluate.yaml
├── data/
│   ├── raw/
│   ├── processed/
│   ├── labels/
│   └── splits/
├── datasets/
│   ├── csi_dataset.py
│   ├── preprocessing.py
│   ├── synchronization.py
│   └── augmentation.py
├── models/
│   ├── spatial_decomposition.py
│   ├── temporal_encoder.py
│   ├── pose_decoder.py
│   └── csi_pose_network.py
├── training/
│   ├── losses.py
│   ├── metrics.py
│   └── trainer.py
├── evaluation/
│   ├── evaluate_pose.py
│   ├── evaluate_posture.py
│   └── visualize_results.py
├── scripts/
│   ├── preprocess_dataset.py
│   ├── train.py
│   ├── test.py
│   └── inference.py
├── notebooks/
├── checkpoints/
├── results/
├── requirements.txt
├── LICENSE
└── README.md
```

Adapt the structure to match the final implementation.

---

## Requirements

* Python 3.10 or later
* PyTorch
* NumPy
* SciPy
* Pandas
* scikit-learn
* OpenCV
* Matplotlib
* PyYAML
* h5py
* tqdm
* TensorBoard

Optional dependencies:

* PyWavelets
* einops
* filterpy
* MediaPipe or OpenPose
* Optuna
* Weights & Biases

---

## Installation

Clone the repository:

```bash
git clone https://github.com/USERNAME/CSI-Channel-Spatial-Decomposition.git
cd CSI-Channel-Spatial-Decomposition
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Linux or macOS:

```bash
source .venv/bin/activate
```

Activate it on Windows:

```powershell
.venv\Scripts\activate
```

Install the dependencies:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Install the appropriate CUDA-compatible PyTorch version when GPU acceleration is required.

---

## Dataset Organization

Each sample should contain a synchronized CSI sequence and its corresponding human-pose labels.

```text
data/
├── raw/
│   ├── subject_001/
│   │   ├── scenario_01/
│   │   │   ├── csi.npy
│   │   │   ├── timestamps.npy
│   │   │   ├── pose.npy
│   │   │   └── metadata.json
│   │   └── scenario_02/
│   └── subject_002/
├── processed/
└── splits/
    ├── train.txt
    ├── validation.txt
    └── test.txt
```

Example metadata:

```json
{
  "subject_id": "subject_001",
  "scenario": "smoke_room",
  "propagation": "NLOS",
  "posture": "crawling",
  "tx_antennas": 1,
  "rx_antennas": 3,
  "subcarriers": 30,
  "sampling_rate_hz": 100,
  "pose_dimensions": 2,
  "number_of_keypoints": 17
}
```

---

## CSI Preprocessing

The preprocessing pipeline may include:

* Invalid-packet removal.
* Packet reordering.
* Missing-packet interpolation.
* Amplitude normalization.
* Phase unwrapping.
* Linear phase-error removal.
* Carrier-frequency-offset compensation.
* Sampling-frequency-offset compensation.
* Inter-antenna phase-difference calculation.
* Median, Hampel, or low-pass filtering.
* Static-background subtraction.
* Temporal resampling.
* Sliding-window segmentation.
* CSI and pose-label synchronization.

Run preprocessing with:

```bash
python scripts/preprocess_dataset.py \
    --input-dir data/raw \
    --output-dir data/processed \
    --config configs/dataset.yaml
```

Example configuration:

```yaml
window_length: 256
window_stride: 32
target_sampling_rate_hz: 100

representation:
  amplitude: true
  phase: true
  antenna_phase_difference: true

filtering:
  median_kernel: 5
  lowpass_cutoff_hz: 20.0

normalization:
  method: zscore
  per_antenna_link: true
  per_subcarrier: true

static_suppression:
  enabled: true
  method: moving_average
  kernel_size: 101
```

---

## Training

Configure the experiment in:

```text
configs/train.yaml
```

Example:

```yaml
seed: 42
device: cuda

dataset:
  root: data/processed
  train_split: data/splits/train.txt
  validation_split: data/splits/validation.txt
  number_of_keypoints: 17
  pose_dimensions: 2

model:
  input_channels: 3
  hidden_dimension: 128
  spatial_blocks: 4
  temporal_encoder: transformer
  temporal_layers: 4
  attention_heads: 8
  dropout: 0.2

training:
  epochs: 100
  batch_size: 64
  learning_rate: 0.0001
  weight_decay: 0.00001

loss:
  coordinate_weight: 1.0
  bone_weight: 0.25
  temporal_weight: 0.10
  confidence_weight: 0.10
```

Start training:

```bash
python scripts/train.py --config configs/train.yaml
```

Resume from a checkpoint:

```bash
python scripts/train.py \
    --config configs/train.yaml \
    --resume checkpoints/last.pt
```

Monitor the experiment:

```bash
tensorboard --logdir results/logs
```

---

## Evaluation

Evaluate the trained model:

```bash
python scripts/test.py \
    --config configs/evaluate.yaml \
    --checkpoint checkpoints/best.pt
```

Recommended pose-estimation metrics include:

* Mean Per-Joint Position Error.
* Percentage of Correct Keypoints.
* Object Keypoint Similarity.
* Normalized Mean Error.
* Mean Average Precision.
* Bone-length error.
* Temporal jitter.
* Inference latency.
* Throughput.
* Model size.

Recommended rescue-oriented metrics include:

* Fallen-person detection accuracy.
* Crawling-posture recall.
* Motion-detection sensitivity.
* False-alarm rate.
* Detection latency.
* LOS and NLOS performance.
* Cross-subject generalization.
* Cross-room generalization.
* Confidence-calibration error.

Raw CSI measurements were collected for each participant while performing five activities:

* Fall (FA)
* Get Up (GU)
* Lie Down (LD)
* Sit Down (SD)
* Walk (WA)
  
![](https://github.com/1Px-Vision/WiFi-CSI-SAR/blob/main/CSI_activity_CM.jpg)

---

## Experimental Protocol

Randomly splitting windows from the same recording can produce overly optimistic results. Dataset splits should therefore be defined by subject, room, or recording session.

### Cross-Subject Evaluation

```text
Training:   S01–S12
Validation: S13–S15
Testing:    S16–S20
```

### Cross-Environment Evaluation

```text
Training:   Rooms A and B
Validation: Room C
Testing:    Rooms D and E
```

### Rescue Postures

Suggested posture classes include:

* Standing
* Walking
* Sitting
* Kneeling
* Crawling
* Lying supine
* Lying prone
* Fallen
* Motionless
* Partially occluded

---

## Inference

Run inference on a CSI sample:

```bash
python scripts/inference.py \
    --checkpoint checkpoints/best.pt \
    --input data/examples/sample_csi.npy \
    --output results/sample_prediction.json
```

Example output:

```json
{
  "timestamp": 12.48,
  "pose_dimension": 2,
  "posture": "crawling",
  "posture_confidence": 0.91,
  "keypoints": [
    {
      "name": "nose",
      "x": 0.51,
      "y": 0.18,
      "confidence": 0.83
    },
    {
      "name": "left_shoulder",
      "x": 0.44,
      "y": 0.31,
      "confidence": 0.88
    }
  ]
}
```

Run streaming inference:

```bash
python scripts/inference.py \
    --checkpoint checkpoints/best.pt \
    --stream \
    --receiver-interface wlan0
```

Real-time operation depends on the CSI extraction platform, wireless chipset, driver, packet rate, and operating system.

---

## Visualization

Generate CSI and pose visualizations:

```bash
python evaluation/visualize_results.py \
    --predictions results/predictions.json \
    --output results/pose_animation.mp4
```

Supported visualizations may include:

* CSI amplitude and phase.
* Antenna-link correlation.
* Subcarrier attention maps.
* Doppler spectra.
* Predicted and reference skeletons.
* Joint-confidence values.
* Per-joint pose error.
* Rescue-posture timelines.

---

## Data Augmentation

Possible CSI augmentations include:

* Additive noise.
* Random packet loss.
* Temporal masking.
* Subcarrier masking.
* Antenna-link dropout.
* Amplitude scaling.
* Phase perturbation.
* Frequency-selective attenuation.
* Simulated interference.
* Variable signal-to-noise ratio.

Augmentation parameters should preserve physically plausible channel behavior.

---

## Supported Hardware

The framework can be adapted to CSI data collected with:

* Modified WiFi network-interface cards.
* Intel 5300 CSI tools.
* Nexmon CSI.
* ESP32 CSI tools.
* PicoScenes-compatible devices.
* Software-defined radios.
* Multi-antenna IEEE 802.11n/ac/ax research platforms.

Hardware-specific preprocessing may be required because the number of subcarriers, phase characteristics, packet rate, and CSI format differ among acquisition platforms.

---

## Limitations

Current limitations may include:

* Sensitivity to changes in room geometry.
* Performance degradation in unseen environments.
* Limited spatial resolution compared with cameras.
* Difficulty separating multiple people.
* Dependence on antenna placement.
* Hardware-specific CSI distortions.
* Reduced accuracy for motionless subjects.
* Ambiguity between similar body configurations.
* Sensitivity to external wireless interference.
* Limited generalization across devices and frequency bands.

A predicted pose does not determine a person’s identity, medical condition, survivability, or exact location.

---

## Privacy and Responsible Use

Although CSI sensing does not generate conventional images, it can reveal human presence, motion, and posture.

Users of this project should:

* Collect data only with authorization and informed consent.
* Follow applicable privacy and research-ethics requirements.
* Avoid covert or unauthorized monitoring.
* Secure CSI recordings and pose annotations.
* Remove identifying information from datasets.
* Report environmental and demographic biases.
* Expose prediction confidence and uncertainty.
* Maintain human oversight in rescue-related decisions.

This repository is intended for academic, humanitarian, and authorized research.

---

## Roadmap

* [ ] Real-time CSI streaming
* [ ] Multi-person pose estimation
* [ ] 3D human-pose reconstruction
* [ ] Cross-room domain adaptation
* [ ] Cross-device generalization
* [ ] Self-supervised CSI representation learning
* [ ] Transformer-based spatial decomposition
* [ ] CSI and thermal-camera fusion
* [ ] CSI and radar fusion
* [ ] Uncertainty-aware pose estimation
* [ ] Fallen-person detection
* [ ] Rescue-robot integration
* [ ] UAV-assisted WiFi sensing
* [ ] Edge-device deployment
* [ ] Public rescue-scenario benchmark

---

## Contributing

Contributions are welcome for:

* CSI calibration and preprocessing.
* Spatial-decomposition methods.
* Temporal models.
* Pose-estimation architectures.
* Dataset tools.
* Rescue-scenario evaluation.
* Visualization.
* Documentation and testing.

Create a feature branch:

```bash
git checkout -b feature/new-module
```

Commit and push the changes:

```bash
git commit -m "Add new CSI decomposition module"
git push origin feature/new-module
```

Then open a pull request describing the implementation and validation results.

---

## Citation

Use the following citation when referencing this repository:

```bibtex
@misc{osorioquero2026csichannel,
  title        = {CSI-Channel Spatial Decomposition for WiFi-Based Human Pose Estimation in Rescue Scenarios},
  author       = {Osorio-Quero, Carlos A.},
  year         = {2026},
  howpublished = {\url{https://github.com/USERNAME/CSI-Channel-Spatial-Decomposition}},
  note         = {Research software repository}
}
```

Replace `USERNAME` with the final GitHub account or organization name.

---

## License

This project is distributed under the terms provided in the [`LICENSE`](LICENSE) file.

Third-party datasets, pretrained models, CSI extraction tools, and external libraries may be governed by separate licenses.

---

## Disclaimer

This repository contains experimental research software. It has not been certified for emergency response, medical diagnosis, public-safety operations, or other safety-critical applications.

The system may produce incorrect or uncertain predictions. Its output must be evaluated alongside other sensors and reviewed by qualified personnel.

---

## Acknowledgments

This project builds upon research in:

* WiFi Channel State Information sensing.
* Device-free human sensing.
* RF-based human pose estimation.
* Wireless signal processing.
* Spatial-temporal deep learning.
* Privacy-preserving sensing.
* Search-and-rescue robotics.
