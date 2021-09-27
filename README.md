# thymio-road-network
This semester project was made in colaboration with Benjamin Kern.

[![thymio-road-network](https://github.com/loicdubois/thymio-road-network/blob/main/documentation/thymio-road-network.jpg)](https://www.youtube.com/watch?v=cV4ZRwwuIH8)
(Click the picture to watch a video of the network in action)

## Description
This project consisted in the realisation of a road network for the [Thymio](https://www.thymio.org/), an educative robot with many sensors and actuators.

A road network consits in a finite number of locations connected by several roads. I had to first design the road. then design barcodes to collect informations from the network and a robust reading method associated with it. I also implemented two different collision avoidance method. One that slows down the speed of the robot until a given threshold and then stops the robot and the other one that directly stops the robot once a threshold is reached. Finally we deigned four different type of intersections branching, roundabout, location and crossroad. Each intersection requires a specific control sequence to fulfil the choice made by the robot.

The main issue for the line following was the loss of the road. Due to the design chosen, a gradient line, the control implemented works well on one side of the road only.I tried different solutions but none of them gave satisfying results.

After developping the method for the reading, it appeared that it was relatively robust for modest changes of speed. Moreover, I also discovered, thanks to the dynamic sequence of action adaptation, that there is a wide rang of speeds in which we can read the barcode. I also implemented a security to avoid triggering the reading when the sensor responsible for this action comes on the black side of the road.

The collision avoidance methods gave also satisfying results. At first I only implemented it for the forward motion but I extended it to the backward motion as well as when there is no line to follow and we must respect a timing. I even created a more complex method in case of the presence of an other robot on the code just before a Thymio starts reading. The coming robot will perform a backward maneuverer and then re-start to move again but at the lowest speed defined to minimize the dynamics effect on the reading.

Finally some intersections caused more problems than others. The branching and the roundabout were simple to design and implement but their control required to cross some road. Therefore the robot had to stop the line following for a while. Due to straightness problem, I enforced a light left turn with the commands sent to the robot to increase its chances to find the road back. In the crossroad, the Thymio had to cross four times a road with small distances to reach the reuired orientation. It appeared that the robot was often missing the last code and could not leave the corresponding state. I forced therefore the last continue action directly after the third one.

The calibration of the robots was mandatory but I discovered I had to balance sharp left turns without leaving the road and right turns without triggering the reading when setting the grey reference for the line following. It was not always possible to avoid both problems.

## Folder structure
- _designs_: Tracks and 3-bits barcodes ready to use. Includes also map examples
- _documentation_: Report for the semester project in French and English for the global infrastructure, English only for the local infrastructure
- _src_: Code for the vehicles (Thymio Road), parking traffic light (Signal Parking) and crossroad traffic light (SignalCrossroad)

Note the map implemented in the vehicles corresponds to the map below in the _designs_ folder

![network](https://github.com/loicdubois/thymio-road-network/blob/main/designs/maps/map3.jpg)
