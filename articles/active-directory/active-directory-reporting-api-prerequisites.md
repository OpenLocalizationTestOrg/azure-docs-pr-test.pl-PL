---
title: aaaPrerequisites tooaccess hello Azure AD raportowania interfejsu API. | Microsoft Docs
description: "Dowiedz się więcej o API raportowania hello wymagania wstępne tooaccess hello Azure AD"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>Wymagania wstępne tooaccess hello Azure AD raportowania interfejsu API
Witaj [raportowania interfejsów API usługi Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) umożliwiają dostęp programistyczny toohello danych za pomocą zestawu opartego na interfejsie REST API. Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.

Witaj reporting używa interfejsu API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize dostępu toohello interfejsów API sieci web. 

tooprepare z interfejsem API raportowania toohello dostępu, musi:

1. Tworzenie aplikacji w dzierżawie usługi Azure AD 
2. Tooaccess odpowiednie uprawnienia aplikacji hello GRANT hello danych usługi Azure AD
3. Zbierz ustawienia konfiguracji z katalogu

Pytania, problemy lub opinie, skontaktuj się z [Pomoc raportowania usługi AAD](mailto:aadreportinghelp@microsoft.com).

## <a name="create-an-azure-ad-application"></a>Tworzenie aplikacji usługi Azure AD
tooconfigure katalogu tooaccess hello Azure AD raportowania interfejsu API, musisz zalogować się toohello klasycznego portalu Azure przy użyciu konta administratora subskrypcji platformy Azure, który jest członkiem roli hello administratora globalnego katalogu, w dzierżawie usługi Azure AD.

> [!IMPORTANT]
> Aplikacje uruchomione w ramach poświadczeń z uprawnieniami "Administrator", jak mogą być bardzo zaawansowane, więc należy być bezpieczne czy tookeep hello identyfikator/klucz tajny poświadczenia aplikacji.
> 
> 

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Z hello **usługi active directory** listy, wybierz swój katalog.
3. W menu hello na górze hello, kliknij przycisk **aplikacji**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Na pasku dolnej powitania kliknij **Dodaj**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/03.png) 
5. Na powitania **co chcesz toodo?** okna dialogowego, kliknij przycisk **Dodaj aplikację moją organizację**. 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/04.png) 
6. Na powitania **Powiedz nam o aplikacji** okna dialogowego, wykonaj następujące kroki hello: 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    a. W hello **nazwa** tekstowym, wpisz nazwę (np.: Aplikacja interfejsu API raportowania).
   
    b. Wybierz **aplikacji sieci Web i/lub interfejs API sieci web**.
   
    c. Kliknij przycisk **Dalej**.
7. Na powitania **właściwości aplikacji** okna dialogowego, wykonaj następujące kroki hello: 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    a. W hello **adres URL logowania** pole tekstowe, typ `https://localhost`.
   
    b. W hello **identyfikator URI aplikacji** pole tekstowe, typ ```https://localhost/ReportingApiApp```.
   
    c. Kliknij przycisk **Complete** (Zakończ).

## <a name="grant-your-application-permission-toouse-hello-api"></a>Przyznaj hello toouse uprawnień z aplikacji interfejsu API
1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com/)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Z hello **usługi active directory** listy, wybierz swój katalog.
3. W menu hello na górze hello, kliknij przycisk **aplikacji**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png)
4. Z listy aplikacji hello wybierz nowo utworzonej aplikacji.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/07.png)
5. W menu hello na górze hello, kliknij przycisk **Konfiguruj**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/08.png)
6. W hello **uprawnienia aplikacji tooother** sekcji, aby hello **usługi Azure Active Directory** zasobów, kliknij hello **uprawnienia aplikacji** listy rozwijanej, a następnie Wybierz **odczytuj dane katalogu**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/09.png)
7. Na pasku dolnej powitania kliknij **zapisać**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>Zbierz ustawienia konfiguracji z katalogu
W tej sekcji opisano sposób hello tooget następujące ustawienia z katalogu:

* Nazwa domeny
* Identyfikator klienta
* Klucz tajny klienta

Należy korzystać z tych wartości podczas konfigurowania raportowania interfejsu API toohello wywołania. 

### <a name="get-your-domain-name"></a>Pobierz nazwę domeny
1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Z hello **usługi active directory** listy, wybierz swój katalog.
3. W menu hello na górze hello, kliknij przycisk **domen**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/11.png) 
4. W hello **nazwy domeny** kolumny, skopiuj nazwę domeny.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a>Pobieranie Identyfikatora klienta aplikacji hello
1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Z hello **usługi active directory** listy, wybierz swój katalog.
3. W menu hello na górze hello, kliknij przycisk **aplikacji**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Z listy aplikacji hello wybierz nowo utworzonej aplikacji.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/07.png)
5. W menu hello na górze hello, kliknij przycisk **Konfiguruj**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/08.png)
6. Kopiowanie z **identyfikator klienta**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a>Pobierz klucz tajny klienta aplikacji hello
tooget klienta aplikacji tajne, należy toocreate nowy klucz i zapisz jego wartości podczas zapisywania nowego klucza hello, ponieważ nie jest możliwe tooretrieve później już tej wartości.

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Z hello **usługi active directory** listy, wybierz swój katalog.
3. W menu hello na górze hello, kliknij przycisk **aplikacji**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Z listy aplikacji hello wybierz nowo utworzonej aplikacji.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/07.png)
5. W menu hello na górze hello, kliknij przycisk **Konfiguruj**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/08.png)
6. W hello **klucze** sekcji, wykonaj następujące kroki hello: 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/14.png)
   
    a. Z listy czas trwania hello wybierz czas trwania
   
    b. Na pasku dolnej powitania kliknij **zapisać**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. Skopiuj wartość klucza hello.

## <a name="next-steps"></a>Następne kroki
* Czy można tak, jak dane z usługi Azure AD hello hello tooaccess raportowania interfejsu API w sposób programowy Zapoznaj się z [wprowadzenie hello Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).
* Jeśli chcesz toofind się więcej o usłudze Azure Active Directory, zobacz hello [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).  

