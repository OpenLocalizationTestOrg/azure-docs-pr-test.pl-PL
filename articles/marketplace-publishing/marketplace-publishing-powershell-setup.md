---
title: "aaaSet się toocreate PowerShell maszyny Wirtualnej dla hello Marketplace | Dokumentacja firmy Microsoft"
description: "Instrukcje dotyczące konfigurowania programu Azure PowerShell i używać go jako opcjonalny procesu przepływu toodeploy obrazów maszyny Wirtualnej toocreate i sprzedawać w, hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a>Konfigurowanie programu Azure PowerShell toocreate ofertę hello Azure Marketplace
Aby uzyskać szczegółowe informacje na temat tooset się programu PowerShell w programie Azure, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). Proste podejście jest toouse hello certyfikatu metodę, która pobiera i importuje certyfikatu wymagane do uwierzytelniania. Witaj tooobtain potrzebne certyfikatów, należy użyć hello **Get-AzurePublishSettingsFile** polecenia cmdlet. Zapisz plik hello, po wyświetleniu monitu. certyfikat hello tooimport w sesji programu PowerShell, użyj hello **AzurePublishSettingsFile importu** polecenia cmdlet.

tooconfigure i zapisać hello wspólnej Microsoft Azure subskrypcji ustawienia hello sesji programu PowerShell, użyj hello **AzureSubscription zestaw** i **AzureSubscription wybierz** poleceń cmdlet:

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

pierwsze polecenie Hello kojarzy domyślne konto magazynu z subskrypcji hello (wymagane dla niektórych operacji inicjowania obsługi administracyjnej maszyn wirtualnych).  Witaj drugi sprawia, że subskrypcja hello hello obecną (rozpoznawane przez inne polecenia cmdlet).

## <a name="see-also"></a>Zobacz też
* [Wprowadzenie: jak toopublish toohello oferta portalu Azure Marketplace](marketplace-publishing-getting-started.md)
* [Tworzenie obrazu maszyny wirtualnej dla hello Marketplace](marketplace-publishing-vm-image-creation.md)

