---
title: "firmowe aaaAdd logowania tooyour i strony panelu dostępu"
description: "Dowiedz się, jak tooadd strony toohello Azure logowania w znakowaniu firmy i hello dostępu do strony panelu"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f74621b4-4ef0-4899-8c0e-0c20347a8c31
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/23/2017
ms.author: curtand
ms.openlocfilehash: b1c6442028393552bff3d380312c8cd1bfda5d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-and-access-panel-pages"></a>Dodaj firmowe logowania tooyour i strony panelu dostępu
tooavoid pomyłek, w wielu firmach tooapply spójny wygląd i zachowanie we wszystkich hello witryn sieci Web i usługach, którymi zarządzają. Azure Active Directory zapewnia tę funkcję, umożliwiając toocustomize wygląd hello hello następujących stron sieci web z logo firmy i niestandardowych schematów kolorów:

* **Strona logowania** — jest to strona hello wyświetlana podczas logowania tooOffice 365 lub innych aplikacji opartych na sieci web, które używają usługi Azure AD jako dostawcy tożsamości. Użytkownik interakcji z tą stroną wchodzisz podczas odnajdowania obszaru macierzystego lub tooenter swoje poświadczenia. Witaj odnajdowania obszaru macierzystego umożliwia hello systemu tooredirect federacyjnych użytkowników tootheir lokalnej usługi STS (np. usługi AD FS).
* **Strona panelu dostępu** — hello Panel dostępu jest opartych na sieci web portalu, która pozwala tooview i aplikacje oparte na chmurze hello uruchamiania administrator usługi Azure AD udzielił Ci dostępu do. tooaccess hello Panel dostępu, hello Użyj następującego adresu URL: [https://myapps.microsoft.com](https://myapps.microsoft.com).

W tym temacie wyjaśniono, jak można dostosować hello strony logowania i strony panelu dostępu hello.

> [!NOTE]
> * Logo firmy jest funkcją, która jest dostępna tylko w przypadku uaktualnienia toohello Premium lub podstawowa edition usługi Azure Active Directory lub użytkowników usługi Office 365. Aby uzyskać więcej informacji, zobacz [Wersje usługi Azure Active Directory](active-directory-editions.md).
> * Azure Active Directory Premium i podstawowa wydań są dostępne dla klientów w Chinach przy użyciu hello na całym świecie wystąpienia usługi Azure Active Directory. Azure Active Directory Premium i podstawowa wersje nie są obecnie obsługiwane w hello Microsoft Azure świadczonej przez 21Vianet w Chinach. Aby uzyskać więcej informacji, skontaktuj się z nami na powitania [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).
>
>

## <a name="customizing-hello-sign-in-page"></a>Dostosowywanie strony logowania hello
Zwykle dostęp za pośrednictwem przeglądarki tooyour chmury aplikacji i usług, które subskrybuje Twoja organizacja, należy użyć hello strony logowania.

Jeśli strona logowania tooyour zmiany zostały zastosowane, może potrwać do godziny tooan hello tooappear zmiany.

Strona logowania z oznaczeniami firmowymi jest wyświetlana tylko podczas odwiedzania usługi za pomocą adresu URL specyficznego dla dzierżawy, takiego jak https://outlook.com/**contoso**.com lub https://mail.**contoso**.com.

W przypadku odwiedzania usługi za pomocą adresów URL innych niż specyficzne dla dzierżawy (np. https://mail.office365.com) wyświetlana jest strona logowania bez firmowego znakowania. W takim przypadku znakowanie zostanie wyświetlone po wprowadzeniu identyfikatora użytkownika lub wybraniu kafelka użytkownika.

> [!NOTE]
> * Nazwa domeny musi występować jako "Aktywna" w hello **usługi Active Directory** > **katalogu** > **domen** sekcji hello klasycznego portalu Azure Jeżeli skonfigurowano znakowanie.
> * Znakowanie strony logowania nie jest przenoszone toohello konsumenta logowania firmy Microsoft. Jeśli zalogujesz się osobistego konta Microsoft, mogą zobaczyć lista kafelków użytkowników renderowana przez usługę Azure AD, ale hello znakowanie organizacji nie ma zastosowania toohello strony logowania na koncie Microsoft.
>
>

Jeśli chcesz tooshow swoje firmowe oznaczenia, kolory i inne dostosowywalne elementy na tej stronie, zobacz następujące obrazy toounderstand hello różnicę między obydwoma środowiskami hello hello.

Witaj, wykonując zrzut ekranu przedstawia oraz przykład dla usługi Office 365 hello strony logowania na komputerze stacjonarnym **przed** dostosowaniem:

![Strona logowania usługi Office 365 przed dostosowaniem][1]

Witaj, wykonując zrzut ekranu przedstawia oraz przykład dla usługi Office 365 hello strony logowania na komputerze stacjonarnym **po** dostosowaniem:

![Strona logowania usługi Office 365 po dostosowaniu][2]

Witaj Poniższy zrzut ekranu przedstawia przykład strony logowania usługi Office 365 hello na urządzeniu przenośnym **przed** dostosowaniem:

![Strona logowania usługi Office 365 przed dostosowaniem][3]

Witaj Poniższy zrzut ekranu przedstawia przykład strony logowania usługi Office 365 hello na urządzeniu przenośnym **po** dostosowaniem:

![Strona logowania usługi Office 365 po dostosowaniu][4]

Podczas zmiany rozmiaru okna przeglądarki duża ilustracja hello, takich jak hello pokazana wcześniej, jest często przycinana tooaccommodate różnych współczynników proporcji ekranu. Pamiętając o tym należy spróbować hello tookeep kluczowe elementy wizualne na ilustracji hello tak, aby zawsze były wyświetlane w hello lewym górnym rogu (prawym górnym dla języków od prawej do lewej). Jest to ważne, ponieważ zmiana rozmiaru zwykle odbywa się wydostawać hello prawego dolnego rogu w kierunku hello górnego / lewego lub od hello dołu do góry hello.

Witaj poniższej ilustracji przedstawiono sposób przycięcia ilustracji hello hello przeglądarki po zmianie rozmiaru toohello po lewej:

![][6]

Oto jak ilustracja wygląda po zmianie rozmiaru przeglądarki hello w górnym hello:

![][7]

## <a name="what-elements-on-hello-page-can-i-customize"></a>Jakie elementy na stronie powitania można dostosować?
Można dostosować następujące elementy na stronie logowania hello hello:

![][5]

| Element strony | Lokalizacja na stronie powitania |
|:--- | --- |
| Baner logo |Wyświetlane na powitania prawym górnym rogu strony hello. Zastępuje lokacji docelowej hello logo hello, które tworzysz w toodisplays (np. Office 365 lub Azure). |
| Duża ilustracja/kolor tła |Wyświetlane po lewej stronie powitania hello. Zastępuje lokacji docelowej hello obraz powitania, który tworzysz toodisplays. zamiast dużej ilustracji hello połączeń o niskiej przepustowości lub na wąskich ekranach może być wyświetlany Hello kolor tła. |
| Nie wylogowuj mnie |Wyświetlany w obszarze hello tekstowe hasła. |
| Tekst strony logowania |Powyższy hello stopki strony, gdy będziesz potrzebować tooconvey pomocne informacje przed zalogowaniem się przy użyciu konta służbowego. Można na przykład tooinclude hello phone liczba tooyour pomocy technicznej lub klauzulę prawną. |

> [!NOTE]
> Wszystkie elementy są opcjonalne. Na przykład jeśli określisz Baner Logo, ale nie skonfigurujesz dużej ilustracji, strony logowania hello przedstawia Twojego logo i hello ilustracja dla lokacji docelowej hello (to znaczy hello Office 365 obraz Kalifornijskiej autostrady).
>
>

Na stronie logowania hello **wylogowuj mnie** wyboru pozwala tooremain użytkownik zalogowany po ich zamknięcie i ponowne otwarcie przeglądarki. Opcja nie ma wpływu na okres istnienia sesji. Pole wyboru hello na stronę logowania w usłudze Azure Active Directory hello można ukryć.

Określa, czy pole wyboru hello jest wyświetlane zależy od ustawienia hello **Ukryj KMSI**.

![][9]

toohide wyboru hello, skonfiguruj to ustawienie zbyt**Hidden**.

> [!NOTE]
> Niektóre funkcje pakietu Office 2010 i SharePoint Online są zależne od użytkownicy będą mogli toocheck tego pola. Jeśli konfigurujesz toohidden to ustawienie, dodatkowe i nieoczekiwane monity toosign w może widzą użytkownicy.
>
>

Możesz również dostosować wszystkie elementy na tej stronie. Po skonfigurowaniu „domyślnego” zestawu elementów dostosowania można skonfigurować więcej wersji dla różnych ustawień regionalnych. Możesz także mieszać i dopasowywać różne elementy. Można na przykład:

* Utworzyć „domyślną” dużą ilustrację działającą dla wszystkich języków, a następnie utworzyć specyficzne wersje dla angielskiego i francuskiego. Po ustawieniu tooone Twojego przeglądarki z tych dwóch języków wyświetlany będzie określony obraz powitania, podczas gdy ilustracja domyślna hello będzie wyświetlana dla wszystkich pozostałych języków.
* Skonfigurować różne wersje logo dla organizacji (np. wersję japońską lub hebrajską).

## <a name="access-panel-page-customization"></a>Dostosowywanie strony panelu dostępu
Strona panelu dostępu Hello jest zasadniczo stroną portalu szybki dostęp toohello aplikacji w chmurze, które przyznano Ci dostęp tooby administratora. Na tej stronie aplikacje są wyświetlane jako aktywne kafelki aplikacji do kliknięcia.

powitania po zrzut ekranu przedstawia przykład strony panelu dostępu po dostosowaniu.

![][8]

## <a name="configure-your-directory-with-company-branding"></a>Konfigurowanie katalogu za pomocą znaków firmowych
Można skonfigurować jeden domyślny zestaw elementów dostosowywalnych dla każdego katalogu w hello klasycznego portalu Azure. Po zapisaniu ustawień domyślnych hello, administrator może dodać zlokalizowane wersje każdego elementu dla różnych języków / ustawień regionalnych. Wszystkie elementy dostosowywalne są opcjonalne.

Na przykład jeśli skonfigurujesz domyślny Baner Logo, ale nie skonfigurujesz dużej ilustracji hello logowania zostanie wyświetlona strona logo w prawym górnym rogu hello. Jednak hello domyślna ilustracja lokacji hello jest wyświetlany.

Wyobraź sobie hello następującej konfiguracji:

* domyślny baner logo i tekst strony logowania w języku angielskim
* tekst strony logowania specyficzny dla języka skonfigurowany dla języka niemieckiego

Jeśli preferowanym językiem jest niemiecki, możesz uzyskać hello domyślny Baner Logo, ale hello niemiecki tekst.

Podczas technicznie można skonfigurować różne zestawy dla każdego z języków obsługiwanych przez usługę Azure AD, zaleca się utrzymywanie hello liczby wersji niski, ze względu na konserwacji i wydajności.

> [!IMPORTANT]
> Yammer nie nie Pokaż hello Azure AD marki strony logowania do czasu, po zalogowaniu użytkownika hello. Witaj użytkownik widzi najpierw hello ogólnego strony logowania usługi Office 365, a następnie hello marki strony po tym.   
 
 
**tooadd firmy znakowania tooyour katalogu, wykonaj następujące kroki hello:**

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) jako administrator katalogu hello ma toocustomize.
2. Wybierz katalog hello ma toocustomize.
3. Witaj pasku narzędzi u góry hello, kliknij przycisk **Konfiguruj**.
4. Kliknij pozycję **Customize Branding (Dostosuj znakowanie)**.
5. Zmodyfikuj elementy hello ma toocustomize. Wszystkie pola są opcjonalne.
6. Kliknij pozycję **Zapisz**.

Może potrwać godzinę tooan nowych zmian zostanie wykonane toohello strony logowania znakowania tooappear.

**tooadd specyficzny dla języka firmowe, wykonaj następujące kroki hello:**

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) jako administrator katalogu hello ma toocustomize.
2. Wybierz katalog hello ma toocustomize.
fs3. Witaj pasku narzędzi u góry hello, kliknij przycisk **Konfiguruj**.
4. Kliknij pozycję **Customize Branding (Dostosuj znakowanie)**.
5. Kliknij pozycję **Add branding for a specific language (Dodaj znakowanie dla określonego języka)**.
6. Wybierz język hello mają toocustomize hello logo, a następnie kliknij przycisk **dalej**.
7. Edytuj tylko hello elementy, dla których chcesz zastępuje tooconfigure specyficzny dla języka. Wszystkie pola są opcjonalne. Jeśli pole pozostanie puste, następnie hello niestandardowe domyślne wartości zostanie wyświetlony (lub hello domyślna firmy Microsoft, jeśli nie skonfigurowano niestandardowe domyślne).
8. Kliknij pozycję **Zapisz**.

