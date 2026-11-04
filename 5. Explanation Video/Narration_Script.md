# Explanation Video 1039 — narration transcript

Voice: neural text-to-speech (Microsoft "en-IN-PrabhatNeural", male Indian-English, via edge-tts) — synthesized because no
microphone was available at recording time. Slide visuals are the project's own generated outputs.
Total duration: ~3 min 48 s, 1280x720 mp4.

Slide 1 — Title (0:00)
"Hello, and welcome. This is the explanation of my Computer Vision CCA three practical coding assignment, for units three, four and five. Student ID ten thirty nine. The project implements four tasks: image processing, feature extraction and matching, object detection, and video analysis, all in a single notebook that runs on Google Colab and locally."

Slide 2 — Repository structure (0:29)
"The repository layout is on screen. The original inputs folder has the images and the video. The source code folder has the notebook. Generated figures live in the outputs folders for each task, the technical report documents everything, and the explanation video is what you are watching now. The README explains how to reproduce the project."

Slide 3 — Inputs (0:57)
"Three inputs are used. The original image combines a portrait and a street scene, so it has faces as well as many everyday objects. The second image is a rotated, resized and re lit version of it. And a seven second video shows moving objects over the street background with a slow lighting change."

Slide 4 — Task 1: Image Processing (1:21)
"Task one, image processing. We add Gaussian and salt and pepper noise, then denoise with median and Gaussian filters. The PSNR and SSIM table quantifies the results: the median filter clearly wins against salt and pepper noise. We then apply KMeans colour quantisation, Otsu thresholding, morphological operations, Canny edges, and marker based watershed segmentation, whose region boundaries are drawn in red."

Slide 5 — Task 2: Feature Extraction and Matching (1:55)
"Task two, features. The HOG descriptor represents dense gradient orientations, and the built in person detector finds candidate people. SIFT detects thousands of keypoints, and Brute Force matching with the Lowe ratio and RANSAC finds about two thousand seven hundred geometrically consistent matches between the original and the transformed image. Matching remains strong under forty five and ninety degree rotations and scale changes, which confirms SIFT's invariance."

Slide 6 — Task 3: Object Detection (2:29)
"Task three, detection. The classical Viola Jones cascade finds the frontal faces in green, with eyes marked inside. The modern YOLO version eight nano detects fifteen objects in the image and thirteen in the middle video frame, mostly persons, each with a confidence box."

Slide 7 — Task 4: Video Analysis (2:51)
"Task four, video analysis. We sample frames and compute frame differences to spot motion. MOG two provides an adaptive background model whose foreground improves as frames accumulate. Lucas Kanade optical flow then tracks one hundred fifty corner points across the video, producing colour coded trails for the moving car, ball, and walking figure."

Slide 8 — Outputs and documentation (3:19)
"Every figure is saved automatically into the outputs folder for its task, twenty eight images in total. The technical report documents the methodology, results, and conclusions for each task, so the work is fully reproducible."

Slide 9 — Summary (3:37)
"To summarise: the notebook implements the full computer vision pipeline, from image restoration and segmentation, through invariant feature matching, to classical and deep object detection, and finally motion analysis in video. Thank you for watching."
