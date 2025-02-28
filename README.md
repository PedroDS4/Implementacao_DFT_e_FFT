# Implementacao_DFT_e_FFT
Este Projeto implementa a transformada discreta de fourier(DFT) computacionalmente, e também implementa a FFT a partir do algorítmo de decimação par e impar.

#**Transformada de Fourier Discreta**
A transformada de fourier discreta é basicamente a discretização da transformada de fourier contínua, para que seja possível implementar num computador, que é digital, a integral de fourier se torna um somatório e no espectro o sinal espectral original é amostrado com frequência de amostragem $Ω_0$.

A transformada de fourier de um sinal é dada pela equação:

$$
X(\Omega) = ∫_{-∞}^{∞} x(t)e^{-j{\Omega}t}dt
$$

Essa integral pode ser discretizada, sabendo que o sinal $x[n]$ é o sinal x(t) aplicado em alguns instantes de tempo periódicos multiplos do período de amostragem $T_s$, então

$$
X(k{\Omega}_0) = ∑_{0}^{N_0-1} x(nT_s) \cdot e^{-jk{\Omega}_0t} \cdot T_s
$$

se agora definirmos $x[n] = T_s x(nT_s) $, a equação fica

$$
X(k{\Omega}_0) = ∑_{0}^{N_0-1} x[n] \cdot e^{-jk{\Omega}_0t}
$$



##**Demonstração formal da transformada de fourier discreta**
Seja um sinal x(t), a sua transformada de fourier de tempo contínuo é dada por

$$
X(\Omega) = ∫_{-∞}^{∞} x(t)e^{-j{\Omega}t}dt
$$

Considere ainda o sinal amostrado obtido a partir da amostragem do sinal $x(t)$

$$
\bar{x}(t) = \sum_{n = -∞}^{∞} x(nT_s) \delta (t - nT_s)
$$


Porém se calcularmos a transformada de fourier do sinal amostrado $\bar{x}(t)$, obtemos

$$
\bar{X}(\Omega) = ∫_{-∞}^{∞}   \sum_{n = -∞}^{∞} x(nT_s) \delta (t - nT_s) e^{-j{\Omega}t}dt
$$

Podemos ainda inverter a ordem do somatório com a integral

$$
\bar{X}(\Omega) = \sum_{n = -∞}^{∞}  ∫_{-∞}^{∞}  x(nT_s) \delta (t - nT_s) e^{-j{\Omega}t}dt
$$

e podemos ainda ver que o termo $x(nT_s)$ é uma constante em relação a t, então temos

$$
\bar{X}(\Omega) = \sum_{n = -∞}^{∞} x(nT_s)   ∫_{-∞}^{∞} \delta (t - nT_s) e^{-j{\Omega}t}dt
$$

agora utilizando a noção de integrais com impulso, vemos que o resultado dessa integral é o valor do da função exponencial no deslocamento do impulso, assim por fim temos

$$
\bar{X}(\Omega) = \sum_{n = -∞}^{∞} x(nT_s)  e^{-j\Omega nT_s}
$$

porém temos ainda que

$$
X(\Omega) = T_s \bar{X}(\Omega)
$$

assim a transformada de fourier do sinal fica

$$
X(\Omega) = \sum_{n = -∞}^{∞} T_s x(nT_s)  e^{-j\Omega nT_s}
$$

definindo $T_s x(nT_s) = x[n]$

temos enfim

$$
X(\Omega) = \sum_{n = -∞}^{∞} x[n]  e^{-j\Omega nT_s}
$$

agora discretizando a frequência como

$$
\Omega = k\Omega_0 = 2 k \pi f_0
$$

temos

$$
X(k \Omega_0) = \sum_{n = -∞}^{∞} x[n]  e^{-jk \Omega_0 nT_s}
$$

e por fim assumindo que

$$
f_0 \cdot T_s = \frac{T_s}{T_0} = \frac{1}{M}
$$

onde $M$ é o número de amostras espaçadas em $T_s$ no período $T_0$

chegamos na equação final da DFT, onde tempo e frequência estão discretizados, assim

$$
X(k \Omega_0) = \sum_{n = -∞}^{∞} x[n]  e^{-j 2\pi \frac{k}{M} n}
$$

**Complexidade da DFT**
A complexidade equivale ao número de iterações necessárias para realizar o algoritmo completamente
Para computarmos a DFT, temos que


##**Transformada rápida de fourier(FFT)**
A transformada rápida de fourier é um algorítmo que reduz a complexidade do cálculo da DFT, utilizando uma estrutura de implementação recursiva onde o sinal é decomposto em sub sinais a partir dos indices pares e impares, até esses sinais se tornarem uma única amostra, e a partir daí essa função recursiva calcula todas as amostras da FFT.

Seja um sinal discreto $x[n]$, a sua transformada de fourier pode ser calculada pela DFT como

$$
X[k] =  \sum_{n = -∞}^{∞} x[n]  e^{-j 2\pi \frac{k}{M} n}
$$

porém o sinal $x[n]$ pode ser decomposto da forma

$$
x_{odd}[n] = x[2n+1]
$$
que forma um novo sinal a partir das amostras ímpares do sinal $x[n]$ original.

$$
x_{even}[n] = x[2n]  
$$
que forma um novo sinal a partir das amostras pares do sinal $x[n]$ original, e podedemos calcular agora a DFT como

$$
X[k] =  \sum_{n = -∞}^{∞} x_{odd}[n]   e^{-j 2\pi \frac{k}{M} n}  + \sum_{n = -∞}^{∞} x_{even}[n]  e^{-j 2\pi \frac{k}{M} n}
$$

fazendo essa decomposição M vezes, recursivamente, até que

$$
x_{{odd}^M}[n] = y_0
$$

e

$$
x_{{even}^M}[n] = z_0
$$

onde $z_0$ e $y_0$ são números complexos, esse é o resultado final da função recursiva que implementa a FFT, cuja complexidade será demonstrada a seguir.


**Complexidade da FFT**


