```matlab 
%% Short-Time Fourier Transform
%% STFT

N = 128;
n = 0:N - 1;      % Eje x
Fs1 = 0.22;
Fs2 = 0.34;
x1 = sin (2 * pi * n * Fs1);    % señal 1
x2 = sin (2 * pi * n * Fs2);    % señal 2

x3 = x1(1:N/2);
x3((N/2) + 1:N) = x2(1:N/2);
%ventana hamming
specgram(x3, 64, 1, hamming (32), 0);

%ventana de Taylor
specgram(x3, 64, 1, taylorwin (32), 0);

%ventana de Kaiser
specgram(x3, 64, 1, kaiser (32), 0);

%ventana Bohman
specgram(x3, 64, 1, bohmanwin (32), 0);

%ventana de Tukey
specgram(x3, 64, 1, tukeywin (32), 0);

%ventana Gaussiana
specgram(x3, 64, 1, gausswin (32), 0);
```


