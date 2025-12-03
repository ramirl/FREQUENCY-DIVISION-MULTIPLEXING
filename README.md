# FREQUENCY-DIVISION-MULTIPLEXING

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
t = linspace(0, 1, 1000);
fs = 1000; 


freqs = [8, 10, 12, 14, 16, 18]; 

signals = zeros(6, length(t));
for i = 1:6
  signals(i, :) = cos(2 * %pi * freqs(i) * t);
end

fdm_signal = zeros(1, length(t));
for i = 1:6
  fdm_signal = fdm_signal + signals(i, :);
end

order = 100; 
cutoff_freq = 15 / (fs/2);  
h = ffilt("lp", order, cutoff_freq);

demux_signals = zeros(6, length(t));
for i = 1:6
  mixed = fdm_signal .* cos(2 * %pi * freqs(i) * t);
  demux_signals(i, :) = filter(h, 1, mixed);
end

scf(1); clf;
for i = 1:6
  subplot(3,2,i);
  plot(t, signals(i, :));
  title('Original Signal f=' + string(freqs(i)));
end

scf(2); clf;
plot(t, fdm_signal);
title('FDM Signal');

scf(3); clf;
for i = 1:6
  subplot(3,2,i);
  plot(t, demux_signals(i, :));
  title('Demultiplexed Signal f=' + string(freqs(i)));
end


```

## OUTPUT WAVEFORM
<img width="1917" height="1038" alt="image" src="https://github.com/user-attachments/assets/1c1bd763-9388-4d16-928b-ea8b60333b32" />
<img width="1916" height="1047" alt="image" src="https://github.com/user-attachments/assets/fce98fc6-2ce4-431f-9945-19178f7bf982" />
<img width="1919" height="1000" alt="image" src="https://github.com/user-attachments/assets/d755e922-79a4-4a63-949a-10c7db2cd0b1" />


## CALCULATION
![WhatsApp Image 2025-12-03 at 19 58 24_e87f8a17](https://github.com/user-attachments/assets/bd9da047-afe9-4920-a16f-a7b282a4fb04)
![WhatsApp Image 2025-12-03 at 19 58 24_fb3e376f](https://github.com/user-attachments/assets/ca635684-bb76-4b5b-ab57-d20b1eff193c)
![WhatsApp Image 2025-12-03 at 19 58 24_fdcb148e](https://github.com/user-attachments/assets/af96ffc1-39aa-47c8-86f3-1a6ede3ba9a3)

## RESULT
Six different message signals were generated and modulated using FDM. All modulated signals were added to form a multiplexed FDM signal. Each message was successfully recovered using coherent demodulation followed by low-pass filtering. The plots confirmed accurate multiplexing and demultiplexing.
