---
title: "Do usługi uwierzytelniania: usługi Data Lake Store w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wykonać uwierzytelnianie usługi do usługi z usługi Data Lake Store za pomocą usługi Azure Active Directory"
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
ms.openlocfilehash: 27ec0a4f48115d44da98dd048868b044aedf173c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a>Aby usługa uwierzytelniania za pomocą usługi Data Lake Store za pomocą usługi Azure Active Directory
> [!div class="op_single_selector"]
> * [Uwierzytelnianie między usługami](data-lake-store-authenticate-using-active-directory.md)
> * [Uwierzytelnianie użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store używa usługi Azure Active Directory do uwierzytelniania. Przed tworzenia aplikacji, która współdziała z usługi Azure Data Lake Store i usługą Azure Data Lake Analytics, należy najpierw wybrać sposób uwierzytelniania aplikacji z usługą Azure Active Directory (Azure AD). Główne dostępne są dwie opcje:

* Uwierzytelnianie użytkowników końcowych 
* Do usługi uwierzytelniania (w tym artykule) 

Obie te opcje spowodować aplikacji dostarczanej z token OAuth 2.0, który pobiera dołączony do każdego żądania kierowane do usługi Azure Data Lake Store lub usługi Azure Data Lake Analytics.

Ten artykuł omówiono sposób tworzenia **aplikacji sieci web usługi Azure AD do usługi uwierzytelniania**. Instrukcje konfiguracji aplikacji usługi Azure AD do uwierzytelniania użytkowników końcowych można znaleźć [uwierzytelniania użytkowników końcowych za pomocą usługi Data Lake Store za pomocą usługi Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Wymagania wstępne
* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="step-1-create-an-active-directory-web-application"></a>Krok 1: Tworzenie aplikacji sieci web usługi Active Directory

Tworzenie i konfigurowanie aplikacji sieci web usługi Azure AD do usługi uwierzytelniania z usługi Azure Data Lake Store za pomocą usługi Azure Active Directory. Aby uzyskać instrukcje, zobacz [tworzy aplikację usługi Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Podczas następujące instrukcje powyższego łącza, upewnij się, że wybrano **aplikacji sieci Web / interfejs API** dla typu aplikacji, jak pokazano na poniższym zrzucie ekranu.

![Tworzenie aplikacji sieci web](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "tworzenie aplikacji sieci web")

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a>Krok 2: Uzyskaj identyfikator aplikacji, klucz uwierzytelniania i identyfikatora dzierżawcy
Podczas logowania programowo, potrzebny jest identyfikator aplikacji. Jeśli aplikacja jest uruchamiana własne poświadczenia, konieczne będzie także klucz uwierzytelniania.

* Aby uzyskać instrukcje dotyczące pobierania klucz identyfikator i uwierzytelniania aplikacji (nazywane także klucz tajny klienta) dla aplikacji, zobacz [klucz identyfikator i uwierzytelniania aplikacji Get](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).

* Aby uzyskać instrukcje, jak uzyskać identyfikator dzierżawy, zobacz [uzyskanie Identyfikatora dzierżawy](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).

## <a name="step-3-assign-the-azure-ad-application-to-the-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a>Krok 3: Przypisz aplikację usługi Azure AD do usługi Azure Data Lake Store konta pliku lub folderu (tylko w przypadku uwierzytelniania service-to-service)
1. Zaloguj się do nowego [portalu Azure](https://portal.azure.com) i otwórz konto usługi Azure Data Lake Store, które chcesz skojarzyć z wcześniej utworzoną aplikację usługi Azure Active Directory.
2. W bloku konta usługi Data Lake Store kliknij pozycję **Eksplorator danych**.
   
    ![Tworzenie katalogów w ramach konta usługi Data Lake Store](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Tworzenie katalogów w ramach konta usługi Data Lake")
3. W **Eksploratora danych** bloku, kliknij plik lub folder, dla którego chcesz zapewnić dostęp do aplikacji usługi Azure AD, a następnie kliknij przycisk **dostępu**. Aby skonfigurować dostęp do pliku, należy kliknąć opcję **dostępu** z **podglądu pliku** bloku.
   
    ![Ustaw listy kontroli dostępu w systemie plików usługi Data Lake](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Ustaw listy kontroli dostępu w systemie plików usługi Data Lake")
4. **Dostępu** bloku wymieniono dostępu standardowego i niestandardowego dostępu już przypisany do katalogu głównego. Kliknij przycisk **Dodaj** ikonę, aby dodać poziom niestandardowy listy kontroli dostępu.
   
    ![Lista dostępu standardowe i niestandardowe](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "listy dostępu standardowe i niestandardowe")
5. Kliknij przycisk **Dodaj** ikonę, aby otworzyć **dodać niestandardowe dostępu** bloku. W tym bloku, kliknij przycisk **Wybieranie użytkownika lub grupy**, a następnie w **Wybieranie użytkownika lub grupy** bloku, poszukaj wcześniej utworzoną aplikację usługi Azure Active Directory. Jeśli masz dużą liczbę grup objętych wyszukiwaniem z, użyj pola tekstowego u góry, aby odfiltrować nazwę grupy. Kliknij grupę, w której chcesz dodać, a następnie kliknij przycisk **wybierz**.
   
    ![Dodaj grupę](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Dodaj grupę")
6. Kliknij przycisk **wybierz uprawnienia**, wybierz uprawnienia i czy chcesz przypisać uprawnienia domyślnie listy ACL, dostępu do listy ACL, lub obie. Kliknij przycisk **OK**.
   
    ![Przypisywanie uprawnień do grupy](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "przypisywanie uprawnień do grupy")
   
    Aby uzyskać więcej informacji na temat uprawnień w usłudze Data Lake Store i dostęp do i domyślnej listy kontroli dostępu, zobacz [kontroli dostępu w usłudze Data Lake Store](data-lake-store-access-control.md).
7. W **dodać niestandardowe dostępu** bloku, kliknij przycisk **OK**. Nowo dodana grupa, z skojarzone uprawnienia będzie teraz wyświetlany w **dostępu** bloku.
   
    ![Przypisywanie uprawnień do grupy](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "przypisywanie uprawnień do grupy")

## <a name="step-4-get-the-oauth-20-token-endpoint-only-for-java-based-applications"></a>Krok 4: Pobrać punktu końcowego tokenu OAuth 2.0 (tylko dla aplikacji opartych na języku Java)

1. Zaloguj się do nowego [portalu Azure](https://portal.azure.com) i kliknij polecenie usługi Active Directory w okienku po lewej stronie.

2. W okienku po lewej stronie kliknij **rejestracji aplikacji**.

3. W górnej części bloku rejestracji aplikacji, kliknij polecenie **punkty końcowe**.

    ![Punkt końcowy tokenu OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "końcowym tokenów OAuth")

4. Z listy punktów końcowych skopiuj punktu końcowego tokenu OAuth 2.0.

    ![Punkt końcowy tokenu OAuth](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "końcowym tokenów OAuth")   

## <a name="next-steps"></a>Następne kroki
W tym artykule utworzona aplikacja sieci web usługi Azure AD i zebranych informacji w aplikacjach klienckich tworzyć przy użyciu zestawu .NET SDK, zestaw SDK Java itp. Możesz teraz przejść do następujące artykuły, które porozmawiać na temat sposobu korzystania z aplikacji sieci web usługi Azure AD najpierw uwierzytelnić się z usługą Data Lake Store i wykonywać inne operacje w magazynie.

* [Rozpoczynanie pracy z usługą Azure Data Lake Store z użyciem zestawu SDK .NET](data-lake-store-get-started-net-sdk.md)
* [Wprowadzenie do usługi Azure Data Lake Store przy użyciu zestawu SDK Java](data-lake-store-get-started-java-sdk.md)

W tym artykule udał podstawowe kroki niezbędne do pobrania główna się użytkownika i uruchamiania aplikacji. Można przyjrzeć się następujące artykuły, aby uzyskać szczegółowe informacje:
* [Tworzenie nazwy głównej usługi przy użyciu programu PowerShell](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Uwierzytelnianie certyfikatu dla uwierzytelniania głównej usługi](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [Inne metody do uwierzytelniania usługi Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)


