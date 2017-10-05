---
title: Co to jest Microsoft Power BI Embedded?
description: "Usługa Power BI Embedded umożliwia integrację raportów usługi Power BI do sieci web lub aplikacji dla urządzeń przenośnych, dzięki czemu nie trzeba tworzyć niestandardowe rozwiązania."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 03649b72-b7d7-40ca-b077-12356d72d4f3
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/20/2017
ms.author: asaxton
ms.openlocfilehash: 0b5f7a2c3fd16ac32b0bc382616ca6600d378bb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>Co to jest Microsoft Power BI Embedded?
Z **Power BI Embedded**, można zintegrować raportów usługi Power BI bezpośrednio z sieci web lub aplikacji dla urządzeń przenośnych.

![](media/powerbi-embedded-whats-is/what-is.png)

Usługa Power BI Embedded jest **usługi Azure** niezależnym dostawcom oprogramowania i deweloperom aplikacji na powierzchni środowiska danych usługi Power BI w swoich aplikacjach. Deweloper zostały już utworzone w aplikacji, a te aplikacje mają własne użytkowników i zestawem funkcji. Te aplikacje może się również zdarzyć mają niektóre elementy wbudowane danych, takich jak wykresy i raporty, które teraz mogą być obsługiwane przez Microsoft Power BI Embedded. Nie potrzebujesz konta usługi Power BI, aby móc korzystać z aplikacji. Możesz zalogować się do aplikacji, tak jak wcześniej i wyświetlić i korzystać z usługi Power BI reporting obsługi bez konieczności wprowadzania dodatkowych licencji.

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Licencjonowanie Microsoft Power BI Embedded
W **Microsoft Power BI Embedded** model zastosowania, licencjonowania dla usługi Power BI nie jest odpowiedzialny za użytkownika końcowego.  Zamiast tego **sesji** zakupionych przez dewelopera aplikacji, która zużywa wizualnych i zostają zobowiązane do subskrypcji, która jest właścicielem tych zasobów. Dodatkowe informacje można znaleźć w [cennikiem](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/).

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Microsoft Power BI Embedded model koncepcyjny

![](media/powerbi-embedded-whats-is/model.png)

