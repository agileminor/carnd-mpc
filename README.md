# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

## Model

# State
*x: current x location
*y: current y location
*psi: current angle
*v: current speed
*cte: current cross track error
*epsi: current psi error

# Actuators
*steer_angle: range of -1, 1
*acceleration: range of -0.5, 0.5

## N/dt

Started with N = 25, dt = 0.05, was too unstable and drove off road.<br>

Reduced acceleration upper/lower bound and reduced dt to 0.01 and car could make a loop but very unstable.<br>

Best values of N found were N = 8, dt in range 0.06-0.08. Once latency adjustment was added, car could drive track at ~50mph.

## Polynomial Fitting and MPC Preprocessing
Chose to adjust waypoints to car coordinates before fitting. This makes x, y and psi 0 (before latency adjustment). Used a 3rd order polynomial.

## Latency

Adjusted for latency by moving car position by v * latency in x before solving for MPC. More improvements might be possible by taking into account current steer_angle for latency adjustment.






