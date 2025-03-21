# Ansible

Docs: [Ansible Docs](https://docs.ansible.com/ansible/latest/getting_started/index.html)

## Description

É ótimo para automatizar configurações de servidores

Ferramenta para automatização de tarefas escrita em python para configuração, updates, instalações e processos relacionados a gestão de servidores. Esta ferramenta entra via ssh nas máquinas e executa instruções que passamos para ele.

É um utilitário similar ao TerraForm

É baseado em um arquivo de inventário

Tem plugins e estruturas que podemos plugar além de utilizar comandos e sistemas do linux


## Ansible x TerraForm

Geralmente as empresas utilizam o TerraForm para fazer o provisionamento dos servidores e o ansible para executar a configuração desses servidores.

Enquanto TerraForm é muito bom para o provisionamento das máquinas, Ansible é muito bom para o gerenciamento das configurações de cada máquina.

Nas tarefas de Pipeline CI/CD utiliza-se também o Ansible para configurar o ambiente

Exemplo:
Subimos as máquinas EC2 AWS com TerraForm e fazemos as configurações da máquina (Instalar docker, node, NGinx, Configurar FireWall, etc...) com o Ansible


## Processo de instalação

#### Pegadinha...
Toda vez que rodamos o Ansible para executar processos em outras máquinas, o node não pode ser rodado em ambiente windows. Sempre que instalarmos o Ansible, precisaremos estar dentro do ambiente Linux ou no MacOS



## Como trabalhar com Ansible

* Criamos um arquivo chamado `hosts` este é o nosso arquivo de **Inventário**. Nele nós colocaremos os endereços das máquinas 

```Shell
localhost ansible_connection=local # 
```

* Comando para dar um ping de dentro das máquinas

```Shell
ansible -i hosts all -m ping
# -i -> indica o arquivo de inventário
# all -> é para rodar em todas as máquinas
# -m -> módulo que queremos rodar nesse caso rodaremos o ping
```

* Obs: Posso também passar o caminho do meu interpretador python na máquina para não precisar que o Ansible descubra automáticamente. (Geralmente fica em /usr/bin/python)