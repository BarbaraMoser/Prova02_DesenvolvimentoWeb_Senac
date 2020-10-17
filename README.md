# Prova02_DesenvolvimentoWeb_Senac
App desenvolvido segundo o que foi solicitado no enunciado da prova.

Descrição das questões:
Em uma universidade foi solicitado o desenvolvimento de um aplicativo web para controlar o financiamento de projetos. Cada projeto está descrito como se segue:
•	nome;
•	área (tecnológica, humanas, médica);
•	prazo (em dias);
•	orçamento (de R$ 5.000,00 a R$ 100.000,00)
Desenvolva um aplicativo web:
1.	Página principal com dois menus: “Dashboard” e “Projetos”
2.	No menu “Projetos”, adicionar um formulário para inserir projeto
3.	No menu “Dashboard”, mostrar um painel com as seguintes informações dos projetos:
1.	A porcentagem do orçamento total destinada a cada área
2.	Os 5 projetos mais caros ordenados pelo valor do orçamento 
3.	Orçamento total  

Para inserir um projeto utilizar a api localizada em https://projeto-prova.herokuapp.com/projeto. Enviar um POST para https://projeto-prova.herokuapp.com/projeto com o conteúdo: 

{
    "nome": "projeto xpto",
    "area": "MEDICA",
    "prazo": 50,
    "orcamento": 16000.00
}

Para ler os dados projeto: GET: https://projeto-prova.herokuapp.com/projeto 

