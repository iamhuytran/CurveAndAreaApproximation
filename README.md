# CurveAndAreaApproximation
Approximate curves using Cubic Spline, Continuous Trigonometric Polynomial, and Discrete Trigonometric Polynomial approximation. 
Approximate areas using Simpson’s Rule and Trapezoidal’s Rule.



clc;
clear;


% 2.)
% fprintf('Head')
x1=[1 1.25 3 3.25 4 6 10 11.5 13];
y1=[4 6 7 9.5 10 11.25 11 10 8.5];
[a b c d]=CubicSpline_HuyTran(x1,y1,8,-1);
fprintf('\n')
h1func=@(x)4 + 8*(x-1) + 5.8651*(x-1).^2 + -23.4606*(x-1).^3;
% h1=fplot(@(x)4 + 8*(x-1) + 5.8651*(x-1).^2 + -23.4606*(x-1).^3,[1,1.25],'g');
h2func=@(x)6 + 6.5337*(x-1.25) + -11.7303*(x-1.25).^2 + 4.7562*(x-1.25).^3;
% h2=fplot(@(x)6 + 6.5337*(x-1.25) + -11.7303*(x-1.25).^2 + 4.7562*(x-1.25).^3,[1.25,3],'g');
h3func=@(x)7 + 9.1749*(x-3) + 13.2395*(x-3).^2 + -39.7559*(x-3).^3;
% h3=fplot(@(x)7 + 9.1749*(x-3) + 13.2395*(x-3).^2 + -39.7559*(x-3).^3,[3,3.25],'g');
h4func=@(x)9.5 + 8.3404*(x-3.25) + -16.5774*(x-3.25).^2 + 8.461*(x-3.25).^3;
% h4=fplot(@(x)9.5 + 8.3404*(x-3.25) + -16.5774*(x-3.25).^2 + 8.461*(x-3.25).^3,[3.25,4],'g');
h5func=@(x)10 + -2.2477*(x-4) + 2.4599*(x-4).^2 + -0.51178*(x-4).^3;
% h5=fplot(@(x)10 + -2.2477*(x-4) + 2.4599*(x-4).^2 + -0.51178*(x-4).^3,[4,6],'g');
h6func=@(x)11.25 + 1.4506*(x-6) + -0.61075*(x-6).^2 + 0.058118*(x-6).^3;
% h6=fplot(@(x)11.25 + 1.4506*(x-6) + -0.61075*(x-6).^2 + 0.058118*(x-6).^3,[6,10],'g');
h7func=@(x)11 + -0.64572*(x-10) + 0.086669*(x-10).^2 + -0.067091*(x-10).^3;
% h7=fplot(@(x)11 + -0.64572*(x-10) + 0.086669*(x-10).^2 + -0.067091*(x-10).^3,[10,11.5],'g');
h8func=@(x)10 + -0.83857*(x-11.5) + -0.21524*(x-11.5).^2 + 0.071746*(x-11.5).^3;
% h8=fplot(@(x)10 + -0.83857*(x-11.5) + -0.21524*(x-11.5).^2 + 0.071746*(x-11.5).^3,[11.5,13],'g');



% fprintf('Back')
x2=[13 15.5 19 21 23];
y2=[8.5 11 13 13.5 16.5];
[a b c d]=CubicSpline_HuyTran(x2,y2,-1,1.5);
fprintf('\n')
b1func=@(x)8.5 + -1*(x-13) + 1.3881*(x-13).^2 + -0.23525*(x-13).^3;
% b1=fplot(@(x)8.5 + -1*(x-13) + 1.3881*(x-13).^2 + -0.23525*(x-13).^3,[13,15.5],'g');
b2func=@(x)11 + 1.5297*(x-15.5) + -0.37623*(x-15.5).^2 + 0.029266*(x-15.5).^3;
% b2=fplot(@(x)11 + 1.5297*(x-15.5) + -0.37623*(x-15.5).^2 + 0.029266*(x-15.5).^3,[15.5,19],'g');
b3func=@(x)13 + -0.028357*(x-19) + -0.068938*(x-19).^2 + 0.10406*(x-19).^3;
% b3=fplot(@(x)13 + -0.028357*(x-19) + -0.068938*(x-19).^2 + 0.10406*(x-19).^3,[19,21],'g');
b4func=@(x)13.5 + 0.94459*(x-21) + 0.55541*(x-21).^2 + -0.13885*(x-21).^3;
% b4=fplot(@(x)13.5 + 0.94459*(x-21) + 0.55541*(x-21).^2 + -0.13885*(x-21).^3,[21,23],'g');

syms pw(x)
pw(x)=piecewise((x>=1)&(x<1.25),h1func,(x>=1.25)&(x<3),h2func,(x>=3)&(x<3.25),h3func,(x>=3.25)&(x<4),h4func,(x>=4)&(x<6),h5func,(x>=6)&(x<10),h6func,(x>=10)&(x<11.5),h7func,(x>=11.5)&(x<13),h8func,(x>=13)&(x<15.5),b1func,(x>=15.5)&(x<19),b2func,(x>=19)&(x<21),b3func,(x>=21)&(x<=23),b4func);
fplot(pw,[1,23],'g')
hold on
xlim([0,25]);
ylim([-5,45]);
title('Huy Tran');
xlabel('x-axis');
ylabel('y-axis');



