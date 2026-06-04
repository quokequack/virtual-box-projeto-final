# Passo a passo — Configuração das VMs (Ubuntu Server)

Este documento descreve, de forma detalhada e fundamentada, o procedimento de instalação e
configuração aplicado a **cada uma das 8 máquinas virtuais** do Grupo 4. Os comandos são
idênticos para todas as VMs; alteram-se apenas os valores específicos de cada máquina
(**hostname**, **IP** e **responsável**), indicados entre colchetes `[ ]`.

> **Convenção:** substitua os campos entre colchetes pelos valores da VM correspondente,
> conforme as tabelas das seções 5 e 6 do [`README.md`](../README.md).

---

## 0. Pré-requisitos e credenciais

Durante a instalação do Ubuntu Server, foi criada a conta administrativa padrão:

- **Login:** `administrador`
- **Senha:** `adminifal`

Esta conta é utilizada para o primeiro acesso e para a execução dos comandos com `sudo`.

---

## 1. Criação da máquina virtual

Crie uma **nova** VM no hipervisor para o projeto (não reutilizar VMs anteriores), com a
seguinte configuração de hardware:

| Recurso | Valor |
|---------|-------|
| Memória RAM | 512 MB |
| Processadores | 1 vCPU (1 núcleo) |
| Disco | 32 GB |
| ISO | Ubuntu Server |

**Por quê esse dimensionamento?** O Ubuntu Server opera em modo texto (sem ambiente
gráfico), de modo que 512 MB de RAM e 1 núcleo são suficientes para o sistema e o serviço
SSH. Como o hospedeiro precisa executar 8 VMs ao mesmo tempo, manter cada uma enxuta evita
sobrecarga de memória e CPU no computador físico.

---

## 2. Idioma e localização

Verifique a configuração de idioma atual:

```bash
locale
localectl status
```

Instale o pacote de idioma português:

```bash
sudo apt update
sudo apt install language-pack-pt -y
```

**Por quê?** O `apt update` atualiza a lista de pacotes disponíveis nos repositórios antes
de qualquer instalação. O `language-pack-pt` adiciona as traduções e a configuração regional
(locale) em português, padronizando mensagens do sistema — útil em um ambiente acadêmico
local.

---

## 3. Layout de teclado (ABNT2)

Edite o arquivo de configuração do teclado:

```bash
sudo nano /etc/default/keyboard
```

Deixe o conteúdo exatamente assim:

```ini
XKBMODEL="pc105"
XKBLAYOUT="br"
XKBVARIANT="abnt2"
XKBOPTIONS=""
BACKSPACE="guess"
```

Aplique a configuração e reinicie:

```bash
sudo dpkg-reconfigure keyboard-configuration
sudo reboot
```

**Por quê?** O layout `br`/`abnt2` corresponde ao teclado brasileiro, garantindo que
caracteres como `ç`, acentos e símbolos sejam digitados corretamente no console. O
`dpkg-reconfigure` regenera a configuração do teclado já em uso, e o `reboot` assegura que
todas as mudanças de idioma/teclado sejam plenamente aplicadas.

---

## 4. Definição do hostname

Defina o nome curto da máquina (sem o domínio):

```bash
sudo hostnamectl set-hostname [hostname]
```

Exemplo para a primeira VM:

```bash
sudo hostnamectl set-hostname g4-pc1-vm1
```

Confirme:

```bash
hostnamectl
```

**Por quê?** O `hostnamectl` define o nome de identificação do host de forma persistente
(grava em `/etc/hostname` e notifica o `systemd`). Adotou-se o **nome curto** como hostname;
o **FQDN** completo é associado ao IP no arquivo `/etc/hosts` (seção 6), separando a
identidade local da resolução de nomes.

---

## 5. Configuração de rede (Netplan)

Liste o(s) arquivo(s) de configuração de rede:

```bash
ls /etc/netplan
```

Abra o arquivo existente (o nome pode variar):

```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

Configure o conteúdo conforme o modelo abaixo, ajustando o **nome da interface** e o
**endereço IP** da VM:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    ens160:
      dhcp4: no
      dhcp6: no
      addresses:
        - 192.168.26.49/28
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
      optional: true   # evita que o boot trave ao mudar para a rede interna
```

Aplique e valide:

```bash
sudo netplan generate
sudo netplan apply
ip a
ip route
```

### 5.1. Fundamentação de cada parâmetro

