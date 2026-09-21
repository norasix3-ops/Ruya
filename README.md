# Ru’ya | UAV-Based Crowd Detection & Monitoring

**Ru’ya (رؤيا)** — Arabic for *Vision* — is a graduation project that explores how lightweight artificial intelligence and unmanned aerial vehicles (UAVs) can support crowd monitoring and situational awareness. The system uses computer vision to detect people in aerial imagery, estimate localized crowd density, and visualize potentially crowded areas.

Developed at **Imam Abdulrahman Bin Faisal University (IAU)**, College of Computer Sciences & Information Technology, Saudi Arabia.

## Project overview

Large gatherings require timely information about how people are distributed across an area. Ru’ya investigates a mobile, aerial approach to crowd analysis that combines:

- **Person detection:** A YOLOv8s model trained on person-related annotations from the VisDrone dataset.
- **Crowd density estimation:** A 6 × 6 grid that counts detections within individual regions of each frame.
- **Risk visualization:** Color-coded low, medium, and high crowding categories based on detected counts per grid cell.
- **UAV prototype:** An assembled F450 quadcopter platform with Pixhawk flight control, GPS, telemetry, and an onboard camera.
- **Monitoring interface:** A dashboard component for viewing and interpreting crowd-monitoring information.

The project is designed with edge processing and privacy considerations in mind. Full onboard AI integration and real-world flight evaluation remain future work; the results below come from model evaluation and simulation, not a completed operational deployment.

## How it works

```text
Aerial image / video frame
          ↓
  YOLOv8s person detection
          ↓
 Bounding boxes + person count
          ↓
  6 × 6 grid-based analysis
          ↓
 Localized density + crowding levels
          ↓
 Visualization / monitoring dashboard
```

Grid density is **relative to image area**, not a calibrated estimate of people per square meter. The low/medium/high categories are experimental indicators, not validated public-safety thresholds.

## Model and evaluation

The person-detection model was trained using **Ultralytics YOLOv8s** with VisDrone imagery filtered to person-related classes.

| Metric | Reported result |
| --- | ---: |
| Precision | 72.76% |
| Recall | 61.68% |
| mAP@50 | 68.94% |
| mAP@50–95 | 33.52% |
| Average inference time | 23 ms/image |
| Reported video processing speed | ~34.87 FPS |

These are the results reported for the project’s model evaluation; they **do not establish equivalent performance on the assembled UAV or an embedded processor**. Detection can be less reliable for small, overlapping, distant, or poorly illuminated people. In particular, missed detections can lead to underestimated crowd density.

### Simulation testing

The project also evaluated person detection in synthetic aerial crowd scenes across three simulated altitude levels and five visual conditions: clear weather, rain, fog, dust, and low light. **YOLOv8n** was used in the altitude/weather simulation, while **YOLOv8s** was used for the main trained person-detection pipeline. The simulations highlighted reduced detection reliability as apparent person size and visibility decreased.

## Technology

**AI and data:** Python · Ultralytics YOLOv8 · VisDrone · computer vision · grid-based crowd analysis  
**UAV hardware and configuration:** F450 quadcopter · Pixhawk · GPS · telemetry · camera · Mission Planner  
**Interface:** Web-based monitoring dashboard

## Development status

Ru’ya is a **research and engineering prototype**. The person-detection and grid-based crowd-analysis pipeline was developed and evaluated, and the team assembled and configured a UAV prototype. Complete integration of the AI pipeline with the UAV and controlled real-world testing are identified as next steps in the final report.

This repository documents the project and may include its code, dashboard, experimental results, and supporting materials as they are added. Repository contents, rather than this overview, indicate which components are currently available to run.

## Responsible use

Ru’ya focuses on detecting and counting people **without identifying individuals**. Privacy-preserving processing, including face blurring, is part of the project's planned enhancements; it should not be assumed to be fully implemented in every component. This prototype is **not certified for autonomous flight, operational surveillance, or safety-critical crowd decisions**. UAV operation and any collection of real-world imagery require the relevant permissions and safeguards.

## Team and acknowledgements

This project was made possible through the shared effort of our graduation-project team:

- **Nora Abdullah Aljomuh** — Project Leader
- **Mozoon Alkhalis** — Team Member
- **Ritaj Alhamli** — Team Member
- **Joud Alahmari** — Team Member
- **Sarah Alashgar** — Team Member

**A special thank-you to my teammates — Mozoon, Ritaj, Joud, and Sarah — for their dedication, collaboration, and support throughout every stage of Ru’ya. I am grateful to have worked with you on this project.**

We also extend our sincere thanks to **Dr. Rabab Alkhalifa**, our supervisor, and **Mrs. Mehwash Farooqui**, our co-supervisor, for their guidance and encouragement.

---

*Graduation project · Imam Abdulrahman Bin Faisal University · 2025–2026*
