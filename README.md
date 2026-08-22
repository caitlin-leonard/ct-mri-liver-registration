# CT–MRI Liver Registration

**Medical Image Processing and AI Research Internship | Perfint Healthcare, Chennai**

Developed a patient-specific, landmark-initialized diffeomorphic pipeline for CT–MRI liver registration, targeting image-guided radiofrequency ablation (RFA) planning for liver tumours.

> **Source code:** Confidential — not included in this repository.  
> **Technical report:** Available upon request, subject to confidentiality approval. 📄 [Request access here](https://drive.google.com/file/d/1I2fyMKU_ZXV8zEQGDxHN_sucuY_i1Hdj/view?usp=drive_link)

---

## The Problem

RFA planning for liver tumours benefits from fusing two modalities: **contrast-enhanced CT** (bone and vasculature detail) and **T2-weighted MRI** (superior soft-tissue and lesion contrast). Using both requires *registration* — computing a spatial transformation that maps one scan into the other's coordinate frame so corresponding anatomy overlaps.

Cross-modal CT–MRI liver registration is difficult because of three key challenges:

1. **No linear intensity relationship** — structures can have very different appearances across CT and MRI, making straightforward intensity-based alignment unreliable.
2. **Field-of-view mismatch** — clinical CT can span a much larger extent than MRI, making standard automatic initialization unreliable.
3. **Respiratory deformation** — the liver shifts and deforms between acquisitions, so rigid/affine alignment alone may be insufficient.

---

## My Contribution

- Diagnosed a **metric-level failure mode** in an earlier automatic pipeline: a high global similarity score (NMI) could coincide with an anatomically incorrect alignment under FOV mismatch. This motivated a redesign.
- Redesigned the pipeline around **manual anatomical landmark initialization**, robust to FOV mismatch.
- Implemented a **GPU diffeomorphic deformable registration stage** using a stationary velocity field, scaling-and-squaring integration, and a windowed local-NCC objective.
- Designed an **honest per-patient validation protocol** using held-out landmark Target Registration Error (TRE), separating validation landmarks from those used for registration.
- Built the workflow as **GUI-driven desktop applications** for segmentation, registration, and validation.

---

## Technologies

**Python** · **SimpleITK** · **PyTorch (CUDA)** · **N4ITK** · **MRSegmentator** · **ANTs/SyN (earlier pipeline / comparison)** · **NumPy** · **GUI development**

---

## Results

- Evaluated registration accuracy using **held-out landmark TRE**.
- The diffeomorphic stage improved upon the landmark-only linear baseline in the representative validated case.
- Results were reported **per patient** rather than presented as a generalized clinical claim.
- Where confident landmark placement was not possible without expert radiological input, **no TRE was reported** — an honest gap over a potentially misleading figure.

---

## Key Engineering Insight

> **A high global similarity score is not necessarily evidence of anatomically correct registration.**

The earlier intensity-driven approach demonstrated that NMI could score anatomically incorrect alignments highly under cross-modal FOV mismatch.

This motivated a shift toward:

**anatomical landmark initialization → localized deformable refinement → held-out anatomical validation**

rather than relying on a single global similarity metric as an acceptance criterion.

---

## Confidentiality

Source code, clinical data, patient images, proprietary algorithms, and internal implementation details are not included.

This repository is a **documentation-only portfolio artifact** describing work conducted during my internship at Perfint Healthcare.

---

## Technical Report

A detailed technical report describing the methodology, experiments, and engineering findings is available upon request, subject to confidentiality approval.

📄 **[Request access to the technical report](https://drive.google.com/file/d/1I2fyMKU_ZXV8zEQGDxHN_sucuY_i1Hdj/view?usp=drive_link)**

---

## Disclaimer

This repository is a portfolio-level technical overview and is **not a clinical software release or medical device**.
