---
title: "Usługa Azure Active Directory B2C: Rozwiązywanie problemów dotyczących zasad niestandardowych | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat podejścia toosolving błędy podczas pracy z niestandardowych zasad w usłudze Azure Active Directory."
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: joroja
ms.openlocfilehash: b9e1b46df1ddb29cdb90953e4a0d6f1dd085441f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a>Rozwiązywanie problemów z niestandardowych zasad usługi Azure AD B2C i Framework obsługi tożsamości

Jeśli używasz usługi Azure Active Directory B2C zasad niestandardowych (Azure AD B2C), mogą pojawić się wyzwania Konfigurowanie hello Framework środowisko tożsamości w formacie XML język zasad.  Learning toowrite niestandardowych zasad może być jak uczenia nowego języka. W tym artykule opisano narzędzia i wskazówki, które mogą ułatwić szybkie odnajdywanie i rozwiązywania problemów. 

> [!NOTE]
> Ten artykuł skupia się na rozwiązywaniu problemów z konfiguracją zasad niestandardowych usługi Azure AD B2C. Nie jej adres hello jednostki uzależnionej aplikacji lub jej biblioteki tożsamości.

## <a name="xml-editing"></a>Edytowanie XML

Witaj najczęściej wystąpił błąd podczas konfigurowania niestandardowych zasad jest nieprawidłowo sformatowany XML. Niemal ważne jest dobrym edytora XML. Dobrym edytora XML Wyświetla XML w sposób macierzysty, color-codes zawartości powoduje wstępne wypełnienie typowe terminy, przechowuje elementy XML indeksowane i sprawdzić ze schematem. Poniżej przedstawiono dwa naszych ulubionych edytory XML:

* [Visual Studio Code](https://code.visualstudio.com/)
* [Notatnik ++](https://notepad-plus-plus.org/)

Sprawdzanie poprawności schematu XML identyfikuje błędy, aby przesłać plik XML. W folderze głównym hello hello początkowego pakietu Pobierz definicję schematu XML hello TrustFrameworkPolicy_0.3.0.0.xsd. Aby uzyskać więcej informacji, w dokumentacji hello w edytorze XML, wyszukaj *narzędzia XML* i *sprawdzanie poprawności kodu XML*.

Przegląd reguł XML może okazać się przydatne. Usługa Azure AD B2C odrzuca wszystkie formatowania błędów wykrytych XML. Czasami niepoprawnie sformatowany XML może spowodować komunikaty o błędach, które są błędne.

## <a name="upload-policies-and-policy-validation"></a>Zasady przekazywania i sprawdzanie zasad

 Sprawdzanie poprawności kodu XML pliku przekazywania odbywa się automatycznie. Większość błędów powodują hello toofail przekazywania. Sprawdzanie poprawności obejmuje hello pliku zasad, które przekazujesz. Zawiera również łańcucha hello plików hello przekazywanego pliku odwołuje się zbyt (hello jednostki uzależnionej pliku zasad firmy, hello rozszerzeń plików i hello pliku podstawowego). 
 
 Typowe błędy sprawdzania poprawności obejmują następujące hello.

Fragment kodu błędu:`... makes a reference tooClaimType with id "displaName" but neither hello policy nor any of its base policies contain such an element`
* Hello wartość typu oświadczenia mogą być zawiera błąd pisowni lub nie istnieje w schemacie hello.
* Typ oświadczenia wartości muszą być zdefiniowane w co najmniej jednego z plików hello w zasadach hello. 
    Na przykład: ` <ClaimType Id="socialIdpUserId">`
* Jeśli typ oświadczenia jest zdefiniowana w pliku rozszerzenia hello, ale jest również używana wartość TechnicalProfile w pliku podstawowego hello, przekazywanie pliku podstawowego hello powoduje błąd.

Fragment kodu błędu:`...makes a reference tooa ClaimsTransformation with id...`
* Witaj przyczyny dla hello błąd może być hello takie same jak w przypadku błędu typu oświadczenia hello.

Fragment kodu błędu:`Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order toomanage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`
* Sprawdź tego wartość TenantId hello hello  **\<TrustFrameworkPolicy\>**  i  **\<BasePolicy\>**  elementy zgodne urządzenie docelowe usługi Azure AD B2C Dzierżawca.  

## <a name="troubleshoot-hello-runtime"></a>Rozwiązywanie problemów z hello środowiska wykonawczego

* Użyj `Run Now` i `https://jwt.io` tootest zasad niezależnie od sieci web lub aplikacji mobilnej. Ta witryna sieci Web działa jak jednostki uzależnionej aplikacji firmy. Wyświetla zawartość hello hello JSON Web Token (JWT) generowany przez zasady usługi Azure AD B2C. toocreate aplikacja testowa, w ramach obsługi tożsamości, użyj hello następujące wartości:
    * Nazwa: TestApp
    * Aplikacja/interfejs API sieci Web w sieci Web: nie
    * Aplikacja Native client: nie

* tootrace hello wymiana wiadomości między przeglądarki klienta i usługi Azure AD B2C, użyj [Fiddler](http://www.telerik.com/fiddler). Może pomóc Ci wskazanie gdzie podróży użytkownika nie działa prawidłowo w krokach Twojej aranżacji.

* W **tryb programowania**, użyj **usługi Application Insights** tootrace działania hello podróży Framework obsługi tożsamości użytkownika. W **tryb programowania**, można obserwować exchange hello oświadczeń między hello Framework obsługi tożsamości i jeśli hello różnych dostawców, którzy są definiowane przez techniczne profile, takie jak dostawców tożsamości, oparty na interfejsach API usług Hello Azure AD B2C katalogu użytkowników i innych usług, takich jak Azure kilku-Factor uwierzytelniania.  

## <a name="recommended-practices"></a>Zalecane wskazówki

**Przechowywać wiele wersji scenariuszy. Grupowania ich w projekcie z aplikacją.** Hello base, rozszerzenia i jednostki uzależnionej plików firm są bezpośrednio zależne od siebie nawzajem. Zapisz je jako grupa. Nowe funkcje zostaną dodane zasady tooyour, zachować różne wersje robocze. Etap wersji pracy w ramach własnego pliku system z kodem aplikacji hello, które współdziałają z.  Aplikacje mogą wywoływać wiele różnych jednostki uzależnionej zasady firmy, w dzierżawie. Mogą być zależne od hello oświadczenia, które oczekiwane z zasad usługi Azure AD B2C.

**Opracowanie i przetestowanie techniczne profile z użyciem podróże znanych użytkowników.** Użyj przetestowane początkowego pakietu zasady tooset zapasowej profili technicznych. Testowane oddzielnie przed włączyć je do własnych podróże użytkownika.

**Opracowanie i przetestowanie podróże użytkownika z profilami techniczne przetestowane.** Zmień kroki aranżacji hello podróży użytkownika przyrostowo. Kompilacji stopniowego zamierzonego scenariuszy.

## <a name="next-steps"></a>Następne kroki

* W usłudze GitHub Pobierz plik zip (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) [active-directory-b2c-custom-policy-starterpack] hello.
