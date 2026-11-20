# Joint-Angle Trajectories from Video: Falls vs Everyday Movement(By:Ruba Sawalha)

A single video frame can be misleading: sitting down and the start of a fall can look alike. This project runs an open-source pose-estimation model over short video sequences and analyses **hip, knee and trunk-lean angles as trajectories over time** to compare falls with activities of daily living (ADL).

## Data
[UR Fall Detection Dataset](https://fenix.ur.edu.pl/~mkepski/ds/uf.html) (University of Rzeszów), front camera, 30 fps, CC BY-NC-SA 4.0. Five fall and five ADL sequences were used.
Kwolek, B., & Kepski, M. (2014). *Computer Methods and Programs in Biomedicine*, 117(3), 489–501.

## Method
1. **MediaPipe Pose Landmarker** (BlazePose, full model) run frame by frame in video mode → 33 landmarks per frame.
2. Hip, knee and trunk-lean angles computed per frame, gaps interpolated, smoothed (Savitzky–Golay).
3. Temporal features per sequence: maximum trunk lean, peak trunk angular velocity, time above 60°.

## Key findings
- Single-frame hip and knee angles overlapped between sitting down and falling; **trajectories separated most falls** (trunk lean rising above 100° within about one second).
- A fast "lying down" ADL and a slower fall still overlapped, so simple hand-crafted features are not enough on their own.
- **fall-03:** the subject fell along the camera's viewing direction, so the 2D trunk lean reached only 26° (foreshortening).
- Running on the **compressed MP4** instead of PNG frames kept the trajectory shape (r = 0.90) but reduced detection from 91% to 61% of frames and halved the peak angle.

## Limitations
2D single camera; detection gaps when the person is partly out of view or lying down; small sample of young adults acting out falls; no motion-capture ground truth.

## How to run
Open the notebook in Google Colab and select **Runtime → Run all**. Data and model are downloaded automatically.
