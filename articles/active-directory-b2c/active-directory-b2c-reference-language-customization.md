---
title: "Usługi Azure Active Directory B2C: Dostosowywanie języka przy użyciu | Dokumentacja firmy Microsoft"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: sama
ms.openlocfilehash: a8e4037014f5adf929dac7b5dc4db72ba0f5b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a>Usługi Azure Active Directory B2C: Dostosowywanie języka przy użyciu

>[!NOTE] 
>Ta funkcja jest dostępna w publicznej wersji zapoznawczej.  Zalecane jest użycie dzierżawy testowej podczas używania tej funkcji.  Nie planujemy zmiany podziału hello Podgląd toohello ogólnodostępnej wersji, ale możemy zarezerwować toomake prawo hello takich funkcji hello tooimprove zmian.  Gdy już funkcji tootry szansy, podaj opinii na temat doświadczeniami i jak firma Microsoft może ją ulepszyć.  Musisz podać informacje zwrotne przez hello portalu Azure narzędziem krój uśmiech hello na powitania w prawym górnym narożniku.   Jeśli istnieje wymaganie biznesowe dla toogo należy na żywo, za pomocą tej funkcji w fazie Podgląd hello, Przekaż nam scenariuszy i firma Microsoft zapewnia pomoc i wskazówki prawidłowego hello.  Skontaktuj się z nami pod adresem [ aadb2cpreview@microsoft.com ](mailto:aadb2cpreview@microsoft.com).

