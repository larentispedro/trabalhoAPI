# README - Parte 1: Assembly MIPS

## 1. Simulador Utilizado

O código `adivinhe_numero.asm` foi desenvolvido e testado utilizando o simulador **MARS (MIPS Assembler and Runtime Simulator)**, versão 4.5.

O MARS foi usado para montar e executar o código MIPS32, utilizando sua interface de console para as operações de entrada (leitura da semente e palpites) e saída (exibição das mensagens).

## 2. Papel dos Registradores

Para implementar a lógica do jogo, utilizamos os seguintes registradores principais:

| Registrador | Propósito no Jogo |
| :--- | :--- |
| `$v0` | **Código da Syscall:** Define qual operação do sistema será executada (Ex: 4 para `print_string`, 5 para `read_int`, 1 para `print_int`, 10 para `exit`). |
| `$a0` | **Argumento da Syscall:** Passa o argumento para a syscall (Ex: o endereço de uma string (`.data`) a ser impressa, ou o valor de um inteiro a ser exibido). |
| `$s0` | **Número Secreto (Target):** Registrador "salvo" que armazena o valor-alvo (`(seed % 100) + 1`) durante toda a execução do jogo. |
| `$s1` | **Contador de Tentativas:** Registrador "salvo" inicializado em 0 e incrementado (`addi`) a cada palpite válido. |
| `$t0` | **Armazenamento Temporário (Seed/Palpite):** Usado inicialmente para guardar a `semente` lida. Dentro do loop, é reutilizado para guardar o `palpite` atual do usuário. |
| `$t1` | **Constante '100' / Resultado `slt`:** Usado para carregar a constante 100 (para a operação `rem`) e, depois, reutilizado para guardar o resultado (0 ou 1) das comparações `slt`. |
| `$t2` | **Resultado do Módulo:** Usado para guardar o resultado temporário da operação `rem` (semente % 100). |
| `$zero` | **Constante '0':** Usado na comparação `beq $t0, $zero, sair_jogo` para verificar se o palpite foi 0. |