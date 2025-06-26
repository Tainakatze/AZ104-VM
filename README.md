# 🧪 Gerenciamento de Máquinas Virtuais no Azure

## 📜 Índice:

1. [Introdução](#introdução)  
2. [Importância do Gerenciamento de VMs no Azure](#importância-do-gerenciamento-de-vms-no-azure)  
3. [Objetivos do Gerenciamento](#objetivos-do-gerenciamento)  
4. [Pré-requisitos](#pré-requisitos)  
5. [Arquitetura de Referência](#arquitetura-de-referência)  
6. [Gerenciamento da VM e Recursos](#gerenciamento-da-vm-e-recursos)  
7. [Exemplos Práticos](#exemplos-práticos)  
8. [FAQ](#faq)  
9. [Links Úteis](#links-úteis)  
10. [Referências](#referências)  
11. [Conclusão](#conclusão)  

---

## 📜 Introdução:

As **máquinas virtuais (VMs)** são a base para muitos workloads no Azure. Gerenciá-las adequadamente  desde o provisionamento até o monitoramento e segurança garante que os serviços rodem com **alta disponibilidade, segurança e economia**.

---

## 🌟 Importância do Gerenciamento de VMs no Azure:

O gerenciamento correto das VMs é vital para empresas que desejam:
- ✅ Garantir segurança contra acessos indevidos  
- ✅ Reduzir custos evitando recursos ociosos  
- ✅ Escalar automaticamente para suportar picos  
- ✅ Simplificar a manutenção e o ciclo de vida  
- ✅ Ter visibilidade completa com monitoramento e alertas  

---

## 🎯 Objetivos do Gerenciamento:

- ✅ Criar e configurar VMs seguras  
- ✅ Gerenciar o ciclo de vida (início, parada, reinício, exclusão)  
- ✅ Implementar backups e patches automaticamente  
- ✅ Automatizar o provisionamento com IaC (Bicep, ARM, CLI)  
- ✅ Aplicar segurança de rede e RBAC  
- ✅ Redimensionar e escalar automaticamente conforme a demanda  

---

## 🧰 Pré-requisitos:

- ✅ Conta ativa no [Azure Portal](https://portal.azure.com)  
- ✅ Permissões de **Contribuidor** ou superior  
- ✅ Familiaridade com **Azure CLI**, **PowerShell** e redes virtuais  
- ✅ Gerenciador de chaves SSH para acesso seguro  
- ✅ Opcional: [Visual Studio Code](https://code.visualstudio.com) para editar templates Bicep  

---

## 📂 Arquitetura de Referência:
```
VNet (10.0.0.0/16)
  └─ Subnet (10.0.0.0/24)
       ├─ Network Security Group (NSG)
       ├─ VM NIC
       │    └─ VM (Linux/Windows)
       └─ IP Público
Backup Vault
Azure Bastion
Azure Monitor
```

![Meu diagrama](meu_diagrama.png)

---

## Gerenciamento da VM e Recursos:

### 1️⃣ Configuração inicial
- Especifique o tamanho da VM (SKU), tipo de SO e autenticação  
- Configure apenas portas necessárias no NSG  
- Ative o Backup e criptografe os discos para segurança  

### 2️⃣ Conexão segura
- Utilize o **Azure Bastion** para acesso remoto seguro  
- Configure acesso via SSH com chaves públicas, evitando senhas  

### 3️⃣ Ciclo de vida
Use a CLI para controlar o estado da VM:
```bash
az vm start --resource-group rg-gerenciamento-vm --name vm-azure
az vm stop --resource-group rg-gerenciamento-vm --name vm-azure
az vm restart --resource-group rg-gerenciamento-vm --name vm-azure
az vm delete --resource-group rg-gerenciamento-vm --name vm-azure
```

Redimensione a VM quando necessário:
```bash
az vm resize --resource-group rg-gerenciamento-vm --name vm-azure --size Standard_B2ms
```

### 4️⃣ Gerenciamento avançado
- Configure backups regulares com o **Azure Backup**  
- Capture **snapshots** antes de atualizações críticas  
- Gerencie o tráfego com NSGs e aplique regras personalizadas  
- Habilite alertas e painéis com o **Azure Monitor**  
- Gerencie permissões com **RBAC** e Azure Active Directory  
- Use **VM Scale Sets** para workloads que demandam escalonamento automático  

---

## 🧪 Exemplos Práticos:

#### Criar VM com CLI
```bash
az vm create --resource-group rg-gerenciamento-vm --name vm-azure --image UbuntuLTS --size B2s --generate-ssh-keys
```

#### Listar VMs
```bash
az vm list --output table
```

#### Redimensionar VM
```bash
az vm resize --resource-group rg-gerenciamento-vm --name vm-azure --size Standard_B2ms
```

#### Bicep simples
```bicep
resource vm 'Microsoft.Compute/virtualMachines@2021-07-01' = {
  name: 'vm-azure-lab'
  location: resourceGroup().location
  properties: {
    hardwareProfile: { vmSize: 'Standard_B2s' }
  }
}
```

---

## ❓ FAQ:

- 💬 **Qual VM menor para testes?**  
  B1s ou B2s são as opções mais econômicas para testes.  

- 💬 **Como acesso a VM com segurança?**  
  Use o Azure Bastion e autenticação por SSH.  

- 💬 **Como economizar?**  
  Programe o desligamento automático quando a VM estiver ociosa.  

- 💬 **Qual a diferença entre VM Spot e regular?**  
  Spot são mais baratas, mas podem ser interrompidas quando o Azure precisa da capacidade.  

- 💬 **O que são discos gerenciados?**  
  São discos que o Azure gerencia automaticamente quanto à resiliência e desempenho.  

---

## Links Úteis:

- [Azure Virtual Machines Docs](https://learn.microsoft.com/azure/virtual-machines/)  
- [Azure Bastion Docs](https://learn.microsoft.com/azure/bastion/bastion-overview)  
- [Azure Backup Docs](https://learn.microsoft.com/azure/backup/backup-overview)  
- [RBAC Overview](https://learn.microsoft.com/azure/role-based-access-control/overview)  
- [IaC com ARM e Bicep](https://learn.microsoft.com/azure/azure-resource-manager/templates/overview)  

---

## 📚 Referências:

- [Microsoft Docs — Azure Virtual Machines](https://learn.microsoft.com/azure/virtual-machines/)  
- [Microsoft Docs — Azure Backup](https://learn.microsoft.com/azure/backup/backup-overview)  
- [Microsoft Docs — Azure Monitor](https://learn.microsoft.com/azure/azure-monitor/overview)  
- [Microsoft Docs — Bicep e ARM Templates](https://learn.microsoft.com/azure/azure-resource-manager/templates/overview)  

---

## 🎯 Minhas conclusões:

O gerenciamento de máquinas virtuais no Azure vai além da simples criação. Envolve garantir segurança, economia, backups e monitoramento, além da automação e práticas que tornam a operação robusta e eficiente. Dominar essas habilidades é fundamental para qualquer profissional que atua na nuvem e quer entregar valor com qualidade.




