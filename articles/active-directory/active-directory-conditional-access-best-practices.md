---
title: "aaaBest rozwiązań dla dostępu warunkowego w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Co to jest się, że należy unikać zrobić podczas konfigurowania zasad dostępu warunkowego i Dowiedz się więcej o rzeczy, o których należy wiedzieć."
services: active-directory
keywords: "tooapps dostępu warunkowego, dostępu warunkowego z usługą Azure AD, bezpieczny dostęp do zasobów toocompany, zasady dostępu warunkowego"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a>Najlepsze rozwiązania dotyczące dostępu warunkowego w usłudze Azure Active Directory

Ten temat zawiera informacje o rzeczy, o których należy wiedzieć, i jakie są się, że należy unikać zrobić podczas konfigurowania zasad dostępu warunkowego. Przed przeczytaniem tego tematu, należy się zapoznać z hello pojęcia i terminologia hello określone w [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md)

## <a name="what-you-should-know"></a>Co należy wiedzieć

### <a name="whats-required-toomake-a-policy-work"></a>Co to są wymagane toomake pracy zasady?

Podczas tworzenia nowych zasad nie ma żadnych użytkowników, grup, aplikacji ani wybrane kontroli dostępu.

![Aplikacje w chmurze](./media/active-directory-conditional-access-best-practices/02.png)


Praca z zasadami toomake, należy skonfigurować następujące hello:


|Co           | Jak                                  | Dlaczego|
|:--            | :--                                  | :-- |
|**Aplikacje w chmurze** |Należy tooselect co najmniej jedną aplikację.  | Celem Hello zasady dostępu warunkowego jest tooenable toofine strojenia jak autoryzowani użytkownicy mają dostęp do Twojej aplikacji.|
| **Użytkownicy i grupy** | Należy tooselect co najmniej jednego użytkownika lub grupę, która jest autoryzowany wybrane aplikacje w chmurze hello tooaccess. | Zasady dostępu warunkowego, który nie ma użytkowników i grupy przypisane, nigdy nie zostanie wywołany. |
| **Kontrola dostępu** | Należy tooselect co najmniej jeden kontroli dostępu. | Procesor zasady musi tooknow jakie toodo Jeśli warunki są spełnione.|


W przypadku dodawania toothese podstawowych wymagań, w wielu przypadkach należy także skonfigurować warunek. Gdy zasady również będzie działać bez skonfigurowanego warunku, warunki są hello współczynnik pobudzenie Dostrajanie aplikacji tooyour dostępu.


