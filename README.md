# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

## Model

# State
  * x: current x location
  * y: current y location
  * psi: current angle
  * v: current speed
  * cte: current cross track error
  * epsi: current psi error

# Actuators
  * steer_angle: range of -1, 1
  * acceleration: range of -0.5, 0.5

# Update
Model equations given by:
* x_t+1 = xt + vt * cos(psi_t) * dt
* yt+1 = yt + vt * sin(psi_t) * dt 
* psit+1 = psit + vt / Lf * steer_angle * dt
* vt+1 = vt + at * dt

We then create simulations of the model with various steer_angle and at, trying to minimize errors of various constraints.

Constraints used: (All squared error)
* cte
* epsi
* v - ref_v
* steer_angle
* a
* steer_anglet+1 - steer_angle (with extra weight to smooth path)
* at+1 - at

## N/dt

Started with N = 25, dt = 0.05, was too unstable and drove off road.<br>

Reduced acceleration upper/lower bound and reduced dt to 0.01 and car could make a loop but very unstable.<br>

Best values of N found were N = 8, dt in range 0.06-0.08. Once latency adjustment was added, car could drive track at ~50mph.

## Polynomial Fitting and MPC Preprocessing
Chose to adjust waypoints to car coordinates before fitting. This makes x, y and psi 0 (before latency adjustment). Used a 3rd order polynomial.

## Latency

Adjusted for latency by moving car position by v * latency in x before solving for MPC. More improvements might be possible by taking into account current steer_angle for latency adjustment.






