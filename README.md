% Questao 6.11 da 7ªed do livro do Fitzgerald
clear all;
R1 = 0.07;
R2 = 0.152;
X1 = 0.743i;
X2 = 0.764i;
XM = 40.1i;
q=3; % quantidade de fases
V1 = 460/sqrt(3);
fe = 60; %frequencia da rede eletrica
polos = 4;
Pnucleo=325;
Rc=651;% Rc = (3*V1^2)/Pnucleo;

%s = 0.01;disp("Para s=1%") 
%s = 0.02;disp("Para s=2%")
s = 0.03;disp("Para s=3%")
%______________________Calcule a velocidade
ns= (120*fe)/polos; % velocidade sincrona
n = (1-s)*ns;% velocidade do eixo
%_____________________Corrente de terminal
Zin=1/(1/(1/(1/((R2/s)+X2)+1/(XM)) + (R1+X1))+1/XM);
I1 = V1/ ( 1/(1/((R2/s)+X2)+1/(XM)) + (R1+X1)); %% 
Sin3F=V1*conj(I1);
FP = cos(angle(Sin3F));
FP2=rad2deg(angle(I1));
i23=abs(I1);
i24=real(I1);
%_____________________ achando Peixo_________________________
Pin3F = V1*real(I1)*3;
%Pin3F = real(V1*I1)*3;
FP2=abs(Pin3F)/(3*V1*abs(I1));

Patr = 390; %perdas de atrito e ventilação
Pestator3F=q*real(I1)^2*R1;
Pgap= Pin3F-Pestator3F ; %potencia no entreferro
Protor3F = s.*Pgap;
Pmec=(1-s)*Pgap;%potencia eletromagnetica desenvolvida pelo motor
Peixo =( Pmec-Patr);
% outro modo de fazer Peixo achando I2
I2= I1*(XM/(XM+X2+R2/s));
Peixo2=q*real(I2)^2*R2*((1-s)/s)-Patr;
%_____________________ rendimento
Rendimento = Peixo/(Pin3F+Pnucleo);
%______________________conjugado
Wm=(1-s)*((4*pi*fe)/polos);
Teixo=Peixo/Wm;
%___impressao dos valores na janela de comando
fprintf('Velocidade = %f(RPM)\n',n)
fprintf('Conjugado = %f(N.m)\n',Teixo)
fprintf('Potencia de saida= %f(W)\n',Peixo)
fprintf('Potencia de entrada= %f(W)\n',Pin3F)
fprintf('Fator de Potencia= %f\n',FP)
fprintf('Rendimento= %f\n',Rendimento*100)