![Aplikacje w chmurze](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a>Jak są analizowane przypisania

Wszystkie przypisania są logicznie **and**. Jeśli masz więcej niż jeden przypisania skonfigurowane, tootrigger zasady, muszą być spełnione wszystkie przypisania.  

Tooconfigure lokalizacji warunek, który dotyczy połączeń tooall z poza siecią organizacji, należy można osiągnąć to przez:

- W tym **wszystkich lokalizacji**
- Z wyjątkiem **wszystkich zaufanych adresów IP**

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a>Co się stanie, jeśli masz zasady w hello klasycznego portalu Azure i portalu Azure skonfigurowane?  
Obie zasady są wymuszane przez usługę Azure Active Directory i hello użytkownik uzyskuje dostęp tylko wtedy, gdy są spełnione wszystkie wymagania.

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a>Co się stanie, jeśli masz zasady w hello portalu Intune Silverlight i hello Azure Portal?
Obie zasady są wymuszane przez usługę Azure Active Directory i hello użytkownik uzyskuje dostęp tylko wtedy, gdy są spełnione wszystkie wymagania.

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a>Co się stanie, jeśli wiele zasad dla tego samego użytkownika skonfigurowane hello?  
Dla każdego logowania Azure Active Directory ocenia wszystkie zasady i zapewnia, że przed przyznany dostęp użytkownika toohello spełnione są wszystkie wymagania.


### <a name="does-conditional-access-work-with-exchange-activesync"></a>Dostęp warunkowy działa z programem Exchange ActiveSync?

Tak, można użyć programu Exchange ActiveSync w zasadach dostępu warunkowego.


## <a name="what-you-should-avoid-doing"></a>Co należy zrobić

Witaj dostępu warunkowego framework zapewnia elastyczność dużą konfiguracji. Jednak dużą elastyczność oznacza również należy dokładnie przejrzeć każdej konfiguracji zasad przed tooreleasing go tooavoid niepożądane wyniki. W tym kontekście, trzeba zwrócić szczególną uwagę tooassignments wpływających na zestawy, takie jak **wszyscy użytkownicy / grupy / aplikacji w chmurze**.

W środowisku należy unikać hello następujące konfiguracje:


**Dla wszystkich użytkowników wszystkich aplikacji w chmurze:**

- **Blokowanie dostępu** — ta konfiguracja zablokuje całej organizacji, który ostatecznie nie jest dobrym rozwiązaniem.

- **Wymagają zgodnego urządzenia** — dla użytkowników, która nie zarejestrowali swoich urządzeń, ale ta zasada blokuje dostęp w tym portalu Intune toohello dostępu. Jeśli jesteś administratorem bez zarejestrowanego urządzenia te zasady blokuje powrót do hello Azure toochange portalu hello zasad.

- **Wymagane było przyłączenie do domeny** — ten blok zasady dostępu ma również hello potencjalne tooblock dostęp dla wszystkich użytkowników w organizacji, jeśli nie masz jeszcze urządzenia przyłączone do domeny.


**Dla wszystkich użytkowników, wszystkie aplikacje w chmurze, wszystkie platformy urządzeń:**

- **Blokowanie dostępu** — ta konfiguracja zablokuje całej organizacji, który ostatecznie nie jest dobrym rozwiązaniem.


## <a name="common-scenarios"></a>Typowe scenariusze

### <a name="requiring-multi-factor-authentication-for-apps"></a>Wymagania uwierzytelniania wieloskładnikowego dla aplikacji

Wiele środowisk ma aplikacje wymagające wyższego poziomu ochrony niż hello innych użytkowników.
Jest to, na przykład w przypadku aplikacji, które mają dostęp do danych toosensitive hello.
Jeśli chcesz tooadd kolejną warstwę ochrony toothese aplikacji, można skonfigurować zasady dostępu warunkowego, która wymaga usługi Multi-Factor authentication, gdy użytkownicy uzyskują dostęp do tych aplikacji.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Wymagania uwierzytelniania wieloskładnikowego dla dostępu z sieci, które nie są zaufane

Ten scenariusz jest podobne toohello poprzednim scenariuszu, ponieważ powoduje ona dodanie wymaganie uwierzytelniania wieloskładnikowego.
Główna różnica hello jest jednak warunek hello tego wymagania.  
Podczas hello fokus poprzednim scenariuszu hello na aplikacje z danymi toosensitve dostępu hello w tym scenariuszu koncentruje się na zaufanych lokalizacji.  
Innymi słowy może być wymagane uwierzytelnianie wieloskładnikowe, jeśli aplikacja jest dostępna przez użytkownika z sieci, której nie ufasz.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Tylko zaufane urządzenia mają dostęp do usług Office 365

Jeśli używasz usługi Intune w danym środowisku, mogą natychmiast rozpocząć korzystanie hello interfejs zasad dostępu warunkowego w hello konsoli platformy Azure.

Wielu klientów usługi Intune korzystają z dostępu warunkowego tooensure, że tylko zaufane urządzenia mają dostęp do usług Office 365. Oznacza to, że urządzenia przenośne zarejestrowane w usłudze Intune i spełnić wymagania zasad zgodności oraz czy komputery z systemem Windows są tooan przyłączone do domeny lokalnej. Poprawy klucza jest, że nie masz tooset hello te same zasady dla każdej z usług hello usługi Office 365.  Podczas tworzenia nowych zasad konfigurowania hello chmury aplikacji tooinclude każdej aplikacji hello usługi Office 365, które mają tooprotect z przy użyciu dostępu warunkowego.

## <a name="next-steps"></a>Następne kroki

Jeśli chcesz, aby tooknow tooconfigure zasady dostępu warunkowego, zobacz temat [wprowadzenie dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).
