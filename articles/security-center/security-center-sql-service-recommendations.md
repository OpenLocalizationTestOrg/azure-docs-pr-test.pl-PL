---
title: "aaaProtecting Azure SQL service i danych w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten adres dokumentu zalecenia w Centrum zabezpieczeń Azure, które ułatwiają ochronę danych i usługą SQL platformy Azure i są aktualizowane zgodnie z zasadami zabezpieczeń."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a>Ochrona usługi Azure SQL i danych w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure analizuje hello stan zabezpieczeń zasobów platformy Azure. Jeśli Centrum zabezpieczeń zostanie zidentyfikowana potencjalnych luk w zabezpieczeniach, tworzy zaleceń, które przeprowadzają użytkownika przez proces konfigurowania kontrolek hello potrzebne hello.  Zalecenia dotyczące zastosować tooAzure typy zasobów: maszynach wirtualnych (VM), sieci, SQL i danych i aplikacji.

W tym artykule opisano zalecenia dotyczące usługi SQL tooAzure i danych. Zalecenia Centrum wokół Włączanie inspekcji baz danych, włączenie szyfrowania dla baz danych i włączenie szyfrowania konta magazynu Azure i serwerów SQL platformy Azure.  Użyj hello poniższej tabeli jako toohelp odwołanie zrozumieć hello dostępne SQL service i dane zalecenia i jak każdej z nich działa w przypadku zastosowania.

## <a name="available-sql-service-and-data-recommendations"></a>Dostępne zalecenia usługi i danych SQL
| Zalecenie | Opis |
| --- | --- |
| [Włączanie inspekcji i wykrywania zagrożeń na serwerach SQL](security-center-enable-auditing-on-sql-servers.md) |Zaleca się włączenie inspekcji i wykrywania zagrożeń dla serwerów SQL platformy Azure (usługą SQL platformy Azure; nie zawiera SQL uruchomionych na maszynach wirtualnych). |
| [Włączanie inspekcji i wykrywania zagrożeń w bazach danych SQL](security-center-enable-auditing-on-sql-databases.md) |Zaleca się włączenie inspekcji i wykrywania zagrożeń dla baz danych Azure SQL (usługą SQL platformy Azure; nie zawiera SQL uruchomionych na maszynach wirtualnych). |
| [Funkcja przezroczystego szyfrowania danych, Włącz bazy danych SQL](security-center-enable-transparent-data-encryption.md) |Zaleca się, aby włączyć szyfrowanie dla bazy danych SQL (tylko usługa Azure SQL). |

## <a name="see-also"></a>Zobacz też
toolearn więcej informacji na temat zaleceń, które są stosowane tooother typów zasobów platformy Azure, zobacz następujące hello:

* [Ochrona maszyn wirtualnych w Centrum zabezpieczeń Azure](security-center-virtual-machine-recommendations.md)
* [Ochrona aplikacji w Centrum zabezpieczeń Azure](security-center-application-recommendations.md)
* [Ochrona sieci w Centrum zabezpieczeń Azure](security-center-network-recommendations.md)

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
