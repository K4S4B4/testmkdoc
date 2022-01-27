# カメラ校正の実施

## 内部パラメータの取得

- [この画像](https://raw.githubusercontent.com/Akiya-Research-Institute/MocapForAll-Wiki/main/resources/calibration/IntrinsicCalibration.png)を任意のアプリで画面にできるだけ大きく表示します。
- MocapForAllで「Camera > Calibration > Intrinsic」の下の「Start」ボタンをクリックします。  
- 10秒間程度、さまざまな角度からカメラで画像を写してください。カメラを固定済みの場合は、カメラでなく画像の方を動かします。  

カメラ校正が完了すると、アプリの画面上に内部パラメータが表示され、「Intrinsic  ☑Calibrated」となります。

![](../../images/Camera-Calibration-Intrinsic-Execution.gif){ loading=lazy }

完了したら「Save」からカメラ校正結果を保存しておきます。

## 外部パラメータの取得

先に説明した[外部パラメータの取得の4つの方式](../what-is-camera-calibration/#4)により、手順が異なります。

=== "ChArUcoボードを使うやり方  "
    - [外部パラメータの取得で使う画像の印刷](../prepare-markers/#_3)で印刷した画像を床に置きます。これがモーションキャプチャの原点になります。   
    - 床に置いた画像が見える場所にカメラを設置します。  
    - MocapForAllで「Settings > Calibration > Extrinsic calibration method」で「**ChArUco board (default)**」を選択します。
    - 「Camera > Calibration > Extrinsic」の下の「Start」ボタンをクリックします。
    
    キャリブレーションが完了すると、外部パラメータが表示され、「Extrinsic  ☑Calibrated」となります。
 
    マーカの読み取りがうまく実施できない場合は、[マーカをうまく読み取れない場合](#_4)を試してみてください。

    ![](../../images/Camera-Calibration-Extrinsic-Execution-Charuco.gif){ loading=lazy }
    
=== "ArUcoクラスターを使う方法 "
    - Place the images printed in [Prepare markers](../prepare-markers/#print-marker-for-extrinsic-parameter-calibration) section on the floor. `arucoMarker0.png` will be the origin of the captured motion.  
    - Place the cameras where they can see the placed images.  
    - In MocapForAll, select `ArUco cluster` in `Settings > Calibration > Extrinsic calibration method`.  
    - Click `Scan markers` button under `Camera > Calibration > Extrinsic`.  This will scan the relative positions of the markers. After a while, the markers will appear in the 3D viewport.
    - After all markers appeared, click **`Stop scanning`** and then **`Start`** under `Camera > Calibration > Extrinsic`.
    
    When calibration is completed, extrinsic parameters and the camera position will be displayed, and it will shows `Extrinsic  ☑Calibrated`.  
    
    If it does not read the AR marker properly, try [If the marker cannot be read properly](#if-the-marker-cannot-be-read-properly).
    
    ![](../../images/Camera-Calibration-Extrinsic-Execution-Aruco.gif){ loading=lazy }
   
=== "Diamondクラスターを使う方法"
    - Place the images printed in [Prepare markers](../prepare-markers/#print-marker-for-extrinsic-parameter-calibration) section at a distance that fits in a frame of the camera. It does not have to be in the same plane. `diamondMarker0.png` will be the origin of the captured motion, so place this on the floor.  
    - In MocapForAll, select **`Diamond cluster`** in `Settings > Calibration > Extrinsic calibration method`.  
    - Click **`Scan markers`** button under `Camera > Calibration > Extrinsic` in one of the cameras. Take pictures of `diamondMarker0.png` and one of the markers at the same time. After a while, the position of another marker will be fixed with `diamondMarker0.png` as the origin, and the marker will be displayed on the 3D viewport. 
    - Repeat the above step for markers whose positions have been fixed and markers whose positions have not been fixed, and click `Stop scanning` when the positions of all markers have been fixed.
    - Place the cameras where they can see at least one of the markers whose position is fixed. 
    - Click **`Start`** under `Camera > Calibration > Extrinsic`.
    
    When calibration is completed, extrinsic parameters and the camera position will be displayed, and it will shows `Extrinsic  ☑Calibrated`.  
    
    If it does not read the AR marker properly, try [If the marker cannot be read properly](#if-the-marker-cannot-be-read-properly).

    ![](../../images/Camera-Calibration-Extrinsic-Execution-Diamond.gif){ loading=lazy }

=== "体の動きを使う方法" 
    - Place the cameras so that at least two of them can see your whole body at the same time.
    - In MocapForAll, select **`Human motion`** in `Settings > Calibration > Extrinsic calibration method`.  
    - Select **`GPU_DirectML`** in `Settings > General > Run DNN on` if your hardware support it. (If you have already installed the `GPU_TensorRT` mode in the Appendix, you can also use it.）  
    - Select **`Speed`** in `Settings > General > Capture body` if your PC's performance is enough for it. (If you have already installed the `Precision` mode in the Appendix, you can also use it.）  
    - Click **`Start calibration` button at the top of the window**, and walk around on the floor where the cameras can see your whole body.  
    Your motion will be captured and the positions of your joints will be used to find the cameras relative positions.
    
    After all cameras' extrinsic parameters calibrated, click the **`Find Ground`** button at the top of the window and walk around in the same way as [If the marker cannot be read properly](#if-the-marker-cannot-be-read-properly) described below. This will determine the absolute position of the cameras.  
    
    ![](../../images/Camera-Calibration-Extrinsic-Execution-Human.gif){ loading=lazy }

### マーカをうまく読み取れない場合
!!! Tip "If the marker cannot be read properly"

    Since the position of the marker will be the plane with zero height of the captured motion, it is basically recommended to place the marker on the floor, but it may be difficult to read the marker on the floor depending on the placement and specification of the camera.

    In that case, you can **hang the marker on the wall to calibrate the camera and adjust the floor level later** as follows:

    - Replace the word "on the floor" with "on the wall" and execute the calibration procedure.  
    - Select **`GPU_DirectML`** in `Settings > General > Run DNN on` if your hardware support it. (If you have already installed the `GPU_TensorRT` mode in the Appendix, you can also use it.）  
      Select **`Speed`** in `Settings > General > Capture body` if your PC's performance is enough for it. (If you have already installed the `Precision` mode in the Appendix, you can also use it.）  
    - Click the **`Find Ground`** button at the top of the window and walk around where at least 2 cameras can see your whole body. After a while, the position of the floor level will be adjusted automatically.  

    ![](../../images/Camera-Calibration-Extrinsic-Execution-FindGround.gif){ loading=lazy }

### Confirm the results

If you have input the correct marker size in [Prepare markers](../prepare-markers/#measure-the-marker-size) section, you can see the position of the camera in the 3D viewport.  
Use the WASD key and mouse drag to move the viewport on MocapForAll.  
<img src="../../../images/App-wasd.png" alt="App-wasd" style="zoom:50%;" />  
Note that the camera may appear below the floor (in this case, the calibration has failed).

## Save and load the results
![](../../images/Camera-Calibration-Save.gif){ loading=lazy }

### For each camera 
After calibration is completed, save the calibration result of each camera by clicking **`Save`** under `Camera > Calibration > Intrinsic` and `Extrinsic`. The saved result can be loaded by clicking **`Load`** button.  

### For all cameras
You can save and load the whole camera setup by clicking **`Save All Cameras`** and **`Load All Cameras`** buttons.  

!!! Warning
    The camera selection is saved as the index inside the combo box. If you remove cameras from your PC, the order of the cameras in the combo box will change and you will not be able to load the cameras properly.
