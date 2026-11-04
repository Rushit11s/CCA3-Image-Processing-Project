# CCA 3 — Explanation Video Plan + Pipeline Diagrams

This folder originally holds the explanation video. Until it is recorded, the diagrams
below serve as the **storyboard / recording script** for that video, and the main
pipeline diagram is also embedded in `README.md`.

Suggested video: **3–5 minutes**, screen recording of the notebook + results, narrated
Node-by-node following Storyboard diagram at the bottom.

---

## 1. Main pipeline diagram (also embedded in README.md)

```mermaid
flowchart TD
    START["Open notebook in Colab or Jupyter"] --> CFG["Config cell: detect Colab vs local, set paths"]
    CFG --> DC{"Dataset check passes?<br/>original.jpg - second.jpg - original_video.mp4"}
    DC -- "no: place inputs in 1. Original Inputs/" --> DC
    DC -- "yes" --> LOAD["Load images + read video properties"]

    subgraph T1["Task 1 - Image Processing"]
        direction TB
        T1A["Add Gaussian noise + Salt-and-Pepper noise"] --> T1B["Denoise: Median filter + Gaussian filter"]
        T1B --> T1C["Quality evaluation: PSNR + SSIM table"]
        T1C --> T1D["KMeans colour quantisation K = 2, 4, 8"]
        T1D --> T1E["Otsu thresholding + histogram"]
        T1E --> T1F["Morphology: erode, dilate, open, close, gradient"]
        T1F --> T1G["Canny edge detection: raw vs smoothed"]
        T1G --> T1H["Marker-based watershed segmentation"]
    end

    subgraph T2["Task 2 - Feature Extraction and Matching"]
        direction TB
        T2A["HOG descriptor + HOG-SVM person detector"] --> T2B["SIFT keypoints on both images"]
        T2B --> T2C["Brute-Force knn matching + Lowe ratio 0.75"]
        T2C --> T2D["RANSAC homography -> inlier count"]
        T2D --> T2E["Invariance study: rotate 45/90, resize 50/150 percent"]
        T2E --> T2F["Invariance bar chart + comparison"]
    end

    subgraph T3["Task 3 - Object Detection"]
        direction TB
        T3A["Viola-Jones Haar cascade: faces + eyes"]
        T3B["YOLOv8-Nano: 80 COCO classes"]
        T3A --> T3C["Image detection"]
        T3B --> T3C
        T3A --> T3D["Middle video frame detection"]
        T3B --> T3D
    end

    subgraph T4["Task 4 - Video Analysis"]
        direction TB
        T4A["Frame sampling + properties"] --> T4B["Frame differencing + threshold"]
        T4B --> T4C["MOG2 background subtraction, 120 sampled frames"]
        T4C --> T4D["Lucas-Kanade optical flow tracking"]
        T4D --> T4E["Composite motion panel"]
    end

    LOAD --> T1A
    LOAD --> T2A
    LOAD --> T3A
    LOAD --> T4A

    T1H --> O1[("3. Outputs / Task 1")]
    T2F --> O2[("3. Outputs / Task 2")]
    T3D --> O3[("3. Outputs / Task 3")]
    T4E --> O4[("3. Outputs / Task 4")]

    O1 --> REP["4. Technical Report"]
    O2 --> REP
    O3 --> REP
    O4 --> REP
    REP --> SUB["Submit: notebook + outputs + report + README"]
```

---

## 2. Video storyboard (record in this order)

```mermaid
flowchart LR
    V0["0:00 - Intro: project + 4 tasks + repo layout"] --> V1["0:30 - Notebook config: Colab vs local paths"]
    V1 --> V2["1:00 - Task 1: show noise, denoised grid, PSNR/SSIM table"]
    V2 --> V3["2:00 - Task 2: show HOG visual, SIFT matches, invariance chart"]
    V3 --> V4["3:00 - Task 3: show face boxes + YOLO detections"]
    V4 --> V5["4:00 - Task 4: show diff, MOG2 masks, LK tracks"]
    V5 --> V6["4:45 - Outputs folder + technical report tour"]
    V6 --> V7["5:00 - Conclusion: what was learned"]
```

---

## 3. Recording checklist

- [ ] Screen + microphone recording (OBS / Zoom / Xbox Game Bar)
- [ ] Notebook executed top-to-bottom before recording (no pip-wait pauses)
- [ ] Keep the PSNR/SSIM table, invariance bar chart and one watershed figure in frame — these carry the "quantified results" discussion
- [ ] Mention where each figure in `3. Outputs/` comes from while scrolling
- [ ] Export as MP4/MOV into this folder and rename to include your ID, e.g. `Explanation Video 1039.mp4`
