# Meraki MV Computer Vision Project

This project uses Meraki’s built-in APIs and MQTT services to send MV sensor data and snapshots for image analysis to AWS Rekognition. This solution can be used for security automation by detecting any object, change in luminosity, people count and facial analysis to secure premises and office environments. 

 ![Alt text](/diagrams/dashboard.png "UI Dashboard")

In addition, PPE detection was developed to recognise face mask and hard hat protection within the image.

The information then is presented in a UI dashboard (Node-RED) or with alerts configured to messaging platforms for greater visibility and instant detection of threats.

![Alt text](/diagrams/architecture.png =250x250 "Architecture")

## Architecture

Meraki have expanded their ecosystem to now include cameras and sensors within the product range. These are smart sensors and far from traditional cameras. 

Their built in processor enables machine learning capabilities and an architecture that reduces physical infrastructure (NVRs) and software requirements as shown above. The footage is stored directly on the smart sensors with options for cloud archive storage. 


![Alt text](/diagrams/architecure_2.png?raw=true "Architecture")

Data is then processed by an algorithm that can detect, classify, and track objects such as people and vehicles within a frame. This provides developers with processed, high-value data and insights without needing any additional hardware, software, or infrastructure and to create bespoke business solutions.


## Orchestration

For the facial analysis, object and text detection, a python script was used to orchestrate the image snapshot to AWS rekognition which then returns a label of the objects it finds in the image. 


![Alt text](/diagrams/orchestration.png?raw=true "Orchestration")

This script also takes that information back from AWS and publishes it to the Node-RED dashboard for so the end user can see the data displayed in a dashboard UI format.


## End Result

The final dashboard is split between the direct API call on the left and the AWS Rekognition orchestration via a python script on the right.

The left panel has direct feeds to the Meraki MV which subscribes to current and historic people count as well as instant and historic light (Lux) levels.

This is then displayed using Node-RED built in graphs and gauges. 

![Alt text](/diagrams/end_result.png "UI Display")

The right side of the dashboard contains the AWS analysis. First the Meraki snapshot taken via API (this is used for the analysis).

Then we have object and text detection which will display a percentage which is how likely the object is actually in the image.

![Alt text](/diagrams/end_result_2.png "PPE Detection")

Lastly PPE detection returns a percentage of any objects that are coving the head and face.

## Beyond Cameras

The cameras in this demo could easily be replaced with the Meraki MT sensors that can measure motion, temperature and water or even the Meraki MR which when used in a large deployments can send client location data and be plotted within the floorplan map. 
