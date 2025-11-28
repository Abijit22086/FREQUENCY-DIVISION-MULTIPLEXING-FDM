# FREQUENCY-DIVISION-MULTIPLEXING-FDM


### AIM:

To write a Scilab program to simulate frequency division multiplexing and demultiplexing for six different frequencies, and verify the demultiplexed outputs correspond to the original signals.  

### EQUIPMENTS Needed

Computer with Scilab installed  

### ALGORITHM

1.Define six different frequencies to generate six sine wave signals.  
2.Generate the time vector to represent time samples.  
3.Compute six sine signals for each frequency over the time vector.  
4.Frequency Division Multiplexing: sum all six sine signals to make one multiplexed signal.  
5.Frequency Division Demultiplexing: for each frequency, multiply the multiplexed signal by a sine wave of that frequency (mixing), then apply a lowpass filter to extract the baseband (original) signal.  
6.Plot original signals, multiplexed signal, and demultiplexed signals for verification.  

### PROCEDURE
  Refer Algorithms and write code for the experiment.  
  • Open SCILAB in System  
  • Type your code in New Editor  
  • Save the file  
  • Execute the code  
  • If any Error, correct it in code and execute again  
  • Verify the generated waveform using Tabulation and Model Waveform  
  
### PROGRAM

```
t = linspace(0, 1, 1000);
fs = 1000; 

freqs = [5, 11, 17, 23, 29, 35];

signals = zeros(6, length(t));
for i = 1:6
    signals(i, :) = cos(2 * %pi * freqs(i) * t);
end

fdm_signal = zeros(1, length(t));
for i = 1:6
    fdm_signal = fdm_signal + signals(i, :);
end

order = 50;
cutoff_freq = 8 / (fs/2); 
h = ffilt("lp", order, cutoff_freq);

demux_signals = zeros(6, length(t));
for i = 1:6
    mixed = fdm_signal .* cos(2 * %pi * freqs(i) * t);
    demux_signals(i, :) = filter(h, 1, mixed);
end

scf(1);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, signals(i, :));
    title('Original Signal f=' + string(freqs(i)));
end

scf(2);
clf;
plot(t, fdm_signal);
title('FDM Signal');

scf(3);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, demux_signals(i, :));
    title('Demultiplexed Signal f=' + string(freqs(i)));
end


```
### TABULATION:

<img width="871" height="1280" alt="image" src="https://github.com/user-attachments/assets/d84ee05e-bf94-4178-8bc3-4d9162b52acf" />


### GRAPH:
<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/91c12e83-d0bb-410c-aa46-212fb8685b13" />
<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/2f09c4b1-0c17-4ee5-aee2-fe913114396e" />
<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/97faa143-e509-4a4e-9a39-0d21e5794ed2" />

### RESULT:
The program successfully simulates FDM and demultiplexing for multiple frequency signals with filtering to recover original signals accurately in Scilab.
