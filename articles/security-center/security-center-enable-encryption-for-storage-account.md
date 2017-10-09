---
title: "szyfrowanie aaaEnable dla konta magazynu w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zaleceń Centrum zabezpieczeń Azure ** włączenie szyfrowania dla usługi Azure magazynu konta **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>Włącz szyfrowanie dla konta magazynu Azure w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure może zalecić Włącz szyfrowanie usługi Magazyn Azure dla przechowywanych danych.

Szyfrowanie usługi Magazyn (SSE) polega na szyfrowanie danych hello, gdy jest ona zapisywana tooAzure magazynu i odszyfrowywania danych hello przed pobierania.  SSE jest obecnie dostępny tylko dla hello usługi obiektów Blob platformy Azure i może służyć do blokowe i stronicowe obiekty BLOB i uzupełnialnych obiektów blob.  toolearn więcej, zobacz [szyfrowanie usługi Magazyn danych magazynowanych](../storage/common/storage-service-encryption.md).


> [!Note]
> Po włączeniu szyfrowania, tylko nowe dane są szyfrowane. Wszystkie istniejące obiekty BLOB na koncie magazynu pozostać niezaszyfrowana. tooencrypt istniejące obiekty BLOB, zobacz hello [często zadawane pytania dotyczące magazynu usługi szyfrowania](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).
>
>

Szyfrowanie usługi Magazyn jest obsługiwana tylko na kontach magazynu Menedżera zasobów. Klasycznych kont magazynu nie są obecnie obsługiwane. hello toounderstand klasycznego i modeli wdrażania usługi Resource Manager, zobacz [modele wdrażania Azure](../azure-classic-rm.md).

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.  Ten dokument nie jest przewodnik krok po kroku.
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **zalecenia** bloku, wybierz opcję **Włącz szyfrowanie dla konta magazynu Azure**.
   ![Włączanie szyfrowania dla konta magazynu][1]
2. Witaj **Włącz szyfrowanie magazynu** zostanie otwarty blok. Ten blok lista kont magazynu Azure hello wyłączonym szyfrowanie magazynu. W tym przykładzie załóżmy wybierz **storageacct1**.
   ![Włącz szyfrowanie magazynu][2]
3. Witaj **szyfrowania** bloku **storageacct1** otwiera. Wybierz **włączone**.
   ![Blok szyfrowania][3]
4. Wybierz pozycję **Zapisz**.

Teraz ma włączone szyfrowanie magazynu dla **storageacct1**.


## <a name="see-also"></a>Zobacz też
Ten dokument pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "Włącz szyfrowanie dla konta magazynu Azure." toolearn więcej informacji na temat szyfrowanie usługi Magazyn Azure, zobacz następujące hello:

* [Szyfrowanie usługi Magazyn Azure dla przechowywanych danych](../storage/common/storage-service-encryption.md)

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
