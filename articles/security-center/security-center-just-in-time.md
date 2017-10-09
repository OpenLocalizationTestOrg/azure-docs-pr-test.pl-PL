---
title: "dostęp aaaJust w czasie maszyny wirtualnej w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przeprowadzi Cię przez kolejne jak tylko w czasie dostępu do maszyny Wirtualnej w Centrum zabezpieczeń Azure ułatwia sterowanie dostępu tooyour Azure maszyn wirtualnych."
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
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a>Zarządzanie dostępem do maszyny wirtualnej przy użyciu tylko w czasie

Tylko w czasie maszyny wirtualnej (VM) dostępu może być używane toolock dół tooyour ruch przychodzący maszynach wirtualnych platformy Azure, zmniejszenie zagrożeń tooattacks zapewniając łatwy dostęp tooconnect tooVMs w razie potrzeby.

> [!NOTE]
> Witaj tylko w funkcji czasu jest w wersji zapoznawczej i jest dostępny na powitania warstwy standardowa, Centrum zabezpieczeń.  Zobacz [cennik](security-center-pricing.md) toolearn więcej informacji na temat Centrum zabezpieczeń firmy warstw cenowych.
>
>

## <a name="attack-scenario"></a>Atak

Atak siłowy ataków często porty docelowe zarządzania jako oznacza tooa dostępu toogain maszyny Wirtualnej. Jeśli to się powiedzie, osoba atakująca może przejąć kontrolę nad hello maszyny Wirtualnej i nawiązywać stopień do środowiska.

Ataków siłowych tooa narażenia jednokierunkowej tooreduce jest toolimit hello ilość czasu, który port jest otwarty. Porty zarządzania czy nie potrzeba toobe otwarte przez cały czas. Potrzebna jest tylko toobe otwarte podczas połączonych toohello maszyny Wirtualnej, na przykład tooperform są zadania zarządzania i konserwacji. Gdy tylko w czasie jest włączona, Centrum zabezpieczeń używa [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) reguły (NSG), które ograniczają porty toomanagement dostępu, więc nie może być wskazywane przez osoby atakujące.

![Tylko w scenariuszu czasu][1]

## <a name="how-does-just-in-time-access-work"></a>Jak tylko w czasie pracy?

Gdy tylko w czasie jest włączona, Centrum zabezpieczeń blokuje ruch przychodzący tooyour maszynach wirtualnych platformy Azure przez tworzenie reguły NSG. Wybierz porty hello na powitania toowhich maszyny Wirtualnej zostanie zablokowana ruchu przychodzącego. Te porty są kontrolowane przez hello tylko w rozwiązaniu czasu.

Gdy użytkownik zażąda dostępu tooa maszyny Wirtualnej, Centrum zabezpieczeń sprawdza użytkownika hello [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md) uprawnienia, które zapewniają dostęp do zapisu dla hello zasobów platformy Azure. Jeśli mają one uprawnienia do zapisu, hello żądanie zostanie zatwierdzone i Centrum zabezpieczeń automatycznie konfiguruje hello tooallow grup zabezpieczeń sieci (NSG) ruchu przychodzącego ruchu toohello zarządzania porty hello ilość czasu, można określić. Po upływie czasu hello, Centrum zabezpieczeń przywraca hello grup NSG tootheir poprzedniego stanu.

> [!NOTE]
> Centrum zabezpieczeń na wszelki dostęp do maszyny Wirtualnej czasu aktualnie obsługuje tylko maszyn wirtualnych wdrożonych za pośrednictwem usługi Azure Resource Manager. toolearn więcej informacji o hello klasycznego i modeli wdrażania usługi Resource Manager zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne](../azure-resource-manager/resource-manager-deployment-model.md).
>
>

## <a name="using-just-in-time-access"></a>Przy użyciu tylko w czasie

Witaj **bezpośrednio w dostęp maszyny Wirtualnej** Kafelek na powitania **Centrum zabezpieczeń** bloku pokazuje hello liczbę maszyn wirtualnych skonfigurowanych dla tylko w czasie dostępu i hello liczby żądań zatwierdzonych dostępu wprowadzone w hello ostatniego tygodnia.

Wybierz hello **bezpośrednio w dostęp maszyny Wirtualnej** Kafelek i hello **bezpośrednio w dostęp maszyny Wirtualnej** zostanie otwarty blok.

![Tylko w czasie dostępu do maszyny Wirtualnej kafelka][2]

Witaj **bezpośrednio w dostęp do maszyny Wirtualnej czasu** blok zawiera informacje dotyczące stanu hello maszyn wirtualnych:

