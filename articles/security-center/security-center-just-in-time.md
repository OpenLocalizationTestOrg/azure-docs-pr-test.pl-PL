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
ms.date: 10/04/2017
ms.author: terrylan
ms.openlocfilehash: c715afe55a3aedd5c4f826bc34c3c56e167d2f82
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time-preview"></a>Zarządzanie dostępem do maszyny wirtualnej przy użyciu tylko w czasie (wersja zapoznawcza)

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

Gdy użytkownik żąda dostępu do maszyny Wirtualnej, Centrum zabezpieczeń sprawdza, czy użytkownik ma [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md) uprawnienia, które zapewniają dostęp do zapisu dla maszyny Wirtualnej. Jeśli mają one uprawnienia do zapisu, żądanie zostanie zatwierdzone i Centrum zabezpieczeń automatycznie konfiguruje grup zabezpieczeń sieci (NSG) zezwalająca na ruch przychodzący do portów zarządzania przez czas określony. Po upływie czasu Centrum zabezpieczeń przywraca grup NSG do poprzedniego stanu.

> [!NOTE]
> Centrum zabezpieczeń na wszelki dostęp do maszyny Wirtualnej czasu aktualnie obsługuje tylko maszyn wirtualnych wdrożonych za pośrednictwem usługi Azure Resource Manager. Aby dowiedzieć się więcej o klasycznego i modeli wdrażania usługi Resource Manager, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne](../azure-resource-manager/resource-manager-deployment-model.md).
>
>

## <a name="using-just-in-time-access"></a>Przy użyciu tylko w czasie

**Bezpośrednio w dostęp do maszyny Wirtualnej czasu** kafelka w obszarze **Centrum zabezpieczeń** pokazuje liczbę maszyn wirtualnych skonfigurowanych dla tylko w czasie dostępu oraz numer zatwierdzenia żądań dostępu w ostatnim tygodniu.

![Tylko w czasie dostępu do maszyny Wirtualnej kafelka][2]

Wybierz **bezpośrednio w dostęp do maszyny Wirtualnej czasu** Kafelek i **bezpośrednio w dostęp maszyny Wirtualnej** otwiera.

![Tylko w czasie dostępu do maszyny Wirtualnej kafelka][10]

**Na wszelki dostęp do maszyny Wirtualnej czasu** zawiera informacje o stanie maszyn wirtualnych:

