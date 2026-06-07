# Testes de Conectividade (Ping)

Nesta seção são apresentados os resultados dos testes de conectividade entre as VMs do Grupo 4, validando:
- Conectividade **por IP**
- Conectividade **por hostname** (nome curto)
- Conectividade **por FQDN** (nome totalmente qualificado)

Os comandos foram executados em sequência na mesma máquina, e uma única captura de tela documenta os 3 resultados.

---

## 1. Testes a partir de G4-PC1-VM1 (Andrezza)

Os testes foram executados em sequência na mesma máquina.

**Destino:** G4-PC2-VM1

```bash
ping -c 4 192.168.26.51
ping -c 4 g4-pc2-vm1
ping -c 4 g4-pc2-vm1.grupo4-bsi-26-1.maceio.lab
```

![G4-PC1-VM1 → G4-PC2-VM1](../evidencias/ping-g4pc1vm1-g4pc2vm1.png)

---

**Destino:** G4-PC3-VM1

```bash
ping -c 4 192.168.26.53
ping -c 4 g4-pc3-vm1
ping -c 4 g4-pc3-vm1.grupo4-bsi-26-1.maceio.lab
```

![G4-PC1-VM1 → G4-PC3-VM1](../evidencias/ping-g4pc1vm1-g4pc3vm1.png)

---

**Destino:** G4-PC4-VM1

```bash
ping -c 4 192.168.26.55
ping -c 4 g4-pc4-vm1
ping -c 4 g4-pc4-vm1.grupo4-bsi-26-1.maceio.lab
```

![G4-PC1-VM1 → G4-PC4-VM1](../evidencias/ping-g4pc1vm1-g4pc4vm1.png)

---

## 2. Testes a partir de G4-PC2-VM1 (Isaque)

Os testes foram executados em sequência na mesma máquina.

```bash
ping -c 4 192.168.26.49
ping -c 4 g4-pc1-vm1
ping -c 4 g4-pc1-vm1.grupo4-bsi-26-1.maceio.lab
```

![G4-PC2-VM1 → G4-PC1-VM1](../evidencias/ping-g4pc2vm1-g4pc1vm1.png)

---

**Destino:** G4-PC3-VM1

```bash
ping -c 4 192.168.26.53
ping -c 4 g4-pc3-vm1
ping -c 4 g4-pc3-vm1.grupo4-bsi-26-1.maceio.lab
```

![G4-PC2-VM1 → G4-PC3-VM1](../evidencias/ping-g4pc2vm1-g4pc3vm1.png)

---

**Destino:** G4-PC4-VM1

```bash
ping -c 4 192.168.26.55
ping -c 4 g4-pc4-vm1
ping -c 4 g4-pc4-vm1.grupo4-bsi-26-1.maceio.lab
```

![G4-PC2-VM1 → G4-PC4-VM1](../evidencias/ping-g4pc2vm1-g4pc4vm1.png)

---

## 3. Testes a partir de G4-PC3-VM1 (Maria)

Os testes foram executados em sequência na mesma máquina.

```bash
ping -c 4 192.168.26.49
ping -c 4 g4-pc1-vm1
ping -c 4 g4-pc1-vm1.grupo4-bsi-26-1.maceio.lab
```

![G4-PC3-VM1 → G4-PC1-VM1](../evidencias/ping-g4pc3vm1-g4pc1vm1.png)

---

**Destino:** G4-PC2-VM1

```bash
ping -c 4 192.168.26.51
ping -c 4 g4-pc2-vm1
ping -c 4 g4-pc2-vm1.grupo4-bsi-26-1.maceio.lab
```

![G4-PC3-VM1 → G4-PC2-VM1](../evidencias/ping-g4pc3vm1-g4pc2vm1.png)

---

**Destino:** G4-PC4-VM1

```bash
ping -c 4 192.168.26.55
ping -c 4 g4-pc4-vm1
ping -c 4 g4-pc4-vm1.grupo4-bsi-26-1.maceio.lab
```

![G4-PC3-VM1 → G4-PC4-VM1](../evidencias/ping-g4pc3vm1-g4pc4vm1.png)

---

## 4. Testes a partir de G4-PC4-VM1 (Renilson)

Os testes foram executados em sequência na mesma máquina.

**Destino:** G4-PC1-VM1

```bash
ping -c 4 192.168.26.49
ping -c 4 g4-pc1-vm1
ping -c 4 g4-pc1-vm1.grupo4-bsi-26-1.maceio.lab
```

![G4-PC4-VM1 → G4-PC1-VM1](../evidencias/ping-g4pc4vm1-g4pc1vm1.png)

---

**Destino:** G4-PC2-VM1

```bash
ping -c 4 192.168.26.51
ping -c 4 g4-pc2-vm1
ping -c 4 g4-pc2-vm1.grupo4-bsi-26-1.maceio.lab
```

![G4-PC4-VM1 → G4-PC2-VM1](../evidencias/ping-g4pc4vm1-g4pc2vm1.png)

---

**Destino:** G4-PC3-VM1

```bash
ping -c 4 192.168.26.53
ping -c 4 g4-pc3-vm1
ping -c 4 g4-pc3-vm1.grupo4-bsi-26-1.maceio.lab
```

![G4-PC4-VM1 → G4-PC3-VM1](../evidencias/ping-g4pc4vm1-g4pc3vm1.png)

---

## 5. Resumo

**Total de testes:** 12 prints (um de cada origem para 3 destinos aleatórios)

Todos os testes de ping foram bem-sucedidos, demonstrando:
- ✅ Conectividade entre todas as VMs
- ✅ Resolução de nomes funcionando corretamente (hostname)
- ✅ Resolução FQDN funcionando corretamente
- ✅ Mapeamento IP/hostname/FQDN consistente no `/etc/hosts`
