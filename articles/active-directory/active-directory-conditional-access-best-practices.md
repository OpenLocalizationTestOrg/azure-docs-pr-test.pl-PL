---
title: "Najlepsze rozwiązania dla dostępu warunkowego w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Co to jest się, że należy unikać zrobić podczas konfigurowania zasad dostępu warunkowego i Dowiedz się więcej o rzeczy, o których należy wiedzieć."
services: active-directory
keywords: "dostęp warunkowy do aplikacji, dostęp warunkowy przy użyciu usługi Azure AD, bezpieczny dostęp do zasobów firmy, zasady dostępu warunkowego"
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
ms.openlocfilehash: 3e524c116479c1af6eb6a601c9b57d27a697c5a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a>Najlepsze rozwiązania dotyczące dostępu warunkowego w usłudze Azure Active Directory

Ten temat zawiera informacje o rzeczy, o których należy wiedzieć, i jakie są się, że należy unikać zrobić podczas konfigurowania zasad dostępu warunkowego. Przed przeczytaniem tego tematu, należy zapoznać się z pojęciami i terminologii określone w [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md)

## <a name="what-you-should-know"></a>Co należy wiedzieć

### <a name="whats-required-to-make-a-policy-work"></a>Co to są wymagane do zmiany celu zasad pracy?

Podczas tworzenia nowych zasad nie ma żadnych użytkowników, grup, aplikacji ani wybrane kontroli dostępu.

![Aplikacje w chmurze](./media/active-directory-conditional-access-best-practices/02.png)


Aby działać zgodnie z zasadami, należy skonfigurować następujące ustawienia:


|Co           | Jak                                  | Dlaczego|
|:--            | :--                                  | :-- |
|**Aplikacje w chmurze** |Musisz wybrać co najmniej jedną aplikację.  | Celem zasad dostępu warunkowego jest umożliwiają dostrojenie jak autoryzowani użytkownicy mają dostęp do Twojej aplikacji.|
| **Użytkownicy i grupy** | Musisz wybrać co najmniej jednego użytkownika lub grupę, który jest upoważniony do dostępu do aplikacji w chmurze, który wybrano. | Zasady dostępu warunkowego, który nie ma użytkowników i grupy przypisane, nigdy nie zostanie wywołany. |
| **Kontrola dostępu** | Musisz wybrać kontroli dostępu co najmniej jeden. | Procesor zasady musi wiedzieć, co należy zrobić, jeśli warunki są spełnione.|


Oprócz podstawowych wymagań w wielu przypadkach należy także skonfigurować warunek. Gdy zasady również będzie działać bez skonfigurowanego warunku, warunki są pobudzenie współczynnik dostrajanie dostępu do aplikacji.