- **Skonfigurowane** -maszyn wirtualnych, które zostały skonfigurowane do obsługi tylko w dostęp maszyny Wirtualnej. Dane prezentowane jest ostatniego tygodnia i zawiera dla każdej maszyny Wirtualnej liczbę żądań zatwierdzonych, Data ostatniego dostępu i czas i użytkownika, który ostatnio.
- **Zalecane** -maszyn wirtualnych, które obsługują tylko w dostęp maszyny Wirtualnej, ale nie został skonfigurowany do. Zaleca się włączenie tylko w kontroli dostępu wirtualna czasu dla tych maszyn wirtualnych. Zobacz [Konfigurowanie tylko w zasadach dostępu czas](#configuring-a-just-in-time-access-policy).
- **Brak rekomendacji** -przyczyny, które mogą spowodować maszyny Wirtualnej, aby nie zaleca się to:
  - Brak grupy NSG — tylko w czasie rozwiązanie wymaga grupy NSG w miejscu.
  - Klasycznym VM - Centrum zabezpieczeń na wszelki dostęp do maszyny Wirtualnej czasu aktualnie obsługuje tylko maszyn wirtualnych wdrożonych za pośrednictwem usługi Azure Resource Manager. Wdrożenie klasyczne nie jest obsługiwana przez tylko w rozwiązaniu czasu.
  - Inne - maszyny Wirtualnej jest w tej kategorii jeśli tylko w czasie rozwiązania jest wyłączona w zasadach zabezpieczeń subskrypcji lub grupy zasobów bądź czy maszyna wirtualna nie ma publicznego adresu IP i nie ma grupy NSG w miejscu.

## <a name="configuring-a-just-in-time-access-policy"></a>Konfigurowanie tylko w czasie zasad dostępu

Aby wybrać maszyny wirtualne, które chcesz włączyć:

1. W obszarze **bezpośrednio w dostęp do maszyny Wirtualnej czasu**, wybierz pozycję **zalecane** kartę.

  ![Włącz tylko w czasie][3]

2. W obszarze **maszyny WIRTUALNEJ**, wybierz maszyny wirtualne, które chcesz włączyć. Spowoduje to umieszczenie znacznik wyboru obok maszyny Wirtualnej.
3. Wybierz **włączyć JIT na maszynach wirtualnych**.
4. Wybierz pozycję **Zapisz**.

### <a name="default-ports"></a>Porty domyślne

Widać domyślnych portów, które Centrum zabezpieczeń zaleca włączenie tylko w czasie.

1. W obszarze **bezpośrednio w dostęp do maszyny Wirtualnej czasu**, wybierz pozycję **zalecane** kartę.

  ![Wyświetlanie domyślnych portów][6]

2. W obszarze **maszyn wirtualnych**, wybierz maszynę Wirtualną. To jest zaznaczone, obok maszyny Wirtualnej i otwiera **Konfiguracja dostępu do maszyny Wirtualnej JIT**. Ten blok zawiera domyślne porty.

### <a name="add-ports"></a>Dodawanie portów

W obszarze **Konfiguracja dostępu do maszyny Wirtualnej JIT**, można także dodać i skonfigurować nowy port, na którym chcesz włączyć tylko w rozwiązaniu czasu.

1. W obszarze **Konfiguracja dostępu do maszyny Wirtualnej JIT**, wybierz pozycję **Dodaj**. Spowoduje to otwarcie **konfiguracji portów Dodaj**.

  ![Konfiguracja portów][7]

2. W obszarze **konfiguracji portów Dodaj**, zidentyfikuj port, typ protokołu, źródła dozwolonych adresów IP i czas maksymalny żądania.

  Źródła dozwolonych adresów IP są zakresów IP mogą uzyskać dostęp na żądanie zatwierdzone.

  Czas żądania maksymalna jest okno maksymalny czas, można otworzyć określonego portu.

3. Kliknij przycisk **OK**.

## <a name="requesting-access-to-a-vm"></a>Żądanie dostępu do maszyny Wirtualnej

Aby uzyskać dostęp do maszyny Wirtualnej:

1. W obszarze **bezpośrednio w dostęp do maszyny Wirtualnej czasu**, wybierz pozycję **skonfigurowana** kartę.
2. W obszarze **maszyn wirtualnych**, wybierz maszyny wirtualne, które chcesz włączyć dostęp. Spowoduje to umieszczenie znacznik wyboru obok maszyny Wirtualnej.
3. Wybierz **poprosić o dostęp**. Spowoduje to otwarcie **poprosić o dostęp**.

  ![Żądanie dostępu do maszyny Wirtualnej][4]

4. W obszarze **poprosić o dostęp**, skonfigurowaniu porty, aby otworzyć wraz z otwartym port źródłowy adres IP i przedział czasu, dla którego jest otwarty port dla każdej maszyny Wirtualnej. Można zażądać dostępu tylko do portów, które są skonfigurowane w tylko w czasie zasad. Każdy port może zawierać maksymalnie dozwolony czas pochodną tylko w czasie zasad.
5. Wybierz **otworzyć porty**.

## <a name="editing-a-just-in-time-access-policy"></a>Edytowanie tylko w czasie zasad dostępu

Można zmienić dla maszyny Wirtualnej istniejących tylko w czasie zasad przez dodanie i skonfigurowanie nowy port, aby otworzyć dla tej maszyny Wirtualnej lub zmieniając innych parametrów związane z portem już chroniony.

Aby edytować istniejące tylko w zasadach czasu maszyny wirtualnej, **skonfigurowana** karta jest używana:

1. W obszarze **maszyn wirtualnych**, wybierz maszynę Wirtualną można dodać portu do, klikając trzy kropki znajdujące się w obrębie wiersza dla tej maszyny Wirtualnej. Spowoduje to otwarcie menu.
2. Wybierz **Edytuj** w menu. Spowoduje to otwarcie **Konfiguracja dostępu do maszyny Wirtualnej JIT**.

  ![Edytowanie zasad][8]

3. W obszarze **Konfiguracja dostępu do maszyny Wirtualnej JIT**, albo można edytować istniejące ustawienia portu już chronionych, klikając jej portu, lub wybrać **Dodaj**. Spowoduje to otwarcie **konfiguracji portów Dodaj**.

  ![Dodaj port][7]

4. W obszarze **konfiguracji portów Dodaj**, ustalić port, protokół typu dozwolone źródła adresów IP i maksymalny czas żądania.
5. Kliknij przycisk **OK**.
6. Wybierz pozycję **Zapisz**.

## <a name="auditing-just-in-time-access-activity"></a>Inspekcja tylko w czasie działania dostępu

Aby uzyskać wgląd w działania maszyny Wirtualnej przy użyciu wyszukiwania dziennika. Aby wyświetlić dzienniki:

1. W obszarze **bezpośrednio w dostęp do maszyny Wirtualnej czasu**, wybierz pozycję **skonfigurowana** kartę.
2. W obszarze **maszyn wirtualnych**, wybierz maszynę Wirtualną, aby wyświetlić informacje o klikając trzy kropki znajdujące się w obrębie wiersza dla tej maszyny Wirtualnej. Spowoduje to otwarcie menu.
3. Wybierz **dziennik aktywności** w menu. Spowoduje to otwarcie **dziennik aktywności**.

  ![Wybierz dziennik aktywności][9]

  **Dziennik aktywności** udostępnia widok filtrowany poprzednich operacji dla tej maszyny Wirtualnej oraz czas, datę i subskrypcji.

  ![Wyświetl dziennik aktywności][5]

Można pobrać informacji dziennika, wybierając **kliknij tutaj, aby pobrać wszystkie elementy CSV jako**.

Zmodyfikuj filtry i wybierz **Zastosuj** Tworzenie wyszukiwania i dziennika.

## <a name="using-just-in-time-vm-access-via-powershell"></a>Przy użyciu tylko w czasie dostępu do maszyny Wirtualnej za pomocą programu PowerShell

Aby można było używać tylko w rozwiązaniu czasu za pomocą programu PowerShell, upewnij się, masz [najnowsze](/powershell/azure/install-azurerm-ps) wersji programu Azure PowerShell.
Gdy to zrobisz, musisz zainstalować [najnowsze](https://aka.ms/asc-psgallery) Centrum zabezpieczeń Azure z galerii programu PowerShell.

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
[10]: ./media/security-center-just-in-time/just-in-time-access.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
