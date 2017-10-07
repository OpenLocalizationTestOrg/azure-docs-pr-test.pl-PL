---
title: "problemy dostępności aaaApplication i usługi Microsoft Azure Cloud Services często zadawane pytania | Dokumentacja firmy Microsoft"
description: "W tym artykule wymieniono hello często zadawane pytania dotyczące aplikacji i dostępności usługi dla usługi w chmurze Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Aplikacji i problemów dotyczących dostępności usługi dla usług Azure Cloud Services: często zadawane pytania (FAQ)

Ten artykuł zawiera często zadawane pytania dotyczące aplikacji i problemów dotyczących dostępności usługi dla [usługi w chmurze Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Można również znaleźć hello [strony rozmiar maszyny Wirtualnej usługi w chmurze](cloud-services-sizes-specs.md) dla informacji o rozmiarze.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a>Moje roli został ponownie przetworzony. Były aktualizację wprowadzanie dla usługi w chmurze?
Około raz w miesiącu, firma Microsoft udostępnia nową wersję systemu operacyjnego gościa dla maszyn wirtualnych systemu Windows Azure PaaS. System operacyjny gościa jest tylko jeden taki aktualizacji w potoku hello. Inne czynniki mogą mieć wpływ zlecenia. Ponadto Azure działa na setki tysięcy komputerów. W związku z tym jest niemożliwe toopredict hello dokładnej dacie i godzinie, w gdy role zostanie ponownie uruchomiony. Aktualizujemy hello gościa systemu operacyjnego zaktualizować źródła danych RSS z hello najnowsze informacje, które zostały, ale należy rozważyć, które zostały zgłoszone toobe czasu przybliżona wartość. Firma Microsoft wiedzą, że jest to powodować problemy dla klientów i pracy toolimit planu lub dokładnie czas ponownego uruchomienia.

Aby uzyskać szczegółowe informacje o najnowsze aktualizacje systemu operacyjnego gościa, zobacz [wersji systemu operacyjnego gościa Azure i zgodność pakietu SDK](cloud-services-guestos-update-matrix.md).

Pomocne informacje dotyczące ponownego uruchomienia i wskaźniki szczegóły tootechnical aktualizacji systemu operacyjnego hosta i gościa znajdują się w temacie hello MSDN wpisie w blogu [roli wystąpienia uruchamia ponownie z powodu uaktualnienia tooOS](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a>Dlaczego hello pierwszego żądania toomy usługi w chmurze po pewnym czasie hello usługi trwa dłużej niż zwykle?
Powitania serwera sieci Web odebrania pierwszego żądania hello najpierw rekompiluje hello kodu, a następnie je przetwarza żądanie hello. Który jest dlaczego hello pierwszego żądania trwa dłużej niż hello innych użytkowników. Domyślnie pula aplikacji hello pobiera Zamknij w przypadku braku aktywności użytkownika. Pula aplikacji Hello odtwarzana również domyślnie co 1,740 minut (29 godzin).

Pule aplikacji usług Internet Information Services (IIS) może być niestabilny stanów tooavoid okresowo odtwarzania, które może spowodować awarię tooapplication, zawiesza się lub przecieki pamięci.

Hello następujące dokumenty ułatwią zrozumienie i ograniczenia tego problemu:
* [Ustalania powolnego ładowania początkowego dla usług IIS](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [Pierwsze żądanie aplikacji sieci web usług IIS 7.5 po bardzo wolno odtwarzania puli aplikacji](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

Jeśli chcesz toochange hello domyślne zachowanie usług IIS, należy toouse uruchomienia zadania, ponieważ ręcznie zastosować wystąpień roli sieci Web toohello zmian, zmiany powitania po pewnym czasie zostaną utracone.

Aby uzyskać więcej informacji, zobacz [sposób uruchamiania tooconfigure i uruchom zadania dla usługi w chmurze](cloud-services-startup-tasks.md).