- **`renderer: networkd`** — O Netplan é apenas uma *camada de configuração*: ele lê o YAML e
  gera a configuração para um *backend* (renderer) que efetivamente gerencia a rede. Há dois
  backends: o **`systemd-networkd`** (`networkd`) e o **`NetworkManager`**. O `NetworkManager`
  é voltado a desktops, com integração gráfica e gerenciamento dinâmico de conexões. O
  **`systemd-networkd` é o padrão e o mais adequado para servidores**: é leve, integrado ao
  `systemd`, não exige interface gráfica e é ideal para hosts headless com endereçamento
  estático — exatamente o caso deste projeto. Por isso adotamos `renderer: networkd`.

- **`ens160`** — É o nome da interface de rede. **Atenção:** esse nome depende do hipervisor.
  Em VMware costuma ser `ens160`; no VirtualBox normalmente é `enp0s3` (NAT) ou `enp0s8`
  (rede interna). **Verifique o nome real com `ip a`** e substitua no arquivo, caso seja
  diferente.

- **`dhcp4: no` / `dhcp6: no`** — Desativa a obtenção automática de endereço via DHCP. Um
  servidor precisa de um **IP fixo e previsível**, pois outros hosts o referenciam por
  endereço/nome. Se o IP mudasse a cada inicialização, a resolução de nomes e o acesso SSH
  ficariam inconsistentes.

- **`addresses: - 192.168.26.49/28`** — Define o **endereço IP estático** da VM, já com o
  **prefixo `/28`**, que indica a máscara `255.255.255.240`. O prefixo é obrigatório: é ele
  que informa ao sistema quais endereços pertencem à mesma sub-rede (e, portanto, são
  alcançáveis diretamente em camada de enlace).

- **`nameservers: addresses: [8.8.8.8, 1.1.1.1]`** — Define os servidores **DNS** usados para
  traduzir nomes de domínio da internet em IPs. Foram escolhidos o DNS público do Google
  (`8.8.8.8`) e o da Cloudflare (`1.1.1.1`), úteis quando a VM precisa baixar pacotes. A
  resolução *entre as VMs* do projeto, porém, é feita localmente pelo `/etc/hosts` (seção 6),
  sem depender de DNS.

- **`optional: true`** — **Este é o parâmetro central da estabilidade do boot.** Por padrão, o
  serviço `systemd-networkd-wait-online` faz o sistema **aguardar a interface ficar "online"**
  antes de concluir a inicialização. Quando a VM é movida para uma **rede interna isolada**
  (sem DHCP nem enlace ativo de saída), a interface pode não atingir esse estado, e o boot
  **trava por até ~2 minutos** exibindo a mensagem *"A start job is running for Wait for
  Network to be Configured"*. Ao marcar a interface como `optional: true`, informamos ao
  `systemd` que ela **não é obrigatória** para o sistema iniciar — assim o boot prossegue
  imediatamente, sem travas, mesmo quando a rede é trocada para o modo interno. Era exatamente
  esse o objetivo da observação "pra não quebrar quando mudar pra rede interna".

> **Cuidado com a indentação do YAML.** O formato YAML é sensível a espaços: use sempre
> **espaços** (não tabulações) e mantenha o alinhamento exato do modelo acima. Uma indentação
> incorreta faz o `netplan apply` falhar.

---

## 6. Resolução de nomes local (`/etc/hosts`)

Edite o arquivo de hosts:

```bash
sudo nano /etc/hosts
```

Deixe-o assim (as duas primeiras linhas usam o hostname/FQDN **da própria VM**; em seguida,
o mapeamento de **todas** as VMs do grupo):

```text
127.0.0.1   localhost
127.0.1.1   [hostname] [FQDN]

192.168.26.49   g4-pc1-vm1.grupo4-bsi-26-1.maceio.lab   g4-pc1-vm1
192.168.26.50   g4-pc1-vm2.grupo4-bsi-26-1.maceio.lab   g4-pc1-vm2
192.168.26.51   g4-pc2-vm1.grupo4-bsi-26-1.maceio.lab   g4-pc2-vm1
192.168.26.52   g4-pc2-vm2.grupo4-bsi-26-1.maceio.lab   g4-pc2-vm2
192.168.26.53   g4-pc3-vm1.grupo4-bsi-26-1.maceio.lab   g4-pc3-vm1
192.168.26.54   g4-pc3-vm2.grupo4-bsi-26-1.maceio.lab   g4-pc3-vm2
192.168.26.55   g4-pc4-vm1.grupo4-bsi-26-1.maceio.lab   g4-pc4-vm1
192.168.26.56   g4-pc4-vm2.grupo4-bsi-26-1.maceio.lab   g4-pc4-vm2
```

