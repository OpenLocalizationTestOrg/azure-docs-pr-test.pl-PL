---
title: "Certyfikaty federacyjnych aaaManage w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Data wygaśnięcia hello toocustomize certyfikaty federacyjnych i jak toorenew certyfikaty, które wkrótce wygaśnie."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f516f7f0-b25a-4901-8247-f5964666ce23
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2017
ms.author: jeedes
ms.openlocfilehash: e17622d25c9babfa295cc0bb68c24e21b8c574d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a>Zarządzanie certyfikatami federacyjnego logowania jednokrotnego w usłudze Azure Active Directory
W tym artykule opisano często zadawane pytania i informacje związane z certyfikatami toohello utworzoną za pomocą usługi Azure Active Directory (Azure AD) tooestablish federacyjnych pojedynczego logowania jednokrotnego (SSO) tooyour aplikacji SaaS. Dodaj aplikacje z galerii aplikacji Azure AD hello lub przy użyciu szablonu z systemem innym niż galerii aplikacji. Konfigurowanie aplikacji hello przy użyciu opcji rejestracji Jednokrotnej hello federacyjnych.

W tym artykule jest odpowiednie tylko tooapps, które są skonfigurowane toouse logowania jednokrotnego programu Azure AD przy użyciu Federacji SAML pokazane na powitania poniższy przykład:

![Azure AD rejestracji jednokrotnej](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a>Automatycznie wygenerowany certyfikat dla aplikacji i innych niż galerii
Dodaj nową aplikację z galerii hello i skonfigurować na języku SAML logowania, usługi Azure AD generuje certyfikatu dla aplikacji hello, który jest ważny przez 3 lata. Można pobrać tego certyfikatu z hello **certyfikat podpisywania SAML** sekcji. W przypadku galerii aplikacji w tej sekcji mogą być wyświetlane opcja toodownload hello certyfikatu i metadanych, w zależności od wymagań hello aplikacji hello.

![Azure AD rejestracji jednokrotnej](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-hello-expiration-date-for-your-federation-certificate-and-roll-it-over-tooa-new-certificate"></a>Dostosowywanie hello datę wygaśnięcia certyfikatu federacyjnego i przerzucane tooa nowego certyfikatu
Domyślnie certyfikaty są ustawiane tooexpire po trzy lata. Można wybrać datę wygaśnięcia różnych dla certyfikatu, wykonując następujące kroki hello.
zrzuty ekranu Hello używać Salesforce dla zapewnienia hello przykładzie, ale te kroki można zastosować aplikacji SaaS tooany federacyjnych.

1. W hello [portalu Azure](https://aad.portal.azure.com), kliknij przycisk **aplikacja całościowa** w lewym okienku hello, a następnie kliknij przycisk **nowej aplikacji** na powitania **omówienie** Strona:

   ![Kreator konfiguracji Otwórz hello logowania jednokrotnego](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. Wyszukaj hello galerii aplikacji, a następnie wybierz hello aplikacji, które mają tooadd. Jeśli nie możesz znaleźć aplikacji hello wymagane, dodania aplikacji hello przy użyciu hello **Non galerii aplikacji** opcji. Ta funkcja jest dostępna tylko w hello SKU Azure AD Premium (P1 i P2).

    ![Azure AD rejestracji jednokrotnej](./media/active-directory-sso-certs/add_gallery_application.png)

3. Kliknij hello **logowanie jednokrotne** łącze w hello lewe okienko i zmień **tryb rejestracji jednokrotnej** za**na języku SAML logowania jednokrotnego**. Ten krok wygeneruje certyfikat z trzech lat w aplikacji.

4. toocreate nowego świadectwa, kliknij przycisk hello **Utwórz nowy certyfikat** łącze w hello **certyfikat podpisywania SAML** sekcji.

    ![Wygeneruj nowy certyfikat](./media/active-directory-sso-certs/create_new_certficate.png)

5. Witaj **Utwórz nowy certyfikat** łącze powoduje otwarcie hello formant kalendarza. Można ustawić żadnych daty i godziny w górę toothree lat od hello bieżącą datę. Hello wybrana data i czas jest hello nowe datę i godzinę wygaśnięcia nowego certyfikatu. Kliknij pozycję **Zapisz**.

    ![Pobierz, a następnie przekaż certyfikat hello](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. Teraz hello nowy certyfikat jest dostępny toodownload. Kliknij przycisk hello **certyfikatu** link toodownload jej. W tym momencie certyfikat nie jest aktywne. Należy tooroll za pośrednictwem toothis certyfikatu wybierz hello **uaktywnić nowego świadectwa** pole wyboru i kliknij przycisk **zapisać**. Z tego punktu Usługi Azure AD jest uruchamiany przy użyciu hello nowego certyfikatu podpisywania odpowiedzi hello.

7.  toolearn tooupload hello certyfikatu tooyour określonej aplikacji SaaS, kliknij hello **samouczek konfiguracji aplikacji w widoku** łącza.

## <a name="renew-a-certificate-that-will-soon-expire"></a>Odnów certyfikat, który wkrótce wygaśnie
Witaj następujące kroki odnawiania powinno spowodować bez przestojów istotne dla użytkowników. zrzuty ekranu Hello w tej sekcji funkcji Salesforce jako przykład, ale te kroki można zastosować tooany federacyjnych aplikacji SaaS.

1. Na powitania **usługi Azure Active Directory** aplikacji **logowanie jednokrotne** strony, wygeneruj nowy certyfikat hello aplikacji. Można to zrobić, klikając hello **Utwórz nowy certyfikat** łącze w hello **certyfikat podpisywania SAML** sekcji.

    ![Wygeneruj nowy certyfikat](./media/active-directory-sso-certs/create_new_certficate.png)

2. Wybierz hello potrzeby Data wygaśnięcia i godzina dla nowego certyfikatu i kliknij przycisk **zapisać**.

3. Pobierz certyfikat hello w hello **certyfikat podpisywania SAML** opcji. Przekaż ekranie konfiguracji rejestracji jednokrotnej hello nowego świadectwa toohello SaaS aplikacji. toolearn jak toodo dla określonej aplikacji SaaS, kliknij przycisk hello **samouczek konfiguracji aplikacji w widoku** łącza.
   
4. tooactivate hello nowego certyfikatu w usłudze Azure AD, wybierz hello **uaktywnić nowego świadectwa** pole wyboru, a następnie kliknij przycisk hello **zapisać** przycisk u góry hello hello strony. Zbiorcze za pośrednictwem hello nowego certyfikatu na powitania po stronie usługi Azure AD. zmiany stanu Hello hello certyfikatu z **nowy** za**Active**. Z tego punktu Usługi Azure AD jest uruchamiany przy użyciu hello nowego certyfikatu podpisywania odpowiedzi hello. 
   
    ![Wygeneruj nowy certyfikat](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a>Pokrewne artykuły:
* [Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Rozwiązywanie problemów z systemem SAML logowania jednokrotnego](active-directory-saml-debugging.md)