**tooremove znakowanie firmowe z katalogu, wykonaj następujące kroki hello:**

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) jako administrator katalogu hello ma toocustomize.
2. Wybierz katalog hello ma toocustomize.
3. Witaj pasku narzędzi u góry hello, kliknij przycisk **Konfiguruj**.
4. Kliknij pozycję **Customize Branding (Dostosuj znakowanie)**.
5. Na stronie Dostosowywanie znakowania hello wybierz **Edytuj istniejące ustawienia znakowania** , a następnie przejść toohello następnej strony.
6. W zależności od tego, które elementy chcesz tooremove, wykonaj jedną lub więcej z następujących hello:

    a. W obszarze **Banner Logo (Baner logo)** wybierz opcję **Remove uploaded logo (Usuń przekazane logo)**.

    b. W obszarze **Tile Logo (Logo kafelka)** wybierz opcję **Remove uploaded logo (Usuń przekazane logo)**.

    c. Usuń tekst hello ze wszystkich pól tekstowych.

    d. Kliknij przycisk **Dalej**.

    e. Usuń tekst hello ze wszystkich pól tekstowych.
7. Kliknij przycisk **zapisać** tooremove hello elementów.
8. W razie potrzeby kliknij **Dostosowywanie znakowania** ponownie i powtórz te kroki dla wszystkich specyficzny dla języka znakowania wymagające toobe usunięte.
    Wszystkie ustawienia znakowania zostały usunięte po kliknięciu **Dostosowywanie znakowania** i zobacz hello **Dostosuj domyślne znakowanie** formularza z żadnych skonfigurowanych ustawień.