Exemplo da linha `127.0.1.1` para a VM1:

```text
127.0.1.1   g4-pc1-vm1   g4-pc1-vm1.grupo4-bsi-26-1.maceio.lab
```

**Por quê?** O arquivo `/etc/hosts` provê **resolução de nomes estática e local**, sem
necessidade de um servidor DNS dedicado. Com esse mapeamento, é possível executar `ping` e
`ssh` usando o **nome** ou o **FQDN** das máquinas (e não apenas o IP), validando o requisito
de nomenclatura do projeto. A ordem das colunas é: **IP → FQDN (nome canônico) → apelido
(alias)**. A linha `127.0.1.1` associa o próprio host ao seu nome, prática padrão no Debian/Ubuntu.

---

## 7. Criação dos usuários

Em **cada** VM, crie os usuários de **todos** os integrantes do grupo:

```bash
sudo adduser andrezza.magalhaes
sudo adduser isaque.braga
sudo adduser maria.santos
sudo adduser renilson.santos
```

Conceda privilégios administrativos ao **responsável** pela máquina (membro do grupo `sudo`):

```bash
sudo usermod -aG sudo [usuario responsavel pela VM]
```

Exemplo, na G4-PC1-VM1 (responsável: Andrezza):

```bash
sudo usermod -aG sudo andrezza.magalhaes
```

**Por quê?** O requisito do projeto determina que **todas** as VMs contenham a conta
administrativa (`administrador`) e os usuários nomeados de cada integrante — por isso os
quatro usuários são criados em todas as máquinas. O `usermod -aG sudo` adiciona o responsável
ao grupo `sudo`, concedendo a ele a capacidade de executar comandos administrativos naquela
máquina. A opção `-a` (*append*) é essencial: ela **acrescenta** o grupo sem remover os demais
grupos do usuário.

| VM | Responsável (recebe `sudo`) |
|----|------------------------------|
| G4-PC1-VM1 / G4-PC1-VM2 | andrezza.magalhaes |
| G4-PC2-VM1 / G4-PC2-VM2 | isaque.braga |
| G4-PC3-VM1 / G4-PC3-VM2 | maria.santos |
| G4-PC4-VM1 / G4-PC4-VM2 | renilson.santos |

---

## 8. Serviço SSH

Instale, habilite e inicie o servidor SSH:

```bash
sudo apt update
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh
```

**Por quê?** O `openssh-server` permite o **acesso remoto seguro** às VMs. O
`systemctl enable ssh` configura o serviço para iniciar **automaticamente no boot**, enquanto
`start` o inicia imediatamente e `status` confirma que está ativo (`active (running)`). O SSH
é o serviço sobre o qual recaem os testes de acesso remoto da seção 9.

---

## 9. Validação e testes

### 9.1. Nome do host

```bash
hostname
hostnamectl
```

Deve retornar o nome curto configurado (ex.: `g4-pc1-vm1`).

### 9.2. Conectividade (ping)

Teste por **IP** e por **nome**, a partir de uma VM em direção às demais:

```bash
# por IP
ping -c 4 192.168.26.50

# por apelido
ping -c 4 g4-pc1-vm2

# por FQDN
ping -c 4 g4-pc1-vm2.grupo4-bsi-26-1.maceio.lab
```

A opção `-c 4` envia exatamente 4 pacotes e encerra, evitando ping contínuo. O sucesso por
nome confirma que o `/etc/hosts` está correto.

### 9.3. Acesso remoto (SSH)

Teste o login remoto usando os usuários criados, por IP e por nome:

```bash
ssh isaque.braga@192.168.26.51
ssh isaque.braga@g4-pc2-vm1
ssh isaque.braga@g4-pc2-vm1.grupo4-bsi-26-1.maceio.lab
```

---

## 10. Resumo do fluxo

1. Criar a VM (512 MB / 1 vCPU / 32 GB) e instalar o Ubuntu Server.
2. Configurar idioma (`language-pack-pt`) e teclado (`br`/`abnt2`).
3. Definir o hostname com `hostnamectl`.
4. Configurar IP estático no Netplan (`networkd`, `dhcp4: no`, `/28`, `optional: true`).
5. Preencher o `/etc/hosts` com o mapeamento de todas as VMs.
6. Criar os usuários do grupo e conceder `sudo` ao responsável.
7. Instalar e habilitar o SSH.
8. Executar os testes de `ping` e `SSH`.