Podobnie jak inne usługi na platformie Azure, usługa Power BI Embedded zasoby za pośrednictwem [interfejsów API usługi Azure Resource Manager](https://msdn.microsoft.com/library/mt712306.aspx). W tym przypadku dostarczanym zasobem jest **kolekcja obszarów roboczych usługi Power BI**.

## <a name="workspace-collection"></a>Kolekcja obszarów roboczych
A **kolekcji obszarów roboczych** jest kontenerem najwyższego poziomu platformy Azure dla zasobów zawierający 0 lub więcej **obszarów roboczych**.  A **obszaru roboczego** **kolekcji** zawiera wszystkie standardowe właściwości platformy Azure, a także następujące:

* **Klucze dostępu** — kluczy używanych podczas bezpiecznego wywoływania interfejsów API Power BI (opisane w dalszej części artykułu).
* **Użytkownicy** — użytkowników usługi Azure Active Directory (AAD), które mają uprawnienia administratora do zarządzania kolekcji obszarów roboczych Power BI, za pośrednictwem portalu Azure lub interfejsu API usługi Azure Resource Manager.
* **Region** — w ramach udostępniania **kolekcji obszarów roboczych**, można wybrać region na potrzeby aprowizacji w. Aby uzyskać więcej informacji, zobacz [regiony platformy Azure](https://azure.microsoft.com/regions/).

## <a name="workspace"></a>Obszar roboczy
A **obszaru roboczego** jest kontenerem usługi Power BI, zawartości, który może obejmować zestawów danych i raportów. A **obszaru roboczego** jest pusta w momencie utworzenia. Będziesz tworzyć zawartości przy użyciu Power BI Desktop i będzie programowe wdrażanie pliku PBIX do obszaru roboczego przy użyciu [API Import usługi Power BI](https://msdn.microsoft.com/library/mt711504.aspx). Można również programowane Tworzenie zestawu danych i następnie tworzenia raportów w aplikacji zamiast Power BI Desktop.

## <a name="using-workspace-collections-and-workspaces"></a>Przy użyciu obszaru roboczego kolekcje i obszary robocze
**Obszar roboczy kolekcje** i **obszarów roboczych** są kontenerami zawartości, które są używane i organizowane w niezależnie od sposobu najlepiej pasuje do projektu tworzenia aplikacji. Będzie wiele różnych sposobów, że można rozmieścić ich zawartości. Można umieścić całą zawartość w obrębie jednego obszaru roboczego, a następnie później użyć do dalszego podziału zawartości między klientami tokenów aplikacji. Możesz również umieścić wszystkich klientów w oddzielnych obszarów roboczych tak, aby pewne rozdzielenie. Alternatywnie można wybrać do organizowania użytkowników według regionu, a nie przez klienta. Ten elastyczny projekt można wybrać najlepszy sposób organizowania zawartości.

## <a name="cached-datasets"></a>Zestawy danych w pamięci podręcznej
Można pamięci podręcznej zestawów danych.  Jednak nie można odświeżyć danych z pamięci podręcznej, gdy został załadowany do **Microsoft Power BI Embedded**. Zestaw danych pamięci podręcznej oznacza, że dane zostały zaimportowane do programu Power BI Desktop, zamiast korzystać z zapytania bezpośredniego.

## <a name="authentication-and-authorization-with-app-tokens"></a>Uwierzytelnianie i autoryzacja z tokenami aplikacji
**Microsoft Power BI Embedded** różni się do aplikacji do wykonywania wszystkich użytkowników na potrzeby uwierzytelniania i autoryzacji. Nie jest wymagane jawne że użytkownicy końcowi mogą być klienci usługi Azure Active Directory (Azure AD).  Zamiast tego aplikacja wyraża do **Microsoft Power BI Embedded** autoryzacji do renderowania raportu usługi Power BI za pomocą **tokeny uwierzytelniania aplikacji (tokenów aplikacji)**.  Te **tokenów aplikacji** są tworzone zgodnie z potrzebami, gdy aplikacja chce renderowania raportu.

![](media/powerbi-embedded-whats-is/app-tokens.png)

**Tokeny uwierzytelniania aplikacji (tokenów aplikacji)** są używane do uwierzytelniania względem **Microsoft Power BI Embedded**.  Istnieją trzy typy **tokenów aplikacji**:

1. Inicjowanie obsługi tokenów — używane podczas inicjowania obsługi administracyjnej nowej **obszaru roboczego** do **kolekcji obszarów roboczych**
2. Programowanie tokenów — używane podczas wykonywania wywołań bezpośrednio do **API REST usługi Power BI**
3. Osadzanie tokenów — używane podczas wykonywania wywołań do renderowania raportu w osadzonych iframe

Tokeny te służą do różnych faz interakcji z **Microsoft Power BI Embedded**.  Tokeny są zaprojektowane tak, aby delegować uprawnienia z aplikacji do usługi Power BI. Aby uzyskać więcej informacji, zobacz [App Token Flow](power-bi-embedded-app-token-flow.md).

## <a name="create-or-edit-reports-within-your-application"></a>Tworzyć i edytować raporty w aplikacji

Możesz teraz edycji istnieje raportów lub tworzenia nowych raportów bezpośrednio w aplikacji bez konieczności używania Power BI Desktop. Wymaga to, czy zestaw danych istnieją w obszarze roboczym.

## <a name="see-also"></a>Zobacz też

[Typowe scenariusze Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Wprowadzenie do programu Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Rozpoczęcie pracy z przykładem](power-bi-embedded-get-started-sample.md)  
[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)  
[Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Przykład osadzania skryptu JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Usługa Power BI CSharp repozytorium Git](https://github.com/Microsoft/PowerBI-CSharp)  
[Repozytorium Git węzła usługi Power BI](https://github.com/Microsoft/PowerBI-Node)  
Masz więcej pytań? [Dołącz do społeczności użytkowników usługi Power BI](http://community.powerbi.com/)
