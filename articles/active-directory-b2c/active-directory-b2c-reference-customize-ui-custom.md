---
title: "Usługa Azure Active Directory B2C: Odwołanie: dostosowywanie hello interfejsu użytkownika podróży użytkownika z zasady niestandardowe | Dokumentacja firmy Microsoft"
description: "Temat dotyczący zasad niestandardowych usługi Azure Active Directory B2C"
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
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 11f2a7575b95a186399d83266850fe44d650371b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-ui-of-a-user-journey-with-custom-policies"></a>Dostosowywanie hello interfejsu użytkownika podróży użytkownika przy użyciu zasad niestandardowych

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

> [!NOTE]
> W tym artykule jest zaawansowane opis działania dostosowywania interfejsu użytkownika i jak tooenable z zasady niestandardowe B2C, przy użyciu hello Framework obsługi tożsamości


Nie zakłóca pracy użytkowników jest kluczem dla dowolnego rozwiązania biznesowe z klientem. Przez nie zakłóca pracy użytkowników możemy oznacza środowisko na urządzeniu lub w przeglądarce, której przebieg użytkownika za pomocą naszej usługi nie mogą być wyodrębnione z powitania klienta usługi, którego używają.

## <a name="understand-hello-cors-way-for-ui-customization"></a>Zrozumieć sposób CORS hello do dostosowania interfejsu użytkownika

Usługa Azure AD B2C umożliwia możesz toocustomize hello wyglądu i działania środowisko użytkownika (UX) hello różne strony, które mogą potencjalnie obsłużonych i wyświetlane przez usługę Azure AD B2C za pomocą niestandardowych zasad.

