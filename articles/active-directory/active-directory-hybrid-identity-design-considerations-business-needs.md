---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — określanie wymagań dotyczących tożsamości | Dokumentacja firmy Microsoft"
description: "Ustalenie potrzeb firmy hello firmy, które spowoduje toodefine hello wymagań dotyczących projektowania tożsamości hybrydowej hello."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: de690978-84ef-41ad-9dfe-785722d343a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: b2f1cad923b0f08ededa0d8f9a4ea8e799956e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a>Określenie wymagań dotyczących tożsamości dla rozwiązania z tożsamością hybrydową
Witaj pierwszy krok w projektowaniu rozwiązania z tożsamością hybrydową jest toodetermine hello wymagania dotyczące hello biznesowe organizacji, która będzie wykorzystanie tego rozwiązania.  Tożsamość hybrydowa uruchamia rolę pomocniczych (obsługuje on innych rozwiązań w chmurze, zapewniając uwierzytelniania) i przejdzie w możliwości nowe, ciekawe tooprovide, które odblokować nowych obciążeń dla użytkowników.  Te obciążenia lub usługi ma tooadopt użytkowników wyznaczają hello wymagań dotyczących projektowania tożsamości hybrydowej hello.  Te usługi i obciążeń należy tożsamość hybrydowa tooleverage lokalnie i w chmurze hello.  

Należy toogo kluczowymi aspektami hello firm toounderstand co jest wymagane teraz i jakie firmy hello planów dla przyszłych hello. Jeśli nie masz hello widoczność hello długoterminowej strategii dla projektowania tożsamości hybrydowej prawdopodobnie czy rozwiązania nie będzie skalowalne potrzeb biznesowych hello wzrostu i rozwoju.   T on diagramie poniżej przedstawiono przykład hybrydowego tożsamości architektury i hello obciążeń, które są trwa odblokowywanie dla użytkowników. Jest to przykład wszystkich hello nowe możliwości, które można odblokować i dostarczane ze strategią tożsamość hybrydowa stałe. 

Niektóre składniki, które są częścią architektura tożsamości hybrydowej hello![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)

## <a name="determine-business-needs"></a>Określanie potrzeb biznesowych
Każda firma będzie miała inne wymagania, nawet jeśli firmy działają hello tej samej branży, hello rzeczywiste wymagania biznesowe mogą się różnić. Oczywiście można wykorzystywać najlepsze rozwiązania z branży hello, ale ostatecznie to potrzeby biznesowe firmy hello doprowadzi toodefine hello wymagań dotyczących projektowania tożsamości hybrydowej hello. 

Upewnij się, że tooanswer hello następujące pytania dotyczące tooidentify firma musi:

* Firma poszukuje toocut kosztów operacyjnych IT?
* Firma poszukuje toosecure chmury zasoby (aplikacji SaaS, infrastruktury)?
* Czy Twoja firma potrzebuje toomodernize dział IT?
  * Są bardziej mobilni i wymagających IT toocreate wyjątki w sieci DMZ tooallow innego typu ruchu tooaccess różne zasoby użytkowników?
  * Czy firma dysponuje starsze aplikacje, które potrzebne toobe opublikowane użytkownicy nowoczesnych toothese ale nie są łatwe toorewrite?
  * Firmy muszą tooaccomplish te zadania i ustaw kontrolę na powitania jednocześnie?
* Jest firma wyszukiwania tożsamości użytkowników toosecure i ograniczyć ryzyko związane z przełączając nowe narzędzia korzystających z hello doświadczenie firmy Microsoft Azure zabezpieczeń doświadczenia z lokalnymi?
* Jest firma próby tooget usuwanie hello dreaded "external" kont lokalnych i przenieś je chmurze toohello, gdy nie są one nieaktywni zagrożeń w środowisku lokalnym?

## <a name="analyze-on-premises-identity-infrastructure"></a>Analizowanie lokalnej infrastruktury tożsamości
Teraz, gdy masz pomysł dotyczące wymagania biznesowe firmy, należy tooevaluate lokalnej infrastruktury tożsamości. Tej oceny jest ważne w przypadku definiowania toointegrate wymagania techniczne hello bieżącej tożsamości rozwiązania toohello chmury tożsamości systemu zarządzania. Upewnij się, że hello tooanswer następujące pytania:

* Jakie rozwiązania uwierzytelniania i autoryzacji jest firma użyć lokalnego? 
* Czy firma ma obecnie żadnych lokalnych usług synchronizacji?
* Czy firma korzysta żadnych innych dostawców tożsamości (IdP)?

Należy również toobe hello usługi chmury, które firma może mieć świadomość. Modele IaaS i PaaS w środowisku wykonywania oceny toounderstand hello bieżącego integracji z SaaS, jest bardzo ważne. Upewnij się, że hello tooanswer następujące pytania podczas oceny:

* Czy firma dysponuje zintegrowany z dostawcą usług w chmurze?
* Jeśli tak, usług, które są używane?
* Trwa tej integracji w środowisku produkcyjnym lub jest on pilotażu?

