# Ideal, Natural, & Flat-top -Sampling
# Aim
Write a simple Python program for the construction and reconstruction of ideal, natural, and flattop sampling.
# Tools required
Google Colab
# THEORY:
# IMPULSE SAMPLING:
Sampling signal is periodic impulse train . The area of each impulse in the sampled signal is equal to instantaneous value of input signal.
# NATURAL SAMPLING:
It is also called practical sampling.  In this sampling technique, the sampling signal is a pulse train.  In natural sampling method, the top of each pulse in the sampled signal retains the shape of input        signal during pulse interval.
# FLAT-TOP SAMPLING:
The flat-top sampling is also the practical sampling technique.  In the top sampling, the sampling signal is also a pulse train.  The top of each pulse in sampled signal remain constant and is equal to the instantaneous value of input signal x(n) at start of samples.

# Program
# IMPULSE SAMPLING:
```
import numpy as np
import matplotlib.pyplot as plt

# Original signal
t = np.linspace(0,1,500)
x = np.sin(2*np.pi*5*t)

# Sampling
fs = 100
Ts = 1/fs
n = np.arange(0,1,Ts)
xs = np.sin(2*np.pi*5*n)

# Reconstruction
xr = 0
for i in range(len(n)):
    xr += xs[i]*np.sinc((t-n[i])/Ts)

# Plot
plt.plot(t,x,label="Original")
plt.stem(n,xs,label="Impulse Sampling")
plt.plot(t,xr,'g--',label="Reconstructed")

plt.legend()
plt.grid()
plt.show()
```
# NATURAL SAMPLING:
```
import numpy as np
import matplotlib.pyplot as plt

# -----------------------------
# 1. Original Signal
# -----------------------------
t = np.linspace(0, 1, 1000)
f = 5
x = np.sin(2*np.pi*f*t)

# -----------------------------
# 2. Pulse Train
# -----------------------------
fs = 50
Ts = 1/fs
pulse_width = Ts/4

pulse = np.where((t % Ts) < pulse_width, 1, 0)

# -----------------------------
# 3. Natural Sampling
# -----------------------------
sampled = x * pulse

# -----------------------------
# 4. Reconstruction (LPF approx)
# -----------------------------
xr = np.convolve(sampled, np.ones(20)/20, mode='same')

# -----------------------------
# 5. Plot (4 graphs like your image)
# -----------------------------
plt.figure(figsize=(10,8))

# Original signal
plt.subplot(4,1,1)
plt.plot(t, x)
plt.title("Original Message Signal")
plt.grid()

# Pulse train
plt.subplot(4,1,2)
plt.plot(t, pulse)
plt.title("Pulse Train")
plt.grid()

# Natural sampled signal
plt.subplot(4,1,3)
plt.plot(t, sampled)
plt.title("Natural Sampling")
plt.grid()

# Reconstructed signal
plt.subplot(4,1,4)
plt.plot(t, xr, 'g')
plt.title("Reconstructed Message Signal")
plt.grid()

plt.tight_layout()
plt.show()
```
# FLAT-TOP SAMPLING:
```
import numpy as np
import matplotlib.pyplot as plt

# 1. Original signal
t = np.linspace(0, 1, 500)
x = np.sin(2*np.pi*5*t)

# 2. Sampling
fs = 50
Ts = 1/fs
n = np.arange(0, 1, Ts)
xs = np.sin(2*np.pi*5*n)

# 3. Flat-top sampling (hold value)
flat = np.zeros_like(t)
for i in range(len(n)):
    flat[(t >= n[i]) & (t < n[i] + Ts/2)] = xs[i]

# 4. Reconstruction (simple smoothing)
xr = np.convolve(flat, np.ones(10)/10, mode='same')

# 5. Plots
plt.figure(figsize=(8,8))

plt.subplot(4,1,1)
plt.plot(t, x)
plt.title("Original Signal")

plt.subplot(4,1,2)
plt.stem(n, np.ones(len(n)))
plt.title("Sampling Instants")

plt.subplot(4,1,3)
plt.plot(t, flat)
plt.title("Flat-Top Sampled")

plt.subplot(4,1,4)
plt.plot(t, xr)
plt.title("Reconstructed")

plt.tight_layout()
plt.show()
```
# Output Waveform:
# IMPULSE SAMPLING:
<img width="722" height="497" alt="image" src="https://github.com/user-attachments/assets/54ac3c46-80a4-4d63-ae3d-d23581a2a810" />

# NATURAL SAMPLING:
<img width="1259" height="965" alt="Screenshot 2026-04-29 090817" src="https://github.com/user-attachments/assets/9a402bd9-caf3-41ef-9927-bd108f3c064a" />

# FLAT-TOP SAMPLING:
<img width="1008" height="977" alt="Screenshot 2026-04-29 091134" src="https://github.com/user-attachments/assets/cb087eaf-c350-4a6e-8680-2c374d4ce4da" />

# Results
Thus, the construction and reconstruction of Ideal, Natural, and Flat-top sampling were successfully implemented using Python, and the corresponding waveforms were obtained.
