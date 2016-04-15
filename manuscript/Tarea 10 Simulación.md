## Tiz And Mike

Se realizó la simulación de un programa que calcula
la altura solar, el ángulo de incidencia y el ángulo
acimutal, para cualquier coordenada que se le solicite.

Las simulaciones mostradas son para las coordenadas especifícas
de Ensenada, Baja California.

El código utilizado para las simulaciones fue el siguiente:

```%% Geometría Solar para lugares especificos de México```
```clc
clear all
close all 

Lloc=input('Introducir la longitud de la zona actual\n');                                  % Longitud de la zona en cuestión
lat=input('Introducir la latitud del lugar\n');
dh=input('Introducir el desfase horario\n');                                                         % desfase con el meridiano de Greenwich
as=[];                                                                                                                                      % Para guardar el valor de Altura solar 
tz=[];
d=[];
inci=[];
Hs1=720;                                                                                                                                           % Hora solar en minutos
gamma=20;                                                                                                                                        % Ángulo de superficie azimutal -180-180
beta=40;                                                                                                                                              % Ángulo entre el plano y la superficie en cuestión 0<B<180
omega=0;                                                                                                                                            % Ángulo horario
% Para el dia juliano

for n=1:365
% Llamado de funciones
[delta]=omega_delta_min_as(n);                                                                                               % Declinación de la superficie
[theta_z,alpha_s]=Zenit_aSolar_as(lat,omega,delta);                                                          % Ángulo zenit y altitud solar 
alpha_s= asind(sind(lat)*sind(delta)+cosd(lat)*cosd(delta)*cosd(omega));
[theta]=Angulo_incidencia_as(delta,lat,beta,gamma,omega);
inci=[inci(:);theta(:)];
tz=[tz(:);theta_z(:)];
as=[as(:);alpha_s(:)];
d=[d(:);delta(:)];
end

% Gráfica de figuras
    f1 = figure(1);
    plot (as,'r','Linewidth',1)
    title('Altura solar en Mexico','Interpreter','latex','FontSize',16);
    ylabel('Angulo Altura Solar $\alpha_{s}$','Interpreter','latex','FontSize',16,'FontName','Times New Roman');
    xlabel('Dia Juliano $n$','Interpreter','latex','FontSize',16,'FontName','Times New Roman');
    xlim([1 365])
    h = legend('Ensenada');
    hold on
    grid on
    
    f2 = figure(2);
    plot (tz,'b','Linewidth',1)
    title('Angulo Acimutal','Interpreter','latex','FontSize',16);
    ylabel('Angulo Acimutal $\theta_{z}$','Interpreter','latex','FontSize',16,'FontName','Times New Roman');
    xlabel('Dia Juliano $n$','Interpreter','latex','FontSize',16,'FontName','Times New Roman');
    xlim([1 365])
    h = legend('Ensenada');
    hold on
    grid on
    
    f3 = figure(3);
    plot (inci,'m','Linewidth',1)
    title('Angulo incidencia','Interpreter','latex','FontSize',16);
    ylabel('Angulo incidencia $\theta_{z}$','Interpreter','latex','FontSize',16,'FontName','Times New Roman');
    xlabel('Dia Juliano $n$','Interpreter','latex','FontSize',16,'FontName','Times New Roman');
    xlim([1 365])
    h = legend('Ensenada');
    hold on
    grid on
    
    %%  Impresión de figuras
print -f1 -djpeg
print -f2 -djpeg 
print -f3 -djpeg ```


![figure1](https://cloud.githubusercontent.com/assets/16943736/14572974/d6abaf96-0306-11e6-93c1-593b2b0d544b.jpg)
![figure2](https://cloud.githubusercontent.com/assets/16943736/14572975/d6cfedb6-0306-11e6-9dcd-1d647f711d96.jpg)
![figure3](https://cloud.githubusercontent.com/assets/16943736/14572976/d718bbd6-0306-11e6-8845-8e0977a0482f.jpg)

