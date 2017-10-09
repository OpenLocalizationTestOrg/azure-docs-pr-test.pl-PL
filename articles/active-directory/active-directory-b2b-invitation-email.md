---
title: "elementy aaaThe hello Azure Active Directory B2B wiadomość e-mail z zaproszeniem współpracy | Dokumentacja firmy Microsoft"
description: "Azure Active Directory B2B współpracy zaproszenia szablon wiadomości e-mail"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: f4908014d71a63442bbdca2182f54c7a79675a82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-elements-of-hello-b2b-collaboration-invitation-email"></a>elementy Hello hello wiadomość e-mail z zaproszeniem współpracy B2B

Wiadomości e-mail z zaproszeniem są partnerami toobring składnikiem krytycznym, na statku jako użytkowników współpracy B2B w usłudze Azure AD. Można używać ich zaufania tooincrease hello adresata. można dodać legalności i społecznościowych toohello potwierdzającego poczty e-mail, czy odbiorca hello toomake tak doświadczenia z wybranie hello **wprowadzenie** przycisk tooaccept hello zaproszenia. Zaufanie jest klucza oznacza tooreduce udostępnianie tarcia. I mają wygląd e-mail hello toomake doskonałe!

![Azure wiadomość e-mail z zaproszeniem AD B2b](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-hello-email"></a>Wyjaśniający, powitalne wiadomości e-mail
Przyjrzyjmy się kilka elementów poczty e-mail hello więc wiesz, jak najlepiej toouse ich możliwości.

### <a name="subject"></a>Temat
Witaj tematu wiadomości e-mail hello następuje hello następującego wzorca: Zapraszamy toohello &lt;tenantname&gt; organizacji

### <a name="from-address"></a>Adres nadawcy
Używamy wzorzec przypominającej LinkedIn dla hello z adresu.  Należy wyczyść kto jest zapraszającej hello i z którego firmy, a także wyjaśnienie wiadomości powitania pochodzi z adres e-mail konta Microsoft. format Hello: &lt;nazwę wyświetlaną zapraszającej&gt; z &lt;tenantname&gt; (za pośrednictwem firmy Microsoft) <invites@microsoft.com&gt;

### <a name="reply-to"></a>Udzielenie odpowiedzi na
Hello odpowiedzi tooemail ustawiono zapraszającej toohello poczty e-mail, jeśli jest dostępna, tak, aby odpowiadaniu się, że toohello e-mail wysyła zapraszającej wstecz toohello wiadomości e-mail.

### <a name="branding"></a>Znakowania.
zaproszenie Hello wiadomości e-mail z dzierżawą Użyj firmy hello znakowania, które mogą zdefiniowano dzierżawy. Jeśli chcesz, aby tootake z zalet tej możliwości, [tutaj](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) hello szczegółów na temat tooconfigure go. Hello Baner logo jest wyświetlany w wiadomości e-mail hello. Postępuj zgodnie z rozmiarem obrazu na powitania i instrukcje jakości [tutaj](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) dla uzyskania najlepszych wyników. Ponadto nazwa firmy hello również zostaną wyświetlone w hello tooaction wywołania.

### <a name="call-tooaction"></a>Wywołanie tooaction
Witaj wywołania tooaction składa się z dwóch części: wyjaśniający, Dlaczego adresat hello odebrał wiadomości powitania i jakie odbiorcy hello jest pytany, toodo informacji na ten temat.
- Witaj, "Dlaczego" sekcji można reagować, wykonując hello następującego wzorca: już został zaproszony tooaccess aplikacji hello &lt;tenantname&gt; organizacji

- I hello sekcję "co użytkownik jest pytany toodo" jest określane przez hello obecności hello **wprowadzenie** przycisku. Po dodaniu odbiorcy hello bez potrzeby hello zaproszeń do skorzystania z tego przycisku nie pojawiają się.

### <a name="inviters-information"></a>Informacje w zapraszającej
Nazwa wyświetlana zapraszającej Hello znajduje się w wiadomości e-mail hello. I dodatkowo, jeśli ustawiono obraz profilu konta usługi Azure AD, hello zapraszanie poczty e-mail zawierają również obraz. Obie są zamierzone tooincrease zaufania z odbiorców w wiadomości e-mail hello.

Jeśli jeszcze nie skonfigurowano obraz profilu, wyświetlana jest ikona inicjały zapraszającej hello zamiast hello obrazu:

  ![Wyświetlanie inicjały zapraszającej hello](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>Treść
Treść Hello zawiera wiadomość hello tego zapraszającej hello Redaguj lub jest przekazywana zaproszenia hello interfejsu API. Jest obszaru tekstu, więc nie przetwarza tagów HTML ze względów bezpieczeństwa.

### <a name="footer-section"></a>Stopki
Stopka Hello zawiera marki firmy Microsoft hello i umożliwia hello adresata, jeśli hello wiadomość e-mail została wysłana z niemonitorowanego alias. Szczególnych przypadkach:

- zapraszającej Hello nie ma adresu e-mail w hello zapraszanie dzierżawy

  ![Obraz zapraszającej nie ma adresu e-mail w hello zapraszanie dzierżawy](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- Odbiorca Hello nie wymaga tooredeem hello zaproszenia

  ![Jeśli adresat nie musi tooredeem zaproszenia](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Co to jest współpraca B2B usługi Azure AD](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?](active-directory-b2b-admin-add-users.md)
* [Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?](active-directory-b2b-iw-add-users.md)
* [Realizacji zaproszenia współpracy B2B](active-directory-b2b-redemption-experience.md)
* [Azure licencjonowania współpracy B2B usługi AD](active-directory-b2b-licensing.md)
* [Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B](active-directory-b2b-troubleshooting.md)
* [Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)](active-directory-b2b-faq.md)
* [Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API](active-directory-b2b-api.md)
* [Usługa Multi-Factor Authentication dla użytkowników współpracy B2B](active-directory-b2b-mfa-instructions.md)
* [Dodawanie użytkowników współpracy B2B bez zaproszenia](active-directory-b2b-add-user-without-invite.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
