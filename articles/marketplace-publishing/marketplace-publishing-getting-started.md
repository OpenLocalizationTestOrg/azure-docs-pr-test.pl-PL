---
title: "aaaOverview jak toocreate i wdrażanie toohello oferta portalu Marketplace | Dokumentacja firmy Microsoft"
description: "Zrozumienie hello kroki wymagane toobecome zatwierdzonych Microsoft developer i utworzyć i wdrożyć obraz maszyny wirtualnej, szablonu, Usługa danych lub dewelopera usługi hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5343bd26-c6e4-4589-85b7-4a2c00bba8ab
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio
ms.openlocfilehash: ac5480b98b8b1021a595db951ed9c974f74415dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-and-manage-an-offer-in-hello-azure-marketplace"></a>Publikowanie i zarządzanie nimi oferty w portalu Azure Marketplace hello
W tym artykule podano toohelp deweloperom tworzenie, wdrażanie i zarządzanie ich rozwiązania na liście hello Azure Marketplace dla innych klientów platformy Azure i partnerów toopurchase i użycia.

## <a name="marketplace-publishing"></a>Publikowanie witryny Marketplace
Jako wydawca Azure można dystrybuować i sprzedawać innowacyjne rozwiązania lub deweloperzy tooother usług, niezależnym dostawcom oprogramowania, i informatyków wynikające z hello Marketplace. Za pomocą hello Marketplace, możesz uzyskiwać dostęp klientów, którzy chcą tooquickly opracowywania aplikacji opartej na chmurze i rozwiązań mobilnych. Jeśli rozwiązania jest przeznaczony dla użytkowników biznesowych, może być tooconsider hello [AppSource](http://appsource.microsoft.com) marketplace.


## <a name="supported-types-of-solutions"></a>Obsługiwane typy rozwiązań
Witaj pierwszą rzeczą, którą chcesz toodo jako wydawca jest toodefine jakiego rodzaju rozwiązania oferty firmy. Witaj Marketplace obsługuje następujące typy ofert hello:

|Typ rozwiązania|Maszyna wirtualna|Szablon rozwiązania|
|---|---|---|
|**Definicja**|Wstępnie skonfigurowane obrazów za pomocą pełnego zainstalowanego systemu operacyjnego i co najmniej jednej aplikacji. Obraz maszyny wirtualnej zapewnia toocreate niezbędne informacje hello i wdrażanie maszyn wirtualnych w hello usługi maszynach wirtualnych platformy Azure.|Struktura danych, która może odwoływać się co najmniej jednej różne usługi platformy Azure, takich jak usługi opublikowana przez innych sprzedawców. Subskrybenci platformy Azure może być używany toodeploy ofert co najmniej w jednej, skoordynowanej sposób.|
|**Przykład**|Jako wydawca Azure utworzeniu i zweryfikować maszynę Wirtualną za pomocą usługi innowacyjnych bazy danych. Inne subskrybenci platformy Azure mają tooprocure i wdrażanie tej maszyny Wirtualnej w swoich środowiskach usługi w chmurze.|Jako wydawca Azure został powiązany zestaw usług z na platformie Azure, które ułatwiają szybkie toodeploy usługi w chmurze z równoważeniem obciążenia, zwiększone zabezpieczenia i wysokiej dostępności. Inne subskrybenci platformy Azure, można zaoszczędzić czas, przez hello szablon rozwiązania, które spełnia ich cel. Nie posiadają toomanually zlokalizować, Uzyskaj, wdrażanie i konfigurowanie hello takie same lub podobne usług platformy Azure.|

> [!NOTE]
> Niektóre kroki są wspólne dla różnych typów hello rozwiązań, a inne są różne toohello odpowiedniego typu rozwiązania. Ten artykuł zawiera krótki przegląd kroków hello potrzeby toocomplete rozwiązanie.

## <a name="publish-a-solution"></a>Publikowanie rozwiązania
![Wyznaczyć, rejestrowanie, Opublikuj](media/marketplace-publishing-getting-started/img01.png)

### <a name="nominate-your-solution-for-pre-approval"></a>Wyznaczyć rozwiązania na zatwierdzenie przed
toopublish maszynę wirtualną [rozwiązania](https://createopportunity.azurewebsites.net) toohello Marketplace, pełną hello Microsoft Azure certyfikowane **formularza wyznaczenie rozwiązania**.

>[!NOTE]
> Jeśli pracujesz z menedżerem konta partnera lub DX Menedżera partnera, poproś go toonominate rozwiązania dla programu Azure certyfikowane hello. Można także przejść toohello [Microsoft Azure certyfikowane](http://createopportunity.azurewebsites.net) strony sieci Web i wypełnij formularz aplikacji hello. Wprowadź adres e-mail hello menedżerem partnera lub DX Menedżera partnera w hello **skontaktuj się z Microsoft Sponsor** pole.

Jeśli spełniają kryteria hello w hello [zasady uczestnictwa w portalu Azure Marketplace](http://go.microsoft.com/fwlink/?LinkID=526833) i aplikacja została zatwierdzona, możemy rozpocząć pracę możesz tooonboard toohello Twojego rozwiązania Marketplace.

### <a name="register-your-account-as-a-microsoft-seller"></a>Zarejestruj konto przy użyciu jako sprzedawcy firmy Microsoft
Zarejestruj konto Microsoft jako [konta Microsoft Developer](marketplace-publishing-accounts-creation-registration.md).

### <a name="publish-your-solution"></a>Publikowanie rozwiązania
toopublish toohello rozwiązania Marketplace, wykonaj następujące kroki:
1. Spełnianie wymagań nietechnicznym hello.

    a. Spełnienia hello [nietechnicznym wymagania wstępne](marketplace-publishing-pre-requisites.md).

    b. Spełnienia hello [techniczne wymagania wstępne maszyny Wirtualnej](marketplace-publishing-vm-image-creation-prerequisites.md).

    c. Spełnienia hello [wymagania wstępne dotyczące technicznej rozwiązanie szablonu](marketplace-publishing-solution-template-creation-prerequisites.md).

2. Utwórz ofertę.

    a. Utwórz [maszyny wirtualnej](marketplace-publishing-vm-image-creation.md) oferty.

    b. Utwórz [szablon rozwiązania](marketplace-publishing-solution-template-creation.md) oferty.

3. Utwórz ofertę [marketingu zawartości](marketplace-publishing-push-to-staging.md).

4. Przetestuj ofertę tymczasowych.

    a. Testowanie ofertę maszyny Wirtualnej w [przemieszczania](marketplace-publishing-vm-image-test-in-staging.md).

    b. Testowanie ofertę szablon rozwiązania w [przemieszczania](marketplace-publishing-solution-template-test-in-staging.md).

5. Wdrażanie toohello Twojej oferty [Marketplace](marketplace-publishing-push-to-production.md).


### <a name="create-and-manage-a-virtual-machine-image"></a>Tworzenie i zarządzanie nimi obraz maszyny wirtualnej
Tworzenie i zarządzanie nimi obrazu maszyny Wirtualnej przy użyciu tych zasobów:
* Tworzenie obrazu maszyny Wirtualnej [lokalnymi](marketplace-publishing-vm-image-creation-on-premise.md).
* Utwórz maszynę wirtualną działającą [systemu Windows w portalu Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Utwórz maszynę wirtualną działającą [systemu Linux w portalu Azure hello](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Rozwiązywanie typowych problemów podczas [tworzenia dysku VHD](marketplace-publishing-vm-image-creation-troubleshooting.md).

## <a name="manage-your-solution"></a>Rozwiązania do zarządzania
Zarządzanie za pomocą rozwiązania z hello następujące zasoby:
* [Oferuje Przewodnik po produkcji hello odczytu dla maszyny wirtualnej](marketplace-publishing-vm-image-post-publishing.md)
* [Aktualizuj szczegóły nietechnicznym hello oferty lub wersji](marketplace-publishing-vm-image-post-publishing.md#update-the-nontechnical-details-of-an-offer-or-a-sku)
* [Szczegóły techniczne hello oferty lub wersji aktualizacji](marketplace-publishing-vm-image-post-publishing.md#update-the-technical-details-of-a-sku)
* [Dodaj nowe jednostki SKU w ramach wymienionych oferty](marketplace-publishing-vm-image-post-publishing.md#add-a-new-sku-under-a-listed-offer)
* [Zmień liczba dysków danych hello wymienionych jednostki SKU](marketplace-publishing-vm-image-post-publishing.md#change-the-data-disk-count-for-a-listed-sku)
* [Usuń to wymienione oferta z hello Marketplace](marketplace-publishing-vm-image-post-publishing.md)
* [Usuń wymienionych jednostki SKU z hello Marketplace](marketplace-publishing-vm-image-post-publishing.md#delete-a-listed-sku-from-the-marketplace)
* [Usuń hello bieżącej wersji listy jednostki SKU z hello Marketplace](marketplace-publishing-vm-image-post-publishing.md#delete-the-current-version-of-a-listed-sku-from-the-marketplace)
* [Przywróć hello listę wartości tooproduction cen](marketplace-publishing-vm-image-post-publishing.md#revert-the-listing-price-to-production-values)
* [Przywróć hello wartości tooproduction modelu rozliczeń](marketplace-publishing-vm-image-post-publishing.md#revert-the-billing-model-to-production-values)
* [Przywróć ustawienie widoczności hello listy wartości produkcji toohello jednostki SKU](marketplace-publishing-vm-image-post-publishing.md#revert-the-visibility-setting-of-a-listed-sku-to-the-production-value)
* [Zmień programu incentive odsprzedawcy Cloud Solution Provider](marketplace-publishing-csp-incentive.md)
* [Zrozumienie wypłaty raportowaniem](marketplace-publishing-report-payout.md)
* [Uzyskaj pomoc techniczną jako wydawca](marketplace-publishing-get-publisher-support.md)

## <a name="additional-resources"></a>Dodatkowe zasoby
[Konfigurowanie programu Azure PowerShell](marketplace-publishing-powershell-setup.md)
