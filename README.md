Análise Técnica do Projeto - FP02

📝 Descrição do Projeto

Este projeto consiste num conjunto de ficheiros que demonstram a interação básica entre formulários HTML e scripts de processamento PHP. O objetivo principal é ilustrar a submissão de dados de um formulário (client-side) para um script PHP (server-side) para processamento e apresentação de resultados.

O projeto está dividido em duas funcionalidades principais:

1.
Lista de Itens: Submissão de 5 itens e apresentação numa lista não ordenada.

2.
Cálculo de Média: Submissão de 5 notas e cálculo da média, com atribuição de um conceito de avaliação.

🛠️ Tecnologias Utilizadas

Tecnologia
Propósito
HTML5
Criação dos formulários de entrada de dados.
PHP
Processamento dos dados submetidos (lógica de backend).


📂 Estrutura de Ficheiros

O projeto é composto por quatro ficheiros principais:

Plain Text


/
├── form.html   (Formulário para a Lista de Itens)
├── lista.php   (Processamento PHP da Lista de Itens)
├── nota.html   (Formulário para o Cálculo de Média)
├── nota.php    (Processamento PHP do Cálculo de Média)


💻 Análise Detalhada do Código

1. HTML (Formulários)

Os ficheiros form.html e nota.html são responsáveis pela interface de utilizador e pela recolha de dados.

Características Comuns:

•
Estrutura Básica: Ambos utilizam a estrutura mínima de um documento HTML5.

•
Método de Submissão: Ambos os formulários utilizam o método POST (<form action="..." method="POST">), o que é adequado para o envio de dados que não devem ser visíveis no URL.

•
Associação action: O atributo action aponta corretamente para o script PHP responsável pelo processamento:

•
form.html -> action="lista.php"

•
nota.html -> action="nota.php"



Análise Específica de nota.html:

•
Validação Client-Side: Utiliza os atributos type="number", min="0", e max="20" nos campos de nota. Esta é uma boa prática para fornecer validação básica imediata ao utilizador, embora a validação server-side (em PHP) seja sempre necessária para garantir a segurança e integridade dos dados.

2. PHP (Processamento de Dados)

Os ficheiros lista.php e nota.php contêm a lógica de backend para receber, processar e apresentar os dados.

2.1. lista.php (Processamento de Lista)

Este script demonstra a receção de dados de um formulário e a iteração sobre um array.

Linhas
Código PHP
Descrição
2-6
$itemlista1=$_POST["item1"]; ...
Receção de Dados: Recolhe os 5 valores submetidos através do método POST e armazena-os em variáveis individuais.
7
$info=[$itemlista1, ...];
Estrutura de Dados: Cria um array simples ($info) com os valores recebidos.
8-12
echo "<ul>"; foreach(...) { ... } echo "<ul>";
Apresentação de Dados: Utiliza um loop foreach para iterar sobre o array $info e gerar dinamicamente uma lista não ordenada (<ul><li>...</li></ul>) em HTML.
13-25
$turma = ["Ana" => 16, ...];
Exemplo Adicional: Contém um exemplo de como iterar sobre um array associativo ($turma) e gerar uma tabela HTML.


2.2. nota.php (Cálculo de Média)

Este script demonstra o cálculo matemático e a lógica condicional (if/elseif/else).

Linhas
Código PHP
Descrição
2-6
$ava1=$_POST["nota1"]; ...
Receção de Dados: Recolhe as 5 notas submetidas.
7-9
$a=[$ava1, ...]; $limite = count($a); $media=(array_sum($a)/$limite);
Cálculo de Média: Calcula a média das notas utilizando as funções nativas array_sum() e count() para garantir que o cálculo é feito corretamente, independentemente do número de elementos no array (embora o formulário envie sempre 5).
11-19
if($media<10) { ... } elseif { ... }
Lógica Condicional: Implementa uma estrutura if/elseif/else para classificar a média obtida em categorias textuais ("Reprovado", "Satisfaz", "Bom", "Excelente").
20
echo "A tua média é ".$media, " e a tua situação é ".$notaTexto;
Saída: Apresenta o resultado final ao utilizador.


💡 Sugestões de Melhoria e Refatoração

1. Separação de Responsabilidades (HTML e PHP)

Atualmente, os scripts PHP (lista.php e nota.php) geram o HTML diretamente através de echo.

•
Recomendação: Separar a lógica de processamento (PHP) da apresentação (HTML). O PHP deve apenas processar os dados e armazenar os resultados em variáveis. O HTML deve ser escrito de forma estruturada, utilizando o PHP apenas para "imprimir" as variáveis nos locais apropriados.

Exemplo de Refatoração (de nota.php):

PHP


// Lógica de Processamento (no topo do ficheiro)
// ... (cálculo da média e definição de $notaTexto)
?>
<!DOCTYPE html>
<html>
<head>
    <title>Resultado da Média</title>
</head>
<body>
    <h1>Resultado da Avaliação</h1>
    <p>A sua média é: **<?php echo $media; ?>**</p>
    <p>A sua situação é: **<?php echo $notaTexto; ?>**</p>
</body>
</html>


2. Validação de Dados em PHP

Embora o HTML tenha validação client-side, o PHP deve sempre validar os dados recebidos.

•
Recomendação: Utilizar funções como isset(), empty(), e filter_var() para garantir que os dados existem, não estão vazios e são do tipo esperado (por exemplo, que as notas são números).

3. Utilização de um Único Ficheiro PHP

Para um projeto maior (como o "Total 90"), é comum usar um único script PHP para lidar com a submissão de múltiplos formulários, usando um campo oculto para identificar a ação.

•
Exemplo: Adicionar um campo <input type="hidden" name="action" value="calcular_media"> ao formulário e usar uma estrutura if/elseif no PHP para direcionar a lógica.

4. Utilização de Funções

Para melhorar a organização do código, a lógica de cálculo de média e classificação deve ser encapsulada numa função.

