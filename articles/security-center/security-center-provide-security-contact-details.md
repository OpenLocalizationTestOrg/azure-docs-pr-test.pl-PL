---
title: "dane kontaktowe aaaProvide zabezpieczeń w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób zabezpieczeń tooprovide kontaktowe w Centrum zabezpieczeń Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a>Podaj szczegóły dotyczące kontaktu zabezpieczeń w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure zaleca Podaj szczegóły dotyczące kontaktu zabezpieczeń dla subskrypcji platformy Azure, jeśli nie jest jeszcze. Te informacje będą używane przez Microsoft toocontact Jeśli hello Microsoft Security odpowiedzi Center (MSRC) wykrywa, że danych klienta uzyskaniu przez nieautoryzowanego lub nielegalnych stronę. MSRC wykonuje monitorowanie zabezpieczeń wybierz hello sieć platformy Azure i infrastruktury i odbiera zagrożeń analizy i nadużycia utrudnień od osób trzecich.

Wiadomość e-mail z powiadomieniem jest wysyłany na powitania pierwsze codzienne wystąpienie alertu i tylko alerty o wysokim znaczeniu. Preferencje poczty e-mail można konfigurować tylko dla zasad subskrypcji. Grupy zasobów w ramach subskrypcji odziedziczy te ustawienia.

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.  Nie jest to przewodnik krok po kroku.
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **zalecenia** bloku, wybierz opcję **podać szczegóły dotyczące kontaktu zabezpieczeń**.
   ![Podaj kontaktu zabezpieczeń][1]
2. Spowoduje to otwarcie bloku hello **podać szczegóły dotyczące kontaktu zabezpieczeń**. Wybierz informacje kontaktowe tooprovide hello subskrypcji platformy Azure na.
   ![Podawanie szczegółów dotyczących kontaktu ds. zabezpieczeń][2]
3. Drugi **podać szczegóły dotyczące kontaktu zabezpieczeń** zostanie otwarty blok.

   * Wprowadź adres e-mail kontaktu zabezpieczeń hello lub adresów rozdzielonych przecinkami. Ogranicz liczbę toohello adresów e-mail, które można wprowadzić nie istnieje.
   * Wprowadź jeden zabezpieczeń kontaktu międzynarodowy numer telefonu.
   * wiadomości e-mail tooreceive o alerty o wysokim znaczeniu, włącz opcję hello **Wyślij do mnie wiadomość e-mail o alertach**.
   * W przyszłości hello będą miały hello opcja toosend e-mail powiadomienia toosubscription właścicieli. Ta opcja jest obecnie wygaszone.
   * Wybierz **OK** tooapply hello zabezpieczeń subskrypcji tooyour informacji, skontaktuj się z pomocą.

## <a name="see-also"></a>Zobacz też
toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) --hello najnowsze zabezpieczeń platformy Azure i informacji.

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
