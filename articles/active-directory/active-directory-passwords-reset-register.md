---
title: "Usługi Azure AD: Rejestracji SSPR | Dokumentacja firmy Microsoft"
description: "Zarejestruj dane uwierzytelniania dla usługi Azure AD hasła samoobsługi resetowania"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: end-user
ms.openlocfilehash: dfcd0106616218c84d23920b124bed5b202cdd6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="register-for-self-service-password-reset"></a>Rejestrowanie na potrzeby samoobsługowego resetowania hasła

> [!IMPORTANT]
> **Jesteś tutaj, ponieważ masz problemy z logowaniem?** Jeśli tak, [w tym miejscu opisano, jak zmienić i zresetować własne hasło](active-directory-passwords-update-your-own-password.md).

Jako użytkownik końcowy może zresetować hasło lub odblokować konto bez konieczności toospeak tooa osoby za pomocą Samoobsługowego resetowania hasła (SSPR). Przed użyciem tej funkcji, metody uwierzytelniania tooregister lub potwierdź hello wstępnie zdefiniowanych metod uwierzytelniania, jakie administrator ma.

## <a name="register-or-confirm-authentication-data-with-sspr"></a>Rejestrowanie lub potwierdzanie danych uwierzytelniania na potrzeby samoobsługowego resetowania hasła

1. Witaj Otwórz przeglądarkę sieci web na toohello Twojego urządzenia, a następnie przejść [strony rejestracji resetowania haseł](http://aka.ms/ssprsetup)
2. Wprowadź nazwę użytkownika i hasło podane przez administratora
3. W zależności od sposobu konfiguracji działu IT rzeczy, co najmniej jeden z następujących hello opcje są dostępne dla tooconfigure należy i sprawdź. Administrator może wypełnienie pól to dla Ciebie, gdy mają uprawnienia toouse hello informacji.
    * Telefon biurowy to tylko możliwe toobe ustawione przez administratora
    * Numer telefonu uwierzytelniania powinien być ustawiony numer telefonu tooanother toolike dostępu byłyby telefonu komórkowego, który może odbierać SMS lub połączenie.
    * Uwierzytelnianie poczty E-mail powinien być ustawiony tooan alternatywny adres e-mail, który można uzyskać dostęp bez hasła hello należy tooreset.
    * Pytania zabezpieczające przedstawiono listę pytania, które administrator została zatwierdzona dla tooanswer użytkownik. Nie można używać hello tej samej pytanie lub odpowiedzi na więcej niż raz.
4. Podaj i Zweryfikuj informacje o hello wymaganego przez administratora. Jeśli więcej niż jedna opcja jest dostępna, zaleca się zarejestrować wiele metod tooprovide elastyczność, gdy inna metoda jest niedostępny (przykład: tooaccess podróży i telefon biurowy)

    ![Rejestrowanie metod uwierzytelniania i klikanie przycisku Zakończ][Register]

5. Po wykonaniu kroku 4 Wybierz **Zakończ** i będzie teraz stanie toouse samodzielnego resetowania haseł gdy będziesz potrzebować tooin hello przyszłości.

Po wprowadzeniu danych w hello numer telefonu uwierzytelniania lub adres E-mail uwierzytelniania nie jest widoczne w hello katalogu globalnego. Hello tylko osoby, którzy mogą przeglądać dane te są możesz i Administratorzy w Twojej organizacji. Tylko można zauważyć, że hello tooyour pytania zabezpieczeń.

Administratorzy mogą wymagać możesz tooconfirm metody uwierzytelniania po upływie określonego czasu toomake upewnić się, że nadal odpowiednie metody hello zarejestrowany.

## <a name="common-problems-and-their-solutions"></a>Typowe problemy i ich rozwiązania

 Poniżej przedstawiono niektóre typowe przypadki błąd i ich rozwiązania:

| Przypadek błędu| Jakie błąd znaleźć?| Rozwiązanie |
| --- | --- | --- |
| Pojawia się Strona "Skontaktuj się z administratorem" po wprowadzeniu mój identyfikator użytkownika | Skontaktuj się z administratorem <br> <br> Wykryliśmy, że hasło konta użytkownika nie jest zarządzany przez firmę Microsoft. W związku z tym nie możemy tooautomatically zresetowania hasła. <br> <br> Należy toocontact działu IT Aby uzyskać dalszą pomoc. | Ten komunikat jest wyświetlany, ponieważ działu IT zarządza hasła w środowisku lokalnym i nie zezwala tooreset Twojego hasła nie może uzyskać dostępu połączenie z kontem. <br> <br> tooreset hasła, skontaktuj się z pomocą personelu działu IT bezpośrednio dla pomocy i daj poznać mają tooreset hasła, więc ich włączenia tej funkcji można.|
| Pojawia się komunikat o błędzie "Twoje konto nie ma uprawnień do resetowania hasła" po wprowadzeniu mój identyfikator użytkownika | Twoje konto nie ma uprawnień do resetowania hasła <br> <br> Przepraszamy, ale pracownicy działu informatycznego nie skonfigurował tego konta do korzystania z tej usługi. <br> <br> Jeśli chcesz, firma Microsoft może skontaktuj się z administratorem w Twojej organizacji tooreset Twojego hasła. | Ten komunikat jest wyświetlany, ponieważ pracownicy działu informatycznego nie włączył resetowania haseł dla organizacji z nie może uzyskać dostępu połączenie z kontem, lub nie licencji toouse hello funkcji. <br> <br> tooreset hasła, kliknij kontakt toosend łącze administrator firmy tooyour wiadomości e-mail do personelu IT i poinformuj ma tooreset hasła, ich włączenia tej funkcji można. |
| Pojawia się komunikat o błędzie "nie można zweryfikować konto" po wprowadzeniu mój identyfikator użytkownika | Nie można zweryfikować konta <br> <br> Jeśli chcesz, firma Microsoft może skontaktuj się z administratorem w Twojej organizacji tooreset Twojego hasła. | Ten komunikat jest wyświetlany, ponieważ są włączone do resetowania hasła, ale nie została zarejestrowana toouse hello usługi. tooregister hasła resetowania, przejdź toohttp://aka.ms/ssprsetup po ma się odzyskać dostęp tooyour konta. <br> <br> tooreset hasła, kliknij przycisk Skontaktuj się z administratorem łącze toosend firmy tooyour poczty e-mail w personel działu informatycznego. |

## <a name="next-steps"></a>Następne kroki

* [Jak toochange przy użyciu hasła samoobsługowego resetowania hasła](active-directory-passwords-update-your-own-password.md)
* [Strona rejestracji w celu resetowania hasła](http://aka.ms/ssprsetup)
* [Portal resetowania hasła](https://passwordreset.microsoftonline.com/)
* [Nie można zarejestrować w tooyour konta Microsoft](https://support.microsoft.com/help/12429/microsoft-account-sign-in-cant)

[Register]: ./media/active-directory-passwords-reset-register/register-2-methods.png "Strona rejestrowania na potrzeby resetowania hasła, na której widoczne są zarejestrowane metody i przycisk Zakończ"