%  3.)
[h1a0 h1a1 h1a2 h1a3 h1b1 h1b2 h1b3]=trigpoly_HuyTran(@(x)4 + 8*(x-1) + 5.8651*(x-1).^2 + -23.4606*(x-1).^3,1,1.25);
[h2a0 h2a1 h2a2 h2a3 h2b1 h2b2 h2b3]=trigpoly_HuyTran(@(x)6 + 6.5337*(x-1.25) + -11.7303*(x-1.25).^2 + 4.7562*(x-1.25).^3,1.25,3);
[h3a0 h3a1 h3a2 h3a3 h3b1 h3b2 h3b3]=trigpoly_HuyTran(@(x)7 + 9.1749*(x-3) + 13.2395*(x-3).^2 + -39.7559*(x-3).^3,3,3.25);
[h4a0 h4a1 h4a2 h4a3 h4b1 h4b2 h4b3]=trigpoly_HuyTran(@(x)9.5 + 8.3404*(x-3.25) + -16.5774*(x-3.25).^2 + 8.461*(x-3.25).^3,3.25,4);
[h5a0 h5a1 h5a2 h5a3 h5b1 h5b2 h5b3]=trigpoly_HuyTran(@(x)10 + -2.2477*(x-4) + 2.4599*(x-4).^2 + -0.51178*(x-4).^3,4,6);
[h6a0 h6a1 h6a2 h6a3 h6b1 h6b2 h6b3]=trigpoly_HuyTran(@(x)11.25 + 1.4506*(x-6) + -0.61075*(x-6).^2 + 0.058118*(x-6).^3,6,10);
[h7a0 h7a1 h7a2 h7a3 h7b1 h7b2 h7b3]=trigpoly_HuyTran(@(x)11 + -0.64572*(x-10) + 0.086669*(x-10).^2 + -0.067091*(x-10).^3,10,11.5);
[h8a0 h8a1 h8a2 h8a3 h8b1 h8b2 h8b3]=trigpoly_HuyTran(@(x)10 + -0.83857*(x-11.5) + -0.21524*(x-11.5).^2 + 0.071746*(x-11.5).^3,11.5,13);

[b1a0 b1a1 b1a2 b1a3 b1b1 b1b2 b1b3]=trigpoly_HuyTran(@(x)8.5 + -1*(x-13) + 1.3881*(x-13).^2 + -0.23525*(x-13).^3,13,15.5);
[b2a0 b2a1 b2a2 b2a3 b2b1 b2b2 b2b3]=trigpoly_HuyTran(@(x)11 + 1.5297*(x-15.5) + -0.37623*(x-15.5).^2 + 0.029266*(x-15.5).^3,15.5,19);
[b3a0 b3a1 b3a2 b3a3 b3b1 b3b2 b3b3]=trigpoly_HuyTran(@(x)13 + -0.028357*(x-19) + -0.068938*(x-19).^2 + 0.10406*(x-19).^3,19,21);
[b4a0 b4a1 b4a2 b4a3 b4b1 b4b2 b4b3]=trigpoly_HuyTran(@(x)13.5 + 0.94459*(x-21) + 0.55541*(x-21).^2 + -0.13885*(x-21).^3,21,23);

a0=h1a0+h2a0+h3a0+h4a0+h5a0+h6a0+h7a0+h8a0+b1a0+b2a0+b3a0+b4a0;
a1=h1a1+h2a1+h3a1+h4a1+h5a1+h6a1+h7a1+h8a1+b1a1+b2a1+b3a1+b4a1;
a2=h1a2+h2a2+h3a2+h4a2+h5a2+h6a2+h7a2+h8a2+b1a2+b2a2+b3a2+b4a2;
a3=h1a3+h2a3+h3a3+h4a3+h5a3+h6a3+h7a3+h8a3+b1a3+b2a3+b3a3+b4a3;
b1=h1b1+h2b1+h3b1+h4b1+h5b1+h6b1+h7b1+h8b1+b1b1+b2b1+b3b1+b4b1;
b2=h1b2+h2b2+h3b2+h4b2+h5b2+h6b2+h7b2+h8b2+b1b2+b2b2+b3b2+b4b2;
b3=h1b3+h2b3+h3b3+h4b3+h5b3+h6b3+h7b3+h8b3+b1b3+b2b3+b3b3+b4b3;

S3=@(x)a0/2+a1*cos(x)+b1*sin(x)+a2*cos(x.*2)+b2*sin(x.*2)+a3*cos(x.*3)+b3*sin(x.*3);
leadinga=a0/2;
formatspec1='S3 = %4.2f + %4.2fcos(x) + %4.2fsin(x) + %4.2fcos(2x) + %4.2fsin(2x) + %4.2fcos(3x) + %4.2fsin(3x)\n';
fprintf(formatspec1,leadinga,a1,b1,a2,b2,a3,b3)
fplot(S3,[1,23],'b');


% 4.)
ran=randperm(23,20);
scatter(ran,pw(ran),'filled','MarkerFaceColor',[171 104 87]./255)


% 5.)
x=ran;
y=pw(ran);
[b m]=leastsq_HuyTran(x,y);
formatspec2='y = %4.2fx + %4.2f\n';
fprintf(formatspec2,m,b)
lsqline=@(x)m*x+b;
plot(x,lsqline(x),'r')

% 6.)
[a0 a1 b1 a2 b2 a3]=disctrigpoly_HuyTran(x,y);
T3=@(x)a0/2+a1*cos(x)+b1*sin(x)+a2*cos(x.*2)+b2*sin(x.*2)+a3*cos(x.*3);
leadinga2=a0/2;
formatspec1='T3 = %4.2f + %4.2fcos(x) + %4.2fsin(x) + %4.2fcos(2x) + %4.2fsin(2x) + %4.2fcos(3x)\n';
fprintf(formatspec1,leadinga2,a1,b1,a2,b2,a3)
fplot(T3,[1,23],'Color',[.5 0 .5])
legend('top curve','continuous trigonometric method','20 random points','least square method','discrete trigonometric method');

