---
title: aaaConfigure Azure AD z logowania jednokrotnego dla aplikacji | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak usługa tooself łączyć tooAzure aplikacji usługi Active Directory przy użyciu SAML i Usługa rejestracji Jednokrotnej opartego na hasłach"
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 0d42eb0c-6d3f-4557-9030-e88e86709a19
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.reviewer: luleon
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 002a19a6c7ad25ea2f3b9c6a7c7874ed2be23cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-single-sign-on-tooapplications-that-are-not-in-hello-azure-active-directory-application-gallery"></a>Konfigurowanie jednego logowania jednokrotnego tooapplications, które nie znajdują się w galerii aplikacji hello Azure Active Directory
Ten artykuł dotyczy funkcja, która umożliwia administratorom tooconfigure pojedynczego logowania jednokrotnego tooapplications nie znajduje się w galerii aplikacji usługi Azure Active Directory hello *bez pisania kodu*. Ta funkcja została wydana z wersji zapoznawczej technical preview 18 listopada 2015 i znajduje się w [Azure Active Directory Premium](active-directory-editions.md). Jeśli zamiast tego Wyszukaj wskazówki dla deweloperów na temat toointegrate niestandardowych aplikacji w usłudze Azure AD za pomocą kodu, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](active-directory-authentication-scenarios.md).

Witaj galerii aplikacji usługi Azure Active Directory zawiera listę aplikacji, które są znane toosupport formularza rejestracji jednokrotnej z usługą Azure Active Directory, zgodnie z opisem w [w tym artykule](active-directory-appssoaccess-whatis.md). Po (jako IT specjalistyczne lub system integratora w organizacji) znalezieniu aplikacji hello ma tooconnect, możesz rozpocząć pracę przez wykonaj hello instrukcje krok po kroku przedstawiony w hello Azure management portal tooenable rejestracji jednokrotnej.

Klienci z [Azure Active Directory Premium](active-directory-editions.md) licencji również uzyskać te dodatkowe możliwości:

