---
title: aaaQuickstart dla hello Azure AD Graph API | Dokumentacja firmy Microsoft
description: "Hello Azure Active Directory interfejsu API programu Graph zapewnia dostęp programistyczny tooAzure AD przez punkty końcowe interfejsu API REST OData. Aplikacje mogą używać tooperform interfejsu API programu Graph hello tworzenia, odczytu, aktualizacji i usuwania operacji (CRUD) w katalogu danych i obiektów."
services: active-directory
documentationcenter: n/a
author: viv-liu
manager: mbaldwin
editor: 
tags: 
ms.assetid: 9dc268a9-32e8-402c-a43f-02b183c295c5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: b4d3c57f06d212b1d095578f19bb86c932dbcc33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-hello-azure-ad-graph-api"></a>Szybki Start dla hello Azure AD Graph API
Witaj interfejsu API programu Graph usługi Azure Active Directory (AD) zapewnia dostęp programistyczny tooAzure AD przez punkty końcowe interfejsu API REST OData. Aplikacje mogą używać tooperform interfejsu API programu Graph hello tworzenia, odczytu, aktualizacji i usuwania operacji (CRUD) w katalogu danych i obiektów. Na przykład można użyć hello interfejsu API programu Graph toocreate nowego użytkownika, widoku lub zaktualizować właściwości użytkownika, Zmień hasło użytkownika, sprawdź członkostwo grupy dostępu oparte na rolach, wyłącz lub usuń hello użytkownika. Aby uzyskać więcej informacji o funkcji interfejsu API programu Graph hello i scenariuszy aplikacji, zobacz [interfejsu API usługi Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) i [wymagania wstępne programu Azure AD Graph API](https://msdn.microsoft.com/library/hh974476.aspx). 

> [!IMPORTANT]
> Zdecydowanie zaleca się używanie [Microsoft Graph](https://developer.microsoft.com/graph) zamiast interfejsu API usługi Azure AD Graph tooaccess zasobów usługi Azure Active Directory. Obecnie koncentrujemy nasze działania deweloperskie na programie Microsoft Graph i nie planujemy żadnych dodatkowych rozszerzeń dla interfejsu API funkcji Azure AD Graph. Istnieje bardzo ograniczoną liczbę scenariuszy, w których interfejsu API usługi Azure AD Graph nadal może być odpowiednie; Aby uzyskać więcej informacji, zobacz hello [Microsoft Graph lub hello Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) wpis w blogu w hello Centrum deweloperów pakietu Office.
> 
> 

## <a name="how-tooconstruct-a-graph-api-url"></a>Jak tooconstruct URL interfejsu API Graph
W interfejsu API programu Graph, tooaccess katalogu danych i obiektów (innymi słowy, zasobów lub jednostek), z którymi ma tooperform operacji CRUD można użyć adresy URL oparte na powitania protokołu Open Data (OData). Witaj adresy URL używane w interfejsie API Graph składają się z czterech głównych części: Usługa głównego, identyfikator dzierżawy, ścieżka zasobu i opcji ciągu zapytania: `https://graph.windows.net/{tenant-identifier}/{resource-path}?[query-parameters]`. Zająć hello przykład hello następującego adresu URL: `https://graph.windows.net/contoso.com/groups?api-version=1.6`.

* **Katalogu głównego usługi**: W interfejsie API Graph usługi Azure AD, katalogu głównego usługi hello jest zawsze https://graph.windows.net.
* **Identyfikator dzierżawy**: w tej sekcji można nazwę zweryfikowanej domeny (zarejestrowanym) w hello poprzedzających przykładzie contoso.com. Można również go dzierżawy obiektu Identyfikatora lub hello "myorganization" lub "me" alias. Aby uzyskać więcej informacji, zobacz [adresowania jednostki i operacje w hello interfejsu API programu Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-operations-overview)).
* **Ścieżka zasobu**: Ta część adresu URL identyfikuje zasób hello toobe interakcji z (użytkowników, grup, określonego użytkownika lub określonej grupy, itp.) W powyższym przykładzie hello jest tooaddress najwyższego poziomu "grupy" hello, ustawioną zasobów. Można też rozwiązać, określonej jednostki, na przykład "użytkowników / {objectId}" lub "użytkowników/userPrincipalName".
* **Parametry zapytania**: hello pierwszą sekcją ścieżki zasobu z sekcji parametrów zapytania hello oddziela znak zapytania (?). parametr zapytania "api-version" Hello jest wymagany dla wszystkich żądań w hello interfejsu API programu Graph. Witaj interfejsu API programu Graph obsługuje również następujące opcje zapytania OData hello: **$filter**, **$orderby**, **rozwiń $**, **$top**i **$format**. Witaj następujące opcje zapytania nie są obecnie obsługiwane: **$count**, **$inlinecount**, i **$skip**. Aby uzyskać więcej informacji, zobacz [obsługiwane zapytania, filtrów i stronicowania opcji w interfejsie API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options).

## <a name="graph-api-versions"></a>Wersje interfejsu API programu Graph
Parametr zapytania "api-version" hello możesz Określ wersję hello żądania interfejsu API programu Graph. W wersji 1.5 lub nowszym Użyj wartości liczbowe wersji; Interfejs API-version = 1.6. W przypadku wcześniejszych wersji Użyj ciągu daty zgodną toohello format RRRR-MM-DD; na przykład interfejsu api-version = 2013-11-08. Dla funkcji w wersji zapoznawczej Użyj ciągu hello "beta"; na przykład interfejsu api-version = beta. Aby uzyskać więcej informacji na temat różnic między wersjami interfejsu API programu Graph, zobacz [wersji interfejsu API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-versioning).

## <a name="graph-api-metadata"></a>Metadanych interfejsu API programu Graph
tooreturn hello plik metadanych interfejsu API programu Graph, dodaje segmentu hello "$metadata" po identyfikator dzierżawy hello hello adres URL na przykład hello metadanych zwraca adres URL firmy Pokaz: `https://graph.windows.net/GraphDir1.OnMicrosoft.com/$metadata?api-version=1.6`. Można wprowadzić ten adres URL na pasku adresu hello metadanych hello toosee przeglądarki sieci web. Hello CSDL metadane zwrócony opisano hello jednostek i typów złożonych, ich właściwości oraz hello funkcje i udostępnianych przez hello wersji interfejsu API programu Graph żądanej akcji. Pominięcie parametru api-version hello zwraca metadane dla hello najnowszej wersji.

## <a name="common-queries"></a>Typowe zapytania
[Azure AD Graph API typowych kwerend](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options#CommonQueries) wymieniono typowe zapytania, które mogą być używane z hello Azure AD Graph, łącznie z zapytania, które mogą być używane tooaccess zasobów najwyższego poziomu w operacjach tooperform katalogu i zapytań w katalogu.

Na przykład `https://graph.windows.net/contoso.com/tenantDetails?api-version=1.6` zwraca firmy informacji o katalogu contoso.com.

Lub `https://graph.windows.net/contoso.com/users?api-version=1.6` Wyświetla listę wszystkich obiektów użytkownika w katalogu hello w domenie contoso.com.

## <a name="using-hello-graph-explorer"></a>Przy użyciu hello Explorer wykresu
Witaj Explorer wykresu służącego do hello Azure AD Graph API tooquery hello katalogu danych podczas tworzenia aplikacji.

Hello poniżej przedstawiono hello dane wyjściowe będą znajdować się toohello toonavigate Explorer wykresu, zaloguj się i wprowadź `https://graph.windows.net/GraphDir1.OnMicrosoft.com/users?api-version=1.6` toodisplay hello wszystkich użytkowników w hello katalogu zalogowanego użytkownika:

![Azure AD graph api explorer](./media/active-directory-graph-api-quickstart/graph_explorer.png)

**Obciążenia hello Explorer wykres**: tooload hello narzędzia kolejno zbyt[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/). Kliknij przycisk **logowania** i zaloguj się z Twojego toorun poświadczenia konta usługi Azure AD hello Explorer wykresu dla dzierżawy. Jeśli wykonywane Explorer wykres własną dzierżawę, użytkownik lub administrator musi tooconsent podczas logowania. Jeśli masz subskrypcję usługi Office 365, automatycznie jest dzierżawa usługi Azure AD. Użyj toosign w tooOffice 365 poświadczenia Hello są faktycznie, konta usługi Azure AD, a można używać tych poświadczeń z Eksploratora wykresu.

**Uruchom kwerendę**: toorun zapytania, wpisz zapytanie w polu tekstowym hello żądanie i kliknij **UZYSKAĆ** lub kliknij przycisk hello **wprowadź** klucza. w polu odpowiedzi hello są wyświetlane wyniki Hello. Na przykład `https://graph.windows.net/myorganization/groups?api-version=1.6` Wyświetla listę wszystkich obiektów grupy w katalogu hello zalogowanego użytkownika.

Uwaga hello następujące funkcje i ograniczenia hello wykres Explorer:

* Ustawia funkcji AutoComplete w zasobie. toosee tej funkcji, kliknij na powitania żądanie pola tekstowego (gdzie dostępny adres URL firmy hello). Możesz wybrać zestaw z listy rozwijanej hello zasobów.
* Obsługuje Witaj, "me" i "myorganization" adresowania aliasów. Na przykład można użyć `https://graph.windows.net/me?api-version=1.6` obiektu user hello tooreturn hello zalogowanego użytkownika lub `https://graph.windows.net/myorganization/users?api-version=1.6` tooreturn wszyscy użytkownicy w hello bieżącego katalogu.
* Sekcja nagłówków odpowiedzi. W tej sekcji można użyć toohelp rozwiązać problemy występujące podczas uruchamiania zapytań.
* Podgląd JSON odpowiedzi hello z możliwości rozwijanie i zwijanie.
* Brak obsługi do wyświetlania miniatury zdjęcia.

## <a name="using-fiddler-toowrite-toohello-directory"></a>Przy użyciu narzędzia Fiddler toowrite toohello katalogu
Dla celów hello ten przewodnik Szybki Start możesz użyć toopractice Fiddler sieci Web debugera hello wykonywanie operacji względem katalogu usługi Azure AD "write". Aby uzyskać więcej informacji i tooinstall Fiddler, zobacz [http://www.telerik.com/fiddler](http://www.telerik.com/fiddler).

W poniższym przykładzie hello toocreate Fiddler sieci Web debugera nową grupę zabezpieczeń "MyTestGroup" jest używany w katalogu usługi Azure AD.

**Uzyskaj token dostępu**: tooaccess Azure AD Graph, klienci są wymagane toosuccessfully najpierw uwierzytelnić tooAzure AD. Aby uzyskać więcej informacji, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](active-directory-authentication-scenarios.md).

**Napisz, a następnie uruchomić kwerendę**: hello pełną następujące kroki:

1. Otwórz Fiddler sieci Web debugera i Przełącz toohello **Composer** kartę.
2. Ponieważ chcesz, aby toocreate nową grupę zabezpieczeń, wybierz opcję **Post** jako hello metody HTTP z menu rozwijanego hello. Aby uzyskać więcej informacji na temat operacji i uprawnień w obiekcie grupy, zobacz [grupy](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#GroupEntity) w hello [dokumentacja interfejsu API REST usługi Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
3. W hello pole obok zbyt**Post**, wpisz następujące hello hello adresu URL żądania: `https://graph.windows.net/mytenantdomain/groups?api-version=1.6`.
   
   > [!NOTE]
   > Możesz podstawić mytenantdomain z nazwą domeny hello katalogu usługi Azure AD.
   > 
   > 
4. W polu hello bezpośrednio pod rozwijanego Post wpisz następujące hello:
   
    ```
   Host: graph.windows.net
   Authorization: Bearer <your access token>
   Content-Type: application/json
   ```
   
   > [!NOTE]
   > SUBSTITUTE Twojej &lt;tokenu dostępu&gt; hello tokena dostępu dla katalogu usługi Azure AD.
   > 
   > 
5. W hello **treść żądania** wpisz hello następujące czynności:
   
    ```
        {
            "displayName":"MyTestGroup",
            "mailNickname":"MyTestGroup",
            "mailEnabled":"false",
            "securityEnabled": true
        }
   ```
   
    Aby uzyskać więcej informacji o tworzeniu grup, zobacz [Utwórz grupę](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#CreateGroup).

Więcej informacji na temat usługi Azure AD jednostek i typy, które są udostępniane przez wykres i informacje o operacji hello, które można wykonywać na nich za pomocą wykresu, zobacz [dokumentacja interfejsu API REST usługi Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o hello [interfejsu API usługi Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)
* Dowiedz się więcej o [zakresy uprawnień interfejsu API Graph usługi Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)

