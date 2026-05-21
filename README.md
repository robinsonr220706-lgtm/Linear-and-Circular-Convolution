# EXP 1 : Linear and Circular Convolution

## AIM: 

 To perform Linear and Circular Convolution for two given sequence using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (Linear Convolution): 
```
clc;
clear;
close;

// Input
x = input("Enter first sequence: ");
h = input("Enter second sequence: ");

m = length(x);
n = length(h);

// Without built-in
y_manual = zeros(1, m+n-1);

for i = 1:m
    for j = 1:n
        y_manual(i+j-1) = y_manual(i+j-1) + x(i)*h(j);
    end
end

// With built-in
y_builtin = convol(x, h);

// Display
disp("Linear Convolution without built-in:");
disp(y_manual);

disp("Linear Convolution with built-in:");
disp(y_builtin);

// ----------- GRAPH -------------
t1 = 0:m-1;
t2 = 0:n-1;
t3 = 0:m+n-2;

figure(1);

subplot(3,1,1);
plot2d3(t1, x);
title("Input Sequence x(n)");

subplot(3,1,2);
plot2d3(t2, h);
title("Input Sequence h(n)");

subplot(3,1,3);
plot2d3(t3, y_builtin);
title("Linear Convolution Output");
```

## PROGRAM (Circular Convolution): 
```
clc;
clear;
close;

// Input
x = input("Enter first sequence: ");
h = input("Enter second sequence: ");

m = length(x);
n = length(h);

N = max(m, n);

// Zero padding
x_pad = [x zeros(1, N-m)];
h_pad = [h zeros(1, N-n)];

// Without built-in
y_manual = zeros(1, N);

for nn = 1:N
    for k = 1:N
        index = modulo(nn-k, N);
        if index < 0 then
            index = index + N;
        end
        y_manual(nn) = y_manual(nn) + x_pad(k)*h_pad(index+1);
    end
end

// With built-in (FFT)
y_builtin = ifft(fft(x_pad).*fft(h_pad));

// Display
disp("Circular Convolution without built-in:");
disp(y_manual);

disp("Circular Convolution with built-in:");
disp(real(y_builtin));

// ----------- GRAPH -------------
t = 0:N-1;

figure(2);

subplot(3,1,1);
plot2d3(t, x_pad);
title("Input Sequence x(n)");

subplot(3,1,2);
plot2d3(t, h_pad);
title("Input Sequence h(n)");

subplot(3,1,3);
plot2d3(t, real(y_builtin));
title("Circular Convolution Output");
```

## OUTPUT (Linear Convolution): 
<img width="1918" height="1078" alt="Screenshot 2026-05-21 155024" src="https://github.com/user-attachments/assets/7b22ec8d-f8da-4360-859d-d3d2a1c5e356" />



## OUTPUT (Circular Convolution):
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/d4f3f150-8b59-4e2c-a2ca-dae3cce277ca" />



## RESULT: 
Thus, the Linear Convolution and Circular Convolution of the given input sequences were successfully computed using Scilab, and the corresponding output sequences were obtained.
