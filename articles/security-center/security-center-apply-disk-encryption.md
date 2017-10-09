---
title: "Szyfrowanie dysków aaaApply w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** zastosowanie szyfrowania dysku **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: cd803f1120018c5c86da91186eec1e59d425ede7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a>Zastosuj szyfrowanie dysków w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure zaleca zastosowanie szyfrowania dysków, jeśli masz dysków systemu Windows lub maszyny Wirtualnej systemu Linux, które nie są szyfrowane przy użyciu szyfrowania dysków Azure. Szyfrowanie dysku umożliwia zaszyfrowanie dysków systemu Windows i maszyny Wirtualnej systemu Linux IaaS.  Szyfrowanie jest zalecane dla hello systemu operacyjnego i woluminów danych na maszynie Wirtualnej.

Szyfrowanie dysków branżowymi hello [funkcji BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funkcji systemu Windows i hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) funkcji systemu Linux. Funkcje te zapewniają systemu operacyjnego i toohelp szyfrowania danych ochrony i ochrony danych i spełniają organizacji bezpieczeństwa i zgodności zobowiązań. Szyfrowanie dysków jest zintegrowany z [usługi Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp można kontrolować i zarządzać hello dysku szyfrowania kluczy i kluczy tajnych w ramach subskrypcji usługi Key Vault przy jednoczesnym zapewnieniu, że wszystkie dane w przypadku dysków maszyny Wirtualnej hello są szyfrowane, gdy w Twojej [ Usługa Azure Storage](https://azure.microsoft.com/documentation/services/storage/).

> [!NOTE]
> Szyfrowanie dysków Azure jest obsługiwana na powitania po serwera systemu operacyjnego — Windows Server 2008 R2, Windows Server 2012 i Windows Server 2012 R2. Szyfrowanie dysków jest obsługiwana na powitania po operacyjnego z systemem Linux server - Ubuntu, CentOS, SUSE i SUSE Linux Enterprise Server (SLES).
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **zalecenia** bloku, wybierz opcję **zastosować szyfrowanie dysku**.
2. W hello **zastosować szyfrowanie dysku** bloku, zobacz listę maszyn wirtualnych, dla których szyfrowanie dysków jest zalecane.
3. Wykonaj hello instrukcje tooapply szyfrowania toothese maszyn wirtualnych.

![][1]

tooencrypt maszyn wirtualnych platformy Azure, które zostały zidentyfikowane przez Centrum zabezpieczeń jako wymagające szyfrowania, zaleca się hello następujące kroki:

* Zainstaluj i skonfiguruj program Azure PowerShell. Dzięki temu toorun hello PowerShell polecenia wymagane tooset się hello wymagania wstępne wymagane tooencrypt maszyn wirtualnych platformy Azure.
* Uzyskaj i uruchom skrypt programu PowerShell systemu Azure wymagania wstępne szyfrowania dysków Azure hello.
* Zaszyfruj maszyny wirtualne.

[Szyfrowanie maszyny wirtualnej platformy Azure](security-center-disk-encryption.md) przedstawiono te kroki.  W tym temacie założono, że używasz systemu Windows 10 jako komputer kliencki hello, w którym można skonfigurować szyfrowanie dysków.

Istnieje wiele metod, które mogą być używane dla maszyn wirtualnych platformy Azure. Jeśli użytkownik ma dużą wiedzę na temat programu Azure PowerShell lub interfejsu wiersza polecenia Azure, możesz wybrać toouse inne rozwiązania. toolearn o tych metod, zobacz [szyfrowania dysków Azure](../security/azure-security-disk-encryption.md).

## <a name="see-also"></a>Zobacz też
Ten dokument pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "Zastosuj szyfrowanie dysków." toolearn więcej informacji na temat szyfrowania dysków, zobacz następujące hello:

* [Szyfrowanie i klucz Zarządzanie za pomocą usługi Azure Key Vault](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (wideo, 36 min 39 s) — Dowiedz się, jak toouse dysku zarządzania szyfrowania maszyn wirtualnych IaaS i usługi Azure Key Vault toohelp chronić i ochrony danych.
* [Szyfrowanie maszyny wirtualnej platformy Azure](security-center-disk-encryption.md) (dokument) — Dowiedz się, jak tooencrypt maszyn wirtualnych platformy Azure.
* [Szyfrowanie dysków Azure](../security/azure-security-disk-encryption.md) (dokument) — Dowiedz się, jak tooenable dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux.

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
