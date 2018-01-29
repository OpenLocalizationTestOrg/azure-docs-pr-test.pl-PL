---
title: "Tworzenie maszyny wirtualnej systemu Windows z programem SQL Server przy użyciu usługi Azure PowerShell | Microsoft Docs"
description: "W tym samouczku pokazano sposób tworzenia maszyny wirtualnej z programem SQL Server 2017 i systemem Windows przy użyciu usługi Azure PowerShell."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 12/12/2017
ms.author: jroth
ms.openlocfilehash: 9af08fd46314ff102eff95e0832f7ce96bc161d6
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-sql-server-windows-virtual-machine-with-azure-powershell"></a>Tworzenie maszyny wirtualnej z programem SQL Server 2017 i systemem Windows przy użyciu usługi Azure PowerShell

Ten przewodnik Szybki start przeprowadza użytkownika przez proces tworzenia maszyny wirtualnej z programem SQL Server przy użyciu usługi Azure PowerShell.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

Dla tego przewodnika Szybki start jest wymagany moduł Azure PowerShell w wersji 3.6 lub nowszej. Uruchom polecenie `Get-Module -ListAvailable AzureRM`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie modułu Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="configure-powershell"></a>Konfigurowanie programu PowerShell

1. Otwórz program PowerShell i nawiąż połączenie z kontem platformy Azure, uruchamiając polecenie **Add-AzureRmAccount**.

   ```PowerShell
   Add-AzureRmAccount
   ```

1. Powinien zostać wyświetlony ekran logowania z monitem o podanie poświadczeń. Użyj tego samego adresu e-mail i hasła, którego używasz do logowania w witrynie Azure Portal.

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

1. Zdefiniuj zmienną z unikatową nazwą grupy zasobów. Aby uprościć pozostałą część poradnika Szybki start, reszta poleceń będzie używać tej nazwy jako podstawy dla innych nazw zasobów.

   ```PowerShell
   $ResourceGroupName = "sqlvm1"
   ```

1. Zdefiniuj lokalizację docelowego regionu świadczenia usługi Azure dla wszystkich zasobów maszyn wirtualnych.

   ```PowerShell
   $Location = "East US"
   ```

1. Utwórz grupę zasobów.

   ```PowerShell
   New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location
   ```

## <a name="configure-network-settings"></a>Konfigurowanie ustawień sieciowych

1. Utwórz sieć wirtualną, podsieć i publiczny adres IP. Te zasoby są używane do zapewniania łączności sieciowej z maszyną wirtualną i nawiązywania połączenia z Internetem.

   ``` PowerShell
   $SubnetName = $ResourceGroupName + "subnet"
   $VnetName = $ResourceGroupName + "vnet"
   $PipName = $ResourceGroupName + $(Get-Random)

   # Create a subnet configuration
   $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix 192.168.1.0/24

   # Create a virtual network
   $Vnet = New-AzureRmVirtualNetwork -ResourceGroupName $ResourceGroupName -Location $Location `
      -Name VnetName -AddressPrefix 192.168.0.0/16 -Subnet $SubnetConfig

   # Create a public IP address and specify a DNS name
   $Pip = New-AzureRmPublicIpAddress -ResourceGroupName $ResourceGroupName -Location $Location `
      -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name $PipName
   ```

1. Utwórz sieciową grupę zabezpieczeń. Skonfiguruj reguły, aby zezwolić na połączenia między pulpitem zdalnym (RDP) i programem SQL Server.

   ```PowerShell
   # Rule to allow remote desktop (RDP)
   $NsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name "RDPRule" -Protocol Tcp `
      -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * `
      -DestinationAddressPrefix * -DestinationPortRange 3389 -Access Allow

   #Rule to allow SQL Server connections on port 1433
   $NsgRuleSQL = New-AzureRmNetworkSecurityRuleConfig -Name "MSSQLRule"  -Protocol Tcp `
      -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * `
      -DestinationAddressPrefix * -DestinationPortRange 1433 -Access Allow

   # Create the network security group
   $NsgName = $ResourceGroupName + "nsg"
   $Nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $ResourceGroupName `
      -Location $Location -Name $NsgName `
      -SecurityRules $NsgRuleRDP,$NsgRuleSQL
   ```

1. Utwórz interfejs sieciowy.

   ```PowerShell
   $InterfaceName = $ResourceGroupName + "int"
   $Interface = New-AzureRmNetworkInterface -Name $InterfaceName `
      -ResourceGroupName $ResourceGroupName -Location $Location `
      -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $Pip.Id `
      -NetworkSecurityGroupId $Nsg.Id
   ```

## <a name="create-the-sql-vm"></a>Tworzenie maszyny wirtualnej z programem SQL

1. Wprowadź swoje poświadczenia, aby zalogować się do maszyny wirtualnej. Nazwa użytkownika to „azureadmin”. Upewnij się, że hasło zostało zmienione przed uruchomieniem polecenia.

   ``` PowerShell
   # Define a credential object
   $SecurePassword = ConvertTo-SecureString 'Change.This!000' `
      -AsPlainText -Force
   $Cred = New-Object System.Management.Automation.PSCredential ("azureadmin", $securePassword)
   ```

