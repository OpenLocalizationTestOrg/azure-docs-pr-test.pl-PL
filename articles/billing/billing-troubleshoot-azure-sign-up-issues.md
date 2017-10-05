---
title: "Rozwiązywanie problemów tworzenia konta platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób rozwiązywania niektórych typowych znak Azure problemów w górę."
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
ms.openlocfilehash: 647509ea36e487aca5db661adb3268e845988f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>Rozwiązywanie problemów tworzenia konta na platformie Azure
Jeśli nie możesz zalogować na platformie Azure, użyj porady w tym artykule rozwiązywać typowe problemy. Jeśli masz problem z karty kredytowej podczas rejestracji, zobacz [Twojego debetową lub karta kredytowa została odrzucona w Azure rejestracji](billing-credit-card-fails-during-azure-sign-up.md). Jeśli konto platformy Azure, ale nie można się zalogować, zobacz [nie Zaloguj się do zarządzania Moja subskrypcja platformy Azure](billing-cannot-login-subscription.md).

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>W sekcji "Weryfikacji tożsamości przez kartę" zawiesza się paska postępu

Aby ukończyć weryfikację tożsamości za pomocą karty, pliki cookie innych firm może przeglądarki.

![Zrzut ekranu przedstawiający weryfikacji tożsamości przez sekcję karty wiszące podczas tworzenia konta](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

Wykonaj następujące kroki, aby zaktualizować ustawienia plików cookie w przeglądarce.

1. Jeśli używasz programu Chrome, przejdź do **ustawienia** > **Pokaż zaawansowane ustawienia** > **prywatności** > **ustawienia zawartości**. Usuń zaznaczenie pola wyboru **zablokować pliki cookie innych firm, a dane lokacji**.
2. Jeśli używasz krawędzi, przejdź do **ustawienia** > **widoku Zaawansowane ustawienia** > **plików cookie**. Wybierz **nie blokowania plików cookie**.
3. Odśwież stronę tworzenia konta platformy Azure i sprawdź, czy problem został rozwiązany.
4. Jeśli odświeżanie nie rozwiązuje problemu, zamknij i uruchom ponownie przeglądarkę, a następnie spróbuj ponownie.

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>Formularz karty kredytowej nie obsługuje adres do faktury
Adres do rozliczeń musi być w kraju, które wybrano w **informacje o Tobie** sekcji. Upewnij się, że należy wybrać prawidłowy kraj.

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>Brak wiadomości SMS lub wywołań podczas weryfikacji konta rejestracji
Mimo że jest zwykle znacznie szybsze, może upłynąć do czterech minut kod weryfikacyjny do dostarczenia. Numer telefonu, wprowadzona w celu weryfikacji nie są przechowywane jako numer kontaktu dla konta.

Poniżej przedstawiono kilka dodatkowych porad:
* Numer telefonu VOIP nie może służyć do procesu weryfikacji telefonu.
* Sprawdź numer telefonu należy wprowadzić, w tym numer kierunkowy kraju, które wybrano w menu rozwijanym.
* Jeśli Twój telefon nie odbiera wiadomości tekstowych (SMS), spróbuj **Zadzwoń do mnie** opcji.
* Upewnij się, że Twój telefon mogą odbierać wywołań lub wiadomości SMS z liczbą Stanów Zjednoczonych, na podstawie.

Gdy otrzymasz wiadomość SMS lub połączeń telefonicznych, wprowadź kod, który pojawi się w polu tekstowym.

## <a name="credit-card-declined-or-not-accepted"></a>Karta kredytowa, odrzucone lub nie zostały zaakceptowane
Wirtualny lub przedpłaty kredytową lub debetową karty nie są akceptowane jako płatności za subskrypcje platformy Azure. Aby dowiedzieć się, co może spowodować karty zostać odrzucona, zobacz [Twojego debetową lub karta kredytowa została odrzucona w Azure rejestracji](billing-credit-card-fails-during-azure-sign-up.md).

## <a name="free-trial-is-not-available"></a>"Bezpłatna wersja próbna jest niedostępna"
Czy użyto subskrypcji platformy Azure w przeszłości? Azure warunków użytkowania ogranicza bezpłatnej wersji próbnej aktywacji tylko dla użytkownika, który jest nowym składnikiem Azure. Jeśli miało inny typ subskrypcji platformy Azure, nie można uaktywnić bezpłatnej wersji próbnej. Należy wziąć pod uwagę skorzystania [subskrypcji płatność za rzeczywiste użycie](https://azure.microsoft.com/offers/ms-azr-0003p/).

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>Opłat I wyświetlony na moim koncie bezpłatnej wersji próbnej
Może zostać wyświetlony małą weryfikacji przechowywane na Twoim koncie karty kredytowej, po utworzeniu konta, które zostanie usunięta w ciągu 3 – 5 dni. Jeśli jesteś niepokoju Zarządzanie kosztami, przeczytaj więcej na temat [zapobieganie nieoczekiwany koszty](https://docs.microsoft.com/azure/billing/billing-getting-started).

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>Nie można aktywować plan Azure korzyści MSDN, BizSpark, BizSparkPlus lub MPN
Upewnij się, że poświadczenia prawo logowania. Następnie sprawdź program korzyści, aby upewnić się, że masz prawo. 

* MSDN
  * Sprawdź stan kwalifikujących się usług w Twojej [strony konta MSDN](https://msdn.microsoft.com/subscriptions/manage/default.aspx).
  * Jeśli nie można zweryfikować stanu, skontaktuj się z [centrów obsługi klienta subskrypcji MSDN](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * Zaloguj się do [BizSpark portal](https://www.microsoft.com/bizspark/default.aspx#start-two) i sprawdź stan kwalifikujących się usług, BizSpark i BizSpark Plus.
  * Jeśli nie można zweryfikować stanu, możesz [Uzyskaj pomoc na forach BizSpark](http://aka.ms/bzforums).
* MPN
  * Zaloguj się do [MPN portal](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) i sprawdź stan kwalifikujących się usług. Jeśli masz odpowiednie [umiejętności platformy chmury](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), może być uprawnia do skorzystania z dodatkowych korzyści.
  * Jeśli nie można zweryfikować stanu, skontaktuj się z [Obsługa MPN](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).

## <a name="cant-activate-new-azure-in-open-subscription"></a>Nie można aktywować nową subskrypcję platformy Azure w otwartych
Aby utworzyć subskrypcję platformy Azure w otwartych, musi mieć prawidłowy klucz aktywacji usługi Online (OSA) z co najmniej jednego tokenu Azure w otwartych skojarzony. Jeśli nie masz klucza OSA, skontaktuj się z jednego z Partners Microsoft wymienionych w [Microsoft Pinpoint](http://pinpoint.microsoft.com/).

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) uzyskać szybkie rozwiązanie problemu.
