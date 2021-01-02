# Trabalho 1: Máquina virtual e programação com sockets

## Prefácio

Você deve programar o trabalho em Golang.

A máquina virtual é opcional. Você pode ter o ambiente configurado em sua própria máquina.

A trabalho pode ser realizado individualmente ou em dupla.

A cópia do trabalho não deveria ser uma prática. A discussão é saudável.

## Parte A: Configurando a máquina virtual

A primeira parte é configurar a máquina virtual (VM) que você usará no restante do curso. Isso facilitará a instalação de todas as dependências para os trabalhos de programação, poupando o tédio de instalar pacotes individuais e garantindo que seu ambiente de desenvolvimento esteja correto.

### Passo 1: Instale o Vagrant

O Vagrant é uma ferramenta para configurar automaticamente uma VM usando as instruções fornecidas em um único "Vagrantfile".

**macOS e Windows:** você precisa instalar o Vagrant usando o link de download correto para o seu computador aqui: https://www.vagrantup.com/downloads.html.

**Apenas Windows**: será solicitado que você reinicie o computador no final da instalação. Clique em Sim para fazer isso imediatamente ou reinicie manualmente mais tarde, mas não se esqueça de fazer isso ou o Vagrant não funcionará!

**Linux:** Vai depender de que distribuição você utiliza. No caso da minha, ubuntu, ceritifiquei-me primeiramente de atualizar o SO: sudo apt update && sudo apt upgrade -y && sudo apt autoremove.  Para instalar o Vagrant, você deve ter o repositório "Universe" em seu computador; execute: sudo apt-add-repository universe. Finalmente, para instalar o vagrant, execute: sudo apt install vagrant.

### Passo 2: Instale o VirtualBox

VirtualBox é um provedor de máquinas virtuais (hipervisor).

**macOS e Windows:** você precisa instalar o VirtualBox usando o link de download correto para o seu computador aqui: https://www.virtualbox.org/wiki/Downloads.

**Apenas Windows:** Use todas as configurações de instalação padrão, mas você pode desmarcar a caixa de seleção "Iniciar Oracle VirtualBox x.x.x após a instalação".

**Linux:** Vai depender da sua distribuição. No ubuntu execute o comando: sudo apt install virtualbox.
Execute o virtualbox por um terminal de comandos e veja se mensagens de erro ou warning estão aparecendo. Se houver, reiniciar o terminal ou a máquina talvez seja suficiente para que elas deixem de aparecer. Só assim o vagrant funcionará corretamente.

**Observação:** Isso também instalará o aplicativo VirtualBox em seu computador, mas você nunca deve precisar executá-lo, embora possa ser útil (consulte o passo 6).

### Passo 3: instale o Git (e o terminal compatível com SSH no Windows)

Git é um sistema de controle de versão distribuído.

**macOS e Windows:** Você precisa instalar o Git usando o link de download correto
para o seu computador aqui: https://git-scm.com/downloads.

**Apenas macOS:** Depois de abrir o arquivo de instalação .dmg, você verá uma janela do Finder incluindo um arquivo .pkg, que é o instalador. Abrir isso normalmente pode dar a você um aviso dizendo que não pode ser aberto porque é de um desenvolvedor não identificado. Para cancelar esta proteção, clique com o botão direito no arquivo .pkg e selecione "Abrir". Isso mostrará um prompt perguntando se você tem certeza de que deseja abri-lo. Selecione "Sim". Isso o levará para a instalação (direta).

**Apenas Windows:** Você terá muitas opções para escolher durante a instalação; usar tudo padrão será suficiente para este curso (você pode desmarcar "Ver notas de lançamento" no final). A instalação inclui um terminal Bash compatível com SSH, geralmente localizado em `C:\ProgramFiles\Git\bin\ bash.exe`. Você deve usá-lo como seu terminal neste curso, a menos que prefira outro terminal compatível com SSH (o prompt de comando não funcionará). Sinta-se à vontade para criar um atalho para ele; copiar e colar o executável em outro lugar não funcionará, no entanto.

**Linux:** No caso do ubuntu é `sudo apt install git`.

