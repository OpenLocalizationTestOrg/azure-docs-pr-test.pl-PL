---
title: "Do usługi uwierzytelniania: usługi Data Lake Store w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooachieve do usługi uwierzytelniania za pomocą usługi Data Lake Store za pomocą usługi Azure Active Directory"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 820b7c5d-4863-4225-9bd1-df4d8f515537
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 2e56237a75f020067b3248a1e1cfaf3c8df1371c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a>Aby usługa uwierzytelniania za pomocą usługi Data Lake Store za pomocą usługi Azure Active Directory
> [!div class="op_single_selector"]
> * [Uwierzytelnianie między usługami](data-lake-store-authenticate-using-active-directory.md)
> * [Uwierzytelnianie użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store używa usługi Azure Active Directory do uwierzytelniania. Przed tworzenia aplikacji, która współdziała z usługi Azure Data Lake Store i usługą Azure Data Lake Analytics, należy najpierw określić, jak tooauthenticate aplikacji z usługą Azure Active Directory (Azure AD). Witaj głównego dostępne są dwie opcje:

* Uwierzytelnianie użytkowników końcowych 
* Do usługi uwierzytelniania (w tym artykule) 

Obie te opcje spowodować aplikacji dostarczanej z token OAuth 2.0, który pobiera dołączonych tooeach żądania tooAzure usługi Data Lake Store lub usługi Azure Data Lake Analytics.

Ten artykuł omówiono sposób tworzenia **aplikacji sieci web usługi Azure AD do usługi uwierzytelniania**. Instrukcje konfiguracji aplikacji usługi Azure AD do uwierzytelniania użytkowników końcowych można znaleźć [uwierzytelniania użytkowników końcowych za pomocą usługi Data Lake Store za pomocą usługi Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Wymagania wstępne
* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="step-1-create-an-active-directory-web-application"></a>Krok 1: Tworzenie aplikacji sieci web usługi Active Directory

Tworzenie i konfigurowanie aplikacji sieci web usługi Azure AD do usługi uwierzytelniania z usługi Azure Data Lake Store za pomocą usługi Azure Active Directory. Aby uzyskać instrukcje, zobacz [tworzy aplikację usługi Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Podczas instrukcjami hello na powitania powyżej łącze, upewnij się, że wybrano **aplikacji sieci Web / interfejs API** dla typu aplikacji, jak pokazano na poniższym zrzucie ekranu hello.

![Tworzenie aplikacji sieci web](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "tworzenie aplikacji sieci web")

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a>Krok 2: Uzyskaj identyfikator aplikacji, klucz uwierzytelniania i identyfikatora dzierżawcy
Podczas logowania programowo, potrzebny jest identyfikator hello aplikacji. Jeśli aplikacja hello jest uruchamiana własne poświadczenia, konieczne będzie także klucz uwierzytelniania.

* Aby uzyskać instrukcje jak identyfikator aplikacji hello tooretrieve i uwierzytelniania klucz (również o nazwie hello klucz tajny klienta) dla aplikacji, zobacz [klucz identyfikator i uwierzytelniania aplikacji Get](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).

* Aby uzyskać instrukcje dotyczące sposobu tooretrieve hello Identyfikatora dzierżawy, zobacz [uzyskanie Identyfikatora dzierżawy](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).

## <a name="step-3-assign-hello-azure-ad-application-toohello-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a>Krok 3: Przypisz plik konta usługi Azure Data Lake Store toohello aplikacji hello Azure AD lub folderu (tylko w przypadku uwierzytelniania service-to-service)
1. Zaloguj się na nowy toohello [portalu Azure](https://portal.azure.com) , a następnie otwórz hello Azure Data Lake Store konta, które ma tooassociate z hello wcześniej utworzoną aplikację usługi Azure Active Directory.
2. W bloku konta usługi Data Lake Store kliknij pozycję **Eksplorator danych**.
   
    ![Tworzenie katalogów w ramach konta usługi Data Lake Store](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Tworzenie katalogów w ramach konta usługi Data Lake")
3. W hello **Eksploratora danych** bloku, kliknij hello plik lub folder, dla którego chcesz tooprovide dostępu do usługi Azure AD toohello aplikacji, a następnie kliknij **dostępu**. tooconfigure pliku tooa dostępu, należy kliknąć opcję **dostępu** z hello **podglądu pliku** bloku.
   
    ![Ustaw listy kontroli dostępu w systemie plików usługi Data Lake](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Ustaw listy kontroli dostępu w systemie plików usługi Data Lake")
4. Witaj **dostępu** bloku wymieniono hello standardowy dostęp i niestandardowe dostępu jest już przypisany toohello głównego. Kliknij przycisk hello **Dodaj** Poziom niestandardowy ikona tooadd listy kontroli dostępu.
   
    ![Lista dostępu standardowe i niestandardowe](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "listy dostępu standardowe i niestandardowe")
5. Kliknij przycisk hello **Dodaj** hello tooopen ikona **dodać niestandardowe dostępu** bloku. W tym bloku, kliknij przycisk **Wybieranie użytkownika lub grupy**, a następnie w **Wybieranie użytkownika lub grupy** wyszukać wcześniej utworzoną aplikację usługi Azure Active Directory hello bloku. Jeśli masz wiele grup toosearch z używania pola tekstowego hello w górnym toofilter hello na powitania Nazwa grupy. Kliknij grupę hello tooadd a następnie kliknij przycisk **wybierz**.
   
    ![Dodaj grupę](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Dodaj grupę")
6. Kliknij przycisk **wybierz uprawnienia**, wybierz hello uprawnienia i czy ma uprawnienia hello tooassign domyślnie ACL dostępu do listy kontroli dostępu i/lub. Kliknij przycisk **OK**.
   
    ![Przypisz uprawnienia toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "przypisać uprawnienia toogroup")
   
    Aby uzyskać więcej informacji na temat uprawnień w usłudze Data Lake Store i dostęp do i domyślnej listy kontroli dostępu, zobacz [kontroli dostępu w usłudze Data Lake Store](data-lake-store-access-control.md).
7. W hello **dodać niestandardowe dostępu** bloku, kliknij przycisk **OK**. Witaj nowo dodanych grupy z uprawnieniami hello skojarzone będzie teraz wyświetlany w hello **dostępu** bloku.
   
    ![Przypisz uprawnienia toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "przypisać uprawnienia toogroup")

## <a name="step-4-get-hello-oauth-20-token-endpoint-only-for-java-based-applications"></a>Krok 4: Uzyskaj token punkt końcowy protokołu OAuth 2.0 hello (tylko w przypadku aplikacji opartych na języku Java)

1. Zaloguj się na nowy toohello [portalu Azure](https://portal.azure.com) i w okienku po lewej stronie powitania kliknij usługę Active Directory.

2. W okienku po lewej stronie powitania kliknij **rejestracji aplikacji**.

3. Z góry hello bloku rejestracji aplikacji hello, kliknij przycisk **punkty końcowe**.

    ![Punkt końcowy tokenu OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "końcowym tokenów OAuth")

4. Z listy hello punktów końcowych skopiuj punktu końcowego tokena hello OAuth 2.0.

    ![Punkt końcowy tokenu OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "końcowym tokenów OAuth")   

## <a name="next-steps"></a>Następne kroki
W tym artykule utworzona aplikacja sieci web usługi Azure AD i zebranych hello informacje potrzebne w aplikacjach klienckich tworzyć przy użyciu zestawu .NET SDK, zestaw SDK Java itp. Można teraz kontynuować toohello następujące artykuły, które porozmawiać na temat sposobu toouse hello Azure AD w sieci web aplikacji toofirst uwierzytelniania w usłudze Data Lake Store i wykonywać inne operacje na powitania magazynu.

* [Rozpoczynanie pracy z usługą Azure Data Lake Store z użyciem zestawu SDK .NET](data-lake-store-get-started-net-sdk.md)
* [Wprowadzenie do usługi Azure Data Lake Store przy użyciu zestawu SDK Java](data-lake-store-get-started-java-sdk.md)

W tym artykule udał można za pomocą hello podstawowe kroki potrzebne tooget użytkownika podmiotu zabezpieczeń w górę i uruchomione dla aplikacji. Można przyjrzeć się hello następujące artykuły tooget dodatkowe informacje:
* [Użyj nazwy głównej usługi toocreate programu PowerShell](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Uwierzytelnianie certyfikatu dla uwierzytelniania głównej usługi](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [Inne metody tooauthenticate tooAzure AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


