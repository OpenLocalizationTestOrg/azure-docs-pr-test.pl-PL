---
title: "aaaProtecting aplikacji w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten adres dokumentu zalecenia w Centrum zabezpieczeń Azure, które pomagają chronić aplikacje platformy Azure i są aktualizowane zgodnie z zasadami zabezpieczeń."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: b5fc7a9e-24b1-415f-b3b5-62a53f5dd424
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: da5e02cc2bad55c64e4da14e4e10efd6ddeab39e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a>Ochrona aplikacji w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure analizuje hello stan zabezpieczeń zasobów platformy Azure. Jeśli Centrum zabezpieczeń zostanie zidentyfikowana potencjalnych luk w zabezpieczeniach, tworzy zaleceń, które przeprowadzają użytkownika przez proces konfigurowania kontrolek hello potrzebne hello.  Zalecenia dotyczące zastosować tooAzure typy zasobów: maszynach wirtualnych (VM), sieci, SQL i aplikacji.

W tym artykule opisano zaleceń, które są stosowane tooapplications.  Aplikacji Centrum zalecenia dotyczące wdrażania zapory aplikacji sieci web.  Użyj hello poniższej tabeli jako toohelp odwołanie zrozumieć zalecenia dostępnych aplikacji hello i jak każdej z nich działa w przypadku zastosowania.

## <a name="available-application-recommendations"></a>Zalecenia dotyczące dostępnych aplikacji
| Zalecenie | Opis |
| --- | --- |
| [Dodawanie zapory aplikacji sieci Web](security-center-add-web-application-firewall.md) |Zaleca się, że wdrażania zapory aplikacji sieci web (WAF) dla punktów końcowych sieci web. Wszelkie publicznego połączonej adresu IP (IP poziomie wystąpienia lub IP równoważenia obciążenia) zawierający sieciową grupę zabezpieczeń skojarzoną z portami Otwórz przychodzący sieci web (80,443) jest wyświetlane zalecenie zapory aplikacji sieci Web.</br></br>Centrum zabezpieczeń zaleca się, że przepisy toohelp zapory aplikacji sieci Web chronić przed atakami przeznaczonych dla aplikacji sieci web na maszynach wirtualnych i środowiska usługi aplikacji. Środowisko aplikacji (ASE) jest [Premium](https://azure.microsoft.com/pricing/details/app-service/) opcji plan usługi aplikacji Azure, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować z aplikacjami usługi App service. toolearn więcej informacji na temat ASE, zobacz hello [dokumentację środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).</br></br>Wiele aplikacji sieci web w Centrum zabezpieczeń można chronić przez dodanie tych aplikacji tooyour istniejące zapory aplikacji sieci Web wdrożenia. |
| [Finalizowanie ochrony aplikacji](security-center-add-web-application-firewall.md#finalize-application-protection) |toocomplete hello konfigurację zapory aplikacji sieci Web, ruch musi być przekierowany toohello zapory aplikacji sieci Web urządzenia. Po tego zalecenia kończy hello konfiguracji niezbędne zmiany. |

## <a name="see-also"></a>Zobacz też
toolearn więcej informacji na temat zaleceń, które są stosowane tooother typów zasobów platformy Azure, zobacz następujące hello:

* [Ochrona maszyn wirtualnych w Centrum zabezpieczeń Azure](security-center-virtual-machine-recommendations.md)
* [Ochrona sieci w Centrum zabezpieczeń Azure](security-center-network-recommendations.md)
* [Ochrona usługi Azure SQL w Centrum zabezpieczeń Azure](security-center-sql-service-recommendations.md)

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
