---
title: "Wprowadzenie do korzystania z usługi Azure AD raportowania interfejsu API w klasycznym portalu Azure AD | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć pracę z usługą Active Directory Azure, interfejsu API raportowania"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a>Wprowadzenie do korzystania z usługi Azure Active Directory raportowania interfejsu API w klasycznym portalu Azure AD
*Ten temat jest częścią [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).*

Usługa Azure Active Directory oferuje szerokiej gamy raportów. Dane z tych raportów mogą być bardzo przydatne w aplikacjach, takich jak systemy SIEM oraz narzędzia do inspekcji i analizy biznesowej. Interfejsy API raportów usługi Azure AD umożliwiają dostęp programowy do danych za pomocą zestawu interfejsów API opartych na architekturze REST. Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.

Ten artykuł zawiera informacje potrzebne do Rozpoczynanie pracy z usługą Azure AD, na zgłoszenie interfejsów API.
W następnej sekcji możesz znaleźć szczegółowe informacje o użyciu inspekcji i logowania interfejsów API. Dla wszystkich innych interfejsów API, zobacz [raportów usługi Azure AD i events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) artykułu.

Pytania, problemy lub opinie, skontaktuj się z [Pomoc raportowania usługi AAD](mailto:aadreportinghelp@microsoft.com).

## <a name="learning-map"></a>Mapa uczenia się
1. **Przygotowanie** — przed próbek interfejsu API można przetestować, należy wykonać [wymagania wstępne dotyczące raportowania interfejsu API usługi Azure AD dostęp](active-directory-reporting-api-prerequisites.md).
2. **Eksploruj** -uzyskać pierwszy wrażenie raportowania interfejsów API:
   
   * [Korzystanie z przykładów dla inspekcji interfejsu API](active-directory-reporting-api-audit-samples.md) 
   * [Korzystanie z przykładów dla raport aktywności logowania interfejsu API](active-directory-reporting-api-sign-in-activity-samples.md)
3. **Dostosowywanie** — tworzenie własnych rozwiązań: 
   
   * [Przy użyciu audytu dokumentacja interfejsu API](active-directory-reporting-api-audit-reference.md) 
   * [Przy użyciu działań logowania odwołania raportu interfejsu API](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a>Następne kroki
Jeśli zastanawiasz się wyświetlić wszystkie dostępne punkty końcowe interfejsu API usługi Azure AD Graph, przechodząc do [https://graph.windows.net/tenant-name/reports/$ metadanych? api-version = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).

