---
title: "aaaOverview programu Azure Niekorzystającą | Dokumentacja firmy Microsoft"
description: "Tworzenie zaawansowanych rozwiązań w chmurze hello bez konieczności toothink dotyczące infrastruktury."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 7c9c09d96e472edd1631892982ac60aae97342a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-serverless-with-functions-and-logic-apps"></a>Omówienie usługi Azure Niekorzystającą z funkcjami i Logic Apps

Niekorzystającą aplikacje mają zalety zwiększenie szybkości rozwoju, zmniejszenie kodu i prostota o skali.  W tym artykule przechodzi w stan różnych atrybutów hello pliki rozwiązań i niekorzystającą ofertami platformy Azure.

## <a name="what-is-serverless"></a>Co to jest niekorzystającą?

Pliki nie oznacza brak serwerów — wystarczy oznacza to, że deweloper hello nie ma tooworry o serwerach.  Dużą część projektowanie aplikacji tradycyjnych jest udzielenie odpowiedzi na pytania wokół skalowania, hosting i monitorowanie rozwiązania toomeet hello wymagań aplikacji hello.  Z Serverless te pytania są podejmowane obsługę w ramach rozwiązania hello.  Ponadto pliki aplikacji są rozliczane na podstawie zużycia planu.  Jeśli aplikacja hello nigdy nie jest używana, nigdy nie jest naliczeniem opłat.  Te funkcje umożliwiają deweloperom toofocus wyłącznie na logice biznesowej hello hello rozwiązania.

Witaj podstawowe usługi na platformie Azure wokół Serverless są [usługi Azure Functions](https://azure.microsoft.com/services/functions/) i [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).  Oba te rozwiązania hello zasadach powyżej oraz gwarantują deweloperom toobuild niezawodne chmury aplikacje z minimalnym kodu.

## <a name="what-are-azure-functions"></a>Co to są usługi Azure Functions?

Azure Functions to rozwiązanie umożliwiające łatwe uruchamianie małych fragmentów kodu lub "funkcji" w chmurze hello. Można napisać tylko kod hello potrzebne hello problemu, nie martwiąc się o całą aplikację lub hello toorun infrastruktury go. Funkcje programowanie może być jeszcze wydajniejsze i można użyć język programowania wyboru, takich jak C#, F #, Node.js, Python lub PHP. Płać tylko za czas działania kodu hello i Azure skaluje zgodnie z potrzebami.

Jeśli mają prawo toojump i wprowadzenie do usługi Azure Functions, Rozpocznij od [tworzenie pierwszej funkcji platformy Azure](../azure-functions/functions-create-first-azure-function.md). Jeśli chcesz uzyskać więcej informacji technicznych dotyczących funkcji, zobacz hello [dokumentacja dla deweloperów](../azure-functions/functions-reference.md).

## <a name="what-are-azure-logic-apps"></a>Co to jest Azure Logic Apps?

Aplikacje logiki platformy Azure udostępnia toosimplify sposób i wdrażanie skalowalnej integracji oraz przepływy pracy w chmurze hello. Zawiera visual toomodel projektanta i automatyzacji procesu jako serię kroków o nazwie przepływu pracy.  Brak [wiele łączników](../connectors/apis-list.md) w usługach w chmurze i lokalnych tooquickly połączyć aplikację niekorzystającą tooother interfejsów API.  Aplikacja logiki rozpoczyna się od wyzwalacza (jak "po dodaniu konta tooDynamics CRM") i rozpocząć uruchamiania wielu kombinacji akcji, konwersje i logiki warunku.  Logic Apps jest doskonałym wyborem w przypadku organizowanie różnych funkcji Azure w ramach procesu — szczególnie w przypadku, gdy proces hello wymaga interakcji z systemu zewnętrznego lub interfejsu API.

tooget wprowadzenie do aplikacji logiki, zacznij od [tworzenie pierwszej aplikacji logiki](logic-apps-create-a-logic-app.md).  Jeśli chcesz uzyskać więcej informacji technicznych dotyczących Logic Apps, zobacz hello [dokumentacja dla deweloperów](logic-apps-workflow-actions-triggers.md).

## <a name="how-can-i-build-and-deploy-serverless-applications-in-azure"></a>Jak tworzenie i wdrażanie aplikacji Niekorzystającą na platformie Azure?

Platforma Azure oferuje bogaty zestaw narzędzi na projektowanie, wdrażanie i zarządzanie aplikacjami bez serwera.  Aplikacje mogą być wbudowane bezpośrednio w portalu Azure hello, lub z [narzędzi z programu Visual Studio](logic-apps-serverless-get-started-vs.md).  Gdy aplikacja została utworzona może być [natychmiast wdrożyć](logic-apps-create-deploy-template.md).  Platforma Azure udostępnia również monitorowanie bez serwera aplikacji.  Monitorowanie jest możliwy z hello portalu Azure za pośrednictwem interfejsu API hello lub zestawów SDK lub tooOMS zintegrowane narzędzia i usługi Application Insights.

## <a name="next-steps"></a>Następne kroki

* [Rozpoczynanie pracy z tworzeniem Niekorzystającą aplikacji w programie Visual Studio](logic-apps-serverless-get-started-vs.md)
* [Utwórz pulpit nawigacyjny szczegółowych informacji klienta z Serverless](logic-apps-scenario-social-serverless.md)
* [Tworzenie szablonu wdrożenia dla aplikacji logiki](logic-apps-create-deploy-template.md)