---
title: "aaaAzure składników podręcznika dotyczącego fazy weryfikacji koncepcji w usłudze Active Directory | Dokumentacja firmy Microsoft"
description: "Eksploruj i szybkie rozpoczęcie scenariusze Zarządzanie tożsamościami i dostępem"
services: active-directory
keywords: "Usługa Azure active directory, podręcznika dotyczącego koncepcji, aby zapewnić"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a>Usługa Azure Active Directory dowód koncepcji podręcznika dotyczącego składników 

## <a name="theme"></a>Motyw
Usługa Azure AD zapewnia rozwiązania tożsamościami i dostępem w wielu obszarach w przedsiębiorstwie hello. Firma Microsoft klasyfikowania scenariusze hello w hello następujące obszary: 

* [Wiele aplikacji i jednej tożsamości](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [Zwiększające bezpieczeństwo](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [Skalowalność samoobsługi](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

Definiowania motywu tooframe hello fazy weryfikacji koncepcji pomaga wysiłków hello toofocus o korzyściach z cele biznesowe, które często są hello wyzwalaczy hello zainteresowanie weryfikacji koncepcji w miejscu pierwszego hello. 

## <a name="environment"></a>Środowisko

Jest ważne toodetermine hello szczegóły środowiska hello, gdzie będzie dostarczać hello fazy weryfikacji koncepcji. W idealnym przypadku tworzenie można na niej po zakończeniu weryfikacji koncepcji powitalne. środowisko docelowe Hello odgrywa kluczową rolę i powinna być widoczna hello kompromisu między go jako prawdziwe, jak to możliwe i koszty hello ograniczeń lub dodatkowe zagadnienia. Witaj środowisk weryfikacji koncepcji są:
* **Produkcja:** scenariusze hello są realizowane w środowisku na żywo i już wdrożone usługi Microsoft Cloud (środowisko produkcyjne AD, Office 365, rozwiązanie SSO/dzierżawy usługi Azure AD). 
* **Użytkownik akceptacji testu Akceptacyjne / środowiska deweloperskiego:** infrastruktury testu (równoległe AD i potencjalnie Azure AD rozwiązania dzierżawy/logowania jednokrotnego) z danych testowych, podobny do produkcji. Zazwyczaj środowiska testowego hello jest współużytkowana przez wielu projektów w przedsiębiorstwie hello.

Większość scenariuszy, w tym przewodniku są addytywne charakter. W związku z tym ich można wdrożyć w dzierżawie produkcji hello bez wpływu na użytkowników spoza hello fazy weryfikacji koncepcji. W tym dokumencie Zadzwonimy limit scenariusze, które ma wpływ na poziomie dzierżawy. W takich przypadkach możesz tooconsider środowiskach nieprodukcyjnych. 


## <a name="target-users"></a>Użytkownicy docelowi

Jest ważne toodetermine hello docelowy zbiór użytkowników, które wykonują hello scenariuszy, szczególnie w przypadku, gdy środowisko hello jest środowisko produkcyjne lub testu. kategorie Hello użytkowników docelowych do weryfikacji koncepcji są:
* **Użytkownicy pilotażowi:** funkcji zadań rzeczywistych użytkowników w środowisku hello, który będzie używany w rozwiązaniu hello z kontem hello używają w swoich tooday dnia
* **Użytkowników testowych:** konta tworzone w środowisku hello testowe 

Większość scenariuszy, w tym przewodniku może być wykonywane przez użytkowników pilotażowych. W tym dokumencie Zadzwonimy limit uwagi dotyczące użytkownika docelowego w razie potrzeby.


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]