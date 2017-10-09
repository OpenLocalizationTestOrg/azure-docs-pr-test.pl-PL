---
title: "Raportowanie usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Zawiera ogólne omówienie raportów usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a>Raporty w usłudze Azure Active Directory

Dzięki raportom usługi Azure Active Directory możesz uzyskać szczegółowe informacje na temat działania środowiska.  
dane podane Hello umożliwia:

- Określać, jak usługi i aplikacje są wykorzystywane przez użytkowników
- Wykrywanie potencjalnych zagrożeń wpływających na powitania kondycji środowiska
- Rozwiązywać problemy uniemożliwiające użytkownikom wykonywanie pracy  

Architektura raportowania Hello opiera się na dwóch głównych filarach:

- Raporty dotyczące zabezpieczeń
- Raporty dotyczące działań

![Raportowanie](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a>Raporty dotyczące zabezpieczeń

Hello raporty dotyczące zabezpieczeń w usłudze Azure Active Directory pomocy można tooprotect tożsamości organizacji.  
W usłudze Azure Active Directory istnieją dwa typy raportów dotyczących zabezpieczeń:

- **Oflagowani użytkownicy ryzyka** — z hello [użytkownicy oflagowani zagrożenia zabezpieczeń raportu](active-directory-reporting-security-user-at-risk.md), zapoznaj się z omówieniem, kont użytkowników, które może być zagrożone.

- **Ryzykowne logowania** — z hello [raport ryzykowne logowania zabezpieczeń](active-directory-reporting-security-risky-sign-ins.md), możesz uzyskać wskaźnik prób logowania, które mogły zostać wykonane przez osobę, która jest nie hello uzasadnionych właściciela konta użytkownika. 

**Jakie licencji usługi Azure AD potrzebujesz tooaccess raport zabezpieczeń?**  
Wszystkie wersje usługi Azure Active Directory zapewniają dostęp do raportów użytkowników oflagowanych w związku z ryzykiem oraz ryzykownych logowań.  
Jednak hello poziom szczegółowości raportu różni się między wersjami hello: 

- W hello **wersje usługi Azure Active Directory wolnego i Basic**, otrzymasz listę oflagowane ryzyka i ryzykowne logowania użytkowników. 

- Witaj **Azure Active Directory Premium 1** edition rozszerza tego modelu, należy również włączyć tooexamine niektóre hello podstawowy zdarzenia ryzyka, które zostały wykryte dla każdego raportu. 

- Witaj **Azure Active Directory Premium 2** edition udostępnia program hello najbardziej szczegółowe informacje na temat hello podstawowy zdarzenia o podwyższonym ryzyku i pozwala także tooconfigure zasady zabezpieczeń, które automatycznie odpowiadać tooconfigured poziomów ryzyka.


## <a name="activity-reports"></a>Raporty dotyczące działań

W usłudze Azure Active Directory istnieją dwa typy raportów dotyczących działań:

- **Dzienniki inspekcji** — Witaj [dzienniki inspekcji, raport aktywności](active-directory-reporting-activity-audit-logs.md) zapewnia dostęp do historii toohello każde zadanie wykonywane w dzierżawie.

- **Logowania** — z hello [raport aktywności logowania](active-directory-reporting-activity-sign-ins.md), można określić, kto wykonał zadania hello zgłoszone przez raport dzienniki inspekcji hello.



Witaj **dzienniki inspekcji, raport** umożliwia rekordów działania systemu zgodności.
Między innymi hello pod warunkiem, że dane pozwala tooaddress typowych scenariuszy takich jak:

- Ktoś jest w mojej dzierżawy otrzymano grupy administracyjnej tooan dostępu. Kto udzielił tej osobie prawa dostępu? 

- Chcę tooknow hello listę Użytkownicy logujący się do określonej aplikacji od czasu I ostatnio został załadowany hello aplikacji i mają tooknow, jeśli jest również sposób

- Chcę tooknow ile hasła resetuje są wykonywane w mojej dzierżawy


**Jakie licencji usługi Azure AD potrzebujesz raportu dzienniki inspekcji hello tooaccess?**  
Raport dotyczący dzienniki inspekcji Hello jest dostępna dla funkcji, do których posiadasz licencje. Jeśli masz licencję dla określonych funkcji, masz również dostęp toohello informacje dziennika inspekcji.

Aby uzyskać więcej informacji, zobacz **porównanie funkcji ogólnie dostępna hello wolne, Basic i Premium Edition** w [usługi Azure Active Directory, funkcje i możliwości](https://www.microsoft.com/cloud-platform/azure-active-directory-features).   



Witaj **raport aktywności logowania** tootoofind umożliwia odpowiedzi tooquestions, takich jak:

- Co to jest hello logowania wzorzec użytkownika?
- Ilu użytkowników zalogowało się w ciągu tygodnia?
- Co to jest hello stan tych logowania?


**Czy licencji usługi Azure AD, jakie muszą tooaccess hello raport aktywności logowania?**  
tooaccess hello raport aktywności logowania, dzierżawy musi mieć licencji usługi Azure AD Premium skojarzonych z nim.


## <a name="programmatic-access"></a>Dostęp programowy

W interfejsie użytkownika toohello dodanie raportowania usługi Azure Active Directory zapewnia [dostęp programistyczny](active-directory-reporting-api-getting-started-azure-portal.md) toohello danych raportowania. Hello dane z tych raportów mogą być bardzo przydatne tooyour aplikacji, takich jak systemów SIEM, inspekcji i narzędzia do analizy biznesowej. interfejsy API zapewniają dostęp programistyczny toohello danych za pomocą zestawu opartego na interfejsie REST API raportowania Hello Azure AD. Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania. 


## <a name="next-steps"></a>Następne kroki

Więcej informacji na temat hello tooknow różne typy raportów w usłudze Azure Active Directory, zobacz:

- [Raport dotyczący użytkowników oflagowanych w związku z ryzykiem](active-directory-reporting-security-user-at-risk.md)
- [Raport dotyczący ryzykownych logowań](active-directory-reporting-security-risky-sign-ins.md)
- [Raport dotyczący dzienników inspekcji](active-directory-reporting-activity-audit-logs.md)
- [Raport dotyczący dzienników logowania](active-directory-reporting-activity-sign-ins.md)

Więcej informacji na temat uzyskiwania dostępu do raportowania danych przy użyciu interfejsu API raportowania hello hello hello tooknow, zobacz: 

- [Wprowadzenie do korzystania z hello interfejsem API raportowania usługi Azure Active Directory](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png