- **Skonfigurowane** -maszyn wirtualnych, które zostały skonfigurowane toosupport na wszelki dostęp maszyny Wirtualnej. dane Hello podane dotyczy hello w ostatnim tygodniu i zawiera dla każdej maszyny Wirtualnej hello liczby żądań zatwierdzonych, Data ostatniego dostępu i czas i użytkownika, który ostatnio.
- **Zalecane** -maszyn wirtualnych, które obsługują tylko w dostęp maszyny Wirtualnej, ale nie został skonfigurowany do. Zaleca się włączenie tylko w kontroli dostępu wirtualna czasu dla tych maszyn wirtualnych. Zobacz [włączyć tylko w przypadku maszyn wirtualnych dostęp](#enable-just-in-time-vm-access).
- **Brak rekomendacji** -przyczyn, które mogą spowodować maszyny Wirtualnej nie toobe zalecane są:
  - Brak grupy NSG - hello tylko w rozwiązaniu czasu wymaga toobe NSG w miejscu.
  - Klasycznym VM - Centrum zabezpieczeń na wszelki dostęp do maszyny Wirtualnej czasu aktualnie obsługuje tylko maszyn wirtualnych wdrożonych za pośrednictwem usługi Azure Resource Manager. Wdrożenie klasyczne nie jest obsługiwany przez hello tylko w rozwiązaniu czasu.
  - Inne - maszyny Wirtualnej jest w tej kategorii, jeśli hello tylko w czasie, które rozwiązanie jest wyłączona w zasadach zabezpieczeń hello hello subskrypcji lub grupy zasobów hello lub że hello maszyny Wirtualnej nie ma publicznego adresu IP i nie ma grupy NSG w miejscu.

## <a name="configuring-a-just-in-time-access-policy"></a>Konfigurowanie tylko w czasie zasad dostępu

Witaj tooselect maszyn wirtualnych, które mają tooenable:

1. Na powitania **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz hello **zalecane** kartę.

  ![Włącz tylko w czasie][3]

2. W obszarze **maszyn wirtualnych**, wybierz hello maszyn wirtualnych, które mają tooenable. Spowoduje to umieszczenie znacznikiem wyboru tooa dalej maszyny Wirtualnej.
3. Wybierz **włączyć JIT na maszynach wirtualnych**.
4. Wybierz pozycję **Zapisz**.

### <a name="default-ports"></a>Porty domyślne

Widać hello domyślnych portów, które Centrum zabezpieczeń zaleca włączenie tylko w czasie.

1. Na powitania **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz hello **zalecane** kartę.

  ![Wyświetlanie domyślnych portów][6]

2. W obszarze **maszyn wirtualnych**, wybierz maszynę Wirtualną. Spowoduje to umieszczenie znacznikiem wyboru dalej toohello maszyny Wirtualnej i otwiera hello **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku. Ten blok Wyświetla hello domyślnych portów.

### <a name="add-ports"></a>Dodawanie portów

Z hello **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku można również dodać i skonfigurować nowy port, na którym ma zostać hello tooenable tylko w rozwiązaniu czasu.

1. Na powitania **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku, wybierz opcję **Dodaj**. Spowoduje to otwarcie hello **konfiguracji portów Dodaj** bloku.

  ![Konfiguracja portów][7]

2. Na **konfiguracji portów Dodaj** bloku, należy określić port hello typ protokołu dozwolone źródła adresów IP i maksymalny czas żądania.

  Dozwolone źródła adresy IP są dostęp tooget dozwolonych zakresy IP hello na żądanie zatwierdzone.

  Czas żądania maksymalna jest hello maksymalny przedział czasu można otworzyć określonego portu.

3. Kliknij przycisk **OK**.

## <a name="requesting-access-tooa-vm"></a>Żąda dostępu tooa maszyny Wirtualnej

toorequest tooa dostęp do maszyny Wirtualnej:

1. Na powitania **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz hello **skonfigurowana** kartę.
2. W obszarze **maszyn wirtualnych**, wybierz hello maszyn wirtualnych, które mają tooenable dostępu. Spowoduje to umieszczenie znacznikiem wyboru tooa dalej maszyny Wirtualnej.
3. Wybierz **poprosić o dostęp**. Spowoduje to otwarcie hello **poprosić o dostęp** bloku.

  ![Żądanie dostępu tooa maszyny Wirtualnej][4]

4. Na powitania **poprosić o dostęp** bloku, należy skonfigurować dla każdej maszyny Wirtualnej hello porty tooopen wraz z źródłowy adres IP hello, który hello port jest otwarte okno czasu hello tooand dla których hello port jest otwarty. Możesz poprosić o dostęp tylko toohello porty, które zostały skonfigurowane w hello tylko w czasie zasad. Każdy port ma maksymalny czas dozwolonych pochodną hello tylko w czasie zasad.
5. Wybierz **otworzyć porty**.

## <a name="editing-a-just-in-time-access-policy"></a>Edytowanie tylko w czasie zasad dostępu

Można zmienić dla maszyny Wirtualnej istniejące tylko w czasie zasad przez dodanie i skonfigurowanie nowego tooopen port dla tej maszyny Wirtualnej lub zmieniając innych parametrów powiązanych tooan już chroniona portu.

W celu tooedit istniejące tylko w zasadach czasu maszyny wirtualnej, hello **skonfigurowana** karta jest używana:

1. W obszarze **maszyn wirtualnych**, wybierz tooadd wirtualna tooby portu, klikając hello trzy kropki w obrębie hello wiersza dla tej maszyny Wirtualnej. Spowoduje to otwarcie menu.
2. Wybierz **Edytuj** hello menu. Spowoduje to otwarcie hello **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku.

  ![Edytowanie zasad][8]

3. Na powitania **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku, albo można edytować istniejące ustawienia hello port już chronione, klikając jej portu lub wybrać **Dodaj**. Spowoduje to otwarcie hello **konfiguracji portów Dodaj** bloku.

  ![Dodaj port][7]

4. Na **konfiguracji portów Dodaj** bloku zidentyfikować hello portu, typ protokołu źródła dozwolonych adresów IP i czas maksymalny żądania.
5. Kliknij przycisk **OK**.
6. Wybierz pozycję **Zapisz**.

## <a name="auditing-just-in-time-access-activity"></a>Inspekcja tylko w czasie działania dostępu

Aby uzyskać wgląd w działania maszyny Wirtualnej przy użyciu wyszukiwania dziennika. Dzienniki tooview:

1. Na powitania **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz hello **skonfigurowana** kartę.
2. W obszarze **maszyn wirtualnych**, wybierz informacji tooview maszyny Wirtualnej o klikając hello trzy kropki w obrębie hello wiersza dla tej maszyny Wirtualnej. Spowoduje to otwarcie menu.
3. Wybierz **dziennik aktywności** hello menu. Spowoduje to otwarcie hello **dziennik aktywności** bloku.

![Wybierz dziennik aktywności][9]

Witaj **dziennik aktywności** bloku udostępnia widok filtrowany poprzednich operacji dla tej maszyny Wirtualnej oraz czas, datę i subskrypcji.

![Wyświetl dziennik aktywności][5]

Można pobrać informacji dziennika hello wybierając **kliknij tutaj toodownload wszystkie elementy hello CSV jako**.

Zmodyfikuj hello filtry i wybrać **Zastosuj** toocreate wyszukiwania i dziennika.

## <a name="using-just-in-time-vm-access-via-powershell"></a>Przy użyciu tylko w czasie dostępu do maszyny Wirtualnej za pomocą programu PowerShell

Upewnij się, masz hello w kolejności hello toouse tylko w rozwiązaniu czasu za pomocą programu PowerShell, [najnowsze](/powershell/azure/install-azurerm-ps) wersji programu Azure PowerShell.
Po wykonaniu czynności należy tooinstall hello [najnowsze](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Centrum zabezpieczeń Azure z galerii programu PowerShell hello.

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a>Konfigurowanie tylko w zasadach czasu dla maszyny Wirtualnej

tooconfigure tylko w zasadach czasu w odpowiedniej maszyny Wirtualnej, należy toorun tego polecenia w sesji programu PowerShell: ASCJITAccessPolicy zestawu.
Wykonaj toolearn dokumentacji polecenia cmdlet hello więcej.

### <a name="requesting-access-tooa-vm"></a>Żąda dostępu tooa maszyny Wirtualnej

Witaj tooaccess określonej maszyny Wirtualnej, który jest chroniony za pomocą tylko w rozwiązaniu do czasu, należy toorun tego polecenia w sesji programu PowerShell: ASCJITAccess wywołania.
Wykonaj toolearn dokumentacji polecenia cmdlet hello więcej.

## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono sposób tylko w czasie dostępu do maszyny Wirtualnej w Centrum zabezpieczeń ułatwia kontroli dostępu tooyour Azure maszyn wirtualnych.

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

- [Ustawianie zasad zabezpieczeń](security-center-policies.md) — Dowiedz się jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
- [Zarządzanie zaleceniami dotyczącymi zabezpieczeń](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
- [Monitorowanie kondycji zabezpieczeń](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
- [Reagowanie na alerty toosecurity i zarządzanie nimi](security-center-managing-and-responding-alerts.md) — Dowiedz się jak alerty toosecurity toomanage i odpowiada.
- [Monitorowanie rozwiązań partnerskich](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
- [Często zadawane pytania dotyczące Centrum zabezpieczeń](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
- [Blog Azure Security](https://blogs.msdn.microsoft.com/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
