# Linear-systems-codes
Repositório feito com intenção de salvar códigos feitos durante a disciplina de sistema linear


%antonio assis de sousa neto - 390173

%1-) Gere um sinal que é a soma de três funções seno com frequências angulares discretas
%iguais a 0,2T, 0,5π е 0,8¹; e amplitudes iguais a 1, 1,5 e 0,5, ou seja:
%x[n] = sen(0,2.TT.n) + 1,5.sen(0,5.T.n) + 0,5.sen(0,8.TT.n).
%Este sinal deve possuir N=200 pontos. Gere o gráfico deste sinal [sin,figure, plot ou stem].

figure
N = 0:1:200

x = sin(0.2 * pi * N) + (1.5*(sin(0.5*pi*N))) + (0.5*sin(0.8*pi*N))

plot(N, x)
ylabel('Amplitude')
title('Gráfico do sinal')
grid on

![Descrição da imagem](./start_signal.png)

figure
indices_vector = -40:40;  % Vetor de índices

inpulse_signal = zeros(size(n));  % Inicialização da resposta ao impulso

% Toda essa operação pode ser demonstrada tambgém usando-se de um for
valid_indices = (indices_vector >= 0 & indices_vector<=30); % Definir que os valores maiores que 0 e menores que 30 sao valores valido;
inpulse_signal(valid_indices & (indices_vector ~= 15)) = sin(0.3*pi*(indices_vector(valid_indices & (indices_vector ~= 15))-15))./(pi*(indices_vector(valid_indices & (indices_vector ~= 15))-15)); % Atribuição da resposta ao impulso para n diferente de 15 e que são indices válidos
inpulse_signal(indices_vector == 15) = 0.3; % Atribuição da resposta ao impulso para n igual a 15


stem(indices_vector, inpulse_signal, 'filled')  % Plot da resposta ao impulso
xlabel('indices_vector')
ylabel('Amplitude')
title('Resposta ao Impulso')
grid on


% 3-) Filtre o sinal de questão 1 usando a resposta ao impulso gerada na questão 2. Gere o
% gráfico deste sinal filtrado [conv,figure,plot].

figure
conv_result = conv(x, inpulse_signal, 'same')

plot(conv_result)
xlabel('conv_result')
ylabel('Amplitude')
title('Resultado da convolução')
grid on
%4-) O que é observado na questão 3?

% Pode ser observado que mesmo que o sinal de entrada e o sinal inpulso
%tenham sinais não periódicos e com amplitudes diferetentes a convolução
%ou filtrageme entre os dois sinais gerou um sinal periódico que varia 
%sua amplitude entre -1 e 1, com isso dá para perceber que o filtro
%aplicado está afetando de forma a limitar a amplitude do sinal
