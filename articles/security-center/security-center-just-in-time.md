---
title: "Tylko w maszynie wirtualnej czas dostępu w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten przeszukiwań dokumentu dostęp odbywa się za pośrednictwem jak tylko w czasie maszyny Wirtualnej w Centrum zabezpieczeń Azure ułatwia można kontrolować dostęp do maszynach wirtualnych platformy Azure."
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
ms.openlocfilehash: 5bb87488dcfc79ed4baa1dbd81dc4e1174f84e4b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a>Zarządzanie dostępem do maszyny wirtualnej przy użyciu tylko w czasie

Tylko w czasie maszyny wirtualnej (VM) dostępu może służyć do blokowania ruchu przychodzącego na maszynach wirtualnych platformy Azure, ograniczenia narażenia na ataki, zapewniając łatwy dostęp do nawiązania połączenia maszyn wirtualnych w razie potrzeby.

> [!NOTE]
> Tylko w czasie jest funkcja w wersji zapoznawczej i dostępne w warstwie standardowa Centrum zabezpieczeń.  Zobacz [cennik](security-center-pricing.md) Aby dowiedzieć się więcej na temat Centrum zabezpieczeń firmy ceny warstw.
>
>

## <a name="attack-scenario"></a>Atak

Atak siłowy ataków często porty docelowe zarządzania w celu uzyskania dostępu do maszyny Wirtualnej. Jeśli to się powiedzie, osoba atakująca może przejąć kontrolę nad maszyny Wirtualnej i nawiązywać stopień do środowiska.

Jednym ze sposobów zmniejszyć ryzyko ataków siłowych jest ograniczyć czas, który port jest otwarty. Porty zarządzania nie muszą być otwarte przez cały czas. Tylko muszą być otwarte, gdy są połączone z maszyną wirtualną, na przykład w celu wykonywania zadań zarządzania i konserwacji. Gdy tylko w czasie jest włączona, Centrum zabezpieczeń używa [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) reguły (NSG), które ograniczanie dostępu do portów zarządzania, więc nie może być wskazywane przez osoby atakujące.

![Tylko w scenariuszu czasu][1]

## <a name="how-does-just-in-time-access-work"></a>Jak tylko w czasie pracy?

Gdy zostanie włączona funkcja „dokładnie na czas”, usługa Security Center zablokuje ruch przychodzący do maszyn wirtualnych platformy Azure poprzez utworzenie reguły sieciowej grupy zabezpieczeń. Należy wybrać porty na maszynie Wirtualnej, do którego będzie można zablokować ruch przychodzący. Te porty są kontrolowane przez tylko w rozwiązaniu czasu.

Gdy użytkownik żąda dostępu do maszyny Wirtualnej, Centrum zabezpieczeń sprawdza, czy użytkownik ma [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md) uprawnienia, które zapewniają dostęp do zapisu dla zasobów platformy Azure. Jeśli mają one uprawnienia do zapisu, żądanie zostanie zatwierdzone i Centrum zabezpieczeń automatycznie konfiguruje grup zabezpieczeń sieci (NSG) zezwalająca na ruch przychodzący do portów zarządzania przez czas określony. Po upływie czasu Centrum zabezpieczeń przywraca grup NSG do poprzedniego stanu.

> [!NOTE]
> Centrum zabezpieczeń na wszelki dostęp do maszyny Wirtualnej czasu aktualnie obsługuje tylko maszyn wirtualnych wdrożonych za pośrednictwem usługi Azure Resource Manager. Aby dowiedzieć się więcej o klasycznego i modeli wdrażania usługi Resource Manager, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne](../azure-resource-manager/resource-manager-deployment-model.md).
>
>

## <a name="using-just-in-time-access"></a>Przy użyciu tylko w czasie

**Bezpośrednio w dostęp do maszyny Wirtualnej czasu** Kafelek na **Centrum zabezpieczeń** bloku pokazuje liczbę maszyn wirtualnych skonfigurowany dla dokładnie na czas dostępu i liczba żądań zatwierdzonych dostępu wykonanych w ostatnim tygodniu.

Wybierz **bezpośrednio w dostęp do maszyny Wirtualnej czasu** Kafelek i **bezpośrednio w dostęp maszyny Wirtualnej** zostanie otwarty blok.

![Tylko w czasie dostępu do maszyny Wirtualnej kafelka][2]

**Bezpośrednio w dostęp do maszyny Wirtualnej czasu** blok zawiera informacje o stanie maszyn wirtualnych:

