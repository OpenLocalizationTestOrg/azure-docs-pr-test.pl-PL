---
title: "Zarządzanie certyfikatami federacji w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dostosować daty wygaśnięcia certyfikatów Federacji i sposobie odnawiania certyfikatów, które wkrótce wygasną."
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
ms.openlocfilehash: 1283b570200f05003658824760ecbb6722f241d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-certificates-for-federated-single-sign-on-in-azure-active-directory"></a>Zarządzanie certyfikatami federacyjnego logowania jednokrotnego w usłudze Azure Active Directory
W tym artykule omówiono typowe pytania i informacje dotyczące certyfikatów, które usługi Azure Active Directory (Azure AD) tworzy ustanowienie federacyjnej rejestracji jednokrotnej (SSO) do aplikacji SaaS. Dodaj aplikacje z galerii aplikacji Azure AD lub przy użyciu szablonu z systemem innym niż galerii aplikacji. Konfigurowanie aplikacji przy użyciu opcji federacyjnego logowania jednokrotnego.

Ten artykuł dotyczy tylko do aplikacji, które są skonfigurowane do używania usługi Azure AD z logowania jednokrotnego przy użyciu Federacji SAML, jak pokazano w poniższym przykładzie:

![Azure AD rejestracji jednokrotnej](./media/active-directory-sso-certs/saml_sso.PNG)

## <a name="auto-generated-certificate-for-gallery-and-non-gallery-applications"></a>Automatycznie wygenerowany certyfikat dla aplikacji i innych niż galerii
Dodaj nową aplikację z galerii i skonfigurować na języku SAML logowania, usługi Azure AD generuje certyfikat dla aplikacji, która jest ważny przez 3 lata. Można pobrać tego certyfikatu od **certyfikat podpisywania SAML** sekcji. W przypadku aplikacji galerii w tej sekcji mogą być wyświetlane opcję, aby pobrać certyfikat lub metadanych, w zależności od wymagań aplikacji.

![Azure AD rejestracji jednokrotnej](./media/active-directory-sso-certs/saml_certificate_download.png)

## <a name="customize-the-expiration-date-for-your-federation-certificate-and-roll-it-over-to-a-new-certificate"></a>Dostosowywanie datę wygaśnięcia certyfikatu federacyjnego i przerzucane do nowego certyfikatu
Domyślnie certyfikaty są ustawiane wygaśnie po upływie trzech lat. Można wybrać datę wygaśnięcia różnych dla certyfikatu, wykonując następujące kroki.
Zrzuty ekranu używać usług Salesforce przykładach, ale te kroki można zastosować do wszystkich federacyjnych aplikacji SaaS.

1. W [portalu Azure](https://aad.portal.azure.com), kliknij przycisk **aplikacja całościowa** w lewym okienku, a następnie kliknij przycisk **nowej aplikacji** na **omówienie** strony:

   ![Otwórz Kreatora konfiguracji logowania jednokrotnego](./media/active-directory-sso-certs/enterprise_application_new_application.png)

2. Wyszukaj galerii aplikacji, a następnie wybierz aplikację, którą chcesz dodać. Nie można odnaleźć wymaganej aplikacji, dodaj aplikację za pomocą **Non galerii aplikacji** opcji. Ta funkcja jest dostępna tylko w wersji Azure AD Premium (P1 i P2).

    ![Azure AD rejestracji jednokrotnej](./media/active-directory-sso-certs/add_gallery_application.png)

3. Kliknij przycisk **logowanie jednokrotne** łącze w okienku po lewej stronie i zmień **tryb rejestracji jednokrotnej** do **na języku SAML logowania jednokrotnego**. Ten krok wygeneruje certyfikat z trzech lat w aplikacji.

4. Aby utworzyć nowy certyfikat, kliknij przycisk **Utwórz nowy certyfikat** łącze w **certyfikat podpisywania SAML** sekcji.

    ![Wygeneruj nowy certyfikat](./media/active-directory-sso-certs/create_new_certficate.png)

5. **Utwórz nowy certyfikat** łącze powoduje otwarcie formant kalendarza. Można ustawić dowolną datę i godzinę do trzech lat od bieżącej daty. Wybrana data i godzina jest nowy Data i godzina wygaśnięcia nowego certyfikatu. Kliknij pozycję **Zapisz**.

    ![Pobierz, a następnie przekaż certyfikat](./media/active-directory-sso-certs/certifcate_date_selection.PNG)

6. Nowy certyfikat jest teraz dostępne do pobrania. Kliknij przycisk **certyfikatu** link jej pobranie. W tym momencie certyfikat nie jest aktywne. Przeskocz do tego certyfikatu, należy wybrać **uaktywnić nowego świadectwa** pole wyboru i kliknij przycisk **zapisać**. Z tego punktu Usługi Azure AD jest uruchamiany przy użyciu nowego certyfikatu podpisywania odpowiedzi.

7.  Aby dowiedzieć się, jak można przekazać certyfikatu do określonej aplikacji SaaS, kliknij przycisk **samouczek konfiguracji aplikacji w widoku** łącza.

## <a name="renew-a-certificate-that-will-soon-expire"></a>Odnów certyfikat, który wkrótce wygaśnie
Poniższe kroki odnawiania powinno spowodować bez przestojów istotne dla użytkowników. Zrzuty ekranu w tej sekcji funkcji Salesforce jako przykład, ale te kroki można zastosować do wszystkich federacyjnych aplikacji SaaS.

1. Na **usługi Azure Active Directory** aplikacji **logowanie jednokrotne** strony, wygeneruj nowy certyfikat dla aplikacji. Można to zrobić, klikając **Utwórz nowy certyfikat** łącze w **certyfikat podpisywania SAML** sekcji.

    ![Wygeneruj nowy certyfikat](./media/active-directory-sso-certs/create_new_certficate.png)

2. Wybierz odpowiednią datę i godzinę wygaśnięcia dla nowego certyfikatu, a następnie kliknij przycisk **zapisać**.

3. Pobierz certyfikat w **certyfikat podpisywania SAML** opcji. Przekaż nowy certyfikat na ekranie konfiguracji rejestracji jednokrotnej aplikacji SaaS. Aby dowiedzieć się, jak to zrobić dla określonej aplikacji SaaS, kliknij przycisk **samouczek konfiguracji aplikacji w widoku** łącza.
   
4. Aby aktywować nowy certyfikat w usłudze Azure AD, wybierz **uaktywnić nowego świadectwa** pole wyboru i kliknij przycisk **zapisać** u góry strony. Zbiorcze za pośrednictwem nowego świadectwa po stronie usługi Azure AD. Zmiany stanu certyfikatu z **nowy** do **Active**. Z tego punktu Usługi Azure AD jest uruchamiany przy użyciu nowego certyfikatu podpisywania odpowiedzi. 
   
    ![Wygeneruj nowy certyfikat](./media/active-directory-sso-certs/new_certificate_download.png)

## <a name="related-articles"></a>Pokrewne artykuły:
* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Rozwiązywanie problemów z systemem SAML logowania jednokrotnego](active-directory-saml-debugging.md)
