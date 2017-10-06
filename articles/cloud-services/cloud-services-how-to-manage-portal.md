---
title: "zadania zarządzania usługi chmury aaaCommon | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usług w chmurze toomanage w hello portalu Azure. Poniższe przykłady użycia hello portalu Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a>W jaki sposób tooManage usług w chmurze
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](cloud-services-how-to-manage-portal.md)
> * [Klasyczna witryna Azure Portal](cloud-services-how-to-manage.md)
>
>

W hello **usługi w chmurze (klasyczne)** obszaru hello Azure portalu, można zaktualizować roli usługi lub wdrożenie, podwyższyć poziom tooproduction wdrożenia etapowego, Połącz usługi w chmurze tooyour zasobów widać hello zasobów zależności skali razem hello zasobów i usunąć usługi w chmurze lub wdrożenia.

Więcej informacji na temat sposobu tooscale usługi w chmurze jest dostępna [tutaj](cloud-services-how-to-scale-portal.md).

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Porady: aktualizowanie roli usługi w chmurze lub wdrożenia
Jeśli potrzebujesz kodu aplikacji hello tooupdate dla usługi w chmurze użyj **aktualizacji** na powitania chmury usługi bloku. Można aktualizować jedną rolę lub wszystkich ról. tooupdate, możesz przekazać pakiet usługi lub pliku konfiguracji usługi.

1. W hello [portalu Azure][Azure portal], wybierz usługę w chmurze hello ma tooupdate. Ten krok powoduje otwarcie bloku wystąpienia usługi chmury hello.
2. W bloku powitania kliknij hello **aktualizacji** przycisku.

    ![Przycisk Aktualizuj](./media/cloud-services-how-to-manage-portal/update-button.png)

3. Zaktualizuj hello wdrożenia przy użyciu nowego pliku pakietu usługi (cspkg) i pliku konfiguracji usługi (cscfg).

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. **Opcjonalnie** hello etykieta wdrożenia i konto magazynu hello aktualizacji.
5. W przypadku ról tylko jedno wystąpienie roli, należy wybrać hello **Wdróż, nawet jeśli co najmniej jedna rola zawiera pojedyncze wystąpienie** tooenable hello uaktualnienia tooproceed.

    Każda rola ma co najmniej dwa wystąpienia roli (maszyny wirtualne) Azure tylko można gwarantuje dostępność usługi 99,95% podczas aktualizacji usługi chmury. Dwa wystąpienia roli jednej maszyny wirtualnej przetwarza żądania klientów podczas aktualizowania jest hello innych.

6. Sprawdź **rozpocząć wdrażanie** aktualizacji hello toohave stosowane po zakończeniu przekazywania hello hello pakietu.
7. Kliknij przycisk **OK** toobegin aktualizacji hello usługi.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Porady: Zamień toopromote wdrożeń tooproduction wdrożenia etapowego
Po zdecydować toodeploy nową wersję usługi w chmurze, etap i przetestować w środowisku przemieszczania usługi chmury z nową wersją. Użyj **wymiany** adresy URL hello tooswitch przez które hello dwa wdrożenia są opisane i promowania nowego tooproduction wersji.

Można wymienić wdrożenia od hello **usługi w chmurze** strony lub hello pulpitu nawigacyjnego.

1. W hello [portalu Azure][Azure portal], wybierz usługę w chmurze hello ma tooupdate. Ten krok powoduje otwarcie bloku wystąpienia usługi chmury hello.
2. W bloku powitania kliknij hello **wymiany** przycisku.

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. Witaj następujące monit o potwierdzenie zostanie otwarty.

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. Po sprawdzeniu informacji o wdrożeniu powitania kliknij **OK** tooswap hello wdrożeń.

    wymiany wdrożenia Hello odbywa się szybko ponieważ hello jedynym elementem, który zmienia hello wirtualnych adresów IP (VIP) w przypadku wdrożeń hello.

    toosave obliczeń kosztów, możesz usunąć hello przemieszczania wdrożenia po sprawdzeniu, czy wdrożenia produkcyjnego działa zgodnie z oczekiwaniami.