- **Skonfigurowane** -maszyn wirtualnych, które zostały skonfigurowane do obsługi tylko w dostęp maszyny Wirtualnej. Dane prezentowane jest ostatniego tygodnia i zawiera dla każdej maszyny Wirtualnej liczbę żądań zatwierdzonych, Data ostatniego dostępu i czas i użytkownika, który ostatnio.
- **Zalecane** -maszyn wirtualnych, które obsługują tylko w dostęp maszyny Wirtualnej, ale nie został skonfigurowany do. Zaleca się włączenie tylko w kontroli dostępu wirtualna czasu dla tych maszyn wirtualnych. Zobacz [włączyć tylko w przypadku maszyn wirtualnych dostęp](#enable-just-in-time-vm-access).
- **Brak rekomendacji** -przyczyny, które mogą spowodować maszyny Wirtualnej, aby nie zaleca się to:
  - Brak grupy NSG — tylko w czasie rozwiązanie wymaga grupy NSG w miejscu.
  - Klasycznym VM - Centrum zabezpieczeń na wszelki dostęp do maszyny Wirtualnej czasu aktualnie obsługuje tylko maszyn wirtualnych wdrożonych za pośrednictwem usługi Azure Resource Manager. Wdrożenie klasyczne nie jest obsługiwana przez tylko w rozwiązaniu czasu.
  - Inne - maszyny Wirtualnej jest w tej kategorii jeśli tylko w czasie rozwiązania jest wyłączona w zasadach zabezpieczeń subskrypcji lub grupy zasobów bądź czy maszyna wirtualna nie ma publicznego adresu IP i nie ma grupy NSG w miejscu.

## <a name="configuring-a-just-in-time-access-policy"></a>Konfigurowanie tylko w czasie zasad dostępu

Aby wybrać maszyny wirtualne, które chcesz włączyć:

1. Na **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz opcję **zalecane** kartę.

  ![Włącz tylko w czasie][3]

2. W obszarze **maszyn wirtualnych**, wybierz maszyny wirtualne, które chcesz włączyć. Spowoduje to umieszczenie znacznik wyboru obok maszyny Wirtualnej.
3. Wybierz **włączyć JIT na maszynach wirtualnych**.
4. Wybierz pozycję **Zapisz**.

### <a name="default-ports"></a>Porty domyślne

Widać domyślnych portów, które Centrum zabezpieczeń zaleca włączenie tylko w czasie.

1. Na **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz opcję **zalecane** kartę.

  ![Wyświetlanie domyślnych portów][6]

2. W obszarze **maszyn wirtualnych**, wybierz maszynę Wirtualną. To jest zaznaczone, obok maszyny Wirtualnej i otwiera **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku. Ten blok zawiera domyślne porty.

### <a name="add-ports"></a>Dodawanie portów

Z **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku można również dodać i skonfigurować nowy port, na którym chcesz włączyć tylko w rozwiązaniu czasu.

1. Na **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku, wybierz opcję **Dodaj**. Spowoduje to otwarcie **konfiguracji portów Dodaj** bloku.

  ![Konfiguracja portów][7]

2. Na **konfiguracji portów Dodaj** bloku, należy określić port, typ protokołu, dozwolone źródła adresów IP i maksymalny czas żądania.

  Źródła dozwolonych adresów IP są zakresów IP mogą uzyskać dostęp na żądanie zatwierdzone.

  Czas żądania maksymalna jest okno maksymalny czas, można otworzyć określonego portu.

3. Kliknij przycisk **OK**.

## <a name="requesting-access-to-a-vm"></a>Żądanie dostępu do maszyny Wirtualnej

Aby uzyskać dostęp do maszyny Wirtualnej:

1. Na **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz opcję **skonfigurowana** kartę.
2. W obszarze **maszyn wirtualnych**, wybierz maszyny wirtualne, które chcesz włączyć dostęp. Spowoduje to umieszczenie znacznik wyboru obok maszyny Wirtualnej.
3. Wybierz **poprosić o dostęp**. Spowoduje to otwarcie **poprosić o dostęp** bloku.

  ![Żądanie dostępu do maszyny Wirtualnej][4]

4. Na **poprosić o dostęp** bloku konfigurowania dla każdej maszyny Wirtualnej porty, aby otworzyć wraz z otwartym port źródłowy adres IP i przedział czasu, dla którego port jest otwarty. Można zażądać dostępu tylko do portów, które są skonfigurowane w tylko w czasie zasad. Każdy port może zawierać maksymalnie dozwolony czas pochodną tylko w czasie zasad.
5. Wybierz **otworzyć porty**.

## <a name="editing-a-just-in-time-access-policy"></a>Edytowanie tylko w czasie zasad dostępu

Można zmienić dla maszyny Wirtualnej istniejących tylko w czasie zasad przez dodanie i skonfigurowanie nowy port, aby otworzyć dla tej maszyny Wirtualnej lub zmieniając innych parametrów związane z portem już chroniony.

Aby edytować istniejące tylko w zasadach czasu maszyny wirtualnej, **skonfigurowana** karta jest używana:

1. W obszarze **maszyn wirtualnych**, wybierz maszynę Wirtualną można dodać portu do, klikając trzy kropki znajdujące się w obrębie wiersza dla tej maszyny Wirtualnej. Spowoduje to otwarcie menu.
2. Wybierz **Edytuj** w menu. Spowoduje to otwarcie **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku.

  ![Edytowanie zasad][8]

3. Na **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku, albo można edytować istniejące ustawienia portu już chronionych, klikając jej portu lub wybrać **Dodaj**. Spowoduje to otwarcie **konfiguracji portów Dodaj** bloku.

  ![Dodaj port][7]

4. Na **konfiguracji portów Dodaj** bloku zidentyfikować portu, typ protokołu, źródła dozwolonych adresów IP i czas maksymalny żądania.
5. Kliknij przycisk **OK**.
6. Wybierz pozycję **Zapisz**.

## <a name="auditing-just-in-time-access-activity"></a>Inspekcja tylko w czasie działania dostępu

Aby uzyskać wgląd w działania maszyny Wirtualnej przy użyciu wyszukiwania dziennika. Aby wyświetlić dzienniki:

1. Na **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz opcję **skonfigurowana** kartę.
2. W obszarze **maszyn wirtualnych**, wybierz maszynę Wirtualną, aby wyświetlić informacje o klikając trzy kropki znajdujące się w obrębie wiersza dla tej maszyny Wirtualnej. Spowoduje to otwarcie menu.
3. Wybierz **dziennik aktywności** w menu. Spowoduje to otwarcie **dziennik aktywności** bloku.

![Wybierz dziennik aktywności][9]

**Dziennik aktywności** bloku udostępnia widok filtrowany poprzednich operacji dla tej maszyny Wirtualnej oraz czas, datę i subskrypcji.

![Wyświetl dziennik aktywności][5]

Można pobrać informacji dziennika, wybierając **kliknij tutaj, aby pobrać wszystkie elementy CSV jako**.

Zmodyfikuj filtry i wybierz **Zastosuj** Tworzenie wyszukiwania i dziennika.

## <a name="using-just-in-time-vm-access-via-powershell"></a>Przy użyciu tylko w czasie dostępu do maszyny Wirtualnej za pomocą programu PowerShell

Aby można było używać tylko w rozwiązaniu czasu za pomocą programu PowerShell, upewnij się, masz [najnowsze](/powershell/azure/install-azurerm-ps) wersji programu Azure PowerShell.
Gdy to zrobisz, musisz zainstalować [najnowsze](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Centrum zabezpieczeń Azure z galerii programu PowerShell.

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a>Konfigurowanie tylko w zasadach czasu dla maszyny Wirtualnej

Aby skonfigurować tylko w zasadach czasu w odpowiedniej maszyny Wirtualnej, musisz uruchomić to polecenie w sesji programu PowerShell: ASCJITAccessPolicy zestawu.
Postępuj zgodnie z dokumentacją polecenia cmdlet, aby dowiedzieć się więcej.

### <a name="requesting-access-to-a-vm"></a>Żądanie dostępu do maszyny Wirtualnej

Można uzyskać dostępu do określonej maszyny Wirtualnej, który jest chroniony za pomocą tylko w rozwiązaniu czas, musisz uruchomić to polecenie w sesji programu PowerShell: ASCJITAccess wywołania.
Postępuj zgodnie z dokumentacją polecenia cmdlet, aby dowiedzieć się więcej.

## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono sposób tylko w czasie dostępu do maszyny Wirtualnej w Centrum zabezpieczeń ułatwia się, że kontroli dostępu na maszynach wirtualnych platformy Azure.

Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:

- [Ustawianie zasad zabezpieczeń](security-center-policies.md) — informacje o sposobie konfigurowania zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
- [Zarządzanie zaleceniami dotyczącymi zabezpieczeń](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
- [Monitorowanie kondycji zabezpieczeń](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.
- [Reagowanie na alerty zabezpieczeń i zarządzanie nimi](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak reagowania na alerty zabezpieczeń i zarządzania nimi.
- [Monitorowanie rozwiązań partnerskich](security-center-partner-solutions.md) — informacje o sposobie monitorowania stanu kondycji rozwiązań partnerskich.
- [Często zadawane pytania dotyczące Centrum zabezpieczeń](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi wyszukiwania.
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
