---
title: "Zwróć uwagę, wycofywanie 1 rodziny aaaGuest systemu operacyjnego | Dokumentacja firmy Microsoft"
description: "Zawiera informacje na temat sposobu i sytuacji wystąpił wycofania hello 1 rodziny systemu operacyjnego gościa Azure toodetermine, jeśli ma wpływ"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a>Powiadomienie wycofanie 1 rodziny systemu operacyjnego gościa
najpierw ogłoszono Hello wycofanie 1 rodziny systemu operacyjnego na 1 czerwca 2013.

**2 września 2014** hello systemu operacyjnego gościa Azure (systemu operacyjnego gościa) rodziny 1.x, które jest oparte na systemie operacyjnym hello systemu Windows Server 2008, oficjalnie została wycofana. Wszystkie próby toodeploy nowych usług lub uaktualniania istniejących usług przy użyciu 1 rodziny zakończy się niepowodzeniem z komunikatem o błędzie informujący, że hello się, że 1 rodziny systemu operacyjnego gościa został wycofany.

**3 listopada 2014 r.** zakończone rozszerzoną obsługę 1 rodziny systemu operacyjnego gościa i jest w pełni wycofane. Wpłynie na wszystkie usługi nadal na 1 rodziny. Może zatrzymać tych usług w dowolnym momencie. Nie ma żadnej gwarancji, że usługi będą nadal toorun, chyba że należy ręcznie uaktualnić je samodzielnie.

Jeśli masz dodatkowe pytania, odwiedź stronę hello [fora usługi w chmurze](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) lub [skontaktuj się z pomocą techniczną platformy Azure](https://azure.microsoft.com/support/options/).

## <a name="are-you-affected"></a>Możesz dotyczy?
Usługi w chmurze są uwzględnione w przypadku jednego z następujących hello warunków:

1. Ma wartość "rodziny systemów operacyjnych ="1"jawnie określone w pliku pliku ServiceConfiguration.cscfg powitania dla usługi w chmurze.
2. Nie masz wartość dla rodziny systemów operacyjnych jawnie określone w pliku pliku ServiceConfiguration.cscfg powitania dla usługi w chmurze. Obecnie hello system używa hello domyślna wartość "1" w tym przypadku.
3. Witaj portalu Azure zawiera wartość rodziny System operacyjny gościa jako "Windows Server 2008".

toofind, które usługi w chmurze są uruchomione rodziny systemów operacyjnych, które można uruchomić hello następującego skryptu programu Azure PowerShell, ale należy [Konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs) pierwszy. Aby uzyskać więcej informacji na powitania skryptu, zobacz [Azure gościa systemu operacyjnego rodziny 1 End życia: czerwca 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

Usługi w chmurze wpłyną wycofanie 1 rodziny systemu operacyjnego, jeśli kolumna rodziny systemów operacyjnych hello w danych wyjściowych skryptu hello jest pusta lub zawiera wartość "1".

## <a name="recommendations-if-you-are-affected"></a>Zalecenia, jeśli ma wpływ
Firma Microsoft zaleca się, że migracja z tooone ról usługi w chmurze rodzin systemu operacyjnego gościa hello obsługiwane:

**System operacyjny gościa rodziny 4.x** -Windows Server 2012 R2 *(zalecane)*

1. Upewnij się, że aplikacja korzysta z zestawu SDK 2.1 lub nowszej platformy .NET framework 4.0, 4.5 i 4.5.1.
2. Witaj rodziny systemów operacyjnych atrybutu zbyt "4" hello w pliku ServiceConfiguration.cscfg pliku zestawu i wdrożenie usługi w chmurze.

**System operacyjny gościa rodziny 3.x** -Windows Server 2012

1. Upewnij się, że aplikacja korzysta z zestawu SDK 1,8 lub nowszej platformy .NET framework 4.0 lub 4.5.
2. Witaj rodziny systemów operacyjnych atrybutu zbyt "3" hello w pliku ServiceConfiguration.cscfg pliku zestawu i wdrożenie usługi w chmurze.

**System operacyjny gościa rodziny 2.x** -Windows Server 2008 R2

1. Upewnij się, że aplikacja korzysta z zestawu SDK 1.3 i powyżej platformy .NET framework w wersji 3.5 lub 4.0.
2. Witaj rodziny systemów operacyjnych atrybutu zbyt "2" hello w pliku ServiceConfiguration.cscfg pliku zestawu i wdrożenie usługi w chmurze.

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a>Rozszerzona obsługa 1 rodziny systemu operacyjnego gościa zakończył 3 listopada 2014 r.
Usługi w chmurze rodziny systemów operacyjnych gościa 1 nie są już obsługiwane. Migrowanie wyłączone rodziny 1, jak przerw w działaniu usługi tooavoid możliwe.  

## <a name="next-steps"></a>Następne kroki
Przejrzyj hello najnowszych [wersje systemu operacyjnego gościa](cloud-services-guestos-update-matrix.md).