![Aplikacje w chmurze](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a>Jak są analizowane przypisania

Wszystkie przypisania są logicznie **and**. Jeśli masz więcej niż jednego przypisania skonfigurowany, aby wyzwolić zasady, wszystkie przypisania muszą być spełnione.  

Jeśli potrzebujesz Konfigurowanie warunku lokalizacji, która ma zastosowanie do wszystkich połączeń z poza siecią organizacji, można wykonać to przez:

- W tym **wszystkich lokalizacji**
- Z wyjątkiem **wszystkich zaufanych adresów IP**

### <a name="what-happens-if-you-have-policies-in-the-azure-classic-portal-and-azure-portal-configured"></a>Co się stanie, jeśli masz zasady w klasycznym portalu Azure i portalu Azure skonfigurowane?  
Obie zasady są wymuszane przez usługę Azure Active Directory, a użytkownik uzyskuje dostęp tylko wtedy, gdy są spełnione wszystkie wymagania.

### <a name="what-happens-if-you-have-policies-in-the-intune-silverlight-portal-and-the-azure-portal"></a>Co się stanie, jeśli masz zasady w portalu usługi Intune Silverlight i portalu Azure?
Obie zasady są wymuszane przez usługę Azure Active Directory, a użytkownik uzyskuje dostęp tylko wtedy, gdy są spełnione wszystkie wymagania.

### <a name="what-happens-if-i-have-multiple-policies-for-the-same-user-configured"></a>Co się dzieje w przypadku wielu zasad dla tego samego użytkownika skonfigurowane?  
Dla każdego logowania Azure Active Directory ocenia wszystkie zasady i zapewnia, że przed udzielony dostęp do użytkownika spełniono wszystkie wymagania.


### <a name="does-conditional-access-work-with-exchange-activesync"></a>Dostęp warunkowy działa z programem Exchange ActiveSync?

Tak, można użyć programu Exchange ActiveSync w zasadach dostępu warunkowego.


## <a name="what-you-should-avoid-doing"></a>Co należy zrobić

Dostęp warunkowy framework zapewnia elastyczność dużą konfiguracji. Jednak elastyczność oznacza także, należy dokładnie przejrzeć wszystkie zasady konfiguracji przed zwalniania go, aby uniknąć niepożądane wyniki. W tym kontekście, należy zwrócić szczególną uwagę na przydziały wpływające na zestawy, takie jak **wszyscy użytkownicy / grupy / aplikacji w chmurze**.

W środowisku należy unikać następujące konfiguracje:


**Dla wszystkich użytkowników wszystkich aplikacji w chmurze:**

- **Blokowanie dostępu** — ta konfiguracja zablokuje całej organizacji, który ostatecznie nie jest dobrym rozwiązaniem.

- **Wymagają zgodnego urządzenia** — dla użytkowników, która nie zarejestrowali swoich urządzeń, ale ta zasada blokuje dostęp tym do uzyskiwania dostępu do portalu usługi Intune. Jeśli jesteś administratorem bez zarejestrowanego urządzenia te zasady blokuje powrót do portalu Azure do zmiany zasad.

- **Wymagane było przyłączenie do domeny** — ten blok zasady dostępu ma również możliwość zablokowania dostępu dla wszystkich użytkowników w organizacji, jeśli nie masz jeszcze urządzenia przyłączone do domeny.


**Dla wszystkich użytkowników, wszystkie aplikacje w chmurze, wszystkie platformy urządzeń:**

- **Blokowanie dostępu** — ta konfiguracja zablokuje całej organizacji, który ostatecznie nie jest dobrym rozwiązaniem.


## <a name="common-scenarios"></a>Typowe scenariusze

### <a name="requiring-multi-factor-authentication-for-apps"></a>Wymagania uwierzytelniania wieloskładnikowego dla aplikacji

Wiele środowisk ma aplikacje wymagające wyższego poziomu ochrony od innych.
Jest to, na przykład w przypadku aplikacji, które mają dostęp do poufnych danych.
Jeśli chcesz dodać kolejną warstwę ochrony do tych aplikacji, można skonfigurować zasady dostępu warunkowego, która wymaga usługi Multi-Factor authentication, gdy użytkownicy uzyskują dostęp do tych aplikacji.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Wymagania uwierzytelniania wieloskładnikowego dla dostępu z sieci, które nie są zaufane

Ten scenariusz jest podobny do poprzedniego scenariusza, ponieważ powoduje ona dodanie wymaganie uwierzytelniania wieloskładnikowego.
Główną różnicą jest jednak warunek tego wymagania.  
Podczas na aplikacje z dostępem do danych sensitve fokus poprzedniego scenariusza, w tym scenariuszu koncentruje się na zaufanych lokalizacji.  
Innymi słowy może być wymagane uwierzytelnianie wieloskładnikowe, jeśli aplikacja jest dostępna przez użytkownika z sieci, której nie ufasz.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Tylko zaufane urządzenia mają dostęp do usług Office 365

Jeśli używasz usługi Intune w danym środowisku, mogą natychmiast rozpocząć korzystanie interfejs zasad dostępu warunkowego w konsoli platformy Azure.

Wielu klientów usługi Intune są przy użyciu dostępu warunkowego, aby upewnić się, że tylko zaufane urządzenia mają dostęp do usług Office 365. Oznacza to, że urządzenia przenośne zarejestrowane w usłudze Intune i spełnić wymagania zasad zgodności i że komputery z systemem Windows są przyłączone do domeny lokalnej. Poprawy klucza jest, że nie trzeba ustawić te same zasady dla każdej usługi Office 365.  Podczas tworzenia nowych zasad konfigurowania aplikacji w chmurze uwzględnienie wszystkich aplikacji usługi Office 365, które chcesz chronić za pomocą przy użyciu dostępu warunkowego.

## <a name="next-steps"></a>Następne kroki

Jeśli chcesz wiedzieć, jak skonfigurować zasady dostępu warunkowego, zobacz [wprowadzenie dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).
