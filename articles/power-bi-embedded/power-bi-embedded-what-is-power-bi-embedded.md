---
title: Microsoft Power BI Embedded jest aaaWhat?
description: "Power BI Embedded pozwala toointegrate raportów usługi Power BI do sieci web lub aplikacji dla urządzeń przenośnych, nie potrzebujesz toobuild niestandardowych rozwiązań."
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
ms.openlocfilehash: 0353938b6cdd9bb58b123b250f45f76b8cc7abe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>Co to jest Microsoft Power BI Embedded?
Z **Power BI Embedded**, można zintegrować raportów usługi Power BI bezpośrednio z sieci web lub aplikacji dla urządzeń przenośnych.

![](media/powerbi-embedded-whats-is/what-is.png)

Usługa Power BI Embedded jest **usługi Azure** , który umożliwia niezależnym dostawcom oprogramowania i toosurface deweloperzy aplikacji Power BI danych napotka w swoich aplikacjach. Deweloper zostały już utworzone w aplikacji, a te aplikacje mają własne użytkowników i zestawem funkcji. Te aplikacje może się również zdarzyć toohave niektórych elementów danych wbudowanych, takich jak wykresy i raporty, które teraz mogą być obsługiwane przez Microsoft Power BI Embedded. Nie trzeba toouse konta usługi Power BI aplikacji. Możesz kontynuować toosign w aplikacji tooyour tak samo jak wcześniej i wyświetlić i interakcyjnie hello środowisko raportowania usługi Power BI bez żadnych dodatkowych licencji.

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Licencjonowanie Microsoft Power BI Embedded
W hello **Microsoft Power BI Embedded** model zastosowania, licencjonowania dla usługi Power BI nie jest obowiązkiem hello hello przez użytkownika końcowego.  Zamiast tego **sesji** zakupionych przez dewelopera hello aplikacji hello, która zużywa hello elementów wizualnych i są naliczane toohello subskrypcji, która jest właścicielem tych zasobów. Dodatkowe informacje można znaleźć na powitania [cennikiem](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/).

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Microsoft Power BI Embedded model koncepcyjny

![](media/powerbi-embedded-whats-is/model.png)

