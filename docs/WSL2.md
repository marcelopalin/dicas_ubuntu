# WSL2

https://pbpython.com/wsl-python.html

https://dev.to/hymanzhan/setting-up-wsl-2-for-web-development-3202

https://docs.microsoft.com/pt-br/windows/wsl/about

# Acessando o servidor WSL2

https://docs.microsoft.com/pt-br/windows/wsl/wsl-config#configure-per-distro-launch-settings-with-wslconf

Eu criei o arquivo **wsl.conf** dentro do diretório /etc do linux wsl2:

```ini
# Enable extra metadata options by default
[automount]
enabled = true
root = /windir/
options = "metadata,umask=22,fmask=11"
mountFsTab = false

# Enable DNS – even though these are turned on by default, we'll specify here just to be explicit.
[network]
generateHosts = true
generateResolvConf = true
```

Leia em https://docs.microsoft.com/pt-br/windows/wsl/wsl-config#configure-per-distro-launch-settings-with-wslconf
o que siginifica as seções automount e network

# Definir itens de configuração WSL na inicialização com wsl.conf

Existe um arquivo de configuração no WSL em /etc/wsl.conf. Este arquivo contém definições de configuração que são executadas sempre que a distribuição WSL é iniciada. Quando o arquivo wsl.conf existe , WSL irá ingerir qualquer configuração neste arquivo sempre que a distribuição Linux for iniciada.

Existem algumas seções diferentes dentro do arquivo wsl.conf que você pode configurar.

Automount - Montagem de drives do Windows no início
Rede - Gere resolv.conf ou o arquivo hosts
Interop - Ativando ou desativando a interoperabilidade com o Windows
Para obter mais detalhes sobre o arquivo wsl.conf , verifique a página Microsoft Set WSL Launch Settings .


# INSTALANDO PYTHON ON WSL2 

```
sudo apt install python3 python3-pip
```