---
title: "Uwierzytelnianie użytkownika końcowego: usługi Data Lake Store w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooachieve uwierzytelniania użytkowników końcowych za pomocą usługi Data Lake Store za pomocą usługi Azure Active Directory"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a>Uwierzytelnianie użytkownika końcowego za pomocą usługi Data Lake Store za pomocą usługi Azure Active Directory
> [!div class="op_single_selector"]
> * [Uwierzytelnianie między usługami](data-lake-store-authenticate-using-active-directory.md)
> * [Uwierzytelnianie użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store używa usługi Azure Active Directory do uwierzytelniania. Przed tworzenia aplikacji, która współdziała z usługi Azure Data Lake Store i usługą Azure Data Lake Analytics, należy najpierw określić, jak tooauthenticate aplikacji z usługą Azure Active Directory (Azure AD). Witaj głównego dostępne są dwie opcje:

* Uwierzytelnianie użytkownika końcowego (w tym artykule)
* Uwierzytelnianie między usługami

Obie te opcje spowodować aplikacji dostarczanej z token OAuth 2.0, który pobiera dołączonych tooeach żądania tooAzure usługi Data Lake Store lub usługi Azure Data Lake Analytics.

Ten artykuł omówiono sposób tworzenia **natywnych aplikacji usługi Azure AD do uwierzytelniania użytkowników końcowych**. Instrukcje konfiguracji aplikacji usługi Azure AD do usługi uwierzytelniania można znaleźć [do usługi uwierzytelniania za pomocą usługi Data Lake Store za pomocą usługi Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Wymagania wstępne
* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

* Do identyfikatora subskrypcji. Można go pobrać z hello portalu Azure. Na przykład jest dostępny w bloku konta usługi Data Lake Store hello.
  
    ![Pobierz identyfikator subskrypcji](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* Nazwa domeny usługi Azure AD. Można go pobrać aktywowania myszy hello w hello prawym górnym rogu hello portalu Azure. W poniższym zrzucie ekranu hello, nazwa domeny hello jest **contoso.onmicrosoft.com**, i hello identyfikatora GUID w nawiasach kwadratowych jest identyfikatorem hello dzierżawy. 
  
    ![Uzyskaj domenę usługi AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a>Uwierzytelnianie użytkowników końcowych
Jest to hello zalecane podejście, jeśli chcesz, aby toolog użytkowników końcowych w aplikacji tooyour za pomocą usługi Azure AD. Aplikacja będzie w stanie tooaccess zasobów platformy Azure z hello poziomu dostępu hello przez użytkownika końcowego, który jest zalogowany. Użytkownik końcowy musi tooprovide poświadczeń okresowo w kolejności dla programu access toomaintain aplikacji.

wynik Hello o hello przez użytkownika końcowego, zaloguj się za jest, że aplikacji znajduje się token dostępu i token odświeżania. token dostępu Hello pobiera żądania dołączonych tooeach tooData Lake Store lub usługi Data Lake Analytics i jest ważna przez jedną godzinę domyślnie. token odświeżania Hello mogą być używane tooobtain nowy token dostępu który jest ważne dla tygodni tootwo domyślnie, jeśli regularnie używane. Dwa różne podejścia służy do logowania użytkownika końcowego.

### <a name="using-hello-oauth-20-pop-up"></a>Za pomocą menu podręczne hello OAuth 2.0
Aplikacja może wyzwolić podręczne autoryzacji OAuth 2.0, w których hello użytkownika końcowego można wprowadzić swoje poświadczenia. Są one współdziała również z hello procesu uwierzytelniania dwuskładnikowego Azure AD (2FA), jeśli jest to wymagane. 

> [!NOTE]
> Ta metoda nie jest jeszcze obsługiwana w hello Azure AD Authentication Library (ADAL) dla języka Python lub Java.
> 
> 

### <a name="directly-passing-in-user-credentials"></a>Przekazywanie bezpośrednio w poświadczeń użytkownika
Aplikacja może zapewnić bezpośrednio tooAzure poświadczeń użytkownika usługi AD. Ta metoda działa tylko z kontami użytkowników w organizacji identyfikator; nie jest zgodny z osobistego / kończy się rozszerzeniem "live ID" kont użytkowników, łącznie z tymi @outlook.com lub @live.com. Ponadto ta metoda nie jest zgodny z kontami użytkowników, które wymagają uwierzytelniania dwuskładnikowego Azure AD (2FA).

### <a name="what-do-i-need-toouse-this-approach"></a>Czego potrzebuję toouse to rozwiązanie?
* Nazwa domeny w usłudze Azure AD. Jest to wymienione w hello wymaganie wstępne w tym artykule.
* Usługi Azure AD **aplikacji natywnej**
* Identyfikator aplikacji natywnych aplikacji hello Azure AD
* Identyfikator URI przekierowania dla hello natywnych aplikacji usługi Azure AD
* Ustaw uprawnienia delegowane.


## <a name="step-1-create-an-active-directory-native-application"></a>Krok 1: Tworzenie natywnych aplikacji usługi Active Directory

Tworzenie i konfigurowanie usługi Azure AD aplikacji natywnej do uwierzytelniania użytkowników końcowych z usługi Azure Data Lake Store za pomocą usługi Azure Active Directory. Aby uzyskać instrukcje, zobacz [tworzy aplikację usługi Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Podczas instrukcjami hello na powitania powyżej łącze, upewnij się, że wybrano **natywnego** dla typu aplikacji, jak pokazano na poniższym zrzucie ekranu hello.

![Tworzenie aplikacji sieci web](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "tworzenie natywnych aplikacji")

## <a name="step-2-get-application-id-and-redirect-uri"></a>Krok 2: Uzyskiwanie identyfikatora aplikacji i identyfikator URI przekierowania

Zobacz [uzyskiwanie Identyfikatora aplikacji hello](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello identyfikator aplikacji (nazywane również identyfikator klienta hello w hello klasyczny portal Azure) natywnych aplikacji hello Azure AD.

tooretrieve hello identyfikator URI przekierowania, wykonaj poniższe kroki hello.

1. Z hello portalu Azure, wybierz **usługi Azure Active Directory**, kliknij przycisk **rejestracji aplikacji**, a następnie znajdź i kliknij natywnych aplikacji hello Azure AD, nowo utworzony.

2. Z hello **ustawienia** kliknij bloku dla aplikacji hello **identyfikator URI przekierowania**.

    ![Identyfikator URI przekierowania Get](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. Skopiuj wartość hello wyświetlana.


## <a name="step-3-set-permissions"></a>Krok 3: Ustawianie uprawnień

1. Z hello portalu Azure, wybierz **usługi Azure Active Directory**, kliknij przycisk **rejestracji aplikacji**, a następnie znajdź i kliknij natywnych aplikacji hello Azure AD, nowo utworzony.

2. Z hello **ustawienia** kliknij bloku dla aplikacji hello **wymagane uprawnienia**, a następnie kliknij przycisk **Dodaj**.

    ![Identyfikator klienta](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. W hello **dodać dostępu do interfejsu API** bloku, kliknij przycisk **wybierz interfejs API**, kliknij przycisk **usługi Azure Data Lake**, a następnie kliknij przycisk **wybierz**.

    ![Identyfikator klienta](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  W hello **dodać dostępu do interfejsu API** bloku, kliknij przycisk **wybierz uprawnienia**, wybierz hello toogive pole wyboru **pełnego dostępu tooData Lake Store**, a następnie kliknij przycisk **wybierz** .

    ![Identyfikator klienta](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    Kliknij przycisk **Gotowe**.

5. Powtarzania hello ostatnie dwa kroki toogrant uprawnienia dla **interfejs API zarządzania usługami Windows Azure** również.
   
## <a name="next-steps"></a>Następne kroki
W tym artykule tworzone natywnych aplikacji usługi Azure AD i zebranych informacji hello w aplikacjach klienckich tworzyć przy użyciu zestawu .NET SDK, zestaw SDK Java, interfejsu API REST,... itd. Można teraz kontynuować toohello następujące artykuły, które porozmawiać na temat sposobu toouse hello Azure AD w sieci web aplikacji toofirst uwierzytelniania w usłudze Data Lake Store i wykonywać inne operacje na powitania magazynu.

* [Rozpoczynanie pracy z usługą Azure Data Lake Store z użyciem zestawu SDK .NET](data-lake-store-get-started-net-sdk.md)
* [Wprowadzenie do usługi Azure Data Lake Store przy użyciu zestawu SDK Java](data-lake-store-get-started-java-sdk.md)
* [Wprowadzenie do usługi Azure Data Lake Store za pomocą interfejsu API REST](data-lake-store-get-started-rest-api.md)

