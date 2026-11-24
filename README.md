📡 WiFi Dead Zone Fixer

An ESP8266-based adaptive reflector that steers WiFi signal into dead zones using real-time RSSI feedback.

A low-cost hardware demo of the idea behind 6G Reconfigurable Intelligent Surfaces (RIS): instead of moving the router or buying an extender, a servo-steered aluminum reflector physically redirects the existing signal toward the weak spot, and a hill-climbing algorithm finds the best angle automatically.


1. Problem

Indoor WiFi coverage is uneven because of walls, furniture and distance. Typical fixes (extenders, mesh, moving the router) are static: they don't adapt to where the signal is actually weak. This project closes the loop: measure → steer → re-measure.

2. Approach
A receiver node sits in the dead zone and measures RSSI of the router's signal.
It sends the RSSI reading to the controller node.
The controller node rotates a servo-mounted aluminum reflector in small steps.
After each step, RSSI is re-measured. If it improved, keep moving in that direction; if it dropped, reverse (hill-climbing).
The reflector settles at the angle that maximizes RSSI at the dead zone.
 Router ))) ──► [ Reflector on servo ] ──► Dead zone
                      ▲                        │
                      │                        ▼
              Node 2 (servo control)  ◄── Node 1 (RSSI measurement)
<!-- TODO: replace the diagram above with a proper block diagram / flowchart image -->
3. Hardware
Component	Qty	Role
ESP8266 (NodeMCU / [model])	2	Node 1: [fill in role], Node 2: [fill in role]
Servo motor ([model])	[1/2]	Steers the reflector ([pan only / pan + tilt])
Aluminum reflector ([size] cm)	1	Redirects 2.4 GHz signal
Power supply	[ ]	[ ]

📐 Wiring diagram: docs/wiring.png (add)

4. Software
Language: C++ (Arduino framework)
node1_rssi/: [what it does: reads RSSI, transmits to Node 2]
node2_servo/: [what it does: receives RSSI, runs hill-climbing, drives servo]
Algorithm parameters: step size [ ]°, scan range [ ]° to [ ]°, RSSI smoothing [ ] samples
5. Results
Condition	RSSI at dead zone (dBm)
No reflector	[ ]
Reflector, fixed/random angle	[ ]
Reflector, after hill-climbing	[ ]

Test setup: router-to-dead-zone distance [ ] m, obstruction: [wall / door / etc.], band: 2.4 GHz, reflector angle found: [ ]°.

Fill this table with your measured numbers. It's the most important section of the README.

6. Connection to RIS / 6G

A RIS is a surface of many small elements whose phase response is electronically tuned to shape the reflected beam. This project is a simplified mechanical analogue:

	This project	Real RIS
Reflecting element	Single aluminum plate	Array of unit cells
Beam control	Mechanical (servo)	Electronic (PIN diode / varactor phase shift)
Feedback	RSSI	CSI / channel estimation
Optimization	Hill-climbing	Beamforming / ML-based optimization

It demonstrates the closed-loop principle that RIS-aided networks rely on, at hobby-hardware cost.

7. Limitations
Passive specular reflection only (no phase control or gain)
2.4 GHz only; RSSI is noisy and can trap hill-climbing in local maxima
[Single-axis / dual-axis] steering
Tested in [one environment]; results may vary with layout
8. Future Work
Dual-axis steering and a larger reflector
Smarter search (simulated annealing / gradient-free optimizers) to avoid local maxima
Move toward electronically tunable surfaces (varactor/PIN-diode unit cells)
5 GHz support and multi-user dead zones
Logging RSSI vs angle to plot coverage heatmaps
9. Repo Structure
├── node1_rssi/        # Node 1 firmware
├── node2_servo/       # Node 2 firmware
├── docs/              # photos, demo video, wiring diagram, report/PPT
└── README.md
10. Author

K. V. S. L. J. Aparajitha B.Tech, Electronics and Communication Engineering GitHub: aparajithakolluri

Suggested repo topics: esp8266 wifi rssi antenna reflector ris 6g embedded-systems rf-engineering
