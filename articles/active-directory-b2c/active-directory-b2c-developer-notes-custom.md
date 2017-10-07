---
title: "Usługi Azure Active Directory B2C: Uwagi dla deweloperów przy użyciu zasad niestandardowych | Dokumentacja firmy Microsoft"
description: "Uwagi dla deweloperów na skonfigurowaniu i utrzymywaniu z niestandardowych zasad usługi Azure AD B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a>Informacje o wersji dla publicznej wersji zapoznawczej usługi Azure Active Directory B2C zasad niestandardowych
Witaj zestaw funkcji niestandardowych zasad jest teraz dostępna w wersji ewaluacyjnej w publicznej wersji zapoznawczej dla wszystkich usługi Azure Active Directory B2C (Azure AD B2C) klientów. Ten zestaw funkcji jest przeznaczona dla deweloperów zaawansowane tożsamości tworzenia hello najbardziej złożonych rozwiązań tożsamości.  

Obecnie ten zestaw funkcji wymaga deweloperzy tooconfigure hello Framework obsługi tożsamości bezpośrednio za pomocą edycji pliku XML. Ta metoda konfiguracji jest wydajny i złożone. Zaawansowane deweloperzy tożsamości za pomocą hello Framework obsługi tożsamości należy zaplanować tooinvest pewien czas ukończenia przewodników i odczytywanie dokumentów odwołania. 

## <a name="features-included-in-this-public-preview"></a>Funkcje zawarte w tym publicznej wersji zapoznawczej
Witaj wprowadzeniu nowych funkcji wprowadzonych w wersji zapoznawczej hello deweloperzy mogą wykonywać hello następujące zadania:<br>

* Tworzenie i przekazywanie niestandardowe uwierzytelnianie użytkownika podróże za pomocą niestandardowych zasad. 
   * Opisano krok po kroku jako wymiany podróże użytkownika od dostawcy oświadczeń. 
   * Zdefiniuj rozgałęzień warunkowych w podróży użytkownika. 
* Integracja usług korzystających z interfejsu API REST w podróży użytkownika z uwierzytelniania niestandardowego.  
* Dodaj federacji z dostawców tożsamości, zgodnych z hello standardowe OpenIDConnect. <br>
* Dodaj federacji z dostawców tożsamości, zgodnymi z protokołem toohello SAML 2.0. 

## <a name="terms-of-hello-public-preview"></a>Warunki hello publicznej wersji zapoznawczej

* Firma Microsoft zachęca toouse hello nowe funkcje wyłącznie do celów ewaluacyjnych.<br>
* Nowe funkcje nie są przeznaczone do użytku w środowisku produkcyjnym.<br>
* Umowy dotyczące poziomu usług (SLA) nie należy stosować toohello nowych funkcji. <br>
* Żądania pomocy technicznej można złożyć za pośrednictwem kanałów regularne pomocy technicznej. <br>
* Brak bez uzgodnionej daty dla ogólnej dostępności.<br>
* Nasze uznania z dowolnej przyczyny Microsoft może Flaga i odrzucić lub ograniczyć scenariuszy i podróże użytkownika, które wykraczają poza zakres hello hello Azure AD B2C produktu karty tooserve jako platformę zarządzania (CIAM) tożsamości i dostępu klienta.

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a>Obowiązki deweloperów zestaw funkcji zasad niestandardowych
Konfiguracja zasad ręczne przyznaje toohello niższego poziomu dostępu podstawowej platformy Azure AD B2C i powoduje tworzenie hello framework unikatowy zaufania można swobodnie dostosowywać. Możliwych kombinacji dostawców tożsamości niestandardowej, relacje zaufania, integracji z usługami zewnętrznych i przepływy pracy krok po kroku umieścić większe wymagania na powitania zaawansowane deweloperom korzystanie z nich.

toofully korzyści z publicznej wersji zapoznawczej hello, zaleca się, że deweloperów korzystających z zestawu funkcji niestandardowych zasad hello odpowiednia toohello następujące wytyczne:
* Zapoznanie się z języka konfiguracji hello hello aparat obsługi tożsamości i klucz/klucze tajne zarządzania.
* Przejmowanie na własność scenariuszy i niestandardowej integracji.
* Testowanie metodyczny scenariusza.
* Wykonaj rozwoju oprogramowania i przejściowych najlepszych rozwiązań z co najmniej jeden programowanie i środowiska testowego i jednego środowiska produkcyjnego.
* Aktualne informacje o nowych rozwiązań z hello dostawców tożsamości i usług, które można zintegrować z. Na przykład śledzenie pracy w kluczy tajnych i planowanych i nieplanowanych zmiany toohello usługi.
* Konfigurowanie aktywnego monitorowania i monitorowanie czasu reakcji hello środowisk produkcyjnych.
* Aktualizuj adresy e-mail kontaktów i pozostać reakcji toohello Microsoft live witryny zespołu w wiadomości e-mail.
* Podejmowania działań odpowiednim czasie, gdy zaleca toodo Witaj, Microsoft live witryny zespołu. 


>[!NOTE]
>Te funkcje mogą ostatecznie dołączone wbudowane zasady usługi Azure AD, dzięki czemu deweloperzy tooall dostęp.

## <a name="next-steps"></a>Następne kroki
[Wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md).
