---
title: aaaAzure MFA logowania w trakcie weryfikacji dwuetapowej | Dokumentacja firmy Microsoft
description: "Ta strona pozwoli wskazówki na którym toogo toosee hello różne metody logowania dostępny za pomocą usługi Azure MFA."
keywords: "Uwierzytelnianie użytkownika, logowania, zarejestruj się przy użyciu telefonu komórkowego, zarejestruj się przy użyciu telefonu biurowego"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a>Witaj logowania z usługi Azure Multi-Factor Authentication
> [!NOTE]
> Celem tego artykułu Hello jest toowalk za pomocą typowego środowiska logowania. Aby uzyskać pomoc dotyczącą zalogować się lub tootroubleshoot problemów, zobacz [problemy z uwierzytelnianiem wieloskładnikowym Azure](multi-factor-authentication-end-user-troubleshoot.md).

## <a name="what-will-your-sign-in-experience-be"></a>Jakie będzie środowisko logowania
Środowisko logowania różni się w zależności od tego, co możesz wybrać toouse jako Twoje czynnika: połączenie telefoniczne, aplikacja uwierzytelniania lub tekstów. Wybierz opcję hello, która najlepiej opisuje czynności:

| Jak możesz się zalogować? | 
| --- |
| [Przy użyciu połączenia telefonicznego toomy telefon komórkowy lub office telefonu](#signing-in-with-a-phone-call) |
| [Przy użyciu telefonu komórkowego toomy tekstu](#signing-in-with-a-text-message)
| [Z powiadomienia z aplikacji Microsoft Authenticator hello](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [Z kodów weryfikacyjnych z aplikacji Microsoft Authenticator hello](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [Przy użyciu alternatywne metody ponieważ nie można użyć Moje preferowaną metodą w tej chwili](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a>Logowanie się przy użyciu połączeń telefonicznych
Witaj następujących informacji opisano doświadczenia weryfikacji dwuetapowej hello mobile tooyour wywołania lub telefon biurowy.

1. Zaloguj się tooan aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.  
2. Microsoft dzwoni do Ciebie.  
3. Odpowiedzi hello telefonu i naciśnij klawisz # hello.  

## <a name="signing-in-with-a-text-message"></a>Logowanie się przy użyciu wiadomości SMS
Witaj następujących informacji opisano środowisko weryfikacji dwuetapowej hello telefonu komórkowego tooyour wiadomości tekstowych:

1. Zaloguj się tooan aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła. 
2. Firma Microsoft wysyła wiadomość tekstową zawierającą numer kodu. 
3. Wprowadź kod hello w polu hello na powitania strony logowania. 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a>Logowanie się przy użyciu aplikacji Microsoft Authenticator hello 
Witaj następujące informacje w tym artykule opisano hello środowisko przy użyciu aplikacji Microsoft Authenticator hello do weryfikacji dwuetapowej. Istnieją dwa sposoby toouse hello aplikacji. Na urządzeniu może odbierać powiadomienia wypychane, lub możesz otworzyć tooget aplikacji hello kod weryfikacyjny.

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a>toosign się powiadomienie z aplikacji Microsoft Authenticator hello
1. Zaloguj się tooan aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.
2. Firma Microsoft wysyła aplikacji Microsoft Authenticator toohello powiadomienia na urządzeniu.

  ![Firma Microsoft wysyła powiadomienia](./media/multi-factor-authentication-end-user-signin/notify.png)

3. Otwórz hello powiadomień na telefon i wybierz hello **Sprawdź** klucza. Jeśli firma wymaga numeru PIN, wprowadź go tutaj.
4. Powinny teraz być zalogowano.

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a>toosign przy użyciu kodu weryfikacyjnego z aplikacji Microsoft Authenticator hello

Jeśli używasz kodów weryfikacyjnych tooget aplikacji Microsoft Authenticator hello, następnie po otwarciu aplikacji hello jest wyświetlana liczba pod nazwą konta. Liczba ta zmienia co 30 sekund, aby nie używać hello tę samą liczbę dwa razy. Gdy pojawi się monit o kod weryfikacyjny, Otwórz aplikację hello i używać dowolnej wartości są obecnie wyświetlane. 

1. Zaloguj się tooan aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.
2. Microsoft wyświetla monit o podanie kodu weryfikacyjnego.

  ![Wprowadź kod weryfikacyjny](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. Otwórz aplikację Microsoft Authenticator hello na telefonie i wprowadź kod hello w polu hello, w których logujesz.

## <a name="signing-in-with-an-alternate-method"></a>Logowanie się przy użyciu alternatywnych — metoda
Czasami nie masz telefon hello lub urządzenia, które można skonfigurować jako metodę weryfikacji preferowanego. Ta sytuacja jest, dlatego zaleca się skonfigurowanie metody wykonywania kopii zapasowej dla Twojego konta. Witaj poniższej sekcji przedstawiono sposób toosign się przy użyciu alternatywna metoda gdy podstawowej metody nie mogą być dostępne.

1. Zaloguj się tooan aplikacji lub usługi, takiej jak Office 365 przy użyciu nazwy użytkownika i hasła.
2. Wybierz **użyć innej opcji weryfikacji**. Widzisz opcji weryfikacji różnych opartych o ile masz Instalatora.
3. Wybierz alternatywną metodę i zaloguj się.

  ![Należy użyć alternatywnej metody](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a>Następne kroki

Jeśli masz problemy z zarejestrowaniem się przy użyciu weryfikacji dwuetapowej, uzyskać więcej informacji o [problemy z uwierzytelnianiem wieloskładnikowym Azure](multi-factor-authentication-end-user-troubleshoot.md).

Dowiedz się, jak za[zarządzać ustawieniami weryfikacji dwuetapowej](multi-factor-authentication-end-user-manage-settings.md).

Dowiedz się, jak za[wprowadzenie do aplikacji Microsoft Authenticator hello](microsoft-authenticator-app-how-to.md) tak, aby można było używać toosign powiadomienia, zamiast teksty i połączeń telefonicznych. 
