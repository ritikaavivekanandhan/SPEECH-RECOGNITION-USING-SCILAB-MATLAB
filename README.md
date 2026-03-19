# EXP 5 : SPEECH RECOGNITION USING SCILAB

## AIM: 

To perform and verify speech recognition using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM : 
~~~
clc;
clear;
close;

disp("Loading audio files...");

// ---- Read audio files ----
[y1, fs1] = wavread("C:\Users\acer\Downloads\referance.wav");
[y2, fs2] = wavread("C:\Users\acer\Downloads\test.wav");

// ---- Check sampling rate ----
if fs1 <> fs2 then
    error("Sampling rates must match!");
end

// ---- Convert to mono if stereo ----
if size(y1,2) == 2 then
    y1 = mean(y1, 2);
end
if size(y2,2) == 2 then
    y2 = mean(y2, 2);
end

// ---- Make same length ----
n = min(length(y1), length(y2));
y1 = y1(1:n);
y2 = y2(1:n);

// ---- Normalize signals (IMPORTANT) ----
y1 = y1 / max(abs(y1));
y2 = y2 / max(abs(y2));

// ---- Euclidean Distance ----
dist = sqrt(sum((y1 - y2).^2));
disp("Euclidean distance = " + string(dist));

// ---- Decision ----
if dist < 0.5 then
    disp("✅ Matching with reference (same word)");
else
    disp("❌ Not matching with reference (different word)");
end

// ---- Plot individual signals ----
figure(0);

subplot(2,1,1);
plot(y1);
title("REFERENCE VOICE SIGNAL");
xlabel("Samples");
ylabel("Amplitude");

subplot(2,1,2);
plot(y2);
title("TEST VOICE SIGNAL");
xlabel("Samples");
ylabel("Amplitude");

// ---- Overlay comparison ----
figure(1);
plot(y1, 'b');                 // Reference
xset("auto clear", "off");     // IMPORTANT
plot(y2, 'r');                 // Test

title("Reference (Blue) vs Test (Red)");
xlabel("Samples");
ylabel("Amplitude");
legend(["Reference", "Test"]);

// ---- Done ----
disp("Waveforms plotted and compared successfully.");
~~~

## OUTPUT: 


## RESULT: 
Thus the speech recognition using SCILAB was performed and verified.
