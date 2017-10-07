---
title: "aaaMigrate z usługi Azure RemoteApp tooCitrix Essentials program XenApp | Dokumentacja firmy Microsoft"
description: "Jak toomigrate z usługi Azure RemoteApp tooCitrix program XenApp Essentials"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 695a8165-3454-4855-8e21-f2eb2c61201b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aa3ce28bc5a86d5b1dd3408196d51935395f55c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toocitrix-xenapp-essentials"></a>Migrowanie z usługi Azure RemoteApp tooCitrix program XenApp Essentials

Jeśli używasz usługi Azure RemoteApp, tooCitrix toomigrate program XenApp Essentials, istnieje kilka wymagań wstępnych tookeep pamiętać. Najpierw należy odczytać firmy Citrix [przewodnik krok po kroku wdrożenia technicznego Essentials program XenApp Citrix](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) i jego [online biblioteki technicznej](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html). 

## <a name="prerequisite-steps-for-migration"></a>Wstępnie wymagane kroki dotyczące migracji

1. Utwórz nową sieć wirtualną lub określić Azure sieci wirtualnej, który w usłudze Azure Resource Manager w którym będą wdrażane Essentials program XenApp Citrix. Usługa Azure RemoteApp używa hello klasycznego portalu Azure; Citrix program XenApp Essentials obsługuje tylko usługi Azure Resource Manager.  
2. Upewnij się, że tej sieci wirtualnej hello, wybranych ma sieci dostępu tooyour kontrolera domeny, ponieważ Citrix obsługuje tylko wdrożenia hybrydowego. Jeśli używasz usługi Azure RemoteApp wdrożeń w chmurze zapewnić sieci wirtualnej kontrolera domeny usługi Active Directory tooan dostępu do sieci. Można również użyć usługi Azure Active Directory Domain Services (Azure AD DS). 
3. Upewnij się, że DNS jest poprawnie skonfigurowany na potrzeby hello sieci wirtualnej, tak że przyłączenie do domeny zakończy się pomyślnie na pierwsza próba powitalne. Utwórz maszynę wirtualną (VM) w sieci wirtualnej hello wybranych i wykonać tooverify sprzężenia ręczne domeny tego hello DNS i przyłączanie do domeny działa zgodnie z oczekiwaniami. Dzięki temu będą hello pomyślnie wdrożyć Essentials program XenApp Citrix po raz pierwszy. 
4. W razie potrzeby Utwórz sieć wirtualną komunikacji równorzędnej między klasycznego portalu sieci wirtualnej platformy Azure są używane z usługą Azure RemoteApp i sieci wirtualnej Azure Resource Manager. Ten proces komunikacji równorzędnej działa, jeśli Witaj dwie sieci znajdują się w hello sam region. Jeśli nie, użyj sieci wirtualnych hello tooconnect sieci VPN typu lokacja lokacja dla sieci. 
5. W razie potrzeby odczytu [jak toomigrate danych do i z usługi Azure RemoteApp](remoteapp-migrate.md). 
6. Aktualizacja z istniejącej usługi Azure RemoteApp obrazu tooinclude hello składnika Citrix VDA (Aby uzyskać instrukcje, zobacz hello Citrix dokumentacji). 
7. Przejdź toohello portalu Azure Marketplace i rozpocząć wdrażanie Essentials program XenApp Citrix.

## <a name="other-considerations"></a>Inne zagadnienia

Należy pamiętać o hello następujące dodatkowe zagadnienia, podczas migracji:
- Citrix program XenApp Essentials obsługuje tylko wdrożenia hybrydowego. Innymi słowy wymaga dostępu sieciowego tooa kontrolera domeny w przyłączenie do domeny tooperform kolejności. Jeśli używasz wdrożeń w chmurze Azure RemoteApp używać usług Azure AD DS lub upewnij się, że sieci wirtualnej ma tooActive dostępu do katalogu do przyłączania do domeny. 
- toolearn tooCitrix danych użytkownika toomove program XenApp Essentials, zobacz temat [jak toomigrate danych do i z usługi Azure RemoteApp](remoteapp-migrate.md). 
- Citrix program XenApp Essentials obsługuje tylko konta usługi Active Directory. Nie obsługuje kont Microsoft (takich jak outlook.com, msn.com lub usługi). 

## <a name="citrix-xenapp-essentials-billing"></a>Program XenApp Citrix podstawowe informacje dotyczące rozliczeń

Aby uzyskać szczegółowe informacje o cenach, zobacz hello [— często zadawane pytania](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) i [artykuł z omówieniem Citrix](https://www.citrix.com/global-partners/microsoft/remote-app.html). Istnieją trzy składniki rozliczeń Essentials program XenApp tooCitrix:

- Witaj Citrix usługi opłata jest $12 na użytkownika miesięcznie. Podobnie jak wszystkie zakupy w witrynie Azure Marketplace to formę płatności rachunku toohello skojarzone z subskrypcją platformy Azure. W przypadku klientów Enterprise Agreement (EA) nie można używać środków pieniężnych subskrypcji platformy Azure. 
- Zdalne usługi danych (RDS) licencji dostępu klienta (CAL). Obecnie można kupić hello opłata dostępu zdalnego jest powiązane z hello Citrix program XenApp podstawowe informacje dotyczące płatności dla $6,25. W przypadku klienta EA służy toopay środków pieniężnych subskrypcji platformy Azure dla tego. Jeśli chcesz toouse Twojego istniejących RDS CAL, skontaktuj się z nami na [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com), więc można zastosować tego rachunku tooyour. 
- Azure obliczeniowej i pamięci masowej. Jest koszt usługi Azure storage hello i zużycie obliczeniowe dla maszyn wirtualnych hello używane. Należy pamiętać o cenach podczas wybierania gęstość rozmiaru i użytkownika maszyny Wirtualnej. W przypadku klienta EA służy toopay środków pieniężnych subskrypcji platformy Azure dla tego.

Jeśli nadal masz pytania, możesz:
- Wiadomość e-mail na adres [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).
- [Skontaktuj się z pomocą techniczną platformy Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Rozpocznij od [otwieranie sprawy pomocy technicznej platformy Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toohelp z wymagań wstępnych kroki 1 – 5. Kroki od 6 do 7 skontaktuj się z Citrix przez otwarcie biletu pomocy technicznej w portalu zarządzania hello Citrix. 
