---
title: "aplikacje aaaHow są dodawane tooAzure usługi Active Directory."
description: "W tym artykule opisano sposób dodawania aplikacji tooan wystąpienia usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: shoatman
manager: kbrint
editor: 
ms.assetid: 3321d130-f2a8-4e38-b35e-0959693f3576
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2016
ms.author: shoatman
ms.custom: aaddev
ms.openlocfilehash: 3ca710c58a403b52e8b728202ad9010f4873bcea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-and-why-applications-are-added-tooazure-ad"></a>Jak i dlaczego aplikacje są dodawane tooAzure AD
Jeden hello początkowo puzzling czynności podczas przeglądania listy aplikacji w wystąpieniu usługi Azure Active Directory jest zrozumienie, skąd pochodzą aplikacji hello i dlaczego są one dostępne.  W tym artykule zapewni wysokiego poziomu omówienie sposobu aplikacji znajdują się w katalogu hello i dostarczać kontekstu, który pomoże zrozumieć, jak aplikacja pochodzi toobe w katalogu.

## <a name="what-services-does-azure-ad-provide-tooapplications"></a>Jakie usługi Azure AD oferuje tooapplications?
Aplikacje są dodawane tooleverage tooAzure AD co najmniej jednego świadczonych usługach hello.  Te usługi obejmują:

* Aplikacja uwierzytelniania i autoryzacji
* Uwierzytelnianie użytkownika & autoryzacji
* Logowanie jednokrotne (SSO) przy użyciu Federacji lub haseł
* Inicjowanie obsługi użytkowników & synchronizacji
* Kontrola dostępu oparta na rolach; Użyj hello ról tooperform ról katalogu toodefine aplikacji na podstawie sprawdzeń autoryzacji w aplikacji.
* usługi autoryzacji oAuth (używane przez usługi Office 365 i innych zasobów firmy Microsoft aplikacje tooauthorize dostępu tooAPIs /).
* Publikowanie aplikacji & proxy; Publikowanie aplikacji z toohello prywatną siecią internet

## <a name="how-are-applications-represented-in-hello-directory"></a>Jak aplikacje są reprezentowane w katalogu hello?
Aplikacje są reprezentowane w hello Azure AD za pomocą obiektów 2: obiekt główny usługi i obiektu aplikacji.  Istnieje jeden obiekt aplikacji, w zarejestrowany w "home" / directory "właściciela" lub "publikowania" i przynajmniej jedna obiekty główne reprezentujący aplikacji hello w każdym katalogu, w którym działa usługa.  

Witaj obiektu aplikacji opisuje tooAzure aplikacji hello AD (usługa hello wielodostępnej) i może zawierać żadnego z następujących hello: (*Uwaga*: to nie jest kompletną listą.)

* Nazwa, Logo i wydawca
* Klucze tajne (klucze symetryczne i/lub asymetrycznego używane aplikacji hello tooauthenticate)
* Zależności interfejsu API (oAuth)
* Interfejsy API/zasobów/zakresów opublikowane (oAuth)
* Aplikacja ról (RBAC)
* Metadane logowania jednokrotnego i konfiguracji (rejestracji jednokrotnej SSO)
* Inicjowanie obsługi administracyjnej metadanych i konfiguracji użytkownika
* Metadane serwera proxy i konfiguracji

nazwy głównej usługi Hello jest rekordem aplikacji hello w każdym katalogu, w którym aplikacji hello działa, łącznie z jego katalogu macierzystego.  Witaj nazwy głównej usługi:

* Odwołuje się obiekt aplikacji tooan za pomocą właściwości identyfikatora aplikacji hello
* Rejestruje lokalnych użytkowników i grupy przypisań ról aplikacji
* Rejestruje lokalnych użytkowników i administratora uprawnienia toohello aplikacji
  * Na przykład: uprawnienie tooaccess aplikacji hello e-mail użytkowników
* Rejestruje zasady lokalne, łącznie z zasad dostępu warunkowego
* Rejestruje lokalne alternatywne ustawienia lokalne dla aplikacji
  * Reguły przekształcania oświadczeń
  * Mapowanie atrybutów (Inicjowanie obsługi użytkowników)
  * Dzierżawcy ról określonej aplikacji (Jeśli aplikacja hello obsługuje role niestandardowe)
  * Nazwa/Logo

### <a name="a-diagram-of-application-objects-and-service-principals-across-directories"></a>Diagram obiektów aplikacji i nazwy główne usług między katalogami
![Diagram pokazujący sposób aplikacji obiekty i usługi podmiotów istniejących wystąpieniami usługi Azure AD.][apps_service_principals_directory]

Jak widać na powyższym diagramie hello.  Firma Microsoft udostępnia dwa katalogi wewnętrznie (po lewej stronie powitania) używa toopublish aplikacji.

