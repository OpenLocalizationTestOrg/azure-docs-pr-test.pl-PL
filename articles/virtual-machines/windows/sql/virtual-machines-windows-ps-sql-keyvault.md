---
title: aaaIntegrate Key Vault z programem SQL Server na maszynach wirtualnych systemu Windows na platformie Azure (Resource Manager) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooautomate hello konfiguracji programu SQL Server szyfrowania do użycia z usługą Azure Key Vault. W tym temacie wyjaśniono, jak toouse integracji magazynu kluczy Azure z maszyn wirtualnych programu SQL Server utworzone za pomocą Menedżera zasobów."
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
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="9453e-104">Konfigurowanie integracji magazynu kluczy Azure dla programu SQL Server na maszynach wirtualnych Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="9453e-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9453e-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9453e-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="9453e-106">Wdrożenie klasyczne</span><span class="sxs-lookup"><span data-stu-id="9453e-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9453e-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="9453e-107">Overview</span></span>
<span data-ttu-id="9453e-108">Istnieje wiele funkcji szyfrowania programu SQL Server, takich jak [przezroczystego szyfrowania danych (funkcji TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [szyfrowania na poziomie kolumny (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), i [szyfrowania kopii zapasowych](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="9453e-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="9453e-109">Te formy szyfrowania wymaga toomanage i przechowywania kluczy kryptograficznych hello używanego do szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="9453e-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="9453e-110">Witaj usługi Azure Key Vault (AKV) jest zaprojektowana tooimprove hello zabezpieczeń i zarządzanie tych kluczy w lokalizacji bezpieczne i wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="9453e-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="9453e-111">Witaj [Łącznik usług SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) włącza te klucze z usługi Azure Key Vault toouse programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9453e-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

<span data-ttu-id="9453e-112">Zostanie uruchomiony program SQL Server z lokalnej maszyny są [kroki można wykonać tooaccess usługi Azure Key Vault z komputera lokalnego programu SQL Server](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="9453e-112">If you running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="9453e-113">Jednak dla programu SQL Server na maszynach wirtualnych Azure, można oszczędzić czas za pomocą hello *integracji magazynu kluczy Azure* funkcji.</span><span class="sxs-lookup"><span data-stu-id="9453e-113">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="9453e-114">Gdy ta funkcja jest włączona, automatycznie jest instalowana hello Łącznik usług SQL Server, konfiguruje tooaccess dostawcy EKM hello Azure Key Vault i tworzy tooallow poświadczeń hello możesz tooaccess Twojego magazynu.</span><span class="sxs-lookup"><span data-stu-id="9453e-114">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="9453e-115">Jeśli użytkownik przeglądał hello kroki hello wcześniej wymienionymi lokalnej dokumentacji, zobaczysz, że ta funkcja pozwala zautomatyzować kroki 2 i 3.</span><span class="sxs-lookup"><span data-stu-id="9453e-115">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="9453e-116">jedyną operacją Hello nadal musisz toodo ręcznie jest toocreate hello — magazyn kluczy i kluczy.</span><span class="sxs-lookup"><span data-stu-id="9453e-116">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="9453e-117">Dostępne jest zautomatyzowany hello wszystkie ustawienia maszyny wirtualnej SQL.</span><span class="sxs-lookup"><span data-stu-id="9453e-117">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="9453e-118">Po ukończeniu tej konfiguracji tej funkcji można wykonywać toobegin instrukcje T-SQL szyfrowania z bazy danych lub kopii zapasowych w zwykły sposób.</span><span class="sxs-lookup"><span data-stu-id="9453e-118">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="9453e-119">Włączanie i konfigurowanie Integracja</span><span class="sxs-lookup"><span data-stu-id="9453e-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="9453e-120">Można włączyć integracja podczas inicjowania obsługi lub skonfiguruj ją dla istniejących maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9453e-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="9453e-121">Nowe maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="9453e-121">New VMs</span></span>
<span data-ttu-id="9453e-122">W przypadku udostępniania nowej maszyny wirtualnej programu SQL Server za pomocą Menedżera zasobów hello Azure portal udostępnia tooenable krok Integracja magazynu kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="9453e-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, hello Azure portal provides a step tooenable Azure Key Vault integration.</span></span> <span data-ttu-id="9453e-123">Funkcja usługi Azure Key Vault Hello jest dostępna tylko w przypadku hello Enterprise, Developer i wersji ewaluacyjnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9453e-123">hello Azure Key Vault feature is available only for hello Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![Integracja magazynu kluczy Usług SQL Azure](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="9453e-125">Aby uzyskać szczegółowe wskazówki dotyczące inicjowania obsługi administracyjnej, zobacz [Aprowizowanie maszyny wirtualnej programu SQL Server w portalu Azure hello](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="9453e-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="9453e-126">Istniejące maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="9453e-126">Existing VMs</span></span>
<span data-ttu-id="9453e-127">W przypadku istniejących maszyn wirtualnych programu SQL Server należy wybrać maszyny wirtualnej programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9453e-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="9453e-128">Następnie wybierz hello **konfigurację programu SQL Server** sekcji hello **ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="9453e-128">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Integracja programu SQL dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="9453e-130">W hello **konfigurację programu SQL Server** bloku, kliknij hello **Edytuj** przycisku na powitania sekcja Integracja magazynu kluczy automatycznego.</span><span class="sxs-lookup"><span data-stu-id="9453e-130">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated Key Vault integration section.</span></span>

![Konfigurowanie integracja SQL dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="9453e-132">Po zakończeniu kliknij przycisk hello **OK** przycisk u dołu hello hello **konfigurację programu SQL Server** toosave bloku zmiany.</span><span class="sxs-lookup"><span data-stu-id="9453e-132">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="9453e-133">Można również skonfigurować integracja przy użyciu szablonu.</span><span class="sxs-lookup"><span data-stu-id="9453e-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="9453e-134">Aby uzyskać więcej informacji, zobacz [szablonu Azure Szybki Start dla usługi Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span><span class="sxs-lookup"><span data-stu-id="9453e-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

