# TryHackMe - Vulnversity

**Dificuldade:** Fácil

## Sobre essa room

Essa foi a primeira room de CTF que eu completei do início ao fim. 
O objetivo era invadir uma máquina Linux, desde o reconhecimento 
inicial até conseguir acesso total como root.

## O que eu fiz

**Primeiro passo, reconhecimento:**
Usei o Nmap pra ver o que estava rodando na máquina. Apareceram vários 
serviços abertos: FTP, SSH, um proxy e um servidor web numa porta 
diferente do normal.

**Achando caminhos escondidos:**
Com o Gobuster, fui atrás de diretórios que não apareciam no site 
normalmente. Achei uma pasta com um formulário de upload de arquivo.

**Testando o que passava pelo filtro:**
Usei o Burp Suite pra descobrir quais extensões de arquivo o site 
aceitava. Testei .php, .php3, .php4, .php5 e .phtml, e descobri que 
só o .phtml passava sem ser bloqueado.

**Conseguindo acesso:**
Montei um shell reverso em PHP com esse formato de arquivo, deixei 
meu terminal esperando conexão (netcat) e fiz o upload. Assim que 
acessei o arquivo pelo navegador, o shell se conectou de volta e eu 
ganhei acesso ao terminal da máquina.

**Virando root:**
Já dentro da máquina, procurei por arquivos com permissão SUID mal 
configurada. Achei um binário do sistema que dava esse acesso e usei 
ele pra virar root.

## O que eu aprendi

Foi bem mais difícil do que eu esperava, principalmente entender como 
uma ferramenta se conecta com a próxima (Nmap → Gobuster → Burp Suite 
→ shell reverso). Também foi minha primeira vez mexendo de verdade com 
permissão SUID no Linux, e ver na prática como isso pode ser explorado 
foi um baita aprendizado.

Próximo passo: continuar praticando e começar a explorar o lado Blue 
Team, que é onde eu quero atuar.