* Jeden dla Microsoft Apps (katalog usług firmy Microsoft)
* Jeden dla wstępnie zintegrowanych aplikacji firm 3 (Galeria aplikacji katalogu)

Aplikacja wydawców/dostawców, którzy integracji z usługą Azure AD są wymagane toohave katalogu publikowania.  (Niektóre katalogu SAAS).

Aplikacje, które Dodaj siebie obejmują:

* Aplikacje, które utworzono (zintegrowane w usłudze AAD)
* Aplikacje połączone dla single-sign-on
* Aplikacje, które można publikować przy użyciu hello serwera proxy aplikacji usługi Azure AD.

### <a name="a-couple-of-notes-and-exceptions"></a>Kilka uwag i wyjątków
* Nie wszystkie jednostki usługi punktu wstecz tooapplication obiektów.  Huh? Gdy usługi Azure AD został pierwotnie utworzony hello usługi świadczone tooapplications były bardziej ograniczone i nazwy głównej usługi hello został wystarczające do ustalenia tożsamości aplikacji.  nazwy głównej usługi oryginalnego Hello była bardziej toohello kształtu konta usługi Windows Server Active Directory.  Z tego powodu, że jest nadal możliwe toocreate przy użyciu nazwy główne usług hello Azure AD PowerShell bez tworzenia obiektu aplikacji.  Witaj interfejsu API programu Graph wymaga obiektu aplikacji przed utworzeniem usługę podmiotu zabezpieczeń.
* Nie wszystkie hello informacje opisane powyżej obecnie uwidocznioną programowo.  następujące Hello są dostępne tylko w hello interfejsu użytkownika:
  * Reguły przekształcania oświadczeń
  * Mapowanie atrybutów (Inicjowanie obsługi użytkowników)
