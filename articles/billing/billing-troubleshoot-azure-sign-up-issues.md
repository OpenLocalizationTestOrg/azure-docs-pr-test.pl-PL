---
title: "aaaTroubleshoot Azure rejestracji problemów | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tootroubleshoot niektórych typowych Azure Zarejestruj problemy."
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee649bfc3be7ba1fe2dd863fac09e1c2311d835b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>Rozwiązywanie problemów tworzenia konta na platformie Azure
Jeśli nie możesz zalogować na platformie Azure, użyj porady hello w tym artykule tootroubleshoot typowych problemów. Jeśli masz problem z karty kredytowej podczas rejestracji, zobacz [Twojego debetową lub karta kredytowa została odrzucona w Azure rejestracji](billing-credit-card-fails-during-azure-sign-up.md). Jeśli konto platformy Azure, ale nie można się zalogować, zobacz [nie można zarejestrować się w toomanage Moja subskrypcja platformy Azure](billing-cannot-login-subscription.md).

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>W sekcji "Weryfikacji tożsamości przez kartę" zawiesza się paska postępu

toocomplete hello weryfikacji tożsamości przez kartę, pliki cookie innych firm z prawem do przeglądarki.

![Zrzut ekranu przedstawiający hello weryfikacji tożsamości przez sekcję karty wiszące podczas tworzenia konta](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

Użyj następujących hello kroki tooupdate ustawienia plików cookie w przeglądarce.

1. Jeśli używasz programu Chrome, przejdź zbyt**ustawienia** > **Pokaż zaawansowane ustawienia** > **prywatności** > **zawartości ustawienia**. Usuń zaznaczenie pola wyboru **zablokować pliki cookie innych firm, a dane lokacji**.
2. Jeśli używasz krawędzi Przejdź zbyt**ustawienia** > **widoku Zaawansowane ustawienia** > **plików cookie**. Wybierz **nie blokowania plików cookie**.
3. Odśwież hello stronę tworzenia konta platformy Azure i sprawdź, czy hello problem został rozwiązany.
4. Jeśli hello odświeżania nie rozwiązuje problemu hello, zamknij i uruchom ponownie przeglądarkę, a następnie spróbuj ponownie.

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>Formularz karty kredytowej nie obsługuje adres do faktury
Adres do rozliczeń musi toobe w kraju hello, wybranym hello **informacje o Tobie** sekcji. Upewnij się, że należy wybrać prawidłowy kraj hello.

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>Brak wiadomości SMS lub wywołań podczas weryfikacji konta rejestracji
Mimo że jest zwykle znacznie szybsze, może potrwać toofour minut dostarczane toobe kod weryfikacyjny. numer telefonu Hello wprowadzona w celu weryfikacji nie są przechowywane jako numer kontaktowy hello konta.

Poniżej przedstawiono kilka dodatkowych porad:
* Numer telefonu VOIP nie może służyć do procesu weryfikacji hello telefonu.
* Sprawdź numer telefonu hello, który zostanie wprowadzony, w tym kod kraju hello wybranego w menu rozwijanym hello.
* Jeśli Twój telefon nie odbiera wiadomości tekstowych (SMS), spróbuj hello **Zadzwoń do mnie** opcji.
* Upewnij się, że Twój telefon mogą odbierać wywołań lub wiadomości SMS z liczbą Stanów Zjednoczonych, na podstawie.

Gdy pojawi się wiadomość hello lub połączeń telefonicznych, wprowadź kod, który pojawi się w polu tekstowym hello.

## <a name="credit-card-declined-or-not-accepted"></a>Karta kredytowa, odrzucone lub nie zostały zaakceptowane
Wirtualny lub przedpłaty kredytową lub debetową karty nie są akceptowane jako płatności za subskrypcje platformy Azure. toosee, co może spowodować Twojej toobe karty odrzucona, zobacz [Twojego debetową lub karta kredytowa została odrzucona w Azure rejestracji](billing-credit-card-fails-during-azure-sign-up.md).

## <a name="free-trial-is-not-available"></a>"Bezpłatna wersja próbna jest niedostępna"
Zostały użyte subskrypcji platformy Azure w przeszłości hello? Hello Azure warunków użytkowania ogranicza bezpłatnej wersji próbnej aktywacji tylko dla użytkownika, który jest nowy tooAzure. Jeśli miało inny typ subskrypcji platformy Azure, nie można uaktywnić bezpłatnej wersji próbnej. Należy wziąć pod uwagę skorzystania [subskrypcji płatność za rzeczywiste użycie](https://azure.microsoft.com/offers/ms-azr-0003p/).

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>Opłat I wyświetlony na moim koncie bezpłatnej wersji próbnej
Może zostać wyświetlony małą weryfikacji przechowywane na Twoim koncie karty kredytowej, po utworzeniu konta, które zostanie usunięta w ciągu 3 dni too5. Jeśli jesteś niepokoju Zarządzanie kosztami, przeczytaj więcej na temat [zapobieganie nieoczekiwany koszty](https://docs.microsoft.com/azure/billing/billing-getting-started).

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>Nie można aktywować plan Azure korzyści MSDN, BizSpark, BizSparkPlus lub MPN
Upewnij się, że używasz hello prawo logowania poświadczeń. Następnie zaznacz hello korzyści programu toomake się, że masz prawo. 

* MSDN
  * Sprawdź stan kwalifikujących się usług w Twojej [strony konta MSDN](https://msdn.microsoft.com/subscriptions/manage/default.aspx).
  * Jeśli nie można zweryfikować stanu, skontaktuj się z hello [centrów obsługi klienta subskrypcji MSDN](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * Zaloguj się toohello [BizSpark portal](https://www.microsoft.com/bizspark/default.aspx#start-two) i sprawdź stan kwalifikujących się usług, BizSpark i BizSpark Plus.
  * Jeśli nie można zweryfikować stanu, możesz [Uzyskaj pomoc na forach BizSpark hello](http://aka.ms/bzforums).
* MPN
  * Zaloguj się toohello [MPN portal](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) i sprawdź stan kwalifikujących się usług. Jeśli masz odpowiednie hello [umiejętności platformy chmury](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), może być uprawnia do skorzystania z dodatkowych korzyści.
  * Jeśli nie można zweryfikować stanu, skontaktuj się z [Obsługa MPN](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).

## <a name="cant-activate-new-azure-in-open-subscription"></a>Nie można aktywować nową subskrypcję platformy Azure w otwartych
toocreate subskrypcji platformy Azure w otwartych musi mieć prawidłowy klucz aktywacji usługi Online (OSA) z co najmniej jeden Azure w otwartych tooit skojarzonego tokenu. Jeśli nie masz klucza OSA, skontaktuj się z jednego z Partners Microsoft wymienionych w [Microsoft Pinpoint](http://pinpoint.microsoft.com/).

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.
