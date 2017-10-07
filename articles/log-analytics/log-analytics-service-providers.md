---
title: "aaaLog funkcji analizy dla dostawców usług | Dokumentacja firmy Microsoft"
description: "Analiza dzienników może pomóc zarządzanego dostawcy usług (MSPs) dużych przedsiębiorstw niezależni dostawcy oprogramowania (ISV) i dostawcy usług hostingowych zarządzanie i monitorowanie serwerów w lokalnym przez klienta lub infrastruktury chmury."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 3c0a93232293f90385c6c724be436cee1cf855f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-features-for-service-providers"></a>Funkcje analizy dziennika dla dostawców usług
Analiza dzienników może pomóc dostawców usługi zarządzane (MSPs), dużych przedsiębiorstw niezależnym dostawcom oprogramowania (ISV) i dostawcy usług hostingowych zarządzanie i monitorowanie serwerów w lokalnym przez klienta lub infrastruktury chmury. 

Duże przedsiębiorstwa udostępniać wiele podobieństw dostawców usług, zwłaszcza w przypadku scentralizowane zespół IT, który jest odpowiedzialny za zarządzanie IT dla wielu różnych jednostek biznesowych. Dla uproszczenia niniejszym dokumencie użyto termin hello *dostawcy usług* , ale hello tę samą funkcjonalność jest również dostępny do przedsiębiorstwa i innych klientów.

## <a name="cloud-solution-provider"></a>Cloud Solution Provider
Dla partnerów i dostawców usług, które są częścią hello [Cloud Solution Provider (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) program analizy dzienników jest jednym z hello usług platformy Azure, które są dostępne w przypadku subskrypcji dostawcy usług Kryptograficznych. 

Dla analizy dzienników hello następujące funkcje są włączone w *Cloud Solution Provider* subskrypcji.

Jako *Cloud Solution Provider* można wykonywać następujące czynności:

* Tworzenie obszarów roboczych usługi Analiza dzienników w ramach subskrypcji dzierżawy (klienta).
* Dostęp do obszarów roboczych utworzonych przez dzierżawców. 
* Dodawanie i usuwanie roboczym toohello dostępu użytkownika przy użyciu zarządzania użytkowników platformy Azure. Gdy w obszarze roboczym dzierżawcy w hello OMS portalu hello strony zarządzania użytkownikami w obszarze Ustawienia nie jest dostępna
  * Analiza dzienników nie obsługuje dostępu opartej na rolach jeszcze - nadanie użytkownika `reader` uprawnienia w portalu Azure hello pozwala toomake zmiany konfiguracji w portalu OMS hello

toolog w ramach subskrypcji dzierżawy tooa, należy identyfikator dzierżawy hello toospecify. Identyfikator dzierżawy Hello jest często ostatnia część toosign użyty adres e-mail hello w.

* W portalu OMS hello, Dodaj `?tenant=contoso.com` w adresie URL hello hello portalu. Na przykład: `mms.microsoft.com/?tenant=contoso.com`
* W programie PowerShell, użyj hello `-Tenant contoso.com` parametr przy użyciu `Add-AzureRmAccount` polecenia cmdlet
* Identyfikator dzierżawy Hello jest automatycznie dodawany używania hello `OMS portal` link z hello tooopen portalu Azure i zaloguj się w portalu OMS toohello dla obszaru roboczego hello wybrane

Jako *klienta* programu Cloud Solution Provider można wykonywać następujące czynności:

* Tworzenie dziennika analytics obszarów roboczych w ramach subskrypcji dostawcy usług Kryptograficznych
* Dostęp do obszarów roboczych utworzonych przez hello dostawcy usług Kryptograficznych
  * Użyj hello `OMS portal` link z hello tooopen portalu Azure i zaloguj się w portalu OMS toohello dla obszaru roboczego hello wybrane
* Wyświetlanie i używanie hello strony zarządzania użytkownikami w obszarze Ustawienia w portalu OMS hello

> [!NOTE]
> Witaj uwzględnione w kopii zapasowej i rozwiązań usługi Site Recovery dla analizy dzienników nie są magazyn usług odzyskiwania tooa stanie tooconnect i nie można skonfigurować w ramach subskrypcji dostawcy usług Kryptograficznych. 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a>Zarządzanie wielu klientów przy użyciu analizy dzienników
Zalecane jest tworzenie obszaru roboczego analizy dzienników dla poszczególnych klientów, którym zarządzasz. Udostępnia obszaru roboczego analizy dzienników:

* Położenia geograficznego toobe dane przechowywane. 
* Poziom szczegółowości rozliczeń 
* Izolacja danych 
* Unikatowy konfiguracji

Tworząc obszar roboczy na klienta, są możliwe tookeep oddzielnego danych poszczególnych klientów i również śledzić wykorzystanie hello każdego klienta.

Więcej informacji na temat kiedy i dlaczego toocreate wiele obszarów roboczych opisano w [Zarządzanie analytics toolog dostępu](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).

Tworzenie i Konfiguracja klienta obszarów roboczych można zautomatyzować za pomocą [PowerShell](log-analytics-powershell-workspace-configuration.md), [szablonów Resource Manager](log-analytics-template-workspace-configuration.md), lub za pomocą hello [interfejsu API REST](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).

Hello użycie szablony Menedżera zasobów dla obszaru roboczego konfiguracji umożliwia toohave wzorca konfigurację, w której można toocreate używane i skonfigurować obszarów roboczych. Można mieć pewność, że jak obszary robocze są tworzone dla klientów, które są one automatycznie skonfigurowane wymagania tooyour. Po zaktualizowaniu wymagań hello szablonu zostanie zaktualizowana i ponownie zastosować hello istniejących obszarów roboczych. Daje to pewność, że nawet istniejących obszarów roboczych spełniających określone standardy nowe.    

Podczas zarządzania wiele obszarów roboczych usługi Analiza dzienników, firma Microsoft zaleca integrowanie każdego obszaru roboczego z istniejącego systemu obsługi biletów / konsoli operacje przy użyciu hello [alerty](log-analytics-alerts.md) funkcji. Dzięki integracji z istniejących systemów, zespół pomocy technicznej mogą nadal toofollow ich znanych procesów. Analiza dzienników regularnie sprawdza każdego obszaru roboczego hello kryteriów alertu, które określisz i generuje alert, gdy potrzebny jest akcji.

Dostosowanych widoków danych, użyj hello [pulpitu nawigacyjnego](../azure-portal/azure-portal-dashboards.md) możliwości w hello portalu Azure.  

Dla poziomu wykonawczego raporty podsumowujące dane między obszarami roboczymi, korzystając z hello integrację analizy dzienników i [PowerBI](log-analytics-powerbi.md). Toointegrate z innym systemem raportowania, należy można użyć interfejsu API Search hello (za pośrednictwem programu PowerShell lub [REST](log-analytics-log-search-api.md)) toorun zapytania i eksportowanie wyników wyszukiwania.

## <a name="next-steps"></a>Następne kroki
* Zautomatyzować tworzenie i konfiguracja obszarów roboczych przy użyciu [szablonów Resource Manager](log-analytics-template-workspace-configuration.md)
* Zautomatyzować tworzenie obszarów roboczych przy użyciu [środowiska PowerShell](log-analytics-powershell-workspace-configuration.md) 
* Użyj [alerty](log-analytics-alerts.md) toointegrate z istniejącymi systemami
* Generowanie raportu podsumowania przy użyciu [usługi Power BI](log-analytics-powerbi.md)

