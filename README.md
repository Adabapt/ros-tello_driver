# tello_driver package

## Infos:

Ce driver permet de faire communiquer ROS avec le drone Tello EDU en utilisant la librairie de développement SDK de Tello et ça version modifié en Python offrant plus de possibilités.

## Installation:

Télecharger le projet
Mettre le dossier dans le dossier src du catkin_workspace
Faire un catkin_make pour générer le projet
Faire source devel/setup.bash

## Lancement:

Pour lancer le driver :
Allumer le drone
Se connecter au drone sur son wifi TELLO-XXXXXX
Puis enfin : Roslaunch tello_driver tello_driver_node.launch

## Arborescence:

cfg -> contient les configs du Tello EDU  
launch -> contient les fichiers .launch  
msg -> contient le message de status du Tello EDU  
nodes -> contient les exécutables Python  
src -> contient la bibliothèque TelloPy SDK

## Les topics:

### Subscribed topics

* ```/tello/cmd_vel``` [geometry_msgs/Twist](http://docs.ros.org/api/geometry_msgs/html/msg/Twist.html)
* ```/tello/emergency``` [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* ```/tello/fast_mode``` [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* ```/tello/flattrim``` [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* ```/tello/flip``` [std_msgs/Uint8](http://docs.ros.org/api/std_msgs/html/msg/UInt8.html)
* ```/tello/land``` [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* ```/tello/palm_land``` [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* ```/tello/takeoff``` [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* ```/tello/manual_takeoff``` [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* ```/tello/throw_takeoff``` [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)

### Published topics

* ```/tello/camera/camera_info``` [sensor_msgs/CameraInfo](http://docs.ros.org/api/sensor_msgs/html/msg/CameraInfo.html)
* ```/tello/image_raw``` [sensor_msgs/Image](http://docs.ros.org/api/sensor_msgs/html/msg/Image.html)
* ```/tello/imag/raw/h264``` [h264_image_transport/H264Packet](https://github.com/tilk/h264_image_transport/blob/master/msg/H264Packet.msg)
* ```/tello/odom``` [nav_msgs/Odometry](http://docs.ros.org/api/nav_msgs/html/msg/Odometry.html)
* ```/tello/imu``` [sensor_msgs/Imu](http://docs.ros.org/api/sensor_msgs/html/msg/Imu.html)
* ```/tello/status``` [tello_driver/TelloStatus](https://github.com/appie-17/tello_driver/blob/development/msg/TelloStatus.msg)

## Les Nodes:

### Tello_driver:

La première node à lancer qui assure la liaison entre le drone et ROS.
Il reçoie le flux vidéo, le status du drone etc
Et envoie les commandes et la vitesse du drone.

### Keyboard_teleop:

Mappage des commandes du drone sur des boutons du clavier.  
Il y a un bouton pour chaque commande tels que takeoff, land, emergency.  
takeoff permet de décoller  
land d'attérir  
emergency de couper tous les moteurs  
Puis d'autres boutons pour jouer sur le topic /tello/cmd_vel qui règle la vitesse pour chaque direction et angle du drone.

### Autopilot:

Node de déplacement et de rotation.  
Il suffit alors d'imbriquer les fonctions pour paramétrer des trajets.  
Il gère les consignes et la vitesse de la même façon que la node keyboar_teleop.

## Notes:

Ce package est basé sur :  
https://github.com/appie-17/tello_driver.git  
http://wiki.ros.org/tello_driver

