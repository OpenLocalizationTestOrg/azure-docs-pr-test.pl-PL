---
title: Integracja magazynu kluczy z programem SQL Server na maszynach wirtualnych systemu Windows na platformie Azure (Resource Manager) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak zautomatyzować konfigurację programu SQL Server szyfrowania do użycia z usługą Azure Key Vault. W tym temacie opisano sposób integracji magazynu kluczy Azure za pomocą programu SQL Server maszyn wirtualnych utworzonych za pomocą Menedżera zasobów."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 32b9564fa5c9ca6864ade343fda309b2c3edf123
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="7c832-104">Konfigurowanie integracji magazynu kluczy Azure dla programu SQL Server na maszynach wirtualnych Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="7c832-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c832-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7c832-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="7c832-106">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="7c832-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="7c832-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7c832-107">Overview</span></span>
<span data-ttu-id="7c832-108">Istnieje wiele funkcji szyfrowania programu SQL Server, takich jak [przezroczystego szyfrowania danych (funkcji TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [szyfrowania na poziomie kolumny (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), i [szyfrowania kopii zapasowych](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c832-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="7c832-109">Te formy szyfrowania wymagają przechowywania kluczy kryptograficznych używanego do szyfrowania i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="7c832-109">These forms of encryption require you to manage and store the cryptographic keys you use for encryption.</span></span> <span data-ttu-id="7c832-110">Usługa Azure Key Vault (AKV) zaprojektowano w celu poprawy zabezpieczeń i zarządzania tych kluczy w lokalizacji bezpieczne i wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="7c832-110">The Azure Key Vault (AKV) service is designed to improve the security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="7c832-111">[Łącznik usług SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) umożliwia SQL Server do użycia tych kluczy z usługi Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="7c832-111">The [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server to use these keys from Azure Key Vault.</span></span>

<span data-ttu-id="7c832-112">Zostanie uruchomiony program SQL Server z lokalnej maszyny są [kroki można wykonać, aby uzyskać dostęp do usługi Azure Key Vault z komputera lokalnego programu SQL Server](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c832-112">If you running SQL Server with on-premises machines, there are [steps you can follow to access Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="7c832-113">Jednak dla programu SQL Server na maszynach wirtualnych Azure, można oszczędzić czas za pomocą *integracji magazynu kluczy Azure* funkcji.</span><span class="sxs-lookup"><span data-stu-id="7c832-113">But for SQL Server in Azure VMs, you can save time by using the *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="7c832-114">Gdy ta funkcja jest włączona, automatycznie jest instalowana łącznika programu SQL Server, konfiguruje dostawcy EKM. Aby uzyskać dostępu do usługi Azure Key Vault i tworzy poświadczenia, aby umożliwić użytkownikowi dostęp do magazynu.</span><span class="sxs-lookup"><span data-stu-id="7c832-114">When this feature is enabled, it automatically installs the SQL Server Connector, configures the EKM provider to access Azure Key Vault, and creates the credential to allow you to access your vault.</span></span> <span data-ttu-id="7c832-115">Jeśli przeglądał kroki opisane w dokumentacji lokalnego opisane powyżej, zobaczysz, że ta funkcja pozwala zautomatyzować kroki 2 i 3.</span><span class="sxs-lookup"><span data-stu-id="7c832-115">If you looked at the steps in the previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="7c832-116">Jedyną operacją, której nadal trzeba wykonać ręcznie polega na utworzeniu magazynu kluczy i kluczy.</span><span class="sxs-lookup"><span data-stu-id="7c832-116">The only thing you would still need to do manually is to create the key vault and keys.</span></span> <span data-ttu-id="7c832-117">Z tego miejsca wszystkie ustawienia maszyny Wirtualnej SQL jest zautomatyzowany.</span><span class="sxs-lookup"><span data-stu-id="7c832-117">From there, the entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="7c832-118">Po ukończeniu tej konfiguracji tej funkcji można wykonywać instrukcje T-SQL, aby rozpocząć szyfrowania z bazy danych lub kopii zapasowych w zwykły sposób.</span><span class="sxs-lookup"><span data-stu-id="7c832-118">Once this feature has completed this setup, you can execute T-SQL statements to begin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="7c832-119">Włączanie i konfigurowanie Integracja</span><span class="sxs-lookup"><span data-stu-id="7c832-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="7c832-120">Można włączyć integracja podczas inicjowania obsługi lub skonfiguruj ją dla istniejących maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7c832-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="7c832-121">Nowe maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="7c832-121">New VMs</span></span>
<span data-ttu-id="7c832-122">W przypadku udostępniania nowej maszyny wirtualnej programu SQL Server z usługą Resource Manager Azure portal udostępnia krok, aby włączyć integrację z usługą Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="7c832-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, the Azure portal provides a step to enable Azure Key Vault integration.</span></span> <span data-ttu-id="7c832-123">Funkcja usługi Azure Key Vault jest dostępna tylko w przypadku Enterprise, Developer i wersji ewaluacyjnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7c832-123">The Azure Key Vault feature is available only for the Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![Integracja magazynu kluczy Usług SQL Azure](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="7c832-125">Aby uzyskać szczegółowe wskazówki dotyczące inicjowania obsługi administracyjnej, zobacz [Aprowizowanie maszyny wirtualnej programu SQL Server w portalu Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="7c832-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in the Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="7c832-126">Istniejące maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="7c832-126">Existing VMs</span></span>
<span data-ttu-id="7c832-127">W przypadku istniejących maszyn wirtualnych programu SQL Server należy wybrać maszyny wirtualnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7c832-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="7c832-128">Następnie wybierz **konfigurację programu SQL Server** sekcji **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="7c832-128">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Integracja programu SQL dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="7c832-130">W **konfigurację programu SQL Server** bloku, kliknij przycisk **Edytuj** przycisk w sekcji Integracja magazynu kluczy automatycznego.</span><span class="sxs-lookup"><span data-stu-id="7c832-130">In the **SQL Server configuration** blade, click the **Edit** button in the Automated Key Vault integration section.</span></span>

![Konfigurowanie integracja SQL dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="7c832-132">Gdy skończysz, kliknij przycisk **OK** przycisk w dolnej części **konfigurację programu SQL Server** bloku, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="7c832-132">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="7c832-133">Można również skonfigurować integracja przy użyciu szablonu.</span><span class="sxs-lookup"><span data-stu-id="7c832-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="7c832-134">Aby uzyskać więcej informacji, zobacz [szablonu Azure Szybki Start dla usługi Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span><span class="sxs-lookup"><span data-stu-id="7c832-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

