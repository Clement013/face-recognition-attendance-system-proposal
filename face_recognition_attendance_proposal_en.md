# Proposal: Face Recognition Attendance System for Church

## 1. 📝 Overview:

This proposal outlines a smart attendance tracking system using Face Recognition technology for church members. The system leverages live facial detection and recognition to automatically mark attendance during events such as Saturday services, without manual input. It ensures accurate records, reduces human error, and allows later review via a cloud-connected mobile app.

## 2. 🎯 Goals:

- Automate attendance taking for all church members.
- Use face recognition to identify known members.
- Detect and handle unknown or masked individuals.
- Upload attendance data and pictures to the cloud for review.
- Allow admin and pastors to check attendance status via mobile app.

## 3. 🔧 System Flow:

1. **System Startup**
2. **Live Video Feed Begins (Camera)**
3. **Face Detection (RetinaFace)**
4. **Face Recognition (ArcFace)**
5. **Decision Tree:**
   - If face is known:
     - Mark attendance
     - Check if mask:
       - If yes → Do NOT update photo
       - If no → Automatically update file-based database (optional)
   - If face is unknown:
     - Check if wearing mask:
       - If yes → Mark as "Mask Detected", require manual check
       - If no → Add to "Unknown Faces" list for review
6. **After Event**
   - Upload all recognized/unknown images to cloud storage
   - Sync attendance records with cloud database

```
Graphical Flow:

Camera --> Face Detection --> Face Recognition -->
         |                               |
  [Masked or Unknown]             [Known Member]
         |                               |
    Manual Check                  Record Attendance
```

## 4. System Architecture

- **Local System (Church PC)**:
  - Runs face detection & recognition modules
  - Stores temporary image data & logs
- **Cloud Backend**:
  - Firestore for storing user records, attendance logs
  - Firebase Storage for storing uploaded face images
- **Mobile App (Future Phase)**:
  - Allows viewing records, confirming unknowns
  - Admin management features

## 5. Technical Stack:

- Programming Language: Python
- Face Detection: RetinaFace (via DeepFace)
- Face Recognition: ArcFace (via DeepFace)
- Database: Firebase Firestore (NoSQL)
- Storage: Firebase Storage
- Frontend (future): Flutter mobile app

## 6. Data Storage Strategy

- **Local PC**:
  - Temporary face images (processed during event)
  - Offline recognition DB (folder with labeled images)
- **Firebase Firestore**:
  - Member records (name, ID, image references)
  - Attendance logs with timestamps
- **Firebase Storage**:
  - Upload all images after event (both known/unknown)

> Firestore and Firebase Storage are free with usage limits (approx. 50K reads/day, 1GB storage free, can expand later if needed).

## 7. Hardware & Deployment Options

### Current Church PC:

- CPU: Intel i5-4460
- RAM: 16GB
- GPU: Intel HD Graphics (no dedicated GPU)
- Usage: Also used for OBS livestreaming

### Suggested Upgrade:

- **GPU**: Add NVIDIA RTX 3060 (\~RM1200)
- **RAM**: Upgrade to 32GB (additional \~RM200)
- **CPU**: Upgrade to modern CPU for smoother multitasking (INTEL CORE I5 12400F \~RM600)

### Recommendation:

- Use this upgraded PC for **offline processing only**
- Use Firebase as **cloud backend** for data storage and mobile app access

## 8. 📆 Time & Cost Estimation

| Phase          | Tasks                                              | Duration | Cost Estimate (RM)   |
|----------------|----------------------------------------------------| -------- |----------------------|
| Phase 1        | Basic Face Recognition (local), Attendance Logging | 2 weeks  | 0                    |
| Phase 2        | Add Cloud Sync (Firebase), Admin Panel             | 2 weeks  | 0                    |
| Phase 3        | Build Mobile App for Review                        | 2 weeks  | 0                    |
| Testing Phase  | Testing all function                               | 2 weeks  | 0                    |
| Computer       | CPU + GPU + RAM Upgrade + CCTV                     |          | 2000                 |
| Camera         | CCTV (TP-Link Tapo C230 5MP 3K Wireless)           |          | 150                  |

****Data storage exceeding the free quota will increase costs** \
**Total Time**: \~8 weeks\
**Total Hardware Cost**: \~RM2500 (hardware only)\
**Allowance Budget**: \~RM1000

## 9. System Benefits

- Reduce manual effort and error in attendance taking
- Centralized and automatic tracking of weekly attendance
- Easy monitoring by church admin/pastors via mobile
- Future-proof system with expandable cloud backend