Podobnie jak inne usługi na platformie Azure, usługa Power BI Embedded zasoby za pośrednictwem hello [interfejsów API usługi Azure Resource Manager](https://msdn.microsoft.com/library/mt712306.aspx). W tym przypadku dostarczanym zasobem hello jest **kolekcji obszarów roboczych usługi Power BI**.

## <a name="workspace-collection"></a>Kolekcja obszarów roboczych
A **kolekcji obszarów roboczych** jest hello najwyższego poziomu kontenera platformy Azure dla zasobów zawierający 0 lub więcej **obszarów roboczych**.  A **obszaru roboczego** **kolekcji** zawiera wszystkie standardowe właściwości Azure hello, jak również następujące hello:

* **Klucze dostępu** — kluczy używana przy wywoływaniu bezpiecznie hello Power BI API (opisane w dalszej części artykułu).
* **Użytkownicy** — Azure Active Directory (AAD) użytkowników, którzy mają toomanage praw administratora hello kolekcji obszarów roboczych usługi Power BI za pomocą hello portalu Azure lub interfejsu API usługi Azure Resource Manager.
* **Region** — w ramach udostępniania **kolekcji obszarów roboczych**, możesz wybrać toobe regionu, udostępniane w. Aby uzyskać więcej informacji, zobacz [regiony platformy Azure](https://azure.microsoft.com/regions/).

## <a name="workspace"></a>Obszar roboczy
A **obszaru roboczego** jest kontenerem usługi Power BI, zawartości, który może obejmować zestawów danych i raportów. A **obszaru roboczego** jest pusta w momencie utworzenia. Będziesz tworzyć zawartości przy użyciu Power BI Desktop i programowo wdrożony hello PBIX do obszaru roboczego przy użyciu hello [API Import usługi Power BI](https://msdn.microsoft.com/library/mt711504.aspx). Można również programowane Tworzenie zestawu danych i następnie tworzenia raportów w aplikacji zamiast Power BI Desktop.

## <a name="using-workspace-collections-and-workspaces"></a>Przy użyciu obszaru roboczego kolekcje i obszary robocze
**Obszar roboczy kolekcje** i **obszarów roboczych** są kontenerami zawartości, które są używane i organizowane w niezależnie od sposobu najlepiej pasuje do hello projekt aplikacji hello tworzona. Będzie wiele różnych sposobów, że można rozmieścić hello zawartości. Możesz wybrać tooput całej zawartości w ramach jednego obszaru roboczego i następnie nowsze toofurther tokenów aplikacji użyj podzielić hello zawartości między klientami. Można też tooput wszystkich klientów w oddzielnych obszarów roboczych, aby Brak niektórych rozdzielenie. Lub możesz wybrać tooorganize użytkowników według regionu, a nie przez klienta. Ten elastyczny projekt pozwala toochoose hello najlepsze sposób tooorganize zawartości.

## <a name="cached-datasets"></a>Zestawy danych w pamięci podręcznej
Można pamięci podręcznej zestawów danych.  Jednak nie można odświeżyć danych z pamięci podręcznej, gdy został załadowany do **Microsoft Power BI Embedded**. Pamięci podręcznej zestawu danych oznacza, że hello dane zostały zaimportowane do Power BI Desktop, zamiast korzystać z zapytania bezpośredniego.

## <a name="authentication-and-authorization-with-app-tokens"></a>Uwierzytelnianie i autoryzacja z tokenami aplikacji
**Microsoft Power BI Embedded** różni tooperform aplikacji tooyour wszystkie hello niezbędne uwierzytelniania i autoryzacji użytkowników. Nie jest wymagane jawne że użytkownicy końcowi mogą być klienci usługi Azure Active Directory (Azure AD).  Zamiast tego aplikacja wyraża zbyt**Microsoft Power BI Embedded** toorender autoryzacji raportu usługi Power BI za pomocą **tokeny uwierzytelniania aplikacji (tokenów aplikacji)**.  Te **tokenów aplikacji** są tworzone zgodnie z potrzebami, gdy aplikacja potrzebuje toorender raportu.

![](media/powerbi-embedded-whats-is/app-tokens.png)

**Tokeny uwierzytelniania aplikacji (tokenów aplikacji)** są używane tooauthenticate przed **Microsoft Power BI Embedded**.  Istnieją trzy typy **tokenów aplikacji**:

1. Inicjowanie obsługi tokenów — używane podczas inicjowania obsługi administracyjnej nowej **obszaru roboczego** do **kolekcji obszarów roboczych**
2. Programowanie tokenów — używany podczas wprowadzania bezpośrednio wywołuje toohello **API REST usługi Power BI**
3. Tokenów — używanego podczas wykonywania wywołania toorender osadzanie raportu w hello osadzonych iframe

Tokeny te służą do hello fazy interakcji z **Microsoft Power BI Embedded**.  tokeny Hello są zaprojektowane tak, aby można delegować uprawnienia w Twojej aplikacji tooPower BI. Aby uzyskać więcej informacji, zobacz [App Token Flow](power-bi-embedded-app-token-flow.md).

## <a name="create-or-edit-reports-within-your-application"></a>Tworzyć i edytować raporty w aplikacji

Możesz teraz edycji istnieje raportów lub tworzenia nowych raportów bezpośrednio w aplikacji bez konieczności toouse Power BI Desktop. Wymaga to, czy zestaw danych istnieją w obszarze roboczym.

## <a name="see-also"></a>Zobacz też

[Typowe scenariusze Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Wprowadzenie do programu Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Rozpoczęcie pracy z przykładem](power-bi-embedded-get-started-sample.md)  
[Embed a report](power-bi-embedded-embed-report.md) (Osadzanie raportu)  
[Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Przykład osadzania skryptu JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Usługa Power BI CSharp repozytorium Git](https://github.com/Microsoft/PowerBI-CSharp)  
[Repozytorium Git węzła usługi Power BI](https://github.com/Microsoft/PowerBI-Node)  
Masz więcej pytań? [Spróbuj hello Power BI społeczności](http://community.powerbi.com/)
