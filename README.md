# CSI-Channel Spatial Decomposition for WiFi-Based Human Pose Estimation in Rescue Scenarios
## Overview

CSI-Channel Spatial Decomposition for WiFi-Based Human Pose Estimation in Rescue Scenarios is a research project focused on estimating human body poses from WiFi Channel State Information (CSI). The proposed framework decomposes CSI measurements across spatial, temporal, antenna, and subcarrier dimensions to extract motion-related features that can be mapped to human keypoints or skeletal poses. Unlike camera-based pose estimation, WiFi sensing does not require visible light and can continue operating under smoke, darkness, partial obstruction, and non-line-of-sight conditions. These properties make CSI-based sensing a promising complementary technology for search-and-rescue operations, indoor monitoring, post-disaster assessment, and privacy-preserving human activity analysis. The project is intended for defensive, humanitarian, and academic research. It does not provide reliable life-safety guarantees and should not replace certified rescue equipment, direct visual inspection, thermal imaging, radar sensing, or trained emergency-response personnel.

## Project Objectives

The main objectives of this project are to:

* Process raw WiFi CSI measurements collected from multiple antennas and OFDM subcarriers.
* Separate static environmental components from human-induced channel variations.
* Learn spatial and temporal representations associated with body movement.
* Estimate two-dimensional or three-dimensional human skeletal keypoints.
* Evaluate pose-estimation performance under line-of-sight and obstructed conditions.
* Investigate WiFi-based sensing for smoke-filled, dark, cluttered, or visually degraded rescue environments.
* Support multimodal rescue systems combining WiFi CSI, thermal cameras, RGB cameras, radar, LiDAR, or inertial sensing.

## Motivation

Conventional human pose estimation relies mainly on RGB or depth cameras. Although these systems can achieve high accuracy in controlled environments, their performance may degrade when:

* Illumination is poor or unavailable.
* Smoke, dust, debris, or walls obstruct the camera.
* The subject is outside the camera field of view.
* Privacy restrictions limit the use of visual recording.
* Rescue personnel cannot safely enter the affected area.

WiFi signals interact with the human body through reflection, diffraction, scattering, attenuation, and multipath propagation. Human movement changes the amplitude and phase of the wireless channel. CSI measurements provide fine-grained information about these changes for individual OFDM subcarriers and antenna links.

------

## Rescue-Scenario Use Cases

Potential research use cases include:

* Locating individuals in smoke-filled indoor environments.
* Detecting standing, sitting, lying, crawling, or fallen postures.
* Monitoring trapped victims behind lightweight obstacles.
* Estimating body orientation before rescue-team entry.
* Identifying possible movement in visually inaccessible areas.
* Assisting post-earthquake or collapsed-building assessment.
* Supporting human–robot and human–UAV rescue coordination.
* Providing privacy-preserving occupancy and posture information.

The system should be treated as an additional sensing layer rather than as an independent decision-making system.

## System Architecture

The processing pipeline is organized into the following stages:

WiFi Transmitter
       |
       v
Multipath Propagation Through the Environment
       |
       v
WiFi CSI Receiver
       |
       v
CSI Calibration and Preprocessing
       |
       v
Static-Channel Suppression
       |
       v
CSI-Channel Spatial Decomposition
       |
       v
Spatial–Temporal Feature Extraction
       |
       v
Pose-Estimation Network
       |
       v
2D/3D Human Keypoints
       |
       v
Rescue-Situation Interpretation

A synchronized camera or motion-capture system may be used during dataset preparation to generate reference pose labels. The camera is needed only for supervision and validation and is not necessarily required during CSI-only inference.

## CSI Data Representation

A CSI sample can be represented as a complex-valued tensor:

[
\mathbf{H}(t) \in
\mathbb{C}^{N_{\mathrm{rx}} \times N_{\mathrm{tx}} \times N_{\mathrm{sc}}},
]

where:

(t) is the CSI packet or time index.
(N_{\mathrm{rx}}) is the number of receiving antennas.
(N_{\mathrm{tx}}) is the number of transmitting antennas.
(N_{\mathrm{sc}}) is the number of OFDM subcarriers.
(\mathbf{H}(t)) contains complex channel coefficients.

For a temporal window containing (T) CSI packets, the input can be arranged as:

[
\mathbf{X} \in
\mathbb{R}^{T \times N_{\mathrm{link}} \times N_{\mathrm{sc}} \times C},
]

where (C) may contain:

CSI amplitude.
Calibrated CSI phase.
Real and imaginary components.
Phase differences between antennas.
Temporal differences.
Doppler-related features.

A common real-valued representation is:

[batch, channels, time, antenna_links, subcarriers]

The exact tensor arrangement depends on the neural-network architecture and CSI acquisition hardware.

## CSI-Channel Spatial Decomposition

The spatial decomposition module is designed to separate channel information associated with different propagation and motion components.

The decomposition may include:

1 **Antenna-link decomposition:** CSI is separated according to transmitter–receiver antenna pairs.

2 **Subcarrier decomposition:** Frequency-selective channel responses are divided into subcarrier groups or learned spectral embeddings.

3 **Static and dynamic decomposition:** Slowly varying environmental components are separated from human-induced temporal variations.

4 **Amplitude and phase decomposition:** CSI magnitude and calibrated phase information are processed independently or jointly.

5 **Low-rank and residual decomposition**
The static channel can be approximated as a low-rank component, while motion is represented by a dynamic residual.

6 **Spatial attention**: Learnable weights emphasize antenna links and subcarrier regions that contain stronger pose-related information.

7 **Temporal-frequency decomposition:** Short-time Fourier transforms, wavelets, Doppler spectra, or learned filters can be used to represent motion dynamics.
By decomposing CSI measurements into meaningful spatial and temporal components, the system attempts to recover motion patterns associated with the positions of major body joints.
