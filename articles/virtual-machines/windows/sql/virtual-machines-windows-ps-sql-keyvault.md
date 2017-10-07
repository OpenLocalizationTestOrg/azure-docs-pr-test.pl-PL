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
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a>Konfigurowanie integracji magazynu kluczy Azure dla programu SQL Server na maszynach wirtualnych Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-ps-sql-keyvault.md)
> * [Wdrożenie klasyczne](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Omówienie
Istnieje wiele funkcji szyfrowania programu SQL Server, takich jak [przezroczystego szyfrowania danych (funkcji TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [szyfrowania na poziomie kolumny (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), i [szyfrowania kopii zapasowych](https://msdn.microsoft.com/library/dn449489.aspx). Te formy szyfrowania wymaga toomanage i przechowywania kluczy kryptograficznych hello używanego do szyfrowania. Witaj usługi Azure Key Vault (AKV) jest zaprojektowana tooimprove hello zabezpieczeń i zarządzanie tych kluczy w lokalizacji bezpieczne i wysokiej dostępności. Witaj [Łącznik usług SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) włącza te klucze z usługi Azure Key Vault toouse programu SQL Server.

Zostanie uruchomiony program SQL Server z lokalnej maszyny są [kroki można wykonać tooaccess usługi Azure Key Vault z komputera lokalnego programu SQL Server](https://msdn.microsoft.com/library/dn198405.aspx). Jednak dla programu SQL Server na maszynach wirtualnych Azure, można oszczędzić czas za pomocą hello *integracji magazynu kluczy Azure* funkcji.

Gdy ta funkcja jest włączona, automatycznie jest instalowana hello Łącznik usług SQL Server, konfiguruje tooaccess dostawcy EKM hello Azure Key Vault i tworzy tooallow poświadczeń hello możesz tooaccess Twojego magazynu. Jeśli użytkownik przeglądał hello kroki hello wcześniej wymienionymi lokalnej dokumentacji, zobaczysz, że ta funkcja pozwala zautomatyzować kroki 2 i 3. jedyną operacją Hello nadal musisz toodo ręcznie jest toocreate hello — magazyn kluczy i kluczy. Dostępne jest zautomatyzowany hello wszystkie ustawienia maszyny wirtualnej SQL. Po ukończeniu tej konfiguracji tej funkcji można wykonywać toobegin instrukcje T-SQL szyfrowania z bazy danych lub kopii zapasowych w zwykły sposób.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a>Włączanie i konfigurowanie Integracja
Można włączyć integracja podczas inicjowania obsługi lub skonfiguruj ją dla istniejących maszyn wirtualnych.

### <a name="new-vms"></a>Nowe maszyny wirtualne
W przypadku udostępniania nowej maszyny wirtualnej programu SQL Server za pomocą Menedżera zasobów hello Azure portal udostępnia tooenable krok Integracja magazynu kluczy Azure. Funkcja usługi Azure Key Vault Hello jest dostępna tylko w przypadku hello Enterprise, Developer i wersji ewaluacyjnej programu SQL Server.

![Integracja magazynu kluczy Usług SQL Azure](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

Aby uzyskać szczegółowe wskazówki dotyczące inicjowania obsługi administracyjnej, zobacz [Aprowizowanie maszyny wirtualnej programu SQL Server w portalu Azure hello](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Istniejące maszyny wirtualne
W przypadku istniejących maszyn wirtualnych programu SQL Server należy wybrać maszyny wirtualnej programu SQL Server. Następnie wybierz hello **konfigurację programu SQL Server** sekcji hello **ustawienia** bloku.

![Integracja programu SQL dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

W hello **konfigurację programu SQL Server** bloku, kliknij hello **Edytuj** przycisku na powitania sekcja Integracja magazynu kluczy automatycznego.

![Konfigurowanie integracja SQL dla istniejących maszyn wirtualnych](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

Po zakończeniu kliknij przycisk hello **OK** przycisk u dołu hello hello **konfigurację programu SQL Server** toosave bloku zmiany.

> [!NOTE]
> Można również skonfigurować integracja przy użyciu szablonu. Aby uzyskać więcej informacji, zobacz [szablonu Azure Szybki Start dla usługi Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