### Passo 4: Instale o servidor X

Você precisará de um servidor X para inserir comandos na máquina virtual.

**macOS:** instale o [XQuartz](https://www.xquartz.org/). Você precisará fazer logout e login novamente para concluir a instalação (conforme mencionado no prompt no final).

**Windows:** Instale o
[Xming](https://sourceforge.net/projects/xming/files/Xming/6.9.0.31/Xming-6-9-0-31-setup.exe/download).
Use as opções padrão e desmarque "Launch Xming" no final.

**Linux:** O servidor X está pré-instalado!

### Passo 5: Clone o repositório de trabalhos Git

Abra seu terminal (use aquele mencionado no passo 3 se estiver usando Windows) e `cd` para onde você quiser manter os arquivos deste curso em seu computador.  

Execute `git clone https://github.com/filipemr/rus0082` para baixar os arquivos do curso no GitHub.

`cd rus0082` para entrar no diretório de trabalhos do curso.

### Passo 6: Provisionando a máquina virtual usando vagrant

No diretório `rus0082` que você acabou de criar, execute o comando `vagrant up` para iniciar a máquina virtual e provisioná-la de acordo com o Vagrantfile. Você provavelmente terá que esperar alguns minutos. Você pode ver avisos/erros em vermelho, como "default: stdin: is not a tty", mas você não deve se preocupar com eles.

**Observação 1**: os comandos a seguir permitirão que você interrompa a VM a qualquer momento (por exemplo, quando terminar de trabalhar em uma tarefa do dia):
* `vagrant suspend` salvará o estado da VM e a parará.
* `vagrant halt` irá desligar normalmente o sistema operacional da VM e desligar a VM.
* `vagrant destroy` irá remover todos os vestígios da VM no seu sistema.

Além disso, o comando `vagrant status` permitirá que você verifique o status de sua máquina caso não tenha certeza (por exemplo, executando, desligado, salvo ...). Você deve estar em algum subdiretório do diretório que contém o Vagrantfile para usar qualquer um dos comandos acima, caso contrário, o Vagrant não saberá a qual máquina virtual você está se referindo.

**Observação 2**: O aplicativo VirtualBox que foi instalado no passo 2 fornece uma interface visual como alternativa a esses comandos, onde você pode ver o status de sua VM e ligá-la/desligá-la ou salvar seu estado. Não é recomendado usá-lo, entretanto, uma vez que não é integrado ao Vagrant, e os comandos de digitação não devem ser mais lentos. Também não é uma alternativa ao `vagrant up` inicial, já que isso cria a máquina virtual.
### Observação extra para usuários Windows

Os finais de linha são simbolizados de maneira diferente no DOS (Windows) e no Unix
(Linux/MacOS). No primeiro, eles são representados por um retorno ao início e pulo de linha (CRLF, ou "\r\n"), e no último, apenas um avanço de linha (LF, ou "\n"). Dado que você executou `git pull` no Windows, git detecta seu sistema operacional e adiciona retorno ao início aos arquivos durante o download. Isso pode levar a problemas de análise dentro da máquina virtual, que executa o Ubuntu (Unix). Felizmente, isso parece afetar apenas os scripts de shell (arquivos \*.sh) que foram escritos para teste. O `Vagrantfile` é configurado para converter automaticamente todos os arquivos de volta para o formato Unix, então ** você não deve se preocupar com isso **. ** No entanto **, se você quiser escrever/editar scripts de shell para ajudar com os testes, ou se encontrar esse problema com algum outro tipo de arquivo, use o programa pré-instalado `dos2unix`. Execute `dos2unix [arquivo]` para convertê-lo para o formato Unix (antes de editarexecutar na máquina virtual) e execute `unix2dos [arquivo]` para convertê-lo para o formato DOS (antes de editar no Windows). Uma boa dica de que você precisa fazer isso ao executar a partir da máquina virtual é alguma mensagem de erro envolvendo `^M` (retorno ao início). Uma boa dica que você precisa fazer ao editar no Windows é a falta de novas linhas. Lembre-se de que fazer isso só deve ser necessário se quiser editar scripts de shell.

