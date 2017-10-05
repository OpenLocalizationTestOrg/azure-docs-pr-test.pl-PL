---
title: "Migracja z usługi Azure RemoteApp do Essentials program Citrix XenApp | Dokumentacja firmy Microsoft"
description: "Jak przeprowadzić migrację z usługi Azure RemoteApp do Essentials program XenApp Citrix"
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
ms.openlocfilehash: fcd96a466d1c0dad17d7012308281ef868463b19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-from-azure-remoteapp-to-citrix-xenapp-essentials"></a>Migracja z usługi Azure RemoteApp do program Citrix XenApp Essentials

Jeśli używasz usługi Azure RemoteApp, i chcesz przeprowadzić migrację do programu Citrix program XenApp Essentials, istnieje kilka wymagań wstępnych należy wziąć pod uwagę. Najpierw należy odczytać firmy Citrix [przewodnik krok po kroku wdrożenia technicznego Essentials program XenApp Citrix](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) i jego [online biblioteki technicznej](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html). 

## <a name="prerequisite-steps-for-migration"></a>Wstępnie wymagane kroki dotyczące migracji

1. Utwórz nową sieć wirtualną lub określić Azure sieci wirtualnej, który w usłudze Azure Resource Manager w którym będą wdrażane Essentials program XenApp Citrix. Usługa Azure RemoteApp używa klasycznego portalu Azure; Citrix program XenApp Essentials obsługuje tylko usługi Azure Resource Manager.  
2. Upewnij się, że wybrana sieć wirtualna ma dostęp do kontrolera domeny, ponieważ Citrix obsługuje tylko wdrożenia hybrydowego. Jeśli korzystają z wdrożeniem usługi Azure RemoteApp w chmurze, upewnij się, że sieci wirtualnej ma dostęp do kontrolera domeny usługi Active Directory. Można również użyć usługi Azure Active Directory Domain Services (Azure AD DS). 
3. Upewnij się, że DNS jest skonfigurowany prawidłowo dla sieci wirtualnej, tak że przyłączenie do domeny zakończy się pomyślnie na pierwsza próba. Utwórz maszynę wirtualną (VM) w wybranej sieci wirtualnej i wykonaj przyłączenie do domeny ręcznie, aby sprawdzić, czy nazwy DNS i domeny przyłączyć działa zgodnie z oczekiwaniami. Dzięki temu możesz są pomyślnie wdrożyć Essentials program XenApp Citrix po raz pierwszy. 
4. W razie potrzeby Utwórz sieć wirtualną komunikacji równorzędnej między klasycznego portalu sieci wirtualnej platformy Azure są używane z usługą Azure RemoteApp i sieci wirtualnej Azure Resource Manager. Ten proces komunikacji równorzędnej działa, jeśli dwie sieci znajdują się w tym samym regionie. Jeśli nie, podłącz sieci wirtualnych sieci za pomocą sieci VPN typu lokacja lokacja. 
5. W razie potrzeby odczytu [jak przeprowadzić migrację danych do i z usługi Azure RemoteApp](remoteapp-migrate.md). 
6. Aktualizowanie istniejącego obrazu usługi Azure RemoteApp uwzględnienie składnika Citrix VDA (Aby uzyskać instrukcje, zobacz dokumentację produktu Citrix). 
7. Przejdź do portalu Azure Marketplace i rozpoczęcie wdrażania Essentials program XenApp Citrix.

## <a name="other-considerations"></a>Inne zagadnienia

Należy pamiętać o następujących kwestiach dodatkowe podczas migracji:
- Citrix program XenApp Essentials obsługuje tylko wdrożenia hybrydowego. Innymi słowy wymaga dostępu do sieci z kontrolerem domeny w celu wykonywania przyłączania do domeny. Jeśli używasz wdrożeń w chmurze Azure RemoteApp używać usług Azure AD DS lub upewnij się, że sieci wirtualnej ma dostęp do usługi Active Directory do przyłączania do domeny. 
- Aby dowiedzieć się, jak przenieść dane użytkownika na Citrix program XenApp Essentials, zobacz [jak przeprowadzić migrację danych do i z usługi Azure RemoteApp](remoteapp-migrate.md). 
- Citrix program XenApp Essentials obsługuje tylko konta usługi Active Directory. Nie obsługuje kont Microsoft (takich jak outlook.com, msn.com lub usługi). 

## <a name="citrix-xenapp-essentials-billing"></a>Program XenApp Citrix podstawowe informacje dotyczące rozliczeń

Aby uzyskać szczegółowe informacje o cenach, zobacz [— często zadawane pytania](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) i [artykuł z omówieniem Citrix](https://www.citrix.com/global-partners/microsoft/remote-app.html). Istnieją trzy składniki rozliczeń do Essentials program XenApp Citrix:

- Opłata usługi Citrix, czyli $12 na użytkownika miesięcznie. Podobnie jak wszystkie zakupy w witrynie Azure Marketplace jest to rozliczony formę płatności skojarzone z subskrypcją platformy Azure. W przypadku klientów Enterprise Agreement (EA) nie można używać środków pieniężnych subskrypcji platformy Azure. 
- Zdalne usługi danych (RDS) licencji dostępu klienta (CAL). Obecnie można kupić opłaty dostępu zdalnego jest powiązany z płatności Essentials program XenApp Citrix dla $6,25. W przypadku klienta EA umożliwia środków pieniężnych subskrypcji Azure płacić za to. Jeśli chcesz korzystać z istniejących RDS CAL, skontaktuj się z nami pod adresem [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com), dlatego firma Microsoft może dotyczyć to rachunku. 
- Azure obliczeniowej i pamięci masowej. Jest to koszt magazynu Azure i używane zużycie obliczeniowe dla maszyn wirtualnych. Należy pamiętać o cenach podczas wybierania gęstość rozmiaru i użytkownika maszyny Wirtualnej. W przypadku klienta EA umożliwia środków pieniężnych subskrypcji Azure płacić za to.

Jeśli nadal masz pytania, możesz:
- Wiadomość e-mail na adres [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).
- [Skontaktuj się z pomocą techniczną platformy Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Rozpocznij od [otwieranie sprawy pomocy technicznej platformy Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ułatwiające pracę z wymagań wstępnych kroki 1 – 5. Kroki od 6 do 7 skontaktuj się z Citrix przez otwarcie biletu pomocy technicznej w portalu zarządzania Citrix. 
