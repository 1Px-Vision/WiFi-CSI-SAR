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




By decomposing CSI measurements into meaningful spatial and temporal components, the system attempts to recover motion patterns associated with the positions of major body joints.