## <a name="testing-and-examples"></a>Testowanie i przykłady
Zalecamy wypróbowanie dostosowań za pomocą dzierżawy testowej przed wprowadzeniem zmian w środowisku produkcyjnym.

**tooverify czy znakowanie zostało zastosowane:**

1. Otwórz sesję InPrivate lub Incognito przeglądarki.
2. Odwiedź stronę https://outlook.com/contoso.com, zastępując hello domeny contoso.com dostosowaną.

Ta metoda działa również z domenami, które mają postać typu contoso.onmicrosoft.com.

toohelp utworzyć zestawy dostosowania skuteczne, dostosowaliśmy hello następujące dwa fikcyjne strony logowania:

* [http://aka.ms/aaddemo001](http://aka.ms/aaddemo001)
* [http://aka.ms/aaddemo002](http://aka.ms/aaddemo002)

ustawienia specyficzne dla języka hello tootest, należy toomodify hello domyślne preferencje języka w języku tooa przeglądarki sieci web, ma ustawiony w dostosowaniu. W programie Internet Explorer, należy skonfigurować to w hello **Opcje internetowe** menu.

## <a name="customizable-elements"></a>Elementy dostosowywalne
Niektóre elementy dostosowywalne w usłudze Azure AD mają wiele zastosowań. Można skonfigurować logo firmy raz dla katalogu i jest używany w obu hello logowania i strony panelu dostępu. Niektóre elementy dostosowywalne są określone tylko toohello strony logowania. Witaj Poniższa tabela zawiera szczegóły dla hello różnych elementów dostosowywalnych.

| Nazwa | Opis | Ograniczenia | Zalecenia |
| --- | --- | --- | --- |
| Baner logo |Witaj Baner Logo jest wyświetlany na powitania strony logowania i panelu dostępu hello. |<p>JPG lub PNG</p><p>60 x 280 pikseli</p><p>10 KB</p> |<p>Użyj pełnego logo organizacji (piktogram i logo)</p><p>Utrzymaj poniżej 30 pikseli tooavoid wysokiej wprowadzenia pasków przewijania na urządzeniach przenośnych</p><p>Utrzymaj rozmiar poniżej 4 KB</p><p>Użyj przezroczystego obrazu PNG (nie zakładaj, że hello strony logowania ma zawsze białe tło)</p> |
| Logo kafelka |(aktualnie nieużywane na stronę logowania w hello) W przyszłości hello ten tekst może być używane tooreplace hello ogólnego "konto służbowe" piktogram w różnych miejscach hello środowisku. |<p>JPG lub PNG</p><p>120 x 120 pikseli</p><p>10 KB</p> |<p>Zachowaj prostotę (Brak małego tekstu), jak ten obraz może być % too50 po zmianie rozmiaru |
| </p> | | | |
| Etykieta nazwy użytkownika strony logowania |(aktualnie nieużywane na stronę logowania w hello) W przyszłości hello ten tekst może być używane tooreplace hello ciąg ogólnego "konto służbowe" w różnych miejscach w środowisku hello. Można ustawić toosomething, takich jak "Konto Contoso" lub "Identyfikator Contoso" |<p>Tekst Unicode, zapasowej too50 znaków</p><p>Tylko zwykły tekst (bez linków lub tagów HTML)</p> |<p>Powinna być krótka i prosta</p><p>Poproś użytkowników, jak zwykle dotyczą pracy toohello lub konto służbowe udostępnione im.</p> |
| Tekst strony logowania |Ten tekst "standardowy" pojawia się poniżej formularza strony logowania hello i mogą być używane toocommunicate dodatkowe instrukcje lub gdy tooget Pomoc i obsługa techniczna. |<p>Tekst Unicode, zapasowej too256 znaków</p><p>Tylko zwykły tekst (bez linków lub tagów HTML)</p> |Zachowaj długość nie więcej niż 250 znaków (około 3 wiersze tekstu) |
| Ilustracja strony logowania |Witaj ilustracja to duży obraz wyświetlany na powitania strony logowania toohello lewo od formularza strony logowania hello. |<p>JPG lub PNG</p><p>1420 x 1200</p><p>500 KB</p> |<p>1420 x 1200 pikseli</p><p>Ważne: zachowaj jak najmniejszy rozmiar, najlepiej poniżej 200 KB. Jeśli ten obraz jest za duży, gdy obraz powitania nie jest buforowany jest wpływ na wydajność hello hello strony logowania</p><p>Ten obraz jest często przycinany tooaccommodate różnych współczynników proporcji ekranu. Zachowaj podstawowe elementy wizualne hello w hello górnym lewym rogu (prawym górnym dla języków RTL), ponieważ zmiana rozmiaru następuje od prawego dolnego rogu hello, w kierunku hello górnego / lewego, ponieważ podczas zmniejszania okna przeglądarki hello.</p> |
| Kolor tła strony logowania |kolor tła strony logowania Hello jest używany w hello obszaru toohello lewo od formularza strony logowania hello. |Wymagany jest kolor RGB w postaci szesnastkowej (przykład: #FFFFFF) |<p>zamiast hello może być wyświetlany kolor tła Hello duża ilustracja połączeń o niskiej przepustowości</p><p>Sugerujemy wybranie podstawowego koloru hello hello Baner Logo</p> |

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie do usługi Azure Active Directory — wersja Premium](active-directory-get-started-premium.md)
* [Wyświetlanie raportów dostępu i użycia](active-directory-view-access-usage-reports.md)

<!--Image references-->
[1]: ./media/active-directory-add-company-branding/SignInPage_beforecustomization.png
[2]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization.png
[3]: ./media/active-directory-add-company-branding/SignInPage_mobile_beforecustomization.png
[4]: ./media/active-directory-add-company-branding/SignInPage_mobile_aftercustomization.png
[5]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_elements.png
[6]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedleft.png
[7]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedtop.png
[8]: ./media/active-directory-add-company-branding/APBranding.png
[9]: ./media/active-directory-add-company-branding/hidekmsi.png
