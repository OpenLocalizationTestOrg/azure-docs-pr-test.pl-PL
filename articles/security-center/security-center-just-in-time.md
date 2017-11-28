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
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="9d379-103">Zarządzanie dostępem do maszyny wirtualnej przy użyciu tylko w czasie</span><span class="sxs-lookup"><span data-stu-id="9d379-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="9d379-104">Tylko w czasie maszyny wirtualnej (VM) dostępu może służyć do blokowania ruchu przychodzącego na maszynach wirtualnych platformy Azure, ograniczenia narażenia na ataki, zapewniając łatwy dostęp do nawiązania połączenia maszyn wirtualnych w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="9d379-104">Just in time virtual machine (VM) access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks while providing easy access to connect to VMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="9d379-105">Tylko w czasie jest funkcja w wersji zapoznawczej i dostępne w warstwie standardowa Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="9d379-105">The just in time feature is in preview and available on the Standard tier of Security Center.</span></span>  <span data-ttu-id="9d379-106">Zobacz [cennik](security-center-pricing.md) Aby dowiedzieć się więcej na temat Centrum zabezpieczeń firmy ceny warstw.</span><span class="sxs-lookup"><span data-stu-id="9d379-106">See [Pricing](security-center-pricing.md) to learn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="9d379-107">Atak</span><span class="sxs-lookup"><span data-stu-id="9d379-107">Attack scenario</span></span>

<span data-ttu-id="9d379-108">Atak siłowy ataków często porty docelowe zarządzania w celu uzyskania dostępu do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d379-108">Brute force attacks commonly target management ports as a means to gain access to a VM.</span></span> <span data-ttu-id="9d379-109">Jeśli to się powiedzie, osoba atakująca może przejąć kontrolę nad maszyny Wirtualnej i nawiązywać stopień do środowiska.</span><span class="sxs-lookup"><span data-stu-id="9d379-109">If successful, an attacker can take control over the VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="9d379-110">Jednym ze sposobów zmniejszyć ryzyko ataków siłowych jest ograniczyć czas, który port jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="9d379-110">One way to reduce exposure to a brute force attack is to limit the amount of time that a port is open.</span></span> <span data-ttu-id="9d379-111">Porty zarządzania nie muszą być otwarte przez cały czas.</span><span class="sxs-lookup"><span data-stu-id="9d379-111">Management ports do not need to be open at all times.</span></span> <span data-ttu-id="9d379-112">Tylko muszą być otwarte, gdy są połączone z maszyną wirtualną, na przykład w celu wykonywania zadań zarządzania i konserwacji.</span><span class="sxs-lookup"><span data-stu-id="9d379-112">They only need to be open while you are connected to the VM, for example to perform management or maintenance tasks.</span></span> <span data-ttu-id="9d379-113">Gdy tylko w czasie jest włączona, Centrum zabezpieczeń używa [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) reguły (NSG), które ograniczanie dostępu do portów zarządzania, więc nie może być wskazywane przez osoby atakujące.</span><span class="sxs-lookup"><span data-stu-id="9d379-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access to management ports so they cannot be targeted by attackers.</span></span>

