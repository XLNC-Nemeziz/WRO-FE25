On May 20, we conducted tests to analyze the effectiveness of different Pixy2 camera configurations for obstacle detection during autonomous driving. We studied how the position, height, and tilt angle affect the camera's ability to track colored obstacles such as red and green pillars. Our goal was to determine the most stable configuration in terms of field of view and obstacle tracking.

<h1> Introduction: </h1>

Pixy2 is a color vision sensor capable of detecting multiple colored objects (signatures) and tracking their positions in real time. In our autonomous robot, we rely on Pixy2 to recognize red and green pillar obstacles on the field. The positioning of the camera (its height, horizontal placement, and tilt) greatly influences how long it can keep obstacles in view, how early detection occurs, and how stable the recognition is.

Small variations in mounting configuration can cause major losses in reliability — obstacles might disappear from view too early or enter the frame too late for proper avoidance maneuvers. Therefore, we performed systematic testing to determine the optimal setup.

<h1> Research: </h1>

Our robot originally used a Pixy2 camera mounted at the rear of the chassis. We also mounted the camera in the center to compare results. The front placement was not tested further after initial trials showed many missed detections due to narrow field of view and occlusion.

We focused on two positions:
<ul>
  <li>Rear of the robot</li>
  <li>Center of the robot</li>
</ul>

We also experimented with different heights (15 cm and 19 cm) and tilt angles (45°, 55°, and 60°).

<div align=center>
 <img src="Pixymon-research/Images/left.jpg" height="350">
 <img src="Pixymon-research/Images/estimatedfov.png" height="350">
</div>
<div align=center>
 Rear mount view (left), estimated FOV (right)
</div>

<div align=center>
 <img src="Pixymon-research/Images/pixymonrearview.png" height="350">
</div>
<div align=center>
 PixyMon rear-mounted camera view of red and green pillars
</div>

<div align=center>
 <img src="Pixymon-research/Images/cameracenterside.png" height="350">
 <img src="Pixymon-research/Images/pixymoncenter.png" height="350">
</div>
<div align=center>
 Center mount view (left), PixyMon center view (right)
</div>

<h2> Geometry: </h2>
To estimate the width of the visible area (field of view) at ground level, we used the formula:
<br><br>
<code>w = 2 × h × tan(α / 2)</code>
<br><br>
Where:
<ul>
  <li>h — height of camera (in cm)</li>
  <li>α — horizontal field of view (60° for Pixy2)</li>
</ul>

At 19 cm height and 60° FOV:
<pre>w ≈ 2 × 19 × tan(30°) ≈ 21.9 cm</pre>

<h2> Test setup: </h2>
We ran the robot 10 times for each configuration with identical code, route, and lighting. We measured how many times the robot correctly avoided both obstacles and tracked them without losing sight in PixyMon.

<h3> Table: </h3>
<div align="center">
<table>
<tr><th colspan="6">Camera Position Testing Summary</th></tr>
<tr align="center">
<th>Position</th>
<th>Height (cm)</th>
<th>Tilt Angle (°)</th>
<th>Successful Runs<br>(out of 10)</th>
<th>Estimated FOV (cm)</th>
<th>Notes</th>
</tr>
<tr align="center">
<td>Rear</td>
<td>19</td>
<td>55</td>
<td>9</td>
<td>21.9</td>
<td>Stable detection, good view range</td>
</tr>
<tr align="center">
<td>Rear</td>
<td>15</td>
<td>45</td>
<td>7</td>
<td>17.3</td>
<td>Narrower FOV, occasional loss of object</td>
</tr>
<tr align="center">
<td>Center</td>
<td>19</td>
<td>55</td>
<td>6</td>
<td>21.9</td>
<td>Pillars leave frame early</td>
</tr>
<tr align="center">
<td>Center</td>
<td>19</td>
<td>60</td>
<td>5</td>
<td>23.0</td>
<td>Too steep, floor glare affected image</td>
</tr>
</table>
</div>

<h2> Graph: </h2>
<div align="center">
 <img src="Pixymon-research/Images/graphsuccesrate.jpeg" height="400">
</div>
<div align="center">
 Success rate for different camera setups
</div>

<h2> Conclusion: </h2>
The best performance was recorded with the rear-mounted camera at 19 cm height and 55° tilt. This setup achieved a wide field of view (~22 cm at ground level) and maintained visual contact with both obstacles in most cases. Reducing height or increasing tilt introduced instability.

We will continue using this configuration in our robot.

<h2> Future Work: </h2>
<ul>
  <li>Log Pixy2 signature strength for tracking quality</li>
  <li>Evaluate setup under various lighting</li>
  <li>Test side-mount configurations for wider FOV</li>
</ul>