* Samoobsługowe integracji z dowolnej aplikacji, która obsługuje dostawców tożsamości SAML 2.0 (zainicjował SP lub inicjowane IdP)
* Samoobsługowe integracji z dowolnej aplikacji sieci web, która ma oparty na języku HTML strony logowania przy użyciu [opartego na hasłach logowania jednokrotnego](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Połączenie aplikacji, które używają protokołu SCIM hello do inicjowania obsługi użytkowników samoobsługi ([opisanych tutaj](active-directory-scim-provisioning.md))
* Możliwość tooadd łączy tooany aplikacji hello [uruchamiania aplikacji usługi Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) lub hello [panel dostępu usługi Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)

To nie tylko aplikacji SaaS używać, ale nie zostały jeszcze toohello dodawanej w galerii aplikacji Azure AD, ale aplikacje sieci web innych firm, które w organizacji wdrożono tooservers kontrolę w chmurze hello lub lokalnymi.

Te możliwości, nazywany również *szablony integracji aplikacji*, podaj punkty połączenia oparte na standardach aplikacji, które obsługują SAML, SCIM lub uwierzytelnianie oparte na formularzach i obejmują elastyczne opcje i ustawienia dla zgodności z szerokim liczbę aplikacji. 

## <a name="adding-an-unlisted-application"></a>Dodawanie nieznajdujące się na liście aplikacji
tooconnect aplikacji przy użyciu szablonu usługi integracji aplikacji, zaloguj się do portalu zarządzania Azure hello przy użyciu konta administratora usługi Azure Active Directory i Przeglądaj toohello **usługi Active Directory > [katalog] > aplikacje**zaznacz **Dodaj**, a następnie **dodać aplikację z galerii hello**. 

![][1]

W galerii aplikacji hello, można dodać nieznajdujące się na liście aplikacji za pomocą hello **niestandardowy** kategorii po lewej stronie powitania lub wybierając hello **Dodawanie nieznajdujące się na liście aplikacji** łącze, które jest wyświetlany w obszarze wyszukiwania hello wyników, jeśli żądanej aplikacji Nie można znaleźć. Po wprowadzeniu nazwy aplikacji, można skonfigurować hello pojedynczego logowania jednokrotnego opcje i zachowania. 

**Szybkie porady**: najlepszym rozwiązaniem, użyj toosee toocheck funkcja wyszukiwania hello, jeśli aplikacja hello już istnieje w galerii aplikacji hello. Jeśli zostanie znaleziony aplikacji hello i podaje opis "jednokrotne", a następnie aplikacja hello jest już obsługiwana federacyjnego logowania jednokrotnego. 

![][2]

Dodawanie aplikacji w ten sposób zapewnia bardzo podobne toohello środowisko, dostępna dla wstępnie zintegrowanych aplikacji. toostart, wybierz opcję **skonfigurować logowanie jednokrotne**. następnym ekranie powitania przedstawia hello następujące trzy opcje dotyczące konfigurowania rejestracji jednokrotnej, które zostały opisane w hello następujące sekcje.

![][3]

## <a name="azure-ad-single-sign-on"></a>Azure AD rejestracji jednokrotnej
Wybierz tej opcję tooconfigure SAML uwierzytelniania dla aplikacji hello. Takie rozwiązanie wymaga hello obsługę aplikacji SAML 2.0 i należy zbierać informacje dotyczące sposobu toouse hello SAML możliwości aplikacji hello przed kontynuowaniem. Po wybraniu **dalej**, będzie tooenter zostanie wyświetlony monit o trzech różnych adresów URL odpowiadającego toohello SAML punktów końcowych aplikacji hello. 

![][4]

Są to:

* **Zaloguj się na adres URL (SP inicjowane tylko)** — w przypadku, gdy użytkownik hello przechodzi toothis toosign w aplikacji. Jeśli aplikacja hello jest skonfigurowana jednym inicjowanych przez dostawcę usługi tooperform logowania, następnie gdy użytkownik nawiguje toothis adres URL, dostawcy usług hello będzie hello niezbędne przekierowanie tooAzure AD tooauthenticate i zaloguj się na powitania użytkownika w. Jeśli to pole zostanie wypełnione, usługi Azure AD będą używać tej aplikacji hello toolaunch adres URL z usługi Office 365 i hello Panel dostępu usługi Azure AD. Jeśli to pole jest ommited, po czym usługi Azure AD będzie zamiast tego wykonaj dostawcy tożsamości-jednokrotnego inicjowane logowania po hello aplikacja jest uruchamiana z usługi Office 365, hello Panel dostępu usługi Azure AD lub hello Azure AD pojedynczego adresu URL (copiable z karty Pulpit nawigacyjny hello).
* **Adres URL wystawcy** — adres URL wystawcy hello musi jednoznacznie wskazywać aplikacji hello, dla których jednym logowania jest skonfigurowane. Jest to wartość hello Azure AD i wysyła wstecz tooapplication jako hello **odbiorców** parametr hello tokenu SAML i aplikacji hello jest oczekiwany toovalidate go. Ta wartość jest także wyświetlany jako hello **identyfikator jednostki** w dowolnym metadanych SAML podał aplikacji hello. W dokumentacji SAML aplikacji hello szczegółowe informacje o tym, co jest identyfikator jednostki lub jest wartość odbiorców. Poniżej znajduje się przykład sposobu wyświetlania hello odbiorców adresu URL w aplikacji toohello zwrócony tokenu SAML hello:

```
    <Subject>
    <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:unspecificed">chad.smith@example.com</NameID>
        <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
      </Subject>
      <Conditions NotBefore="2014-12-19T01:03:14.278Z" NotOnOrAfter="2014-12-19T02:03:14.278Z">
        <AudienceRestriction>
          <Audience>https://tenant.example.com</Audience>
        </AudienceRestriction>
      </Conditions>
```

* **Adres URL odpowiedzi** — adres URL odpowiedzi hello jest, gdzie aplikacja hello oczekuje tokenu SAML hello tooreceive. Dotyczy to również hello tooas określonego **adres URL usługi konsumenta potwierdzenia (ACS)**. Sprawdź aplikacji hello SAML dokumentacji, aby uzyskać szczegółowe informacje o możliwościach jego adres URL odpowiedzi tokenu SAML lub adres URL usługi ACS.
  Po te zostały wprowadzone, kliknij przycisk **dalej** tooproceed toohello następnego ekranu. Ten ekran informuje o jakie toobe potrzeb skonfigurowane na powitania aplikacji po stronie tooenable tooaccept tokenu SAML z usługi Azure AD. 

![][5]

Wartości, które są wymagane będą się różnić w zależności od aplikacji hello, więc spróbuj aplikacji hello SAML dokumentacji, aby uzyskać szczegółowe informacje. Witaj **logowania jednokrotnego** i **wylogowania** adres URL usługi oba rozwiązania toohello tego samego punktu końcowego, który jest hello SAML żądania obsługi z punktu końcowego dla swojego wystąpienia usługi Azure AD. adres URL wystawcy Hello jest wartość hello, który jest wyświetlany jako "Wystawcy" hello, wewnątrz hello aplikacji toohello wystawionego tokenu SAML. 

Po skonfigurowaniu aplikacji kliknij **dalej** przycisk, a następnie hello **Complete** tooclose hello w oknie dialogowym. 

## <a name="assigning-users-and-groups-tooyour-saml-application"></a>Przypisywanie użytkowników i grup tooyour SAML aplikacji
Gdy aplikacja została skonfigurowana toouse usługi Azure AD jako dostawca tożsamości SAML na podstawie, to tootest już prawie gotowe. Jako formant zabezpieczeń usługi Azure AD nie będzie wystawiać token, dzięki czemu toosign do aplikacji hello jeśli przyznano im dostęp przy użyciu usługi Azure AD. Użytkownicy mogą otrzymać dostęp bezpośrednio lub za pośrednictwem grupy, które są członkami. 

tooassign aplikacji tooyour użytkownika lub grupę, kliknij przycisk hello **Przypisz użytkowników** przycisku. Wybierz hello użytkownik lub grupa ma tooassign, a następnie wybierz hello **przypisać** przycisku. 

![][6]

Przypisanie użytkownika umożliwi tooissue usługi Azure AD token dla użytkownika hello, a także powoduje kafelka w celu tooappear tej aplikacji w panelu dostępu hello użytkownika. Kafelka aplikacji również będą wyświetlane w uruchamiania aplikacji hello usługi Office 365, jeśli użytkownik hello korzysta z usługi Office 365. 

Możesz przekazać logo kafelka dla aplikacji hello przy użyciu hello **przekazać Logo** przycisk na powitania **Konfiguruj** kartę aplikacji hello. 

### <a name="customizing-hello-claims-issued-in-hello-saml-token"></a>Dostosowywanie hello oświadczeń wydanych w tokenie SAML hello
Podczas uwierzytelniania użytkownika toohello aplikacji, usługi Azure AD wystawia aplikacji toohello tokenu SAML, który zawiera informacje (lub oświadczenia) dotyczące hello użytkownika, który unikatowo identyfikuje je. Domyślnie w tym nazwę użytkownika, adres e-mail, imię i nazwisko hello użytkownika. 

Umożliwia wyświetlenie i edytowanie hello oświadczenia wysyłane w hello toohello tokenu SAML na podstawie hello **atrybuty** kartę. 

![][7]

Istnieją dwie możliwe przyczyny, dlaczego może być konieczne tooedit hello oświadczeń wydanych w tokenie SAML hello: •hello aplikacji została zapisana toorequire inny zestaw oświadczeń identyfikatorów URI lub oświadczeń wartości •Your aplikacja została wdrożona w taki sposób, który wymaga hello NameIdentifier oświadczeń toobe inną niż hello username (AKA główna nazwa użytkownika) przechowywanych w usłudze Azure Active Directory. 

Aby uzyskać informacje dotyczące sposobu tooadd i Edycja oświadczeń dotyczących następujących scenariuszy, zapoznaj się to [artykuł na temat dostosowywania oświadczeń](active-directory-saml-claims-customization.md). 

### <a name="testing-hello-saml-application"></a>Testowanie aplikacji SAML hello
Po hello SAML URL i certyfikatu zostały skonfigurowane w usłudze Azure AD i w aplikacji hello, użytkowników lub grup z przypisanym toohello aplikacji na platformie Azure i oświadczeń hello zostały sprawdzone i edytować, jeśli to konieczne, a następnie użytkownik hello jest gotowy toosign na powitania aplikacja. 

tootest, po prostu znak w hello Azure AD panelu dostępu pod adresem https://myapps.microsoft.com przy użyciu konta użytkownika, że przypisany toohello aplikacji, a następnie kliknij Kafelek powitania dla tookick aplikacji hello poza hello pojedynczy proces rejestrowania. Alternatywnie możesz przeglądać bezpośrednio toohello adres URL logowania jednokrotnego dla aplikacji hello i logowania z tego miejsca. 

Debugowanie wskazówki, zobacz [artykuł na temat toodebug SAML na podstawie pojedynczego logowania jednokrotnego tooapplications](active-directory-saml-debugging.md) 

## <a name="password-single-sign-on"></a>Hasło logowania jednokrotnego
Wybierz ten tooconfigure opcji [opartego na hasłach rejestracji jednokrotnej](active-directory-appssoaccess-whatis.md) dla aplikacji sieci web, z HTML strony logowania. Logowanie Jednokrotne opartego na hasłach, również tooas określonego hasła vaulting, umożliwia toomanage użytkownika dostępu i hasła tooweb aplikacje, które nie obsługują federacji tożsamości. Jest również przydatne w przypadku scenariuszy, w których wielu użytkowników musi tooshare jednego konta, takich jak konta aplikacji mediów społecznościowych tooyour organizacji. 

Po wybraniu **dalej**, będzie tooenter zostanie wyświetlony monit o hello adres URL aplikacji hello opartych na sieci web strony logowania. Należy pamiętać, że musi to być stronie powitania, zawierającej hello nazwy użytkownika i hasła pól wejściowych. Raz wprowadzona, Azure AD uruchamia proces tooparse hello strony logowania do wprowadzania nazwy użytkownika i wprowadzania hasła. Jeśli proces hello zakończy się niepowodzeniem, następnie kolejno alternatywny proces instalowania rozszerzenia przeglądarki (wymaga programu Internet Explorer, Chrome lub Firefox), co umożliwi toomanually przechwytywania hello pól.

Po przechwyceniu hello strony logowania, można przypisać użytkowników i grup i poświadczeń zasady można ustawić tak jak zwykły [hasło logowania jednokrotnego aplikacji](active-directory-appssoaccess-whatis.md).

Uwaga: Możesz przekazać logo kafelka dla aplikacji hello przy użyciu hello **przekazać Logo** przycisk na powitania **Konfiguruj** kartę aplikacji hello. 

## <a name="existing-single-sign-on"></a>Istniejące rejestracji jednokrotnej
Wybierz łącze tooan aplikacji tooyour organizacji Panel dostępu usługi Azure AD lub usługi Office 365 portalu tooadd tej opcji. Można użyć tego tooadd łącza toocustom aplikacji sieci web, które obecnie używają usługi Azure Active Directory Federation Services (lub innej usługi federacyjnej), zamiast usługi Azure AD na potrzeby uwierzytelniania. Lub można dodać strony programu SharePoint toospecific linków bezpośrednich lub innych stron sieci web, po prostu chcesz tooappear na panele dostępu użytkownika. 

Po wybraniu **dalej**, będzie adres URL hello zostanie wyświetlony monit o tooenter toolink aplikacji hello do. Po ukończeniu użytkowników i grup można przypisać toohello aplikacji, co powoduje, że tooappear aplikacji hello w hello [uruchamiania aplikacji usługi Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) lub hello [panel dostępu usługi Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) dla tych użytkowników.

Uwaga: Możesz przekazać logo kafelka dla aplikacji hello przy użyciu hello **przekazać Logo** przycisk na powitania **Konfiguruj** kartę aplikacji hello.

## <a name="related-articles"></a>Pokrewne artykuły
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [W jaki sposób tooCustomize oświadczenia wydane w hello tokenu SAML dla aplikacji Pre-Integrated](active-directory-saml-claims-customization.md)
* [Rozwiązywanie problemów z systemem SAML logowania jednokrotnego](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saas-custom-apps/customapp1.png
[2]: ./media/active-directory-saas-custom-apps/customapp2.png
[3]: ./media/active-directory-saas-custom-apps/customapp3.png
[4]: ./media/active-directory-saas-custom-apps/customapp4.png
[5]: ./media/active-directory-saas-custom-apps/customapp5.png
[6]: ./media/active-directory-saas-custom-apps/customapp6.png
[7]: ./media/active-directory-saas-custom-apps/customapp7.png
