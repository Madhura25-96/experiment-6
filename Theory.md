# Theory 
In all the previous experiments, we dealth with codes over binary alphabet. Codes can also be constructed over fields of size greater than $2$. In this experiment, we shall focus on finite fields in general. We will describe prime fields, construction of fields of size which is a power of prime, primitive element of a field, minimal polynomials and sub-fields of a finite field.

The theory associated with Experiment-6 is divided into six parts:

(1) Prime Fields  <br />
(2) Ring of polynomials and Extended Euclidean algorithm  <br />
(3) Construction of finite fields of prime power  <br />
(4) Primitive Element of a field  <br />
(5) Minimal Polynomials  <br />
(6) Sub-fields of a field  <br />

## 1 &nbsp; &nbsp;Prime Fields
Consider a set $\mathbb{F}_p = \{0, 1, \ldots, p-1 \}$, where $p$ is prime. The addition and multiplication operations for any $a, b \in \mathbb{F}_p$ are defined as $a +_p b = a+b \mod p$ and $a ._p b = a.b \mod p$. For simplicity of notation, we will use $+$ instead of $+_p$ and $.$ instead of $._p$ subsequently in the theory.

We would like to argue that $(\mathbb{F}_p, +, .)$ is a field. In Experiment-1, field definition is given. It is easy to verify that the following field properties of $(\mathbb{F}_p, +, .)$ 
    - Closure under addition, multiplication
    - Commutativity under addition, multiplication
    - Distributivity with respect to addition and multiplication
    - Additive identity is $0$ and multiplicative identity is $1$
    - Additive inverse of $a$ is $p-a$.
The only property which requires to be verified carefully is the existence of multiplicative inverse for every non-zero element in the field. In order to prove that, we need to invoke the fact that $p$ is prime. Consider $a \neq 1 \in \mathbb{F}_p$. $a$ is co-prime with $p$ as $p$ is a prime number. Hence, $gcd(a,p)=1$. Thus, it turns out, there are two integers $x,y$ such that $ax + py = 1$. Doing $\mod p$ operation on the above relation, we have that $a.(x \mod p) = 1 \mod p$. Thus, $x \mod p$ is the required multiplicative inverse of $a$ in the field $\mathbb{F}_p$.

\begin{example}
Consider the case of $p=7$.
\end{example}

## 2 &nbsp;&nbsp;Ring of Polynomials and Extended Euclidean Division Algorithm
Consider the set of all polynomials with coefficients from $\mathbb{F}_p$, denoted by $\mathbb{F}_p[x]$ where $x$ is an indeterminate. Addition and multiplication are defined as ordinary addition and multiplication with the difference being the coefficient operations are carried out $\mod p$. 

For example, consider the ring of polynomials $\mathbb{F}_7[x]$. Let $a(x) = 1 + 3x + 4x^2 + 6x^5 $ and $b(x) = 

We will now describe the encoding of Hamming code through a diagram of 3 circles as shown in Fig. \ref{fig:hamming}.

%\begin{figure}
%  \centering
%  \fbox{
%  \includegraphics[width=3in]{Hamming_code.png}
%  }
 % \caption{[7,4,3] Hamming code represented using three circles.}
%  \label{fig:hamming}
%\end{figure}

Hamming code is a code over binary field $\mathbb{F}_2$ of length 7, dimension 4 and minimum distance 3. The encoding procedure of the Hamming code is given by the following equations:

\begin{eqnarray*}
p_5 & = & m_1 + m_2 + m_4 \mod 2, \\
p_6 & = & m_1 + m_3 + m_4 \mod 2, \\
p_7 & = & m_2 + m_3 + m_4 \mod 2.
\end{eqnarray*}
Please note that in the above equations, the addition is modulo-2 addition over the binary field. Based on the above equations, the generator matrix of the Hamming code is given by
\begin{equation*}
G = \begin{bmatrix} 1 & 0 & 0 & 0 & 1 & 1 & 0 \\
0 & 1 & 0 & 0 & 1 & 0 & 1 \\
0 & 0 & 1 & 0 & 0 & 1 & 1 \\
0 & 0 & 0 & 1 & 1 & 1 & 1\end{bmatrix}.
\end{equation*}

The parity-check matrix of the Hamming code can be obtained by rewriting the equations as follows:

\begin{eqnarray*}
p_5 + m_1 + m_2 + m_4 & = & 0 \\
p_6 + m_1 + m_3 + m_4 & = & 0, \\
p_7 + m_2 + m_3 + m_4 & = & 0.
\end{eqnarray*}
The parity-check matrix itself is given by

\begin{equation*}
H = \begin{bmatrix} 1 & 1 & 0 & 1 & 1 & 0 & 0 \\
1 & 0 & 1 & 1 & 0 & 1 & 0 \\
0 & 1 & 1 & 1 & 0 & 0 & 1 \end{bmatrix}.
\end{equation*}

The minimum distance of a Hamming code is 3. This can be seen in one of the following two ways:

- Enumerate all possible codewords of the Hamming code and find the minimum Hamming weight of any codeword. 
- In a second method, the minimum distance of a linear code can be obtained by determining the smallest number $s$ such that any $s$ columns of the parity check matrix are linearly independent. The minimum distance of a code in this case is $s+1$. It can be seen from the parity check matrix of the Hamming code that the smallest number $s$ such that any $s$ columns of the parity check matrix are linearly independent is $2$ and hence the minimum distance of the Hamming code is $3$.

## 3 &nbsp;&nbsp;Error Correction
Let the received binary vector be denoted by $[y_1, y_2, y_3, y_4, y_5, y_6, y_7]$. We will give a decoding rule by which we can correct one error.
Calculate the following quantities
\begin{eqnarray*}
s_1 & = & y_1 + y_2 + y_4 + y_5 \\
s_2 & = & y_1 + y_3 + y_4 + y_6 \\
s_3 & = & y_2 + y_3 + y_4 + y_7
\end{eqnarray*}
If $s_1$ is $0$, then it means that the parity equation $p_5 = m_1 + m_2 + m_4$ is said to match and if $s_1$ is $1$, then the parity equation is said to not match.
Similar is the case with $s_2$ and $s_3$.
<br />
-**Case 1: One parity equation does not match:** If $s_1$ is $1$, then $p_5$ is received erroneously. If $s_2$ is $1$, then $p_6$ is received erroneously. If $s_3$ is $1$, then $p_7$ is received erroneously.
<br />
-**Case 2: Two parity equations do not match:** If $s_1 = s_2 = 1$, then $m_1$ is received erroneously. If $s_1 = s_3 = 1$, then $m_2$ is received erroneously. If $s_2 = s_3 = 1$, then $m_3$ is received erroneously.
<br />
-**Case 3: Three parity equations do not match:** If $s_1 = s_2 = s_3 = 1$, then $m_4$ is received erroneously.


