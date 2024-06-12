---
title:  "Simulation WSN!"
subtitle: "WSN comuniication!"
author: "Lib"
avatar: "img/authors/wferr.png"
image: "img/project-solar-energy.jpg"
date:   2024-06-12 08:30:00
---

### Description
<p style="font-size: 15px;">

I discovered Wouter Bulten's work on SLACTest for simulating networks. In this post, I will explain his work a little.

In this simulation, worldwide scenario: a fixed world without obstructions that houses a collection of nodes. Nodes: (such as Access Points or APs), and Users are in motion. All nodes are randomly positioned within the world’s boundaries, and all moving nodes start with random positions.
</p>

## Simple Explanation:

1. Nodes
<p>
- The Node class stores the current position of a node and calculates the distance between nodes. 

- The MovingNode class represents a node that can move, tracking all previous positions. It requires the implementation of a move method. The moveToPosition method moves the node to the given coordinates and updates the trace of its previous positions. 

- The BouncingNode class represents a node that bounces within a box, with movement determined by its rotation (radial direction) and speed.
</p>

2. Network

<p>

- The WirelessEntity class, an abstract base class, represents a wireless entity in a network with properties such as transmitting power and a signal propagation constant. It calculates signal strength using an RSSI function based on distance, signal propagation constant, transmitting power, and noise level.

- The FixedAP class, a subclass of WirelessEntity and Node, represents a stationary access point with specific transmit power and signal strength.

- The MovingAP class, a subclass of WirelessEntity and BouncingNode, represents a moving access point in a wireless network.

</p>

3. Simulation

<p>

- The Controller class controls iterations and handles output. The iterate method increments the iteration count and outputs a message.

- The NetworkController class, extending the Controller class, manages a network simulation. It initializes all nodes with random positions and movements. The iterate method iterates over all nodes, calling their iterate methods, and also invokes the iterate method of the parent Controller class, the NetworkController class is responsible for initializing and updating nodes in a network simulation.
</p>

## Conclusion

I explain the most remarkable parts of that code and suggest adding a container to improve the project. Additionally, I find the work of Wouter Bulten on SLACTest very valuable

GitHub: https://github.com/wouterbulten/SLACTest

## Lastly

Believe in yourself.🧑🏻‍🎤