Dostosowywanie języka umożliwia toochange tooa toosuit innego języka, który klient potrzebuje podróży użytkownika.  Firma Microsoft udostępnia tłumaczenia dla 36 języków (zobacz [dodatkowe informacje](#additional-information)).  Nawet jeśli środowiska jest dostępna wyłącznie dla jednego języka, można dostosować tekst na powitania stron toosuit potrzeb.  

## <a name="how-does-language-customization-work"></a>Jak działa dostosowania języka?
Dostosowywanie języka umożliwia tooselect języki są dostępne w podróży użytkownika.  Po włączeniu funkcji hello, musisz podać parametr ciągu zapytania hello, ui_locales, z poziomu aplikacji.  Po wywołaniu do usługi Azure AD B2C, firma Microsoft tłumaczenia ustawienia regionalne toohello strony, który został wskazany.  Za pomocą typ konfiguracji zapewnia pełną kontrolę nad języków hello w podróży użytkownika i ignoruje ustawienia języka hello powitania klienta przeglądarki. Można również nie może być konieczne tego poziomu kontroli nad jakich języków, zobacz klienta.  Jeśli nie podasz parametru ui_locales powitania klienta zależy ustawienia ich przeglądarki.  Można wybrać, które języki podróży użytkownika jest przetłumaczony tooby dodanie go jako obsługiwanego języka.  Jeśli przeglądarka klienta jest zestaw tooshow język nie ma toosupport, a następnie hello język zamiast pokazany domyślne w obsługiwanych kultur.

1. **Ustawienia regionalne interfejsu użytkownika określony język** — po włączeniu dostosowania języka podróży użytkownika jest język tłumaczenia toohello określone w tym miejscu
2. **Przeglądarka żądany język** — Jeśli nie określono żadnych interfejs użytkownika ustawień regionalnych, dokonuje translacji toohello przeglądarki żądany język **Jeśli została ona uwzględniona w obsługiwane języki**
3. **Język domyślny zasad** — Jeśli hello przeglądarki nie określa język, lub określa, który nie jest obsługiwany, dokonuje translacji toohello zasady domyślny język

>[!NOTE]
>Jeśli używane są atrybuty niestandardowe użytkownika, należy tooprovide własne tłumaczenia. Zobacz "[dostosować z ciągów](#customize-your-strings)" Aby uzyskać więcej informacji.
>

## <a name="support-uilocales-requested-languages"></a>Obsługa ui_locales żądane języki 
Przez włączenie "Języka dostosowania" zasady, teraz można kontrolować języka hello hello użytkownika podróży, dodając parametr ui_locales hello.
1. [Wykonaj te bloku funkcji B2C toohello kroki toonavigate na powitania portalu Azure.](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. Przejdź tooa zasad mają tooenable dla tłumaczenia.
3. Kliknij przycisk **dostosowywania języka**.
4. Przeczytaj uważnie ostrzeżenie hello.  Po włączeniu, nie można wyłączyć "Dostosowania język".
5. Włącz funkcję hello, a następnie kliknij przycisk **OK**.
6. Zapisz zasady na powitania lewego górnego rogu Twojej **edytować zasady** bloku.

## <a name="select-which-languages-your-user-journey-supports"></a>Wybierz języki, które obsługuje podróży użytkownika 
Utwórz listę języków dozwolonych dla Twojego toobe podróży użytkownika przetłumaczony na, jeśli nie podano parametru ui_locales hello.
1. Sprawdź, czy zasady zostały "Języka dostosowania" włączyć za pomocą czynności opisanych.
2. Z sieci **edytować zasady** bloku, wybierz opcję **dostosowywania języka**.
3. Podjęto tooyour **obsługiwanych języków** bloku.  W tym miejscu można wybrać **Dodaj język**.
4. Wybierz wszystkie języki hello, które chcesz toobe obsługiwane.  

>[!NOTE]
>Jeśli nie podano parametru ui_locales, następnie strony hello jest język przeglądarki klienta przetłumaczonego toohello tylko wtedy, gdy znajduje się na tej liście
>

5. Kliknij przycisk **Ok** u dołu hello
6. Zamknij hello **dostosowywania języka** bloku i **zapisać** zgodnie z zasadami.

## <a name="customize-your-strings"></a>Dostosowywanie z ciągów
"Język dostosowania" umożliwia toocustomize dowolnego ciągu w podróży użytkownika.
1. Sprawdź, czy zasady zostały "Języka dostosowania" hello czynności opisanych można włączyć.
2. Z sieci **edytować zasady** bloku, wybierz opcję **dostosowywania języka**.
3. Wybierz z menu nawigacji po lewej stronie powitania **pobierania zawartości**.
4. Wybierz stronę hello ma tooedit.
5. W polu listy rozwijanej hello wybierz hello język tooedit dla.
6. Kliknij pozycję **Pobierz**. 

Następujące kroki umożliwiają służy toostart Edycja ciągów z pliku JSON.

### <a name="changing-any-string-on-hello-page"></a>Zmiana dowolny ciąg na stronie powitania
1. Witaj Otwórz plik JSON pobrane z czynności opisanych w części edytora JSON.
2. Znajdź element hello ma toochange.  Można znaleźć hello `StringId` ciąg hello szukasz, lub Wyszukaj hello `Value` ma toochange.
3. Aktualizacja hello `Value` atrybut o to, co ma być wyświetlany.
4. Zapisz plik hello i Przekaż zmiany.

### <a name="changing-extension-attributes"></a>Zmienianie atrybutów rozszerzenia
Jeśli szukasz atrybut użytkownika niestandardowego ciąg hello toochange lub mają jeden toohello tooadd JSON, znajduje się w hello następującego formatu:
```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": false,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```
>[!IMPORTANT]
>Jeśli potrzebujesz toooverride ciąg, upewnij się hello tooset `Override` wartość zbyt`true`.  Jeśli hello wartość nie ulega zmianie, hello wpis zostanie zignorowany. 
>

Zastąp `<ExtensionAttribute>` o nazwie hello atrybut użytkownika niestandardowego.  
Zastąp `<ExtensionAttributeValue>` z hello nowe toobe ciąg wyświetlany.

### <a name="using-localizedcollections"></a>Przy użyciu LocalizedCollections
Jeśli chcesz tooprovide listę zestaw wartości dla odpowiedzi, należy toocreate `LocalizedCollections`.  A `LocalizedCollections` jest tablicą `Name` i `Value` pary.  Witaj `Name` wyświetleniem a hello `Value` to, co jest zwracany w hello oświadczeń.  tooadd `LocalizedCollections`, ma hello następującego formatu:

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType", 
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": false,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```
>[!IMPORTANT]
>Jeśli potrzebujesz toooverride ciąg, upewnij się hello tooset `Override` wartość zbyt`true`.  Jeśli hello wartość nie ulega zmianie, hello wpis zostanie zignorowany. 
>

* `ElementId`jest hello użytkownika atrybutu tego `LocalizedCollections` odpowiedzi
* `Name`jest hello wartości wyświetlane toohello użytkownika
* `Value`jest to, co jest zwracany w oświadczeń hello po wybraniu tej opcji

### <a name="upload-your-changes"></a>Przekazywanie zmian
1. Po zakończeniu pliku JSON tooyour zmiany hello, przejdź wstecz tooyour dzierżawy B2C.
2. Z sieci **edytować zasady** bloku, wybierz opcję **dostosowywania języka**.
3. Wybierz z menu nawigacji po lewej stronie powitania **przekazać zawartość**.
4. Wybierz stronę hello, którą chcesz tooupload zmiany na.
5. Jeśli chcesz tooupload wcześniej podane JSON dla języka, należy toodelete hello poprzedniej pozycji.  Usuń go, klikając hello `...` hello prawo tego języka i wybierz **usunąć**.
6. Kliknij przycisk **Dodaj** na powitania lewym górnym rogu.
7. Wybierz język hello pliku JSON.
8. Kliknij przycisk folder hello na powitania prawo, a następnie przejdź do pliku JSON.
9. Kliknij przycisk hello **przekazać** przycisk na powitania dolnej części bloku hello.
10. Przejdź wstecz tooyour **edytować zasady** bloku i kliknij przycisk **zapisać**.

## <a name="additional-information"></a>Dodatkowe informacje
### <a name="recommendations-for-language-customization"></a>Zalecenia dotyczące dostosowywania"język"
Zaleca się tylko wprowadzenie wpisy tooyour zasoby dla języka ciągi należy jawnie tooreplace chcesz.  Firma Microsoft wymusić pliku toohello limit rozmiaru skompilowany poza tłumaczeń JSON.  Jeśli pliki zbyt duży, ma wpływ na wydajność hello podróży użytkownika.
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a>Etykiety dostosowania interfejsu użytkownika strony są usuwane po włączeniu "Dostosowania języka"
Po włączeniu "Dostosowania języka" wcześniejszych zmian dla etykiet przy użyciu interfejsu użytkownika strony dostosowania zostaną usunięte z wyjątkiem atrybutów niestandardowych użytkownika.  Ta zmiana jest realizowane tooavoid powoduje konflikt, w którym można edytować z ciągów.  Możesz kontynuować toochange etykiet oraz innych ciągów przekazując zasobów językowych w "Dostosowania język".
### <a name="microsoft-is-committed-tooprovide-hello-most-up-to-date-translations-for-your-use"></a>Firma Microsoft dokłada tłumaczeń aktualną hello tooprovide zatwierdzone do użycia
Firma Microsoft będzie stale poprawy tłumaczenia i przechowywać w zgodności dla Ciebie.  Firma Microsoft będzie zidentyfikować usterki i zmiany w terminologii globalne i bezproblemowo udostępnić hello aktualizacje, które będą działać w podróży użytkownika.
### <a name="support-for-right-to-left-languages"></a>Obsługa języków od prawej do lewej
Nie jest obsługiwane dla języków od prawej do lewej, jeśli potrzebujesz tej funkcji należy głosowania dla tej funkcji na [opinii Azure](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).
### <a name="social-identity-provider-translations"></a>Społecznościowych tłumaczeń dostawcy tożsamości
Firma Microsoft udostępnia hello ui_locales OIDC parametru toosocial logowania, ale nie są honorowane przez niektórych dostawców tożsamości społecznościowych, w tym Facebook i Google. 
### <a name="browser-behavior"></a>Zachowanie przeglądarki
Chrome i Firefox żądania zarówno dla języka ich zestawu i jeśli jest obsługiwany, pojawi się przed hello domyślne.  Krawędź obecnie nie żąda języka i przejdzie do prostych toohello domyślny język.
### <a name="known-issues"></a>Znane problemy
* Przekazywanie zasobów językowych dla strony MFA hello w zasadach edycji profilu jest obecnie niedostępny.
* `LocalizedCollections`nie są generowane dla wartości, gdy jest to wymagane przez hello typ odpowiedzi
### <a name="what-if-i-want-a-language-that-isnt-supported"></a>Co zrobić, jeśli ma języka, który nie jest obsługiwany?
Firma Microsoft są planowania tooprovide rozszerzenie tej funkcji, umożliwiający tooupload zasobu JSON kierunku "języki niestandardowe".  Funkcja Hello pozwala toospecify hello nazwy i języka kodu dla żadnego języka i podaj *wszystkie* hello tłumaczenia dla tego języka.  Jeśli chcesz dodać tę funkcję, Wyślij do nas scenariusz w [ aadb2cpreview@microsoft.com ](mailto:aadb2cpreview@microsoft.com).  

### <a name="what-languages-are-supported"></a>Jakich języków są obsługiwane?

| Język              | Kod języka |
|-----------------------|---------------|
| Bengalski                | BN            |
| Czeski                 | cs            |
| Duński                | da            |
| Niemiecki                | de            |
| Grecki                 | el            |
| Polski               | en            |
| Hiszpański               | es            |
| Fiński               | fi            |
| Francuski                | fr            |
| Gudżarati              | gu            |
| Hindi                 | Cześć            |
| Chorwacki              | hr            |
| Węgierski             | hu            |
| Włoski               | it            |
| Japoński              | ja            |
| Kannada               | kN            |
| Koreański                | ko            |
| Malayalam             | uczenie maszynowe            |
| Marathi               | MR            |
| Malajski                 | MS            |
| Norweski (Nynorsk)      | nb            |
| Holenderski                 | nl            |
| Pendżabski               | dostawcy            |
| Polski                | pl            |
| Portugalski (Brazylia)   | pt-br         |
| Portugalski (Portugalia) | pt-pt         |
| Rumuński              | ro            |
| Rosyjski               | ru            |
| Słowacki                | SK            |
| Szwedzki               | sv            |
| Tamilski                 | Ta            |
| Telugu                | te            |
| Tajski                  | TH            |
| Turecki               | TR            |
| Chiński (uproszczony)  | zh-hans       |
| Chiński — tradycyjny | zh-hant       |
