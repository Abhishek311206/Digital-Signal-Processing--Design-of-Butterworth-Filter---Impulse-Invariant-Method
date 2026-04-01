# Digital-Signal-Processing--Design-of-Butterworth-Filter---Impulse-Invariant-Method
## AIM:
To design of 2nd order Low Pass Butterworth Filter using using Impulse Invariant Transformation 
## SOFTWARE REQUIRED: 
MAT LAB R2012
## ALGORITHM:
Step 1: Open MAT LAB. Write the program. 

Step 2: Read the values of Ap,As,Pass band frequency,Stop band frequency.

Step 3: Initialise some conditions find out the order (N) value.

Step 4: Find out the transfer function of the filter and magnitude of that filter. 

Step 5: Plot the magnitude spectrum with x-label and y-label with suitable title. 

Step 6: Terminate the program.

## PROGRAM:
```
clc;
clear all;
close all;

% INPUT PARAMETERS
Ap = input('enter the value of Ap: ');
As = input('enter the value of As: ');
wp = input('enter the PB frequency: ');
ws = input('enter the SB frequency: ');
T  = input('enter the value of time: ');

% PRE-WARPING
omega_p = wp / T;
omega_s = ws / T;

% ATTENUATION
alpha_p = -20 * log10(Ap);
alpha_s = -20 * log10(As);

% BUTTERWORTH FILTER ORDER
[N, wc] = buttord(omega_p, omega_s, alpha_p, alpha_s, 's');

% ANALOG FILTER (NORMALIZED)
[num, den] = butter(N, 1, 's');
disp('Normalized transfer function:');
hs = tf(num, den)

% ANALOG FILTER (UNNORMALIZED)
[num1, den1] = butter(N, wc, 's');
disp('Unnormalized transfer function:');
hs1 = tf(num1, den1)

% DIGITAL FILTER USING IMPULSE INVARIANCE
[numz, denz] = impinvar(num1, den1, 1/T);
hz = tf(numz, denz, T)

disp('Digital transfer function:');

% FREQUENCY RESPONSE
w = 0:pi/16:pi;
y = freqz(numz, denz, w);

% MAGNITUDE SPECTRUM
y1 = abs(y);
figure;
plot(w, y1);
xlabel('frequency');
ylabel('magnitude');
title('Magnitude response of Butterworth LPF');
```


## OUTPUT:

<img width="659" height="507" alt="image" src="https://github.com/user-attachments/assets/c86b6907-c46f-4ee4-a638-26a6be9a74a1" />

## RESULT:

<img width="899" height="1599" alt="image" src="https://github.com/user-attachments/assets/f364d3f7-00e5-43bb-9d65-e73dc905c2b9" />