1. Utwórz obiekt konfiguracji maszyny wirtualnej, a następnie utwórz maszynę wirtualną. Poniższe polecenie utworzy maszynę wirtualną programu SQL Server 2017 Developer Edition w systemie Windows Server 2016.

   ```PowerShell
   # Create a virtual machine configuration
   $VMName = $ResourceGroupName + "VM"
   $VMConfig = New-AzureRmVMConfig -VMName $VMName -VMSize Standard_DS13 | `
      Set-AzureRmVMOperatingSystem -Windows -ComputerName $VMName -Credential $Cred -ProvisionVMAgent -EnableAutoUpdate | `
      Set-AzureRmVMSourceImage -PublisherName "MicrosoftSQLServer" -Offer "SQL2017-WS2016" -Skus "SQLDEV" -Version "latest" | `
      Add-AzureRmVMNetworkInterface -Id $Interface.Id
   
   # Create the VM
   New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VMConfig
   ```

   > [!TIP]
   > Utworzenie maszyny wirtualnej zajmuje kilka minut.

## <a name="install-the-sql-iaas-agent"></a>Instalacja agenta SQL IaaS

Aby uzyskać integrację portalu z funkcjami maszyny wirtualnej programu SQL, musisz zainstalować [rozszerzenie agenta IaaS programu SQL Server](virtual-machines-windows-sql-server-agent-extension.md). Aby zainstalować agenta na nowej maszynie wirtualnej, uruchom następujące polecenie po jego utworzeniu.

   ```PowerShell
   Set-AzureRmVMSqlServerExtension -ResourceGroupName $ResourceGroupName -VMName $VMName -name "SQLIaasExtension" -version "1.2" -Location $Location
   ```

## <a name="remote-desktop-into-the-vm"></a>Łączenie pulpitu zdalnego z maszyną wirtualną

1. Użyj następującego polecenia, aby pobrać publiczny adres IP dla nowej maszyny wirtualnej.

   ```PowerShell
   Get-AzureRmPublicIpAddress -ResourceGroupName $ResourceGroupName | Select IpAddress
   ```

1. Następnie użyj zwróconego adresu IP i przekaż go jako parametr wiersza polecenia do **mstsc**, aby rozpocząć sesję pulpitu zdalnego w nowej maszynie wirtualnej.

   ```
   mstsc /v:<publicIpAddress>
   ```

1. Po wyświetleniu monitu o poświadczenia wybierz opcję podania poświadczeń dla innego konta. Wprowadź nazwę użytkownika poprzedzoną ukośnikiem odwrotnym (np. `\azureadmin`) oraz hasło ustawione wcześniej w tym poradniku Szybki start.

## <a name="connect-to-sql-server"></a>Ustanawianie połączenia z programem SQL Server

1. Po zalogowaniu w sesji pulpitu zdalnego uruchom program **SQL Server Management Studio 2017** z menu start.

1. W oknie dialogowym **Połącz z serwerem** zachowaj ustawienia domyślne. Nazwa serwera to nazwa maszyny wirtualnej. Uwierzytelnianie jest ustawione na opcję **Uwierzytelnianie systemu Windows**. Kliknij przycisk **Połącz**.

Masz teraz lokalne połączenie z programem SQL Server. Jeśli chcesz nawiązać połączenie zdalne, musisz [skonfigurować łączność](virtual-machines-windows-sql-connect.md) z poziomu portalu lub ręcznie.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli maszyna wirtualna nie musi działać w sposób ciągły, możesz uniknąć niepotrzebnych opłat, zatrzymując ją, gdy jest nieużywana. Następujące polecenie zatrzyma maszynę wirtualną, ale pozostawi ją dostępną do użycia w przyszłości.

```PowerShell
Stop-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
```

Możesz również trwale usunąć wszystkie zasoby skojarzone z maszyną wirtualną, korzystając z polecenia **Remove-AzureRmResourceGroup**. Spowoduje to również trwałe usunięcie maszyny wirtualnej, dlatego tego polecenia należy używać z rozwagą.

## <a name="next-steps"></a>Następne kroki

W tym samouczku Szybki start utworzono maszynę wirtualną z programem SQL Server 2017 przy użyciu usługi Azure PowerShell. Aby dowiedzieć się więcej o sposobie przeprowadzania migracji danych do nowego serwera SQL Server, zobacz następujący artykuł.

> [!div class="nextstepaction"]
> [Migrowanie bazy danych do maszyny wirtualnej SQL](virtual-machines-windows-migrate-sql.md)