W tym celu usługi Azure AD B2C uruchamia kod w przeglądarce sieci użytkownika i używa hello nowoczesnych oraz standardowe metody [udostępniania zasobów między źródłami (CORS)](http://www.w3.org/TR/cors/) tooload niestandardowej zawartości z określonego adresu URL, określonym w zasadach niestandardowych Szablony HTML5/CSS tooyour toopoint. CORS jest mechanizm umożliwiający ograniczone zasoby, takie jak czcionki na toobe strony sieci web, żądanie z innej domeny spoza domeny hello, z którego pochodzi hello zasobów.

W porównaniu toohello starego tradycyjny sposób, gdzie strony szablonów są własnością rozwiązania hello gdzie podane ograniczone tekstu i obrazów, gdzie ograniczone kontrolę nad układ i działanie zostało oferowane wiodące toomore niż tooachieve trudności bezproblemowe, hello CORS sposób obsługuje HTML5 i CSS i umożliwiają:

- Hostowanie zawartości hello i hello rozwiązania injects jego formantów za pomocą skryptu po stronie klienta.
- Mają pełną kontrolę nad każdego piksela układ i działania.

Możesz podać przez obsługuje tworzenie pliki HTML5/CSS, takich jak dowolną liczbę stron zawartości.

> [!NOTE]
> Ze względów bezpieczeństwa hello użycie JavaScript jest obecnie zablokowany do dostosowania. wymagany jest toounblock JavaScript, użycie nazwy domeny niestandardowej dla dzierżawy usługi Azure AD B2C.

W każdej z szablonów HTML5/CSS, można zapewnić *zakotwiczenia* element, który odpowiada toohello wymagane `<div id=”api”>` elementu hello HTML lub hello zawartości stronie jako ilustrują poniżej. Usługa Azure AD B2C musi mieć wszystkie strony z zawartością tego określonego div.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Your page content’s tile!</title>
  </head>
  <body>
    <div id="api"></div>
  </body>
</html>
```

Azure AD B2C związane z zawartości dla strony hello zostaną dodane do tego div podczas hello reszty strony hello jest Twój toocontrol. kod JavaScript Hello Azure AD B2C ściąga zawartości i injects naszych HTML do tego elementu div określone. Usługa Azure AD B2C injects powitania po formanty odpowiednio: konta formantu selektora, kontrolek logowania, wieloskładnikowego formantów (obecnie telefoniczny) i atrybutu kolekcji formantów. Usługa Azure AD B2C zapewnia, że wszystkie formanty hello są HTML5 zgodne i jest dostępny, wszystkie formanty hello można całkowicie stylem i że nie będzie zbadanie kontroli wersji.

Hello scaloną zawartość jest ostatecznie wyświetlana jako hello dynamiczne dokumentu tooyour konsumenta.

tooensure hello powyżej działa zgodnie z oczekiwaniami, należy:

- Upewnij się, że zawartość jest HTML5 zgodne i jest dostępny
- Upewnij się, że serwer zawartości jest włączona dla CORS.
- Udostępniać zawartość za pośrednictwem protokołu HTTPS.
- Używać bezwzględnych adresów URL, takie jak https://yourdomain/content dla wszystkich łączy i zawartość arkusza CSS.

> [!TIP]
> tooverify, który hello lokacji, które prowadzą hosting zawartości na ma włączonego mechanizmu CORS i żądań CORS testu, można użyć hello http://test-cors.org/ lokacji. Dziękujemy toothis lokacji, można po prostu wyślij hello CORS tooa serwer zdalny żądania (tootest, jeśli jest obsługiwana przez CORS), lub wysłać hello CORS żądania tooa testu serwera (tooexplore niektórych funkcji CORS).

> [!TIP]
> http://enable-cors.org/ lokacji Hello stanowi również ponad przydatne zasoby na CORS.

Dzięki toothis opartego na CORS, użytkownicy końcowi hello będzie miał spójne działanie od aplikacji i strony hello obsługiwanych przez usługę Azure AD B2C.

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu

Jako warunek wstępny należy toocreate konta magazynu. Konieczne będzie toocreate subskrypcji platformy Azure konta magazynu obiektów Blob Azure. Możesz utworzyć konto bezpłatnej wersji próbnej na powitania [witryny sieci Web Azure](https://azure.microsoft.com/en-us/pricing/free-trial/).

1. Otwórz sesję przeglądania i przejdź toohello [portalu Azure](https://portal.azure.com).
2. Zaloguj się przy użyciu poświadczeń administracyjnych.
3. Kliknij przycisk **nowy** > **dane i magazyn** > **konta magazynu**.  A **utworzyć konto magazynu** Otwiera blok.
4. W **nazwa**, podaj nazwę konta magazynu hello, na przykład *contoso369b2c*. Ta wartość zostanie później określonego jako zbyt*storageAccountName*.
5. Wybierz hello opcji odpowiednich dla hello warstwa cenowa, grupy zasobów hello i hello subskrypcji. Upewnij się, że masz hello **tooStartboard numeru Pin** zaznaczoną opcją. Kliknij przycisk **Utwórz**.
6. Przejdź wstecz toohello tablicy startowej, a następnie kliknij przycisk hello konta magazynu, który został właśnie utworzony.
7. W hello **usług** kliknij **obiekty BLOB**. A **bloku usługi Blob** otwiera.
8. Kliknij przycisk **+ kontener**.
9. W **nazwa**, na przykład Podaj nazwę kontenera hello *b2c*. Ta wartość będzie później określonego tooas *containerName*.
9. Wybierz **obiektu Blob** jako hello **dostęp typu**. Kliknij przycisk **Utwórz**.
10. na liście hello na powitania pojawi się Hello kontenera, w którym utworzono **bloku usługi Blob**.
11. Zamknij hello **obiekty BLOB** bloku.
12. Na powitania **bloku konto magazynu**, kliknij przycisk hello **klucza** ikony. **Bloku klucze dostępu** otwiera.  
13. Zanotuj wartość hello **klucz1**. Ta wartość zostanie później określonego jako *klucz1*.

## <a name="downloading-hello-helper-tool"></a>Pobieranie narzędzia pomocnika hello

1.  Pobierz narzędzie Pomocnik hello z [GitHub](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip).
2.  Zapisz hello *B2C-AzureBlobStorage-klienta master.zip* plik na komputerze lokalnym.
3.  Wyodrębnij zawartość hello hello B2C-AzureBlobStorage-klienta master.zip pliku na dysku lokalnym, na przykład w obszarze hello **pakietu w przypadku dostosowania interfejsu użytkownika** folderu. Spowoduje to utworzenie *B2C-AzureBlobStorage-klienta master* folderu poniżej.
4.  Otwórz ten folder i Wyodrębnij zawartość hello pliku archiwum hello *B2CAzureStorageClient.zip* w nim.

## <a name="upload-hello-ui-customization-pack-sample-files"></a>Przekaż pliki przykładowe hello pakietu w przypadku dostosowania interfejsu użytkownika

1.  Przy użyciu Eksploratora Windows przejdź do folderu toohello *B2C-AzureBlobStorage-klienta master* znajduje się w obszarze hello *pakietu w przypadku dostosowania interfejsu użytkownika* folder utworzony w poprzedniej sekcji hello.
2.  Uruchom hello *B2CAzureStorageClient.exe* pliku. Ten program po prostu przekazać wszystkie pliki hello w katalogu hello Określ konto magazynu tooyour i włączyć CORS dostęp do tych plików.
3.  Po wyświetleniu monitu podaj:.  Witaj nazwę konta magazynu *storageAccountName*, na przykład *contoso369b2c*.
    b.  Witaj podstawowy klucz dostępu magazynu obiektów blob platformy azure, *klucz1*, na przykład *contoso369b2c*.
    c.  Witaj nazwa kontenera magazynu obiektów blob z magazynu *containerName*, na przykład *b2c*.
    d.  Ścieżka Hello hello *początkowego pakietu* próbki plików, na przykład *... \B2CTemplates\wingtiptoys*.

Po wykonaniu powyższych kroków hello hello pliki CSS i HTML5 hello *pakietu w przypadku dostosowania interfejsu użytkownika* dla fikcyjnej firmy hello **wingtiptoys** teraz wskazanie tooyour konta magazynu.  Możesz sprawdzić, czy zawartość hello został przesłany poprawnie przez otwarcie bloku pokrewne kontenera hello w hello portalu Azure. Alternatywnie można sprawdzić, czy zawartość hello został przesłany prawidłowo po zalogowaniu się do strony hello w przeglądarce. Aby uzyskać więcej informacji, zobacz [usługi Azure Active Directory B2C: Narzędzie Pomocnik użyć funkcji dostosowanie interfejsu użytkownika strony hello toodemonstrate](active-directory-b2c-reference-ui-customization-helper-tool.md).

## <a name="ensure-hello-storage-account-has-cors-enabled"></a>Upewnij się, że konto magazynu hello ma włączonego mechanizmu CORS

CORS (Cross-Origin Resource Sharing) musi być włączona na punkt końcowy dla usługi Azure AD B2C Premium tooload zawartości. Jest to spowodowane zawartości znajduje się w innej domenie niż domeny hello Premium usługi Azure AD B2C będzie obsługująca hello strony z.

tooverify z CORS włączone, hello magazynu, które prowadzą hosting zawartości na kontynuować hello następujące kroki:

1. Otwórz sesję przeglądania i przejdź do strony toohello *unified.html* przy użyciu hello pełny adres URL lokalizacji na koncie magazynu `https://<storageAccountName>.blob.core.windows.net/<containerName>/unified.html`. Na przykład https://contoso369b2c.blob.core.windows.net/b2c/unified.html.
2. Przejdź toohttp://test-cors.org. Ta witryna umożliwia tooverify możesz który hello strony, którego używasz ma włączonego mechanizmu CORS.  
<!--
![test-cors.org](../../media/active-directory-b2c-customize-ui-of-a-user-journey/test-cors.png)
-->

3. W **zdalnego adresu URL**, wprowadź pełny adres URL hello zawartości unified.html i kliknij przycisk **Wyślij żądanie**.
4. Sprawdź te dane wyjściowe hello w hello **wyniki** sekcja zawiera *stan XHR: 200*. Oznacza to, że włączono CORS.
<!--
![CORS enabled](../../media/active-directory-b2c-customize-ui-of-a-user-journey/cors-enabled.png)
-->
Konto magazynu Hello teraz powinna zawierać kontenera obiektów blob o nazwie *b2c* naszych ilustracji, który zawiera hello poniższych szablonów wingtiptoys z hello *początkowego pakietu*.

<!--
![Correctly configured storage account](../../articles/active-directory-b2c/media/active-directory-b2c-reference-customize-ui-custom/storage-account-final.png)
-->

Witaj poniższej tabeli opisano hello celem hello powyżej stron HTML5.

| Szablon HTML5 | Opis |
|----------------|-------------|
| *phonefactor.HTML* | Ta strona może służyć jako szablon dla strony uwierzytelniania wieloskładnikowego. |
| *ResetPassword.HTML* | Ta strona może służyć jako szablon dla nie pamiętasz hasła strony. |
| *selfasserted.HTML* | Ta strona może służyć jako szablon dla kont społecznościowych stronę tworzenia konta, stronę tworzenia konta lokalnego konta lub stronę logowania konta lokalnego. |
| *Unified.HTML* | Ta strona może służyć jako szablon ujednoliconego strony rejestracji lub logowania. |
| *updateprofile.HTML* | Ta strona może służyć jako szablon strony aktualizacji profilu. |

## <a name="add-a-link-tooyour-html5css-templates-tooyour-user-journey"></a>Dodaj łącze tooyour HTML5/CSS szablony tooyour użytkownika podróży

Można dodać łącza tooyour HTML5/CSS szablony tooyour użytkownika podróży bezpośrednio edytując zasad niestandardowych.

toouse Hello do szablonów niestandardowych HTML5/CSS w podróży użytkownika mają toobe określone na liście definicji zawartości, które mogą być używane w podróży tych użytkowników. W tym celu opcjonalny  *<ContentDefinitions>*  — element XML musi być zadeklarowana w obszarze hello  *<BuildingBlocks>*  sekcji w pliku XML zasady niestandardowe.

Witaj poniższej tabeli opisano zestaw hello rozpoznawany przez aparat obsługi tożsamości hello Azure AD B2C i typ hello stron odnosi się toothem identyfikatorów definicji zawartości.

| Identyfikator definicji zawartości | Opis |
|-----------------------|-------------|
| *API.error* | **Strona błędu**. Ta strona jest wyświetlana po napotkaniu wyjątku lub wystąpił błąd. |
| *API.idpselections* | **Strona wyboru dostawcy tożsamości**. Ta strona zawiera listę tożsamość, którą można wybrać dostawców, którzy hello użytkownika podczas logowania. Są to przedsiębiorstwa dostawców tożsamości, dostawców tożsamości społecznościowych, takich jak Facebook i Google + lub kont lokalnych (w oparciu nazwa użytkownika lub adres e-mail). |
| *API.idpselections.Signup* | **Wybór dostawcy tożsamości dla rejestracji**. Ta strona zawiera listę dostawców, którzy hello użytkownika można wybrać podczas tworzenia konta tożsamości. Są to przedsiębiorstwa dostawców tożsamości, dostawców tożsamości społecznościowych, takich jak Facebook i Google + lub kont lokalnych (w oparciu nazwa użytkownika lub adres e-mail). |
| *API.localaccountpasswordreset* | **Nie pamiętasz hasła strony**. Ta strona zawiera formularza, które użytkownik hello ma tooinitiate toofill zresetować swoje hasło.  |
| *API.localaccountsignin* | **Strona logowania konta lokalnego**. Ta strona zawiera formularz logowania hello, które użytkownik ma toofill przy logowaniu się za pomocą konta lokalnego, która jest oparta na adres e-mail lub nazwę użytkownika. Formularz Hello może zawierać pola do wprowadzania tekstu, a w polu wprowadzania hasła. |
| *API.localaccountsignup* | **Stronę tworzenia konta lokalnego konta**. Ta strona zawiera formularz zapisów hello, które użytkownik ma toofill przypadku skorzystania z konta lokalnego, która jest oparta na adres e-mail lub nazwę użytkownika. Formularz Hello może zawierać różne kontrolki wejściowe, takich jak pola do wprowadzania tekstu, pole wprowadzania hasła przycisk radiowy, jednokrotnym zaznaczeniem pola listy rozwijanej i pól wyboru wielokrotnego wyboru. |
| *API.phonefactor* | **Strona uwierzytelniania wieloskładnikowego**. Na tej stronie użytkowników można sprawdzić ich numery telefonów (przy użyciu tekstowych lub głosowych) podczas tworzenia konta lub logowania. |
| *API.selfasserted* | **Strony rejestracji społecznościowych konta**. Ta strona zawiera formularza tworzenia konta, które użytkownik hello ma toofill w podczas rejestracji przy użyciu istniejącego konta od dostawcy tożsamości społecznościowych, takich jak Facebook lub Google +. Ta strona jest podobne toohello powyżej kont społecznościowych stronę tworzenia konta, z wyjątkiem hello pola wprowadzania hasła hello. |
| *API.selfasserted.profileupdate* | **Strona aktualizacji profilu**. Ta strona zawiera formularz użytkownika hello służy tooupdate swój profil. Ta strona jest podobne toohello powyżej kont społecznościowych stronę tworzenia konta, z wyjątkiem hello pola wprowadzania hasła hello. |
| *API.signuporsignin* | **Ujednolicone stronę tworzenia konta lub logowania**.  Ta strona obsługuje zarówno rejestracji i logowania użytkowników, którzy można używać w organizacji dostawcy tożsamości, dostawców tożsamości społecznościowych, takich jak Facebook lub Google + lub kont lokalnych.

## <a name="next-steps"></a>Następne kroki
[Odwołanie: Zrozumieć, jak niestandardowe zasady pracować z hello Framework obsługi tożsamości w B2C](active-directory-b2c-reference-custom-policies-understanding-contents.md)