> [!NOTE]
> Jeśli nie masz dokładne mapowania wszystkich aplikacji i usług w chmurze, można użyć narzędzia Cloud App Discovery hello. To narzędzie można udostępnić dział IT wgląd w Twojej organizacji wszystkie działalności biznesowej i użytkownika aplikacji w chmurze. Który umożliwia łatwiejsze niż kiedykolwiek toodiscover tle IT w organizacji, w tym informacji o sposobie używania oraz żadnych użytkowników uzyskujących dostęp do aplikacji w chmurze. Zobacz tooget uruchomiona [Cloud app discovery](active-directory-cloudappdiscovery-whatis.md).
> 
> 

## <a name="evaluate-identity-integration-requirements"></a>Ocena wymagań integracja tożsamości
Następnie należy tooevaluate hello identity integration wymagania. Tej oceny jest ważne toodefine hello wymagania techniczne dla sposób uwierzytelniania użytkowników, wygląd obecności hello organizacji w chmurze hello, jak dozwolony autoryzacji w organizacji hello i jakie środowisko użytkownika hello jest toobe będzie. Upewnij się, że hello tooanswer następujące pytania:

* Twoja organizacja użyje federacyjnych, standardowe uwierzytelnianie lub obu?
* Jest to wymagane federacyjnej?  Ze względu na powitania następujące czynności:
  * Usługa rejestracji Jednokrotnej opartego na protokole Kerberos
  * Twoja firma ma aplikacji lokalnych (albo utworzona strona wewnętrznych lub 3), które używa SAML lub podobne możliwości federacji.
  * Usługi MFA za pomocą kart inteligentnych. RSA SecurID itp.
  * Reguły dostępu klienta, które rozwiązują hello pytań poniżej:
    1. Czy można zablokować wszystkie tooOffice dostępu zewnętrznego 365 na podstawie adresu IP hello powitania klienta
    2. Czy można zablokować wszystkie tooOffice dostępu zewnętrznego 365, z wyjątkiem programu Exchange ActiveSync?
    3. Czy można zablokować wszystkie tooOffice dostępu zewnętrznego 365, z wyjątkiem aplikacji opartych na przeglądarce (program OWA, SPO)
    4. Dla członków wyznaczonych grup usługi Active Directory można zablokować wszystkie tooOffice dostępu zewnętrznego 365
* Inspekcja zabezpieczeń/problemy
* Już istniejących inwestycji w uwierzytelniania federacyjnego
* Jaką nazwę naszej organizacji będą korzystać z naszych domeny w chmurze hello?
* Witaj organizacja ma niestandardową domenę?
  1. Jest tej domeny publicznej i łatwy do zweryfikowania przy użyciu usługi DNS?
  2. Jeśli nie, następnie masz domeny publicznej, które mogą być używane tooregister alternatywne nazwy UPN w usłudze AD?
* Witaj identyfikatorów użytkowników są spójne dla reprezentacji chmury? 
* Czy organizacja hello ma aplikacje, które wymagają do działania integracji z usługami w chmurze?
* Hello organizacji ma wiele domen i użyje wszystkie standardowe lub federacyjnych uwierzytelniania?

## <a name="evaluate-applications-that-run-in-your-environment"></a>Ocena aplikacji działających w środowisku
Masz pomysł dotyczące lokalnej i w chmurze infrastruktury, trzeba tooevaluate hello aplikacje, które działają w tych środowiskach. Tej oceny jest ważne, toodefine hello toointegrate wymagania techniczne systemu toohello zarządzania tożsamości chmury tych aplikacji. Upewnij się, że hello tooanswer następujące pytania:

* Gdy będzie funkcjonować nasze aplikacje?
* Uzyskują użytkownikom dostęp do lokalnych aplikacji?  W chmurze hello? Czy oba?
* Czy istnieją plany istniejących obciążeń aplikacji hello tootake i przenieś je toohello chmury?
* Czy istnieją plany toodevelop nowe aplikacje, które będą znajdować się lokalnie lub w hello chmury, który będzie używał uwierzytelniania w chmurze?

## <a name="evaluate-user-requirements"></a>Ocena wymagań użytkownika
Masz również wymagania użytkownika hello tooevaluate. Tej oceny jest toodefine ważne hello kroki, które będą potrzebne do dołączania i wspomaganie użytkowników, zgodnie z ich przejście toohello chmury. Upewnij się, że hello tooanswer następujące pytania:

* Uzyskują użytkownikom dostęp do aplikacji lokalnych?
* Uzyskują użytkownikom dostęp do aplikacji w chmurze hello?
* Jak użytkownicy zazwyczaj tootheir logowania lokalnego środowiska?
* Jak użytkownicy logowania toohello będzie chmury?

> [!NOTE]
> Upewnij się, że notatki tootake wszystkie odpowiedzi i zrozumieć hello uzasadnienie hello odpowiedzi. [Określenie wymagań dotyczących odpowiedzi na zdarzenia](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) będą przekazywane hello dostępne opcje oraz zalety/wady każdej opcji.  Po udzieleniu odpowiedzi na te pytania można wybrać opcji najlepiej pasujące do firmy wymaga.
> 
> 

## <a name="next-steps"></a>Następne kroki
[Określenie wymagań synchronizacji katalogu](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a>Zobacz też
[Omówienie zagadnień dotyczących projektowania](active-directory-hybrid-identity-design-considerations-overview.md)

