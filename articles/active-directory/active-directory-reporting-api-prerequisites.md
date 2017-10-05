---
title: "Wymagania wstępne dotyczące raportowania interfejsu API usługi Azure AD dostęp. | Microsoft Docs"
description: "Dowiedz się więcej o wymaganiach wstępnych można uzyskać dostępu do raportowania interfejsu API usługi Azure AD"
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
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a>Wymagania wstępne dotyczące raportowania interfejsu API usługi Azure AD dostęp
[Raportowania interfejsów API usługi Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) umożliwiają programowy dostęp do danych za pomocą zestawu opartego na interfejsie REST API. Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.

Raportowania używa interfejsu API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) do autoryzacji dostępu do interfejsów API sieci web. 

Aby przygotować dostęp do interfejsu API raportowania, należy:

1. Tworzenie aplikacji w dzierżawie usługi Azure AD 
2. Udziel aplikacji uprawnień dostępu do danych usługi Azure AD
3. Zbierz ustawienia konfiguracji z katalogu

Pytania, problemy lub opinie, skontaktuj się z [Pomoc raportowania usługi AAD](mailto:aadreportinghelp@microsoft.com).

## <a name="create-an-azure-ad-application"></a>Tworzenie aplikacji usługi Azure AD
Aby skonfigurować dostęp raportowania interfejsu API usługi Azure AD do katalogu, należy zalogować się do klasycznego portalu Azure przy użyciu konta administratora subskrypcji platformy Azure, który jest członkiem roli administratora globalnego katalogu w dzierżawie usługi Azure AD.

> [!IMPORTANT]
> Aplikacje uruchomione w ramach poświadczeń z uprawnieniami "Administrator", jak mogą być bardzo zaawansowane, więc Pamiętaj zapewnić bezpieczeństwo poświadczeń identyfikator/klucz tajny aplikacji.
> 
> 

1. W [klasycznego portalu Azure](https://manage.windowsazure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Z **usługi active directory** listy, wybierz swój katalog.
3. W menu u góry kliknij **aplikacji**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Na dolnym pasku kliknij **Dodaj**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/03.png) 
5. Na **co chcesz zrobić?** okna dialogowego, kliknij przycisk **Dodaj aplikację moją organizację**. 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/04.png) 
6. Na **Powiedz nam o aplikacji** okna dialogowego, wykonaj następujące czynności: 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    a. W **nazwa** tekstowym, wpisz nazwę (np.: Aplikacja interfejsu API raportowania).
   
    b. Wybierz **aplikacji sieci Web i/lub interfejs API sieci web**.
   
    c. Kliknij przycisk **Dalej**.
7. Na **właściwości aplikacji** okna dialogowego, wykonaj następujące czynności: 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    a. W **adres URL logowania** pole tekstowe, typ `https://localhost`.
   
    b. W **identyfikator URI aplikacji** pole tekstowe, typ ```https://localhost/ReportingApiApp```.
   
    c. Kliknij przycisk **Complete** (Zakończ).

## <a name="grant-your-application-permission-to-use-the-api"></a>Zezwolić aplikacji za pomocą interfejsu API
1. W [klasycznego portalu Azure](https://manage.windowsazure.com/), w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Z **usługi active directory** listy, wybierz swój katalog.
3. W menu u góry kliknij **aplikacji**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png)
4. Na liście aplikacji zaznacz nowo utworzonej aplikacji.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/07.png)
5. W menu u góry kliknij **Konfiguruj**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/08.png)
6. W **uprawnień dotyczących innych aplikacji** sekcji dla **usługi Azure Active Directory** zasobów, kliknij przycisk **uprawnienia aplikacji** listy rozwijanej, a następnie wybierz **Odczytuj dane katalogu**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/09.png)
7. Na dolnym pasku kliknij **zapisać**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>Zbierz ustawienia konfiguracji z katalogu
W tej sekcji przedstawiono sposób uzyskać następujące ustawienia z katalogiem:

* Nazwa domeny
* Identyfikator klienta
* Klucz tajny klienta

Te wartości są wymagane podczas konfigurowania wywołania interfejsu API raportowania. 

### <a name="get-your-domain-name"></a>Pobierz nazwę domeny
1. W [klasycznego portalu Azure](https://manage.windowsazure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Z **usługi active directory** listy, wybierz swój katalog.
3. W menu u góry kliknij **domen**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/11.png) 
4. W **nazwy domeny** kolumny, skopiuj nazwę domeny.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a>Pobieranie Identyfikatora klienta aplikacji
1. W [klasycznego portalu Azure](https://manage.windowsazure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Z **usługi active directory** listy, wybierz swój katalog.
3. W menu u góry kliknij **aplikacji**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Na liście aplikacji zaznacz nowo utworzonej aplikacji.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/07.png)
5. W menu u góry kliknij **Konfiguruj**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/08.png)
6. Kopiowanie z **identyfikator klienta**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a>Pobierz klucz tajny klienta aplikacji
Aby uzyskać klucz tajny klienta aplikacji, musisz utworzyć nowy klucz i zapisać jego wartości podczas zapisywania nowego klucza, ponieważ nie jest możliwe później już pobierania tej wartości.

1. W [klasycznego portalu Azure](https://manage.windowsazure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Z **usługi active directory** listy, wybierz swój katalog.
3. W menu u góry kliknij **aplikacji**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Na liście aplikacji zaznacz nowo utworzonej aplikacji.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/07.png)
5. W menu u góry kliknij **Konfiguruj**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/08.png)
6. W **klucze** sekcji, wykonaj następujące czynności: 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/14.png)
   
    a. Na liście czas trwania wybierz czas trwania
   
    b. Na dolnym pasku kliknij **zapisać**.
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. Skopiuj wartość klucza.

## <a name="next-steps"></a>Następne kroki
* Czy chcesz uzyskać dostęp do danych raportowania interfejsu API w sposób programowy usługi Azure AD? Zapoznaj się z [wprowadzenie do usługi Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).
* Jeśli chcesz dowiedzieć się więcej o usłudze Azure Active Directory, zobacz [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).  

