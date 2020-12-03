# O que é o Ansible?

https://blog.fabricads.com.br/automacao-com-ansible/

O Ansible é uma ferramenta de automação de TI que automatiza o provisionamento em nuvem, o gerenciamento de configurações, a implantação de aplicativos, a orquestração intra-serviço e muitas outras necessidades de TI. É semelhante ao Puppet e Chef, porém com muito mais recursos, mais simples e amplamente utilizada por profissionais de DevOps.

Projetado para implantações de várias camadas desde o primeiro momento, o Ansible modela sua infraestrutura de TI, descrevendo como todos os seus sistemas se inter-relacionam, em vez de apenas gerenciar um sistema por vez. **Um dos seus grandes diferenciais é o fato de utilizar agentes e nenhuma infraestrutura de segurança personalizada adicional**, por isso é fácil de implantar – e o mais importante, usa uma linguagem muito simples (YAML, na forma de Ansible Playbooks).

 

## Arquitetura eficiente

O Ansible funciona conectando-se aos seus nós e executando programas pequenos, chamados “Módulos Ansible”. Esses programas foram criados para serem modelos de recursos do estado desejado do sistema. O Ansible executa esses módulos (por SSH por padrão) e os remove quando finalizados.

Sua biblioteca de módulos pode residir em qualquer máquina e não há servidores, daemons ou bancos de dados necessários. Normalmente, você trabalha com seu programa de terminal favorito, um editor de texto e provavelmente um sistema de controle de versão para acompanhar as alterações no seu conteúdo.


## Mão à obra

https://churrops.io/2018/02/04/primeiros-passos-com-ansible-configurando-e-gerenciando-nginx/

Ansible é uma ferramenta de automação de TI, usada principalmente pela equipe de Infraestrutura para automatizar e garantir o estado desejado do seu ambiente.

Como funciona o Ansible?
Pense que tu tens um servidor com o Ansible instalado, tu cria uma Playbook informando no arquivo o que tu deseja que o Ansible faça e ele automaticamente se conecta nos servidores do seu cluster e executa o que foi solicitado. Ele trabalha em um modelo de idempotência, tu apenas descreve o estado do seu sistema ou serviço e não o que fazer para chegar até aquele estado, não importa em qual estado o serviço esteja o Ansible sabe como fazer as mudanças até chegar no estado desejado, isso é ótimo pois permite configurações confiáveis e seguras.

O Ansible se conecta nos servidores utilizando o protocolo SSH (ele depende disso para funcionar), por isso é preciso ter credenciais e/ou chaves de acesso para chegar em outros servidores, por este motivo é obrigatório estar rodando o serviço SSH. Ele não precisa de agents rodando nos servidores basta a configuração de SSH estar funcionando entre os servidores do seu cluster.


Características do Ansible:

- Escrito em Python.
- Não precisa de agents instalados nos nodes.
- Arquitetura Master to Nodes.
- Utiliza uma linguagem de configuração em formato YAML (chave-valor).
- Grande quantidade de módulos e códigos no Github. Pelo comando ansible-galaxy é possível - baixar e reutilizar playbooks escritos por outros usuários.
- Simples de realizar manutenção

## Instalação no Ubuntu

https://churrops.io/2018/02/04/primeiros-passos-com-ansible-configurando-e-gerenciando-nginx/



# Exemplo de uso do Ansible - instalando o NVM no Linux

```
You can use a task:

- name: nvm
  shell: >
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
  args:
    creates: "{{ ansible_env.HOME }}/.nvm/nvm.sh"
```