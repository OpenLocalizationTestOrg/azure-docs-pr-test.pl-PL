---
title: "zadania zarządzania usługi chmury aaaCommon (klasyczne) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usług w chmurze toomanage w hello klasycznego portalu Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 03b1d632f1480d0f65c87b7f8ffc747417acf7b5
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

W hello **usługi w chmurze** obszaru hello Azure w klasycznym portalu, można zaktualizować roli usługi lub wdrożenie, podwyższyć poziom tooproduction wdrożenia etapowego, Połącz usługi w chmurze tooyour zasobów widać hello zasobów zależności skali razem hello zasobów i usunąć usługi w chmurze lub wdrożenia.

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Porady: aktualizowanie roli usługi w chmurze lub wdrożenia
Jeśli potrzebujesz kodu aplikacji hello tooupdate dla usługi w chmurze użyj **aktualizacji** na pulpicie nawigacyjnym hello, **usługi w chmurze** strony, lub **wystąpień** strony. Można aktualizować jedną rolę lub wszystkich ról. Będziesz potrzebować tooupload nowy pakiet usługi i pliku konfiguracji usługi.

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), na pulpicie nawigacyjnym hello, **usługi w chmurze** strony, lub **wystąpień** kliknij przycisk **aktualizacji**.

    ![UpdateDeployment](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. W **etykieta wdrożenia**, wprowadź nazwę wdrożenia hello tooidentify (na przykład mycloudservice4). Można znaleźć hello etykieta wdrożenia w obszarze **szybki start** na powitania pulpitu nawigacyjnego.
3. W **pakietu**, użyj **Przeglądaj** tooupload hello plik pakietu usług (cspkg).
4. W **konfiguracji**, użyj **Przeglądaj** tooupload hello pliku konfiguracji usługi (cscfg).
5. W **roli**, wybierz pozycję **wszystkie** Chcąc tooupgrade wszystkich ról w hello usługi chmury. tooperform aktualizacji jedną rolę, wybierz hello roli ma tooupdate. Nawet w przypadku wybrania tooupdate określoną rolę, aktualizacje hello w pliku konfiguracji usługi hello są zastosowane tooall ról.
6. Jeśli zmiany w aktualizacji hello hello liczby ról lub rozmiar hello żadnych ról, wybierz hello **zezwolić na aktualizacje w przypadku zmiany rozmiarów ról lub liczby ról** tooproceed aktualizacji hello tooenable pole wyboru.

    Należy pamiętać, że zmiana rozmiaru hello roli (oznacza to, że hello rozmiar maszyny wirtualnej, który jest hostem wystąpienia roli) lub hello liczby ról, każde wystąpienie roli (maszyny wirtualnej) muszą być ponownym utworzeniu obrazu i wszystkie lokalne dane zostaną utracone.

7. W przypadku ról usługi tylko jedno wystąpienie roli, należy wybrać hello **aktualizacji, nawet jeśli co najmniej jeden Rola zawiera pojedyncze wystąpienie pola wyboru** tooenable hello uaktualnienia tooproceed.

    Każda rola ma co najmniej dwa wystąpienia roli (maszyny wirtualne) Azure tylko można gwarantuje dostępność usługi 99,95% podczas aktualizacji usługi chmury. Umożliwiająca jednego żądania klientów tooprocess maszyny wirtualnej podczas aktualizowania hello innych.

8. Kliknij przycisk **OK** aktualizacji usługi hello toobegin (znacznikiem wyboru).

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Porady: Zamień toopromote wdrożeń tooproduction wdrożenia etapowego
Użyj **wymiany** toopromote przemieszczania wdrożenie tooproduction usługi chmury. W przypadku podjęcia decyzji toodeploy nową wersję usługi w chmurze, można przemieścić i przetestować z nową wersją w środowisku przemieszczania usługi chmury, gdy klienci korzystają z bieżącej wersji hello w środowisku produkcyjnym. Jeśli wszystko jest gotowe toopromote hello nowej wersji tooproduction, możesz użyć **wymiany** adresy URL hello tooswitch przez hello, które zostały rozwiązane dwa wdrożenia.

Można wymienić wdrożenia od hello **usługi w chmurze** strony lub hello pulpitu nawigacyjnego.

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**.
2. Na liście hello usługi w chmurze, kliknij przycisk tooselect usługi chmury hello go.
3. Kliknij przycisk **wymiany**.

    Witaj następujące monit o potwierdzenie zostanie otwarty.

    ![Wymiany usługi w chmurze](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. Po sprawdzeniu informacji o wdrożeniu powitania kliknij **tak** tooswap hello wdrożeń.

    wymiany wdrożenia Hello odbywa się szybko ponieważ hello jedynym elementem, który zmienia hello wirtualnych adresów IP (VIP) w przypadku wdrożeń hello.

    toosave obliczeń kosztów, można usunąć wdrożenia hello w hello przemieszczania środowiska po upewnieniu się, że nowe wdrożenia produkcyjnego hello działa zgodnie z oczekiwaniami.

### <a name="common-questions-about-swapping-deployments"></a>Często zadawane pytania dotyczące wymiany wdrożenia

**Jakie są wymagania wstępne hello na wymiany wdrożenia?**

Istnieją dwa kluczowe wymagania wstępne dotyczące wymiany pomyślne wdrożenie:

- Jeśli chcesz toouse statycznego adresu IP dla Twojego miejsca produkcji, musi zarezerwować jeden dla miejsca przemieszczania również. W przeciwnym razie wymiany hello zakończy się niepowodzeniem.

- Wszystkie wystąpienia ról musi być uruchomiona, zanim będzie można wykonać hello wymiany. Możliwość sprawdzenia stanu hello swoich wystąpień w hello klasycznego portalu Azure lub za pomocą [hello polecenia Get-AzureRole w programie Windows PowerShell](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0).

Należy pamiętać, że aktualizacje systemu operacyjnego gościa i naprawianie operacji usługi powodują toofail zamiany wdrożenia. Zobacz [Rozwiązywanie problemów z wdrażaniem usługi chmury](cloud-services-troubleshoot-deployment-problems.md) więcej szczegółów.

**Zamiana wpływa negatywnie przestojów w przypadku mojej aplikacji? Jak należy ją obsługuje?**

Zgodnie z opisem w ostatniej sekcji hello, wymiany wdrożenia zwykle jest bardzo szybko, ponieważ jest on tylko zmiany konfiguracji usługi równoważenia obciążenia Azure hello. W niektórych przypadkach jednak może potrwać co najmniej 10 sekund i powodować błędy połączeń przejściowej. toolimit wpływ tooyour klientów, rozważ zaimplementowanie [Logika ponawiania klienta](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Porady: łączenie usługi w chmurze tooa zasobów
tooshow usługi w chmurze w zależności od innych zasobów, można połączyć wystąpienia bazy danych SQL Azure lub usługi w chmurze toohello konta magazynu. Możesz połączyć i odłączyć zasobów na powitania **połączonych zasobów** strony, a następnie monitorować ich użycia na pulpicie nawigacyjnym usługi chmury hello. Jeśli monitorowanie włączona połączonym koncie magazynu, można monitorować całkowita liczba żądań na pulpicie nawigacyjnym usługi chmury hello.

Użyj **łącze** toolink nowej lub istniejącej bazy danych SQL wystąpienia lub magazynu konta tooyour usługi w chmurze. Następnie można skalować bazy danych hello wraz z rolą usługi chmury hello, który jest używany na powitania **skali** strony. (Konto magazynu skaluje automatycznie wraz ze wzrostem użycia.) Aby uzyskać więcej informacji, zobacz [jak tooScale usługa w chmurze i połączonych zasobów](cloud-services-how-to-scale.md).

Możesz również można monitorować, zarządzanie i skalowania bazy danych hello w hello **baz danych** węzła hello klasycznego portalu Azure.

"Łączenie" zasób w tym sensie nie połączyć zasobu toohello aplikacji. W przypadku utworzenia nowej bazy za pomocą **łącze**, potrzebujesz kodu aplikacji tooyour ciągów połączenia tooadd hello i następnie uaktualnić hello usługi w chmurze. Należy również parametry połączenia tooadd Jeśli aplikacja korzysta z zasobów w połączonym koncie magazynu.

Hello procedury opisano, jak toolink nowe wystąpienie bazy danych SQL wdrożona na nowym serwerze bazy danych SQL, tooa usługi w chmurze.

### <a name="toolink-a-sql-database-instance-tooa-cloud-service"></a>toolink usługi w chmurze tooa wystąpienia bazy danych SQL
1. W hello [klasycznego portalu Azure](http://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**. Następnie kliknij nazwę hello pulpit nawigacyjny hello tooopen hello chmury usługi.
2. Kliknij przycisk **połączone zasobów**.

    Witaj **połączonych zasobów** zostanie otwarta strona.

    ![LinkedResourcesPage](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. Kliknij opcję **Połącz zasób** lub **łącze**.

    Witaj **zasób konsolidacji** zostanie uruchomiony Kreator.

    ![Strona łącze 1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. Kliknij przycisk **utworzyć nowy zasób** lub **Połącz istniejący zasób**.
5. Wybierz typ hello toolink zasobów. W hello [klasycznego portalu Azure](http://manage.windowsazure.com/), kliknij przycisk **bazy danych SQL**. (Tylko hello klasyczny portal Azure obsługuje łączenie z usługą w chmurze tooa konta magazynu).
6. toocomplete hello bazy danych konfiguracji, wykonaj instrukcje w pomocy dla hello **baz danych SQL** obszaru hello klasycznego portalu Azure.

    Możesz wykonać hello postęp hello operację w obszarze wiadomość hello połączenia.

    Po zakończeniu łączenia można monitorować stan hello hello połączonego zasobu na pulpicie nawigacyjnym usługi chmury hello. Aby uzyskać informacji na temat skalowania połączonej bazy danych SQL, zobacz [jak tooScale usługa w chmurze i połączonych zasobów](cloud-services-how-to-scale.md).

### <a name="toounlink-a-linked-resource"></a>toounlink zasobu połączonego
1. W hello [klasycznego portalu Azure](http://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**. Następnie kliknij nazwę hello pulpit nawigacyjny hello tooopen hello chmury usługi.
2. Kliknij przycisk **połączonych zasobów**, a następnie wybierz hello zasobów.
3. Kliknij przycisk **odłączyć**. Następnie kliknij przycisk **tak** na powitania monit o potwierdzenie.

    Odłączanie bazy danych SQL nie ma wpływu na powitania lub bazy danych aplikacji hello połączeń toohello. Można nadal zarządzać bazy danych hello w hello **baz danych SQL** obszaru hello klasycznego portalu Azure.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Porady: usuwanie wdrożeń i usługi w chmurze
Aby można było usunąć usługi w chmurze, należy usunąć poszczególnych istniejącego wdrożenia.

toosave obliczeń kosztów, można usunąć wdrożenia przemieszczania po sprawdzeniu, czy wdrożenia produkcyjnego działa zgodnie z oczekiwaniami. Jesteś kosztów rachunku obliczeniowe dla wystąpień roli, nawet jeśli nie jest uruchomiona usługa w chmurze.

Za pomocą następującej procedury toodelete hello wdrożenia lub usługi w chmurze.

1. W hello [klasycznego portalu Azure](http://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**.
2. Wybierz usługę w chmurze hello, a następnie kliknij przycisk **usunąć**. (tooselect usługi w chmurze bez konieczności otwierania hello pulpitu nawigacyjnego, kliknij w dowolnym z wyjątkiem nazwy hello we wpisie usługi chmury hello.)

    W przypadku wdrożenia w tymczasowym czy produkcyjnym, zobaczysz menu opcji toohello podobne po jednym u dołu okna hello hello. Aby można było usunąć usługi w chmurze hello, musisz usunąć wszystkie istniejące wdrożenia.

    ![Usuń Menu](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. toodelete wdrożenia, kliknij przycisk **usunąć wdrożenia produkcyjnego** lub **usunąć wdrożenie przemieszczania**. Następnie na powitania monit o potwierdzenie, kliknij przycisk **tak**.
4. Jeśli planujesz usługi w chmurze hello toodelete, powtórz krok 3, w razie potrzeby toodelete inne wdrożenia.
5. usługi w chmurze hello toodelete kliknij **usługi w chmurze Delete**. Następnie na powitania monit o potwierdzenie, kliknij przycisk **tak**.

> [!NOTE]
> Pełne monitorowania jest skonfigurowany dla usługi w chmurze, platformy Azure nie powoduje usunięcia hello dane monitorowania z konta magazynu podczas usuwania usługi w chmurze hello. Konieczne będzie toodelete hello danych ręcznie. Informacje, których toofind hello metryki tabel, zobacz "porady: dostęp do pełnych danych monitorowania poza hello klasycznego portalu Azure" w [jak tooMonitor usług w chmurze](cloud-services-how-to-monitor.md).
>
>

## <a name="next-steps"></a>Następne kroki
* [Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure.md).
* Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy.md).
* Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name.md).
* Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate.md).
