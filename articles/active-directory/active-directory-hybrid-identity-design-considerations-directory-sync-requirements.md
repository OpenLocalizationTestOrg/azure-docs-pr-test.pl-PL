---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości - określenie wymagań synchronizacji katalogu | Dokumentacja firmy Microsoft"
description: "Określenie, jakie wymagania niezbędne do synchronizowania wszystkich użytkowników hello między on = lokalnych i chmurze hello przedsiębiorstwa."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6646e3792c65f37c3d62eecdb6c6f3bd257f04f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-directory-synchronization-requirements"></a>Określenie wymagań synchronizacji katalogu
Synchronizacja jest udostępnianie tożsamości w chmurze hello na podstawie ich tożsamości lokalnych użytkowników. Czy zsynchronizowane konta będzie używany do uwierzytelniania lub uwierzytelnianie federacyjne, hello użytkownicy nadal muszą toohave tożsamości w chmurze hello.  Ta tożsamość należy toobe obsługiwane i okresowo aktualizowane.  Witaj aktualizacje mogą mieć wiele form, z tytułu zmiany toopassword zmiany.  

Rozpocznij od obliczenia hello organizacje wymogów dotyczących lokalnego tożsamości rozwiązanie i użytkownika. Tej oceny jest ważne toodefine hello techniczne wymagania dotyczące sposobu tworzenia i przechowywane w chmurze hello tożsamości użytkowników.  W przypadku większości organizacji usługi Active Directory działa lokalnie i będą hello lokalnego katalogu, w którym użytkownicy będą przez synchronizowane z, jednak w niektórych przypadkach to nie będzie hello przypadku.  

Upewnij się, że hello tooanswer następujące pytania:

* Masz jeden las usługi AD, wielu lub Brak?
  
  * Ile katalogów usługi Azure AD będzie można być synchronizowanie?
    
    1. Używasz filtrowania?
    2. Masz wiele serwerów usługi Azure AD Connect planowana?
* Obecnie masz synchronizacji narzędzia lokalnej?
  
  * Jeśli tak, czy użytkownicy, jeśli użytkownicy mają wirtualnego katalogu/integracji tożsamości?
* Masz wszelkie inne katalogu lokalnego, które mają toosynchronize (np. katalogu LDAP, bazy danych działu HR, itp.)?
  * Czy będą toobe wykonaniem dowolnej usługi GALSync?
  * Co to jest hello bieżący stan nazwy UPN w organizacji? 
  * Masz innego katalogu, który uwierzytelniania użytkowników?
  * Firma używa programu Microsoft Exchange?
    * Są one plan o wdrożeniu hybrydowym programu exchange?

Teraz, gdy masz pomysł o wymaganiach synchronizacji należy toodetermine narzędzie, które jest poprawne toomeet jeden hello tych wymagań.  Firma Microsoft udostępnia kilka integracji katalogów tooaccomplish narzędzia i synchronizacji.  Zobacz hello [Tabela porównawcza narzędzi integracji katalogu tożsamości hybrydowej](active-directory-hybrid-identity-design-considerations-tools-comparison.md) Aby uzyskać więcej informacji. 

Teraz, gdy masz wymagań synchronizacji i hello narzędzie, które będą w tym celu w firmie, należy tooevaluate hello aplikacji, które używają tych usług katalogowych. Tej oceny jest ważne, toodefine hello toointegrate wymagania techniczne chmury toohello tych aplikacji. Upewnij się, że hello tooanswer następujące pytania:

* Te aplikacje będą przenoszone toohello w chmurze i użyj katalogu hello?
* Czy istnieją specjalne atrybuty, które muszą mieć chmury toohello toobe synchronizowane umożliwiające tych aplikacji można używać ich pomyślnie?
* Te aplikacje, będą potrzebne toobe ponownie zapisane tootake Zaletą uwierzytelniania w chmurze?
* Te aplikacje będą toolive lokalnymi, podczas gdy użytkownicy uzyskują dostęp do nich przy użyciu hello tożsamość w chmurze?

Należy również toodetermine hello zabezpieczeń wymagań i ograniczeń synchronizacji katalogów. Tej oceny jest ważne tooget listę wymagań hello, które będą potrzebne w kolejności toocreate i Obsługa tożsamości użytkownika w chmurze hello. Upewnij się, że hello tooanswer następujące pytania:

* Gdzie zostaną umieszczone powitania serwera synchronizacji?
* Będzie on zostać przyłączone do domeny?
* Powitania serwera zostanie umieszczony w sieci z ograniczeniami za zaporą, takich jak strefą DMZ?
  * Czy będą mogli tooopen hello wymagane zapory porty toosupport synchronizacji?
* Czy organizacja ma plan odzyskiwania po awarii na powitania serwera synchronizacji?
* Masz konto z hello odpowiednie uprawnienia do wszystkich lasów, które mają toosynch z?
  * Jeśli firma nie może ustalić hello odpowiedzi na to pytanie, przejrzyj sekcję "Uprawnień do synchronizacji haseł" hello, w artykule hello [hello instalacji usługi synchronizacji usługi Azure Active Directory](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) i określić, czy już konta z odpowiednimi uprawnieniami lub jeśli potrzebujesz toocreate jeden.
* Jeśli masz synchronizacji mutli lasu jest hello synchronizacji serwera może tooget tooeach lasu?

> [!NOTE]
> Upewnij się, że notatki tootake wszystkie odpowiedzi i zrozumieć hello uzasadnienie hello odpowiedzi. [Określenie wymagań dotyczących odpowiedzi na zdarzenia](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) będą przekazywane hello dostępnych opcji. Po udzieleniu odpowiedzi na te pytania można wybrać opcji najlepiej pasujące do firmy wymaga.
> 
> 

## <a name="next-steps"></a>Następne kroki
[Określić wymagania dotyczące uwierzytelniania wieloskładnikowego](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a>Zobacz też
[Omówienie zagadnień dotyczących projektowania](active-directory-hybrid-identity-design-considerations-overview.md)