![Tylko w scenariuszu czasu][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="9d379-115">Jak tylko w czasie pracy?</span><span class="sxs-lookup"><span data-stu-id="9d379-115">How does just in time access work?</span></span>

<span data-ttu-id="9d379-116">Gdy zostanie włączona funkcja „dokładnie na czas”, usługa Security Center zablokuje ruch przychodzący do maszyn wirtualnych platformy Azure poprzez utworzenie reguły sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="9d379-116">When just in time is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="9d379-117">Należy wybrać porty na maszynie Wirtualnej, do którego będzie można zablokować ruch przychodzący.</span><span class="sxs-lookup"><span data-stu-id="9d379-117">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="9d379-118">Te porty są kontrolowane przez tylko w rozwiązaniu czasu.</span><span class="sxs-lookup"><span data-stu-id="9d379-118">These ports are controlled by the just in time solution.</span></span>

<span data-ttu-id="9d379-119">Gdy użytkownik żąda dostępu do maszyny Wirtualnej, Centrum zabezpieczeń sprawdza, czy użytkownik ma [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md) uprawnienia, które zapewniają dostęp do zapisu dla zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9d379-119">When a user requests access to a VM, Security Center checks that the user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for the Azure resource.</span></span> <span data-ttu-id="9d379-120">Jeśli mają one uprawnienia do zapisu, żądanie zostanie zatwierdzone i Centrum zabezpieczeń automatycznie konfiguruje grup zabezpieczeń sieci (NSG) zezwalająca na ruch przychodzący do portów zarządzania przez czas określony.</span><span class="sxs-lookup"><span data-stu-id="9d379-120">If they have write permissions, the request is approved and Security Center automatically configures the Network Security Groups (NSGs) to allow inbound traffic to the management ports for the amount of time you specified.</span></span> <span data-ttu-id="9d379-121">Po upływie czasu Centrum zabezpieczeń przywraca grup NSG do poprzedniego stanu.</span><span class="sxs-lookup"><span data-stu-id="9d379-121">After the time has expired, Security Center restores the NSGs to their previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="9d379-122">Centrum zabezpieczeń na wszelki dostęp do maszyny Wirtualnej czasu aktualnie obsługuje tylko maszyn wirtualnych wdrożonych za pośrednictwem usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9d379-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="9d379-123">Aby dowiedzieć się więcej o klasycznego i modeli wdrażania usługi Resource Manager, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9d379-123">To learn more about the classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="9d379-124">Przy użyciu tylko w czasie</span><span class="sxs-lookup"><span data-stu-id="9d379-124">Using just in time access</span></span>

<span data-ttu-id="9d379-125">**Bezpośrednio w dostęp do maszyny Wirtualnej czasu** Kafelek na **Centrum zabezpieczeń** bloku pokazuje liczbę maszyn wirtualnych skonfigurowany dla dokładnie na czas dostępu i liczba żądań zatwierdzonych dostępu wykonanych w ostatnim tygodniu.</span><span class="sxs-lookup"><span data-stu-id="9d379-125">The **Just in time VM access** tile on the **Security Center** blade shows the number of VMs configured for just in time access and the number of approved access requests made in the last week.</span></span>

<span data-ttu-id="9d379-126">Wybierz **bezpośrednio w dostęp do maszyny Wirtualnej czasu** Kafelek i **bezpośrednio w dostęp maszyny Wirtualnej** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="9d379-126">Select the **Just in time VM access** tile and the **Just in time VM access** blade opens.</span></span>

![Tylko w czasie dostępu do maszyny Wirtualnej kafelka][2]

<span data-ttu-id="9d379-128">**Bezpośrednio w dostęp do maszyny Wirtualnej czasu** blok zawiera informacje o stanie maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="9d379-128">The **Just in time VM access** blade provides information on the state of your VMs:</span></span>

- <span data-ttu-id="9d379-129">**Skonfigurowane** -maszyn wirtualnych, które zostały skonfigurowane do obsługi tylko w dostęp maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d379-129">**Configured** - VMs that have been configured to support just in time VM access.</span></span> <span data-ttu-id="9d379-130">Dane prezentowane jest ostatniego tygodnia i zawiera dla każdej maszyny Wirtualnej liczbę żądań zatwierdzonych, Data ostatniego dostępu i czas i użytkownika, który ostatnio.</span><span class="sxs-lookup"><span data-stu-id="9d379-130">The data presented is for the last week and includes for each VM the number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="9d379-131">**Zalecane** -maszyn wirtualnych, które obsługują tylko w dostęp maszyny Wirtualnej, ale nie został skonfigurowany do.</span><span class="sxs-lookup"><span data-stu-id="9d379-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="9d379-132">Zaleca się włączenie tylko w kontroli dostępu wirtualna czasu dla tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9d379-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="9d379-133">Zobacz [włączyć tylko w przypadku maszyn wirtualnych dostęp](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="9d379-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="9d379-134">**Brak rekomendacji** -przyczyny, które mogą spowodować maszyny Wirtualnej, aby nie zaleca się to:</span><span class="sxs-lookup"><span data-stu-id="9d379-134">**No recommendation** - Reasons that can cause a VM not to be recommended are:</span></span>
  - <span data-ttu-id="9d379-135">Brak grupy NSG — tylko w czasie rozwiązanie wymaga grupy NSG w miejscu.</span><span class="sxs-lookup"><span data-stu-id="9d379-135">Missing NSG - The just in time solution requires an NSG to be in place.</span></span>
  - <span data-ttu-id="9d379-136">Klasycznym VM - Centrum zabezpieczeń na wszelki dostęp do maszyny Wirtualnej czasu aktualnie obsługuje tylko maszyn wirtualnych wdrożonych za pośrednictwem usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9d379-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="9d379-137">Wdrożenie klasyczne nie jest obsługiwana przez tylko w rozwiązaniu czasu.</span><span class="sxs-lookup"><span data-stu-id="9d379-137">A classic deployment is not supported by the just in time solution.</span></span>
  - <span data-ttu-id="9d379-138">Inne - maszyny Wirtualnej jest w tej kategorii jeśli tylko w czasie rozwiązania jest wyłączona w zasadach zabezpieczeń subskrypcji lub grupy zasobów bądź czy maszyna wirtualna nie ma publicznego adresu IP i nie ma grupy NSG w miejscu.</span><span class="sxs-lookup"><span data-stu-id="9d379-138">Other - A VM is in this category if the just in time solution is turned off in the security policy of the subscription or the resource group, or that the VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="9d379-139">Konfigurowanie tylko w czasie zasad dostępu</span><span class="sxs-lookup"><span data-stu-id="9d379-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="9d379-140">Aby wybrać maszyny wirtualne, które chcesz włączyć:</span><span class="sxs-lookup"><span data-stu-id="9d379-140">To select the VMs that you want to enable:</span></span>

1. <span data-ttu-id="9d379-141">Na **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz opcję **zalecane** kartę.</span><span class="sxs-lookup"><span data-stu-id="9d379-141">On the **Just in time VM access** blade, select the **Recommended** tab.</span></span>

  ![Włącz tylko w czasie][3]

2. <span data-ttu-id="9d379-143">W obszarze **maszyn wirtualnych**, wybierz maszyny wirtualne, które chcesz włączyć.</span><span class="sxs-lookup"><span data-stu-id="9d379-143">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="9d379-144">Spowoduje to umieszczenie znacznik wyboru obok maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d379-144">This puts a checkmark next to a VM.</span></span>
3. <span data-ttu-id="9d379-145">Wybierz **włączyć JIT na maszynach wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="9d379-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="9d379-146">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9d379-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="9d379-147">Porty domyślne</span><span class="sxs-lookup"><span data-stu-id="9d379-147">Default ports</span></span>

<span data-ttu-id="9d379-148">Widać domyślnych portów, które Centrum zabezpieczeń zaleca włączenie tylko w czasie.</span><span class="sxs-lookup"><span data-stu-id="9d379-148">You can see the default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="9d379-149">Na **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz opcję **zalecane** kartę.</span><span class="sxs-lookup"><span data-stu-id="9d379-149">On the **Just in time VM access** blade, select the **Recommended** tab.</span></span>

  ![Wyświetlanie domyślnych portów][6]

2. <span data-ttu-id="9d379-151">W obszarze **maszyn wirtualnych**, wybierz maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="9d379-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="9d379-152">To jest zaznaczone, obok maszyny Wirtualnej i otwiera **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku.</span><span class="sxs-lookup"><span data-stu-id="9d379-152">This puts a checkmark next to the VM and opens the **JIT VM access configuration** blade.</span></span> <span data-ttu-id="9d379-153">Ten blok zawiera domyślne porty.</span><span class="sxs-lookup"><span data-stu-id="9d379-153">This blade displays the default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="9d379-154">Dodawanie portów</span><span class="sxs-lookup"><span data-stu-id="9d379-154">Add ports</span></span>

<span data-ttu-id="9d379-155">Z **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku można również dodać i skonfigurować nowy port, na którym chcesz włączyć tylko w rozwiązaniu czasu.</span><span class="sxs-lookup"><span data-stu-id="9d379-155">From the **JIT VM access configuration** blade, you can also add and configure a new port on which you want to enable the just in time solution.</span></span>

1. <span data-ttu-id="9d379-156">Na **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="9d379-156">On the **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="9d379-157">Spowoduje to otwarcie **konfiguracji portów Dodaj** bloku.</span><span class="sxs-lookup"><span data-stu-id="9d379-157">This opens the **Add port configuration** blade.</span></span>

  ![Konfiguracja portów][7]

2. <span data-ttu-id="9d379-159">Na **konfiguracji portów Dodaj** bloku, należy określić port, typ protokołu, dozwolone źródła adresów IP i maksymalny czas żądania.</span><span class="sxs-lookup"><span data-stu-id="9d379-159">On **Add port configuration** blade, you identify the port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="9d379-160">Źródła dozwolonych adresów IP są zakresów IP mogą uzyskać dostęp na żądanie zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="9d379-160">Allowed source IPs are the IP ranges allowed to get access upon an approved request.</span></span>

  <span data-ttu-id="9d379-161">Czas żądania maksymalna jest okno maksymalny czas, można otworzyć określonego portu.</span><span class="sxs-lookup"><span data-stu-id="9d379-161">Maximum request time is the maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="9d379-162">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d379-162">Select **OK**.</span></span>

## <a name="requesting-access-to-a-vm"></a><span data-ttu-id="9d379-163">Żądanie dostępu do maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9d379-163">Requesting access to a VM</span></span>

<span data-ttu-id="9d379-164">Aby uzyskać dostęp do maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="9d379-164">To request access to a VM:</span></span>

1. <span data-ttu-id="9d379-165">Na **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz opcję **skonfigurowana** kartę.</span><span class="sxs-lookup"><span data-stu-id="9d379-165">On the **Just in time VM access** blade, select the **Configured** tab.</span></span>
2. <span data-ttu-id="9d379-166">W obszarze **maszyn wirtualnych**, wybierz maszyny wirtualne, które chcesz włączyć dostęp.</span><span class="sxs-lookup"><span data-stu-id="9d379-166">Under **VMs**, select the VMs that you want to enable access.</span></span> <span data-ttu-id="9d379-167">Spowoduje to umieszczenie znacznik wyboru obok maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d379-167">This puts a checkmark next to a VM.</span></span>
3. <span data-ttu-id="9d379-168">Wybierz **poprosić o dostęp**.</span><span class="sxs-lookup"><span data-stu-id="9d379-168">Select **Request access**.</span></span> <span data-ttu-id="9d379-169">Spowoduje to otwarcie **poprosić o dostęp** bloku.</span><span class="sxs-lookup"><span data-stu-id="9d379-169">This opens the **Request access** blade.</span></span>

  ![Żądanie dostępu do maszyny Wirtualnej][4]

4. <span data-ttu-id="9d379-171">Na **poprosić o dostęp** bloku konfigurowania dla każdej maszyny Wirtualnej porty, aby otworzyć wraz z otwartym port źródłowy adres IP i przedział czasu, dla którego port jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="9d379-171">On the **Request access** blade, you configure for each VM the ports to open along with the source IP that the port is opened to and the time window for which the port is opened.</span></span> <span data-ttu-id="9d379-172">Można zażądać dostępu tylko do portów, które są skonfigurowane w tylko w czasie zasad.</span><span class="sxs-lookup"><span data-stu-id="9d379-172">You can request access only to the ports that are configured in the just in time policy.</span></span> <span data-ttu-id="9d379-173">Każdy port może zawierać maksymalnie dozwolony czas pochodną tylko w czasie zasad.</span><span class="sxs-lookup"><span data-stu-id="9d379-173">Each port has a maximum allowed time derived from the just in time policy.</span></span>
5. <span data-ttu-id="9d379-174">Wybierz **otworzyć porty**.</span><span class="sxs-lookup"><span data-stu-id="9d379-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="9d379-175">Edytowanie tylko w czasie zasad dostępu</span><span class="sxs-lookup"><span data-stu-id="9d379-175">Editing a just in time access policy</span></span>

<span data-ttu-id="9d379-176">Można zmienić dla maszyny Wirtualnej istniejących tylko w czasie zasad przez dodanie i skonfigurowanie nowy port, aby otworzyć dla tej maszyny Wirtualnej lub zmieniając innych parametrów związane z portem już chroniony.</span><span class="sxs-lookup"><span data-stu-id="9d379-176">You can change a VM's existing just in time policy by adding and configuring a new port to open for that VM, or by changing any other parameter related to an already protected port.</span></span>

<span data-ttu-id="9d379-177">Aby edytować istniejące tylko w zasadach czasu maszyny wirtualnej, **skonfigurowana** karta jest używana:</span><span class="sxs-lookup"><span data-stu-id="9d379-177">In order to edit an existing just in time policy of a VM, the **Configured** tab is used:</span></span>

1. <span data-ttu-id="9d379-178">W obszarze **maszyn wirtualnych**, wybierz maszynę Wirtualną można dodać portu do, klikając trzy kropki znajdujące się w obrębie wiersza dla tej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d379-178">Under **VMs**, select a VM to add a port to by clicking on the three dots within the row for that VM.</span></span> <span data-ttu-id="9d379-179">Spowoduje to otwarcie menu.</span><span class="sxs-lookup"><span data-stu-id="9d379-179">This opens a menu.</span></span>
2. <span data-ttu-id="9d379-180">Wybierz **Edytuj** w menu.</span><span class="sxs-lookup"><span data-stu-id="9d379-180">Select **Edit** in the menu.</span></span> <span data-ttu-id="9d379-181">Spowoduje to otwarcie **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku.</span><span class="sxs-lookup"><span data-stu-id="9d379-181">This opens the **JIT VM access configuration** blade.</span></span>

  ![Edytowanie zasad][8]

3. <span data-ttu-id="9d379-183">Na **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku, albo można edytować istniejące ustawienia portu już chronionych, klikając jej portu lub wybrać **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="9d379-183">On the **JIT VM access configuration** blade, you can either edit the existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="9d379-184">Spowoduje to otwarcie **konfiguracji portów Dodaj** bloku.</span><span class="sxs-lookup"><span data-stu-id="9d379-184">This opens the **Add port configuration** blade.</span></span>

  ![Dodaj port][7]

4. <span data-ttu-id="9d379-186">Na **konfiguracji portów Dodaj** bloku zidentyfikować portu, typ protokołu, źródła dozwolonych adresów IP i czas maksymalny żądania.</span><span class="sxs-lookup"><span data-stu-id="9d379-186">On **Add port configuration** blade identify the port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="9d379-187">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d379-187">Select **OK**.</span></span>
6. <span data-ttu-id="9d379-188">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9d379-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="9d379-189">Inspekcja tylko w czasie działania dostępu</span><span class="sxs-lookup"><span data-stu-id="9d379-189">Auditing just in time access activity</span></span>

<span data-ttu-id="9d379-190">Aby uzyskać wgląd w działania maszyny Wirtualnej przy użyciu wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="9d379-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="9d379-191">Aby wyświetlić dzienniki:</span><span class="sxs-lookup"><span data-stu-id="9d379-191">To view logs:</span></span>

1. <span data-ttu-id="9d379-192">Na **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz opcję **skonfigurowana** kartę.</span><span class="sxs-lookup"><span data-stu-id="9d379-192">On the **Just in time VM access** blade, select the **Configured** tab.</span></span>
2. <span data-ttu-id="9d379-193">W obszarze **maszyn wirtualnych**, wybierz maszynę Wirtualną, aby wyświetlić informacje o klikając trzy kropki znajdujące się w obrębie wiersza dla tej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9d379-193">Under **VMs**, select a VM to view information about by clicking on the three dots within the row for that VM.</span></span> <span data-ttu-id="9d379-194">Spowoduje to otwarcie menu.</span><span class="sxs-lookup"><span data-stu-id="9d379-194">This opens a menu.</span></span>
3. <span data-ttu-id="9d379-195">Wybierz **dziennik aktywności** w menu.</span><span class="sxs-lookup"><span data-stu-id="9d379-195">Select **Activity Log** in the menu.</span></span> <span data-ttu-id="9d379-196">Spowoduje to otwarcie **dziennik aktywności** bloku.</span><span class="sxs-lookup"><span data-stu-id="9d379-196">This opens the **Activity log** blade.</span></span>

![Wybierz dziennik aktywności][9]

<span data-ttu-id="9d379-198">**Dziennik aktywności** bloku udostępnia widok filtrowany poprzednich operacji dla tej maszyny Wirtualnej oraz czas, datę i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9d379-198">The **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Wyświetl dziennik aktywności][5]

<span data-ttu-id="9d379-200">Można pobrać informacji dziennika, wybierając **kliknij tutaj, aby pobrać wszystkie elementy CSV jako**.</span><span class="sxs-lookup"><span data-stu-id="9d379-200">You can download the log information by selecting **Click here to download all the items as CSV**.</span></span>

<span data-ttu-id="9d379-201">Zmodyfikuj filtry i wybierz **Zastosuj** Tworzenie wyszukiwania i dziennika.</span><span class="sxs-lookup"><span data-stu-id="9d379-201">Modify the filters and select **Apply** to create a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="9d379-202">Przy użyciu tylko w czasie dostępu do maszyny Wirtualnej za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d379-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="9d379-203">Aby można było używać tylko w rozwiązaniu czasu za pomocą programu PowerShell, upewnij się, masz [najnowsze](/powershell/azure/install-azurerm-ps) wersji programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d379-203">In order to use the just in time solution via PowerShell, make sure you have the [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="9d379-204">Gdy to zrobisz, musisz zainstalować [najnowsze](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Centrum zabezpieczeń Azure z galerii programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d379-204">Once you do, you need to install the [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from the PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="9d379-205">Konfigurowanie tylko w zasadach czasu dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9d379-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="9d379-206">Aby skonfigurować tylko w zasadach czasu w odpowiedniej maszyny Wirtualnej, musisz uruchomić to polecenie w sesji programu PowerShell: ASCJITAccessPolicy zestawu.</span><span class="sxs-lookup"><span data-stu-id="9d379-206">To configure a just in time policy on a specific VM, you need to run this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="9d379-207">Postępuj zgodnie z dokumentacją polecenia cmdlet, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="9d379-207">Follow the cmdlet documentation to learn more.</span></span>

### <a name="requesting-access-to-a-vm"></a><span data-ttu-id="9d379-208">Żądanie dostępu do maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9d379-208">Requesting access to a VM</span></span>

<span data-ttu-id="9d379-209">Można uzyskać dostępu do określonej maszyny Wirtualnej, który jest chroniony za pomocą tylko w rozwiązaniu czas, musisz uruchomić to polecenie w sesji programu PowerShell: ASCJITAccess wywołania.</span><span class="sxs-lookup"><span data-stu-id="9d379-209">To access a specific VM that is protected with the just in time solution, you need to run this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="9d379-210">Postępuj zgodnie z dokumentacją polecenia cmdlet, aby dowiedzieć się więcej.</span><span class="sxs-lookup"><span data-stu-id="9d379-210">Follow the cmdlet documentation to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d379-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9d379-211">Next steps</span></span>
<span data-ttu-id="9d379-212">W tym artykule przedstawiono sposób tylko w czasie dostępu do maszyny Wirtualnej w Centrum zabezpieczeń ułatwia się, że kontroli dostępu na maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9d379-212">In this article, you learned how just in time VM access in Security Center helps you control access to your Azure virtual machines.</span></span>

<span data-ttu-id="9d379-213">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="9d379-213">To learn more about Security Center, see the following:</span></span>

- <span data-ttu-id="9d379-214">[Ustawianie zasad zabezpieczeń](security-center-policies.md) — informacje o sposobie konfigurowania zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="9d379-214">[Setting security policies](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="9d379-215">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9d379-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="9d379-216">[Monitorowanie kondycji zabezpieczeń](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9d379-216">[Security health monitoring](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
- <span data-ttu-id="9d379-217">[Reagowanie na alerty zabezpieczeń i zarządzanie nimi](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="9d379-217">[Managing and responding to security alerts](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
- <span data-ttu-id="9d379-218">[Monitorowanie rozwiązań partnerskich](security-center-partner-solutions.md) — informacje o sposobie monitorowania stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="9d379-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
- <span data-ttu-id="9d379-219">[Często zadawane pytania dotyczące Centrum zabezpieczeń](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9d379-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
- <span data-ttu-id="9d379-220">[Blog Azure Security](https://blogs.msdn.microsoft.com/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9d379-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


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