* Aby uzyskać więcej szczegółowych informacji na powitania nazwy głównej usługi i liczby obiektów aplikacji można znaleźć w dokumentacji referencyjnej toohello interfejsu API REST usługi Azure AD Graph.  *Wskazówka*: hello dokumentacji interfejsu API Azure AD Graph jest hello najbliższego operacją tooa odwołanie do schematu dla usługi Azure AD, która jest obecnie dostępna.  
  * [Aplikacji](https://msdn.microsoft.com/library/azure/dn151677.aspx)
  * [Nazwy głównej usługi](https://msdn.microsoft.com/library/azure/dn194452.aspx)

## <a name="how-are-apps-added-toomy-azure-ad-instance"></a>Jak aplikacje są dodawane toomy wystąpienia usługi Azure AD?
Istnieje wiele sposobów tooAzure AD można dodać aplikację:

* Dodaj aplikację z hello [galerii aplikacji programu Azure Active Directory](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)
* Zaloguj się w górę/w 3rd aplikacji firm zintegrowane z usługą Azure Active Directory (na przykład: [Smartsheet](https://app.smartsheet.com/b/home) lub [DocuSign](https://www.docusign.net/member/MemberLogin.aspx))
  * Podczas logowania się/użytkownicy są zadawane toogive uprawnienia toohello aplikacji tooaccess swój profil i inne uprawnienia.  pierwszy toogive osoby Hello zgoda przyczyny reprezentujący katalog dodano toohello toobe aplikacji hello nazwy głównej usługi.
* Zaloguj się w górę/w witrynie Microsoft online services, takich jak [usługi Office 365](http://products.office.com/)
  * Jeśli jesteś subskrybentem tooOffice 365 rozpocząć wersji próbnej jeden lub więcej nazwy główne usług są tworzone w katalogu hello reprezentujący hello różnych usług, które są używane toodeliver wszystkie funkcje hello skojarzony z usługą Office 365.
  * Niektóre usługi Office 365, takich jak SharePoint Utwórz jednostki usługi na podstawie bieżących tooallow bezpiecznej komunikacji między składnikami, włącznie z przepływami pracy.
* Dodaje projektujesz aplikację w portalu zarządzania Azure, zobacz hello: https://msdn.microsoft.com/library/azure/dn132599.aspx
* Dodaj aplikację, której tworzony jest przy użyciu programu Visual Studio, zobacz:
  * [Metody uwierzytelniania platformy ASP.Net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)
  * [Podłączonych usług](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)
* Dodawanie aplikacji toouse toouse hello [serwera Proxy aplikacji usługi Azure AD](https://msdn.microsoft.com/library/azure/dn768219.aspx)
* Łączenie aplikacji dla funkcji logowania jednokrotnego przy użyciu SAML lub hasło logowania jednokrotnego
* Wiele innych, łącznie z różnych uruchomień dewelopera na platformie Azure i/w Eksploratorze interfejsu API napotyka między centrami developer

## <a name="who-has-permission-tooadd-applications-toomy-azure-ad-instance"></a>Kto ma uprawnienia tooadd aplikacji toomy usługi Azure AD wystąpienia?
Tylko administratorzy globalni mogą:

* Dodaj aplikacje z galerii aplikacji hello Azure AD (wstępnie zintegrowanych aplikacji firm 3)
* Publikowanie aplikacji przy użyciu powitania serwera Proxy aplikacji usługi Azure AD

Wszyscy użytkownicy w katalogu mają prawa tooadd aplikacji, które są one opracowywanie i uznania za pośrednictwem aplikacji, które one udziału/udzielanie dostępu tootheir dane.  *Pamiętaj logowania użytkownika w górę/w aplikacji tooan i udzielanie uprawnień może spowodować główna tworzona usługi.*

Ten może początkowo dźwięku dotyczące, ale zachować powitania po pamiętać:

* Aplikacje zostały stanie tooleverage Windows Server Active Directory do uwierzytelniania użytkowników przez wiele lat bez konieczności toobe aplikacji hello zarejestrowany/rejestrowane w katalogu hello.  Teraz hello organizacji zostanie zwiększona tooexactly widoczność jak wiele aplikacji z katalogu hello i what for.
* Administrator zmiennych proces publikowania/rejestracji aplikacji nie jest konieczne.  Z usług federacyjnych Active Directory jest prawdopodobne, że administrator ma tooadd aplikację jako uzależniona imieniu deweloperów.  Deweloperzy mogą teraz samoobsługi.
* Użytkownicy logujący/się przy użyciu konta organizacji do celów biznesowych tooapps jest to przydatne.  Następnie opuszczenia organizacji hello spowoduje utratę dostępu tootheir konta w aplikacji hello, który używa.
* O rekord danych został udostępniony, z którym aplikacja jest to przydatne.  Dane są bardziej przenośne niż kiedykolwiek i o wyczyść rekord kto udostępnionych danych z aplikacji, które jest używany.
* Dokładnie jakie uprawnienia, że użytkownicy będą mogli toogrant tooapplications i uprawnienia, które wymagają tooagree administratora, aby zdecydować, aplikacje, które używają usługi Azure AD do uwierzytelniania oAuth.  Powinien być kierowany bez informujący o tym, że tylko administratorzy mogą wyrazić zgodę toolarger zakresy i bardziej znaczących uprawnienia.
* Użytkownikom dodawanie i pozwalając tooaccess aplikacje, które dane są poddawane inspekcji zdarzeń, aby wyświetlić raporty dotyczące inspekcji hello w toodetermine portalu zarządzania Azure hello jak aplikacji dodano toohello katalogu.

**Uwaga:** *Microsoft sam działał za pomocą konfiguracji domyślnej hello teraz wiele miesięcy.*

Biorąc pod uwagę, że stwierdziła, że jest możliwe tooprevent użytkownicy w katalogu z Dodawanie aplikacji i wykonywać uznania za pośrednictwem jakie informacje są współużytkowane z aplikacji przez zmodyfikowanie konfiguracji katalogu w portalu zarządzania Azure hello.  Witaj następującej konfiguracji są dostępne w portalu zarządzania Azure hello karty "Konfiguruj" w katalogu.

![Zrzut ekranu przedstawiający hello interfejsu użytkownika do konfigurowania ustawień zintegrowanych aplikacji][app_settings]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat tooadd tooAzure aplikacji usługi AD i jak tooconfigure usług dla aplikacji.

* Deweloperzy: [Dowiedz się jak toointegrate aplikacji przy użyciu usługi AAD](https://msdn.microsoft.com/library/azure/dn151122.aspx)
* Deweloperzy: [Przejrzyj przykładowy kod dla aplikacji, zintegrowany z usługą Azure Active Directory w witrynie GitHub](https://github.com/AzureADSamples)
* Deweloperów i specjalistów IT: [hello Azure Active Directory interfejsu API programu Graph hello w dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/hh974478.aspx)
* Informatycy: [Dowiedz się, jak toouse usługi Azure Active Directory wstępnie zintegrowanych aplikacji od hello galerii aplikacji](https://msdn.microsoft.com/library/azure/dn308590.aspx)
* Informatycy: [samouczki dotyczące konfigurowania określonych wstępnie zintegrowanych aplikacji](https://msdn.microsoft.com/library/azure/dn893637.aspx)
* Informatycy: [Dowiedz się, jak toopublish przy użyciu aplikacji hello Azure Proxy aplikacji usługi Active Directory](https://msdn.microsoft.com/library/azure/dn768219.aspx)

## <a name="see-also"></a>Zobacz też
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](../active-directory-apps-index.md)

<!--Image references-->
[apps_service_principals_directory]:../media/active-directory-how-applications-are-added/HowAppsAreAddedToAAD.jpg
[app_settings]:../media/active-directory-how-applications-are-added/IntegratedAppSettings.jpg
