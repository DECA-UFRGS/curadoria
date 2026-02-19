# Exemplos de contribuições para código aberto – Henrique Becker

Nesse documento eu (Henrique Becker) listo algumas das contribuições que fiz a projetos de código aberto. O objetivo é oferecer exemplos realistas de como essas contribuições ocorrem.

## Exemplos de documentação ou padrão LaTex (simples)

Inicialmente, é interessante apontar que contribuições podem ser bastante simples e surgir de forma natural. Por exemplo, podem partir de discussões em fóruns de programação sobre a situação da documentação de um projeto em linguagem, ou tratar de um pequeno problema no modelo LaTex que você precisa usar em um trabalho.

### Contribuições a documentação da linguagem Julia

Um professor no fórum da linguagem Julia reclamou que era confuso para ele e seus alunos que não era mencionado na documentação da linguagem Julia `&&` e `||` eram o mesmo que o `and` e o `or` do Python (linguagem que ele e os seus alunos tinham mais familiaridade). https://discourse.julialang.org/t/and-or-bitwise-or-shortcircuit-what-we-get-searching-docs/46263
Eu concordei com ele na mensagem do fórum ( https://discourse.julialang.org/t/and-or-bitwise-or-shortcircuit-what-we-get-searching-docs/46263/8 ) e criei um simples PR ( https://github.com/JuliaLang/julia/pull/37463 ) referenciando a discussão. Esse PR literalmente só adicionava a o texto "Some languages (like Python) refer to them as `and` (`&&`) and `or` (`||`)." na documentação.

Um dos criadores da linguagem comentou na mesma discussão do fórum que poderíamos colocar menções a `and` e `or` direto na documentação dos operadores acessível pelo comando `?` do terminal do Julia ( https://discourse.julialang.org/t/and-or-bitwise-or-shortcircuit-what-we-get-searching-docs/46263/25 ) e depois criou dois issues para isso ( https://discourse.julialang.org/t/and-or-bitwise-or-shortcircuit-what-we-get-searching-docs/46263/28 ). Para mostrar um pouco o lado de que nem sempre as coisas são tão simples, em um dos issues é feita uma longa discussão com mensagens de vários parágrafos se essa adição na documentação deveria ser feita ou não: https://github.com/JuliaLang/julia/issues/37469 .

Outra pequena contribuição a documentação da linguagem Julia pode ser vista aqui: https://github.com/JuliaLang/julia/pull/38097 

### Reorganizar padrão LaTex para teses do PPGC

O padrão LaTex para escrever a tese de doutorado pelo PPGC não concordava com o padrão da biblioteca, exemplificado em um documento docx. A solução foi simplesmente puxar dois comandos para cima no mesmo arquivo: https://github.com/schnorr/infufrgs/pull/60/commits/2c750eaf5bd885ecfb755441ae282d6a03d9e3e2 .
Confusões sobre l-values, r-values, e e non-l-values
Um usuário da linguagem Julia estava com uma dúvida sobre um detalhe técnico da documentação ( https://discourse.julialang.org/t/class-of-variables/83892 ). Eu aponto como é fácil editar documentação por meio da interface web do Github ( https://discourse.julialang.org/t/class-of-variables/83892/4 ) e abro um PR que só modifica documentação.

### Uma pequena contribuição de código (parse de Racionais em Julia)

Enquanto usando a linguagem Julia eu precisei ler um array de Racionais (números fracionários no formato 1//2, i.e., sem perda de precisão pelas casas após a vírgula) e descobri que o método não funcionava porque a linguagem não implementava o overload da função `parse` para `parse(Rational{Int}, string_com_racional)`. Após procurar se já havia um issue aberto sobre isso encontrei: https://github.com/JuliaLang/julia/issues/18328 . Lá comentei sobre o fato que o issue nunca tinha resultado em código: https://github.com/JuliaLang/julia/issues/18328#issuecomment-1063512734 e perguntei para o usuário que havia criado o issue original se ele ia terminar ou eu podia assumir o issue https://github.com/JuliaLang/julia/issues/18328#issuecomment-1063520663 , como ele disse que não podia no momento eu criei https://github.com/JuliaLang/julia/pull/44550 .

Eu acho que vale a pena a leitura completa do issue. Pois ele começa como uma contribuição de 6 linhas ( https://github.com/JuliaLang/julia/pull/44550/commits/5b1c044b5999170aefb3203d1b29aa68632b2d32 ) só com o código básico para ler dois números separados por “//” e montar um Racional, e depois cresce para 14 linhas de implementação e mais 82 linhas de teste ( https://github.com/JuliaLang/julia/pull/44550/files ) após várias discussões acerca como essa funcionalidade simples mas essencial deveria funcionar.

## Um exemplo mais complexo

Uma contribuição de considerável impacto, mas muito mais específica e trabalhosa, trata de lidar de forma mais eficiente com a deleção de variáveis em formulações matemáticas da biblioteca JuMP. Apesar disso, ainda são somente cerca de 50 à 70 linhas de códigos em 5 repositórios (descontando alguns comentários e testes que inflam a quantidade). A biblioteca JuMP cria uma interface comum e de fácil utilização entre vários resolvedores de formulações matemáticas, como o JuMP e o Gurobi. O problema é que esses resolvedores permitem remover múltiplas variáveis de uma única vez, de uma forma eficiente, enquanto a interface do JuMP só permitia remover uma variável por vez, de uma forma muito mais ineficiente (depois de cada deleção individual a biblioteca precisava fazer um shift em um array de potencialmente milhões de elementos). O speedup para um dos resolvedores foi algo entre 20~1000x dependendo de quantas variáveis eram deletadas, de qual era o número total de variáveis, e o padrão de deleção: https://github.com/jump-dev/CPLEX.jl/pull/273#issuecomment-572252616 .

Como era necessário fazer essa modificação para cada um de dois resolvedores (CPLEX e Gurobi), mais alterar uma camada intermediária de compatibilidade (MOI), a interface de alto nível (JuMP), e adicionar testes, a contribuição ficou espalhada e complexa de coordenar. O post inicial desse issue https://github.com/jump-dev/JuMP.jl/pull/2135 faz link para todos os issues dos outros repositórios.

