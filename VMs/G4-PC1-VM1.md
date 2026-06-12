# G4-PC1-VM1

Ficha individual da máquina virtual no ambiente de rede do Grupo 4.

## Identificação

| Campo | Valor |
|-------|-------|
| Hostname | `g4-pc1-vm1` |
| FQDN | `g4-pc1-vm1.grupo4-bsi-26-1.maceio.lab` |
| Apelido (alias) | `g4-pc1-vm1` |
| Endereço IP | `192.168.26.49/28` |
| Sub-rede | `192.168.26.48/28` (255.255.255.240) |
| Responsável (admin) | Andrezza Abreu de Magalhães (`andrezza.magalhaes`) |

## Hardware

| Recurso | Valor |
|---------|-------|
| RAM | 2048 MB (2 GB) |
| vCPU | 2 núcleos |
| Disco | 32 GB |
| SO | Ubuntu Server |

## Usuários criados nesta VM

| Usuário | Senha |
|---------|-------|
| `andrezza.magalhaes` | `andrezza` |
| `isaque.braga` | `isaque` |
| `maria.santos` | `maria` |
| `renilson.santos` | `renilson` |
| `administrador` | `adminifal` |

> Membro do grupo `sudo` nesta máquina: **`andrezza.magalhaes`**.

## Configuração de rede

### Netplan (`/etc/netplan/00-installer-config.yaml`)

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
      optional: true
```

### `/etc/hosts`

```bash
sudo nano /etc/hosts
```

```text
127.0.0.1   localhost
127.0.1.1   g4-pc1-vm1.grupo4-bsi-26-1.maceio.lab   g4-pc1-vm1

192.168.26.49   g4-pc1-vm1.grupo4-bsi-26-1.maceio.lab   g4-pc1-vm1
192.168.26.50   g4-pc1-vm2.grupo4-bsi-26-1.maceio.lab   g4-pc1-vm2
192.168.26.51   g4-pc2-vm1.grupo4-bsi-26-1.maceio.lab   g4-pc2-vm1
192.168.26.52   g4-pc2-vm2.grupo4-bsi-26-1.maceio.lab   g4-pc2-vm2
192.168.26.53   g4-pc3-vm1.grupo4-bsi-26-1.maceio.lab   g4-pc3-vm1
192.168.26.54   g4-pc3-vm2.grupo4-bsi-26-1.maceio.lab   g4-pc3-vm2
192.168.26.55   g4-pc4-vm1.grupo4-bsi-26-1.maceio.lab   g4-pc4-vm1
192.168.26.56   g4-pc4-vm2.grupo4-bsi-26-1.maceio.lab   g4-pc4-vm2
```

## Configuração aplicada

A configuração seguiu o tutorial em [`../docs/passo-a-passo.md`](../docs/passo-a-passo.md).

## Arquivo da VM

Pasta da VM no Google Drive com os arquivos para download:

[Acessar pasta no Google Drive](https://drive.google.com/drive/folders/18QODpT1YGYubXK_QM6ckjrTuZfiJOhpC?usp=sharing)

> A pasta contém a VM exportada nos formatos **`.ova`** (requisito do professor) e **`.vdi`**.
