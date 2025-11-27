# Frequency Division Multiplexing


## AIM
To implement Frequency Division Multiplexing (FDM) for six different message signals using Scilab, generate the multiplexed signal, and perform demultiplexing to recover all the original message signals. The experiment also includes plotting the message signals, multiplexed signal, and demultiplexed signals.

## APPARATUS REQUIRED

1. Computer System
2. Scilab Software

## ALGORITHM

1. Set sampling frequency, time duration, and time vector.
2. Generate six message signals with different frequencies.
3. Assign six different carrier frequencies.
4. Perform DSB-SC modulation by multiplying each message with its carrier.
5. Add all modulated signals to form the multiplexed FDM signal.
6. For each channel, multiply the multiplexed signal with the same carrier (demodulation).
7. Apply a low-pass filter to extract the recovered message.
8. Plot message signals, multiplexed signal, and recovered s  ignals.

## THEORY

Frequency Division Multiplexing (FDM) is a technique in which multiple message signals are transmitted simultaneously over a single communication channel by assigning each signal a different carrier frequency. Each message modulates its own carrier, and all modulated signals are added to form the multiplexed signal. Since the carrier frequencies are well separated, the signals do not overlap in the frequency domain.

At the receiver, each signal is recovered by multiplying the multiplexed signal with the corresponding carrier (coherent demodulation) and passing it through a low-pass filter to extract the original baseband message. FDM is widely used in radio broadcasting, telephone systems, and cable TV.

## PROGRAM
```
clc;
clear;
close;

// Sampling frequency
fs = 70000;                 // <-- changed sample rate
t = 0:1/fs:0.04;            // <-- changed duration

// NEW message signals (changed amplitudes & frequencies)
m1 = 1.0 * sin(2*%pi*110*t);
m2 = 1.3 * sin(2*%pi*130*t);
m3 = 1.5 * sin(2*%pi*150*t);
m4 = 1.7 * sin(2*%pi*170*t);
m5 = 1.9 * sin(2*%pi*190*t);
m6 = 2.1 * sin(2*%pi*210*t);

// NEW carrier signals (changed frequencies)
c1 = cos(2*%pi*3000*t);
c2 = cos(2*%pi*5000*t);
c3 = cos(2*%pi*7000*t);
c4 = cos(2*%pi*9000*t);
c5 = cos(2*%pi*11000*t);
c6 = cos(2*%pi*13000*t);

// Modulation (DSB-SC)
s1 = m1 .* c1;
s2 = m2 .* c2;
s3 = m3 .* c3;
s4 = m4 .* c4;
s5 = m5 .* c5;
s6 = m6 .* c6;

// FDM multiplexing
fdm = s1 + s2 + s3 + s4 + s5 + s6;

// Demodulation – mixing back
r1 = fdm .* c1;
r2 = fdm .* c2;
r3 = fdm .* c3;
r4 = fdm .* c4;
r5 = fdm .* c5;
r6 = fdm .* c6;

// NEW cutoff frequency
cutoff_hz = 450;                     // changed
norm_cutoff = cutoff_hz / (fs/2);

// NEW filter length
M = 121;                             // changed FIR length

// Low pass filter design
[h, w] = wfir("lp", M, [norm_cutoff, 0], "hm", 0);

// Filtering (LPF)
d1 = conv(r1, h, "same");
d2 = conv(r2, h, "same");
d3 = conv(r3, h, "same");
d4 = conv(r4, h, "same");
d5 = conv(r5, h, "same");
d6 = conv(r6, h, "same");

// Scaling
d1 = 2*d1;
d2 = 2*d2;
d3 = 2*d3;
d4 = 2*d4;
d5 = 2*d5;
d6 = 2*d6;

// PLOTS
figure(1);
subplot(3,2,1); plot(t,m1); title("Message 1");
subplot(3,2,2); plot(t,m2); title("Message 2");
subplot(3,2,3); plot(t,m3); title("Message 3");
subplot(3,2,4); plot(t,m4); title("Message 4");
subplot(3,2,5); plot(t,m5); title("Message 5");
subplot(3,2,6); plot(t,m6); title("Message 6");

figure(2);
plot(t,fdm);
title("FDM Multiplexed Signal");

figure(3);
subplot(3,2,1); plot(t,d1); title("Demod 1");
subplot(3,2,2); plot(t,d2); title("Demod 2");
subplot(3,2,3); plot(t,d3); title("Demod 3");
subplot(3,2,4); plot(t,d4); title("Demod 4");
subplot(3,2,5); plot(t,d5); title("Demod 5");
subplot(3,2,6); plot(t,d6); title("Demod 6");
```
## OUTPUT WAVEFORM
<img width="1908" height="1032" alt="image" src="https://github.com/user-attachments/assets/9c759108-e823-4f4b-a022-1182c0958f3b" />

<img width="1902" height="1013" alt="image" src="https://github.com/user-attachments/assets/513db883-a93f-447a-8ab6-a7ead8ec6b40" />

<img width="1915" height="1023" alt="image" src="https://github.com/user-attachments/assets/6d2c1e2e-185f-415c-8c50-7aee687fdffe" />



## CALCULATION
![WhatsApp Image 2025-11-27 at 09 09 50_2745f5b1](https://github.com/user-attachments/assets/f9f7ca12-f26b-4c8d-b192-6ba22d98a0a0)
![WhatsApp Image 2025-11-27 at 09 09 37_7b5103e0](https://github.com/user-attachments/assets/76770a50-3f0c-4746-b1f3-1fc7daf72350)


## RESULT
Six different message signals were generated and modulated using FDM. All modulated signals were added to form a multiplexed FDM signal. Each message was successfully recovered using coherent demodulation followed by low-pass filtering. The plots confirmed accurate multiplexing and demultiplexing.
