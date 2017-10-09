---
title: "aaaManage usługi Azure Key Vault przy użyciu automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu hello usługi Automatyzacja Azure może być używane toomanage usługi Azure Key Vault."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a>Zarządzanie usługą Azure Key Vault za pomocą usługi Automatyzacja Azure
W tym przewodniku przedstawiono usługi Automatyzacja Azure toohello i jak mogą być używane toosimplify zarządzania kluczy i kluczy tajnych w magazynie kluczy Azure.

## <a name="what-is-azure-automation"></a>Co to jest Azure Automation?
[Automatyzacja Azure](../automation/automation-intro.md) jest usługą platformy Azure, dla uproszczenia zarządzania chmurą za pośrednictwem automatyzacji procesu i konfiguracji żądanego stanu. Zadania ręczne, powtarzane długotrwałe i podatne na błędy przy użyciu usługi Automatyzacja Azure, może być automatycznych tooincrease niezawodności, wydajności i toovalue czasu dla Twojej organizacji.

Automatyzacja Azure umożliwia aparatowi wykonywania przepływów pracy wysoce niezawodne, wysokiej dostępności, która może obsłużyć toomeet potrzeb. W automatyzacji Azure procesów może być rozpoczęte ręcznie, przez systemy 3rd firmy lub w zaplanowanych odstępach czasu tak, aby zadania stanie dokładnie w razie potrzeby.

Obniżenie kosztów operacyjnych i zwolnić IT i toofocus personelu DevOps pracy dodającego wartość biznesową, przenosząc toobe zadań zarządzania z chmury uruchamiane automatycznie przez usługi Automatyzacja Azure.

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a>Jak usługi Automatyzacja Azure ułatwia zarządzanie usługą Azure Key Vault?
Magazyn kluczy można zarządzać w automatyzacji Azure za pomocą hello [poleceń cmdlet usługi Key Vault AzureRM](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) i [poleceń cmdlet klasycznej usługi Azure Key Vault](https://msdn.microsoft.com/library/azure/dn868052.aspx). Hello Azure modułu Zarządzanie klasycznym usługi Key Vault jest dostępny automatycznie w automatyzacji Azure i zaimportować hello [AzureRM KeyVault modułu](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) w automatyzacji Azure tak, aby można było wykonać wiele zarządzania infrastrukturą usługi Key Vault zadania w ramach usługi hello. Tych poleceń cmdlet usługi Automatyzacja Azure, za pomocą poleceń cmdlet powitania dla innych usług platformy Azure, tooautomate złożone zadania może również łączyć 3 systemów firm i usług Azure.

Za pomocą poleceń cmdlet usługi Azure Key Vault hello można wykonać te zadania, między innymi: 

* Tworzenie i Konfigurowanie magazynu kluczy
* Tworzenie lub Importowanie klucza
* Utwórz lub zaktualizuj klucz tajny
* Atrybuty aktualizacji klucza
* Pobierz klucz lub klucz tajny
* Usuwanie klucza lub klucza tajnego

Oto kilka przykładów przy użyciu programu PowerShell toomanage Key Vault:  

* [Usługi Azure Key Vault - krok po kroku](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [Instalowanie i konfigurowanie usługi Azure Key Vault](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello usługi Automatyzacja Azure i jak mogą być używane toomanage usługi Azure Key Vault, wykonaj te toolearn łącza więcej informacji na temat automatyzacji Azure.

* Zobacz hello usługi Automatyzacja Azure [Wprowadzenie — samouczek](../automation/automation-first-runbook-graphical.md).
* Zobacz hello [skryptów programu PowerShell magazynu kluczy Azure](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).

