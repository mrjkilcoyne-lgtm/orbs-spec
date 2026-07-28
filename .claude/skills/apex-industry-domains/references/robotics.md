# Robotics

## Scope
Autonomous systems: perception, planning, control, and safety in physical environments.

## Core principles
- Perception is noisy: sensors (cameras, lidar, IMU, odometry) have errors; sensor fusion (combining multiple sensors) mitigates noise but still fails sometimes (sensor blind spots, weather).
- Reality gap is real: simulation is fast but idealized (perfect physics, no unexpected objects); real-world robots encounter novel situations (unknown obstacles, surface variations) that don't appear in training.
- Safety is non-negotiable: robots interact with humans and physical environments; failure modes must be anticipated and mitigated (e-stops, speed limits, safety zones).
- Sample efficiency is critical: collecting real-world robot training data is expensive (time, hardware, risk); techniques that learn from simulation or limited data are valuable.
- Control has latency: a 100ms control loop seems fast but may be too slow for dynamic tasks (catching a falling object, high-speed driving); latency requirements shape hardware choice.

## Apex practices
- Use sim-to-real transfer learning: train in simulation where data is cheap and fast, then fine-tune on real robot data; domain randomization in simulation improves transfer.
- Implement hierarchical planning: high-level planning (where to go), mid-level (obstacles, energy), low-level (motor control); each layer operates at different timescales.
- Use sensor fusion (Kalman filters, particle filters) to estimate state (position, velocity, orientation) from noisy sensors; sensor disagreement triggers alerts.
- Design with safety in mind: robots should fail safe (stop, return to safe state) not fail dangerously; watchdogs, safe operating ranges, and collision detection are mandatory.

## Pitfalls
- Assuming training data generalizes to real world; robots trained in one environment often fail in slightly different conditions.
- Neglecting safety; a robot can cause harm to people or property; safe boundaries and fail-safes are not optional.
- Underestimating perception difficulty; human vision is effortless, but computer vision in varied lighting, occlusion, and clutter is fragile.

## Tools & references
ROS (Robot Operating System, middleware for robotics), simulation: Gazebo, Isaac Sim, Coppeliasim, perception: OpenCV, PCL (point clouds), planning: MoveIt, control: PID loops, model predictive control, imitation learning and reinforcement learning for robot control.