### <a name="common-questions-about-swapping-deployments"></a>Często zadawane pytania dotyczące wymiany wdrożenia

**Jakie są wymagania wstępne hello na wymiany wdrożenia?**

Istnieją dwa kluczowe wymagania wstępne dotyczące wymiany pomyślne wdrożenie:

- Jeśli chcesz toouse statycznego adresu IP dla Twojego miejsca produkcji, musi zarezerwować jeden dla miejsca przemieszczania również. W przeciwnym razie wymiany hello kończy się niepowodzeniem.

- Wszystkie wystąpienia ról musi być uruchomiona, zanim będzie można wykonać hello wymiany. Możliwość sprawdzenia stanu hello swoich wystąpień, w bloku omówienie hello hello portalu Azure. Alternatywnie można użyć hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) polecenia w programie Windows PowerShell.

Aktualizacje systemu operacyjnego gościa i naprawianie operacji usługi może również spowodować wdrożenia zamienia toofail. Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z wdrażaniem usługi chmury](cloud-services-troubleshoot-deployment-problems.md).

**Zamiana wpływa negatywnie przestojów w przypadku mojej aplikacji? Jak należy ją obsługuje?**

Zgodnie z opisem w ostatniej sekcji hello, wymiany wdrożenia jest zazwyczaj szybkie, ponieważ jest on tylko zmiany konfiguracji usługi równoważenia obciążenia Azure hello. W niektórych przypadkach jednak może potrwać co najmniej 10 sekund i powodować błędy połączeń przejściowej. toolimit wpływ tooyour klientów, rozważ zaimplementowanie [Logika ponawiania klienta](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Porady: łączenie usługi w chmurze tooa zasobów
Witaj portalu Azure nie łączy zasobów ze sobą, jak jest hello bieżącego klasycznego portalu Azure. Zamiast tego należy wdrożyć dodatkowe zasoby toohello tej samej grupie zasobów używanych przez hello usługi w chmurze.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Porady: usuwanie wdrożeń i usługi w chmurze
Aby można było usunąć usługi w chmurze, należy usunąć poszczególnych istniejącego wdrożenia.

toosave obliczeń kosztów, możesz usunąć hello przemieszczania wdrożenia po sprawdzeniu, czy wdrożenia produkcyjnego działa zgodnie z oczekiwaniami. Rozliczenie jest kosztów obliczeniowe dla wystąpień roli wdrożone, które zostały zatrzymane.

Za pomocą następującej procedury toodelete hello wdrożenia lub usługi w chmurze.

1. W hello [portalu Azure][Azure portal], wybierz usługę w chmurze hello ma toodelete. Ten krok powoduje otwarcie bloku wystąpienia usługi chmury hello.
2. W bloku powitania kliknij hello **usunąć** przycisku.

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. Można usunąć usługi w chmurze całego hello sprawdzając **Cloud service i jej wdrożenia** lub wybierz albo hello **wdrożenia produkcyjnego** lub hello **przemieszczania — wdrażanie**.

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. Kliknij przycisk hello **usunąć** u dołu hello.
5. usługi w chmurze hello toodelete kliknij **usługi w chmurze Delete**. Następnie na powitania monit o potwierdzenie, kliknij przycisk **tak**.

> [!NOTE]
> Po usunięciu usługi w chmurze, skonfigurowano pełnego monitorowania, należy usunąć dane hello ręcznie z konta magazynu. Informacje o którym toofind hello metryki tabel, zobacz [to](cloud-services-how-to-monitor.md) artykułu.


## <a name="how-to-find-more-information-about-failed-deployments"></a>Porady: więcej informacji o wdrożeniach nie powiodło się
Witaj **omówienie** bloku ma pasek stanu u góry hello. Po kliknięciu przycisku paska hello nowy blok otwiera i wyświetla informacje o błędzie. Jeśli wdrożenie hello nie zawiera żadnych błędów, blok informacji hello jest pusta.

![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a>Następne kroki
* [Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure-portal.md).
* Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy-portal.md).
* Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name-portal.md).
* Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate-portal.md).
