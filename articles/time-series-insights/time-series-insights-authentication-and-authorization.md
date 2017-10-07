---
title: "aaaConfigure uwierzytelniania i autoryzacji dla aplikacji niestandardowej, która wywołuje interfejs API Azure czas serii szczegółowych informacji hello | Dokumentacja firmy Microsoft"
description: "W tym samouczku opisano, jak tooconfigure uwierzytelniania i autoryzacji dla aplikacji niestandardowej, która wywołuje hello interfejsu API usługi Azure czas serii Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a>Uwierzytelnianie i autoryzacja interfejsu API usługi Azure czas serii Insights

W tym artykule opisano, jak tooconfigure niestandardową aplikację, która wywołuje hello interfejsu API Azure czas serii szczegółowych informacji.

## <a name="service-principal"></a>Nazwy głównej usługi

W tej sekcji opisano, jak tooconfigure tooaccess aplikacji hello interfejsu API Insights serii czasu w imieniu aplikacji hello. Aplikacja Hello można następnie zapytania na danych lub publikować dane referencyjne w środowisku Insights serii czasu hello z poświadczeniami aplikacji i poświadczenia użytkownika nie hello.

Jeśli masz aplikację, która wymaga tooaccess Insights serii czasu, należy skonfigurować aplikację usługi Azure Active Directory i przypisać zasady dostępu hello danych w środowisku Insights serii czasu hello. Ta metoda jest preferowana toorunning aplikacji hello z poświadczeniami użytkownika ponieważ:

* Można przypisać uprawnienia toohello tożsamości aplikacji, które różnią się od własnych uprawnień. Zazwyczaj te uprawnienia są ograniczone tooexactly jakie aplikacji hello musi toodo. Na przykład można zezwolić tooonly aplikacji hello odczytu danych w określonym środowisku Insights serii czasu.
* Użytkownik nie ma poświadczeń aplikacji hello toochange zmienić Twoje obowiązki.
* Po uruchomieniu skryptu instalacji nienadzorowanej, można użyć certyfikatu lub uwierzytelniania klucza tooautomate aplikacji.

W tym artykule opisano, jak te kroki za pośrednictwem tooperform hello portalu Azure. Głównie aplikacji pojedynczej dzierżawy, gdzie aplikacja hello jest zamierzone toorun w tylko jednej z organizacji. Aplikacje pojedynczej dzierżawy jest zazwyczaj używana dla aplikacji — biznesowych, które są uruchamiane w Twojej organizacji.

Przepływ instalacji Hello składa się z trzech ogólne kroki:

1. Tworzenie aplikacji w usłudze Azure Active Directory.
2. Autoryzacja to środowisko czasu serii Insights hello tooaccess aplikacji.
3. Użyj Identyfikatora aplikacji hello i tooacquire klucza tokenu toohello `"https://api.timeseries.azure.com/"` odbiorców lub zasobu. Hello tokenu można następnie hello używane toocall interfejsu API Insights serii czasu.

Poniżej przedstawiono szczegółowy opis kroków hello:

1. Hello portalu Azure, wybierz **usługi Azure Active Directory** > **rejestracji aplikacji** > **nowej rejestracji aplikacji**.

   ![Nowej rejestracji aplikacji w usłudze Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. Nadaj aplikacji hello toobe typu hello nazwa, wybierz opcję **aplikacji sieci Web / interfejs API**, wybierz dowolny prawidłowy identyfikator URI dla **adres URL logowania**i kliknij przycisk **Utwórz**.

   ![Tworzenie aplikacji hello w usłudze Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. Wybierz nowo utworzony aplikacji i skopiuj jej aplikacji identyfikator tooyour ulubionym edytorze tekstów.

   ![Skopiuj identyfikator aplikacji hello](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. Wybierz **klucze**, nazwę klucza hello, wybierz hello wygaśnięcia i kliknij przycisk **zapisać**.

   ![Wybierz klucze aplikacji](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Wprowadź nazwę klucza hello i wygaśnięcia i kliknij przycisk Zapisz](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. Skopiuj hello klucza tooyour ulubionym edytorze tekstów.

   ![Skopiuj klucz aplikacji hello](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. W środowisku Insights serii czasu hello, wybierz **zasady dostępu do danych** i kliknij przycisk **Dodaj**.

   ![Dodanie nowych danych dostęp zasad toohello Insights serii czasu środowiska](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. W hello **wybór użytkownika** okno dialogowe, nazwa aplikacji hello Wklej (z kroku 2) lub identyfikator aplikacji (z kroku 3).

   ![Znajdowanie aplikacji w oknie dialogowym Wybieranie użytkownika hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. Wybierz hello roli (**czytnika** na potrzeby zapytań o dane, **współautora** wykonywania kwerend danych i zmiana danych referencyjnych) i kliknij przycisk **Ok**.

   ![Wybierz w oknie dialogowym Wybierz rolę hello czytelnika lub współautora](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. Zapisz zasady hello klikając **Ok**.

10. Za pomocą Identyfikatora aplikacji hello (z kroku 3) i token hello tooacquire klucza (z kroku 5) aplikacji w imieniu aplikacji hello. Witaj tokenu można następnie przekazać w hello `Authorization` nagłówka podczas wywołania aplikacji hello hello interfejsu API Insights serii czasu.

    Jeśli używasz programu C#, można użyć następującego kodu tooacquire hello token w imieniu aplikacji hello hello. Dla kompletnego przykładu, zobacz [zapytania na danych przy użyciu języka C#](time-series-insights-query-data-csharp.md).

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a>Następne kroki

Użyj Identyfikatora aplikacji hello i klucz w aplikacji. Przykładowy kod wywołuje hello czasu serii Insights API, zobacz [zapytania na danych przy użyciu języka C#](time-series-insights-query-data-csharp.md).

## <a name="see-also"></a>Zobacz też

* [Zapytania interfejsu API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) dla hello pełną dokumentację interfejsu API zapytania
* [Utwórz usługę podmiotu zabezpieczeń w hello portalu Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md)
