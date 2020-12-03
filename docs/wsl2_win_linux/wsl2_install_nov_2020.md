
# WSL2 - Windows Subsystem for Linux 2

Referência: https://github.com/marcelopalin/wsl2-docker-quickstart

Desde maio/2019 nós temos um novo cenário para desenvolver aplicações no Windows.
Antes o desenvolvimento Web era motivo de reclamação geral. Parte do mundo de
desenvolvimento de software foi criado para Linux.

Quais os problemas de desenvolver no Windows:

Muitas ferramentas e linguagens de programação:
- só funcionam no Linux
- ou funcionam melhor no Linux

Configurações e instalações de ferramentas de programação eram muito complicadas.

Quam nunca precisou instalar o Wamp ou Xamp para ter o PHP na sua máquina.
Trazia Apache, Filezilla e uma série de coisas que você não queria.

O terminal do Windows DOS ou POWERSHELL deixam muito a desejar perto dos terminais
Linux.. Não tem Abas nem personalização..

Com o nascimento do Docker este cenário melhorou bastante,
pois podemos montar nosso ambiente de desenvolvimento
baseado em Unix, de forma independente e rápida,
e ainda unificada com outros sistemas operacionais.

O que é Docker:

Docker é uma plataforma open source que possibilita o empacotamento
de uma aplicação dentro de um container. Uma aplicação consegue se
adequar e rodar em qualquer máquina que tenha essa tecnologia instalada.

Para se utilizar Docker no Windows temos três versões:

Docker Toolbox.
Docker Desktop com Hyper-V.
Docker Desktop com WSL2.
Docker Toolbox
Roda em cima do programa de virtualização de sistemas da Oracle, chamado de VirtualBox. O desempenho do Docker Toolbox para muitas aplicações/ferramentas pode ser muito ruim, inviabilizando seu uso.

Docker Desktop com Hyper-V
Roda em cima do Hyper-V da Microsoft em vez de usar o
VirtualBox usando pelo Docker Toolbox. O Docker Desktop com
Hyper-V necessita da versão PROFESSIONAL do Windows 10, portanto é
necessário compra-la se você não a tem.
O Hyper-V costuma requerer muitos recursos da máquina e
apesar do desempenho ser melhor que o Docker Toolbox, a máquina
pode ficar lenta para se utilizar outras coisas no Windows.
A Docker já anunciou que vai remover o suporte ao Hyper-V futuramente.

Finalmente surgiu o Docker Desktop com WSL2
Roda em cima do

Virtual Machine Platform em vez de usar o VirtualBox ou Hyper-V.
Se integra com o WSL2 permitindo rodar o Docker dentro do ambiente do Linux.
Não é necessário adquirir licença PRO do Windows 10,
tem um grande desempenho e consome menos recursos quando
comparado ao Docker Toolbox ou Docker Desktop com Hyper-V.

Temos a grande vantagem de se trabalhar totalmente dentro do Linux para desenvolvimento, portanto, usar WSL2 + Docker é a melhor maneira de se desenvolver aplicações no Windows.


Antes nós usávamos máquinas virtuais

Foi lançado o WSL2 e ele muda o panorama de desenvolvimento no windows.

Seguindo as instruções de https://github.com/marcelopalin/wsl2-docker-quickstart

- Já atualizado o windows
- Já instalado o Kernel do WSL2
- wsl --set-default-version 2

 wsl --set-default-version 2
Para obter informações sobre as principais diferenças em relação ao WSL 2, visite https://aka.ms/wsl2
PS C:\Users\marce> wsl -l -v
  NAME                   STATE           VERSION
* docker-desktop-data    Running         2
  docker-desktop         Running         2
PS C:\Users\marce>

Veja que ainda não tenho o Ubuntu instalado e rodando.

Se acessarmos no Explorer a rede \\wsl$ você verá neste momento as pastas do docker.

- Dica:

Para abrir o Explorer do windows de dentro do linux wsl faça:

explorer.exe .

HABILITANDO Docker

Abra o Docker Desktop e vá em Settings Resources WSL Integration e Habilite o WSL e a
distribuição (no nosso caso é o Ubuntu)

- ATENÇÃO: não crie os seus projetos dentro do /mnt/c$ (fica lento 5x)

Crie os projetos dentro do seu usuário: /home/mpi
