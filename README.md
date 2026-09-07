# IIR-FILTER-DESIGN
# EXP 3 A: DESIGN OF LOW PASS BUTTERWORTH FILTER USING BILINEAR TRANSFORMATION TECHNIQUE

# AIM: 

# To perform design of Butterworth Filter Using Impulse Invariant and Bilinear Transformation Techniques using SCILAB.

# APPARATUS REQUIRED: 
PC installed with SCILAB. 

# PROGRAM: 
```
clc;
close;

// Inputs
wp = input('Enter the pass band frequency (Radians )= ');
ws = input('Enter the stop band frequency (Radians )= ');
alphap = input('Enter the pass band attenuation (dB)=');
alphas = input('Enter the stop band attenuation(dB)=');
T = input('Enter the Value of sampling Time=');

// Pre warping- Bilinear Transformation
omegap = (2/T) * tan(wp/2);
disp(omegap, 'omegap=');
omegas = (2/T) * tan(ws/2);
disp(omegas, 'omegas=');

// Order of the filter
N = log10(((10^(0.1*alphas)) - 1) / ((10^(0.1*alphap)) - 1)) / (2 * log10(omegas/omegap));
disp(N, 'N=');
N = ceil(N);
disp(N, 'Round off value of N=');

// Cut off frequency
omegac = omegap / (((10^(0.1*alphap)) - 1)^(1 / (2 * N)));
disp(omegac, 'omegac=');

disp('Normalised Analog LPF Transfer function H(S)=');
hs_Normalised = analpf(N, 'butt', [0,0], 1);
disp(hs_Normalised);

disp('Analog LPF Transfer function H(S)=');
hs = analpf(N, 'butt', [0,0], omegac);
disp(hs);

// Bilinear Transformation
z = poly(0, 'z'); // Defining variable z
Hz = horner(hs, (2/T) * ((z - 1)/(z + 1)));
disp('Digital LPF Transfer function H(Z)=');
disp(Hz);

// Frequency response
HW = frmag(Hz, 512);
w = 0 : %pi/511 : %pi;
plot(w/%pi, abs(HW));
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude');
title('Frequency Response of Butterworth IIR LPF');
```

# OUTPUT: 
<img width="960" height="1280" alt="WhatsApp Image 2026-09-07 at 09 59 40" src="https://github.com/user-attachments/assets/b50bfb2c-b427-4f36-be1a-2ed0cad5f3d7" />
CALCULATION:
<img width="775" height="1280" alt="image" src="https://github.com/user-attachments/assets/c361f05d-1543-425e-b171-47efbe599102" />
<img width="856" height="1280" alt="image" src="https://github.com/user-attachments/assets/efcc2ab8-3c9a-4b76-8ea7-ddae17e592a9" />
<img width="1072" height="1280" alt="image" src="https://github.com/user-attachments/assets/c31d0133-09b6-4e74-b52a-c629f2abe24d" />
<img width="1280" height="845" alt="image" src="https://github.com/user-attachments/assets/b6ed569c-cea9-4e12-9ddb-9de51aefb4c4" />


# RESULT: 

Thus, design of Butterworth Low pass IIR filter waveforms were plotted and output was verified.

