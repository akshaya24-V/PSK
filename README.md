# PSK
# Aim
Write a simple Python program for the modulation and demodulation of PSK and QPSK.

# Tools required
python IDL 

# Theory
Phase Shift Keying (PSK) is a digital modulation technique in which the phase of the carrier signal is changed according to the binary input data. In Binary Phase Shift Keying (BPSK), binary 0 and 1 are represented using two different phase shifts, usually 0° and 180°. PSK provides better noise immunity and efficient data transmission. In this experiment, the binary message signal is modulated using a carrier signal and later demodulated to recover the original data using Python in Google Colab.

# Program
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter

# Low-pass filter
def lpf(x, fc, fs):
    b, a = butter(4, fc/(0.5*fs), 'low')
    return lfilter(b, a, x)

# Parameters
fs, fc, br, T = 1000, 50, 10, 1
t = np.arange(0, T, 1/fs)
bd = fs // br

# Message signal
bits = np.random.randint(0, 2, br)
msg = np.repeat(bits, bd)

# Carrier
carrier = np.sin(2*np.pi*fc*t)

# BPSK Modulation (0 → 0°, 1 → 180°)
bpsk = np.sin(2*np.pi*fc*t + np.pi*msg)

# Demodulation
demod = lpf(bpsk * carrier, fc, fs)
decoded = (demod[::bd] < 0).astype(int)

# Plot
plt.figure(figsize=(10,9))
plt.suptitle("NAME : AKSHAYA LAKSHMI V \nREG NO : 212224060014",
             fontsize=12, fontweight='bold')

plt.subplot(4,1,1)
plt.plot(t, msg)
plt.title("Message Signal")
plt.grid(True)

plt.subplot(4,1,2)
plt.plot(t, carrier)
plt.title("Carrier Signal")
plt.grid(True)

plt.subplot(4,1,3)
plt.plot(t, bpsk)
plt.title("PSK Modulated Signal")
plt.grid(True)

plt.subplot(4,1,4)
plt.step(range(len(decoded)), decoded, where='mid')
plt.title("Decoded Bits")
plt.grid(True)

plt.tight_layout(rect=[0,0,1,0.93])
plt.show()
```
# Output Waveform

<img width="1000" height="900" alt="image" src="https://github.com/user-attachments/assets/dcdfd378-3547-4c6a-bd07-9c3128016ae3" />

# Results
The PSK signals were successfully modulated and demodulated using CoLab.

