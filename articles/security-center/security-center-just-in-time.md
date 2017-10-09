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
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="2c576-103">Zarządzanie dostępem do maszyny wirtualnej przy użyciu tylko w czasie</span><span class="sxs-lookup"><span data-stu-id="2c576-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="2c576-104">Tylko w czasie maszyny wirtualnej (VM) dostępu może być używane toolock dół tooyour ruch przychodzący maszynach wirtualnych platformy Azure, zmniejszenie zagrożeń tooattacks zapewniając łatwy dostęp tooconnect tooVMs w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="2c576-104">Just in time virtual machine (VM) access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks while providing easy access tooconnect tooVMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="2c576-105">Witaj tylko w funkcji czasu jest w wersji zapoznawczej i jest dostępny na powitania warstwy standardowa, Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2c576-105">hello just in time feature is in preview and available on hello Standard tier of Security Center.</span></span>  <span data-ttu-id="2c576-106">Zobacz [cennik](security-center-pricing.md) toolearn więcej informacji na temat Centrum zabezpieczeń firmy warstw cenowych.</span><span class="sxs-lookup"><span data-stu-id="2c576-106">See [Pricing](security-center-pricing.md) toolearn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="2c576-107">Atak</span><span class="sxs-lookup"><span data-stu-id="2c576-107">Attack scenario</span></span>

<span data-ttu-id="2c576-108">Atak siłowy ataków często porty docelowe zarządzania jako oznacza tooa dostępu toogain maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c576-108">Brute force attacks commonly target management ports as a means toogain access tooa VM.</span></span> <span data-ttu-id="2c576-109">Jeśli to się powiedzie, osoba atakująca może przejąć kontrolę nad hello maszyny Wirtualnej i nawiązywać stopień do środowiska.</span><span class="sxs-lookup"><span data-stu-id="2c576-109">If successful, an attacker can take control over hello VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="2c576-110">Ataków siłowych tooa narażenia jednokierunkowej tooreduce jest toolimit hello ilość czasu, który port jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="2c576-110">One way tooreduce exposure tooa brute force attack is toolimit hello amount of time that a port is open.</span></span> <span data-ttu-id="2c576-111">Porty zarządzania czy nie potrzeba toobe otwarte przez cały czas.</span><span class="sxs-lookup"><span data-stu-id="2c576-111">Management ports do not need toobe open at all times.</span></span> <span data-ttu-id="2c576-112">Potrzebna jest tylko toobe otwarte podczas połączonych toohello maszyny Wirtualnej, na przykład tooperform są zadania zarządzania i konserwacji.</span><span class="sxs-lookup"><span data-stu-id="2c576-112">They only need toobe open while you are connected toohello VM, for example tooperform management or maintenance tasks.</span></span> <span data-ttu-id="2c576-113">Gdy tylko w czasie jest włączona, Centrum zabezpieczeń używa [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) reguły (NSG), które ograniczają porty toomanagement dostępu, więc nie może być wskazywane przez osoby atakujące.</span><span class="sxs-lookup"><span data-stu-id="2c576-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access toomanagement ports so they cannot be targeted by attackers.</span></span>

![Tylko w scenariuszu czasu][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="2c576-115">Jak tylko w czasie pracy?</span><span class="sxs-lookup"><span data-stu-id="2c576-115">How does just in time access work?</span></span>

<span data-ttu-id="2c576-116">Gdy tylko w czasie jest włączona, Centrum zabezpieczeń blokuje ruch przychodzący tooyour maszynach wirtualnych platformy Azure przez tworzenie reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="2c576-116">When just in time is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="2c576-117">Wybierz porty hello na powitania toowhich maszyny Wirtualnej zostanie zablokowana ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="2c576-117">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="2c576-118">Te porty są kontrolowane przez hello tylko w rozwiązaniu czasu.</span><span class="sxs-lookup"><span data-stu-id="2c576-118">These ports are controlled by hello just in time solution.</span></span>

<span data-ttu-id="2c576-119">Gdy użytkownik zażąda dostępu tooa maszyny Wirtualnej, Centrum zabezpieczeń sprawdza użytkownika hello [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md) uprawnienia, które zapewniają dostęp do zapisu dla hello zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c576-119">When a user requests access tooa VM, Security Center checks that hello user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for hello Azure resource.</span></span> <span data-ttu-id="2c576-120">Jeśli mają one uprawnienia do zapisu, hello żądanie zostanie zatwierdzone i Centrum zabezpieczeń automatycznie konfiguruje hello tooallow grup zabezpieczeń sieci (NSG) ruchu przychodzącego ruchu toohello zarządzania porty hello ilość czasu, można określić.</span><span class="sxs-lookup"><span data-stu-id="2c576-120">If they have write permissions, hello request is approved and Security Center automatically configures hello Network Security Groups (NSGs) tooallow inbound traffic toohello management ports for hello amount of time you specified.</span></span> <span data-ttu-id="2c576-121">Po upływie czasu hello, Centrum zabezpieczeń przywraca hello grup NSG tootheir poprzedniego stanu.</span><span class="sxs-lookup"><span data-stu-id="2c576-121">After hello time has expired, Security Center restores hello NSGs tootheir previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="2c576-122">Centrum zabezpieczeń na wszelki dostęp do maszyny Wirtualnej czasu aktualnie obsługuje tylko maszyn wirtualnych wdrożonych za pośrednictwem usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2c576-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="2c576-123">toolearn więcej informacji o hello klasycznego i modeli wdrażania usługi Resource Manager zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2c576-123">toolearn more about hello classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="2c576-124">Przy użyciu tylko w czasie</span><span class="sxs-lookup"><span data-stu-id="2c576-124">Using just in time access</span></span>

<span data-ttu-id="2c576-125">Witaj **bezpośrednio w dostęp maszyny Wirtualnej** Kafelek na powitania **Centrum zabezpieczeń** bloku pokazuje hello liczbę maszyn wirtualnych skonfigurowanych dla tylko w czasie dostępu i hello liczby żądań zatwierdzonych dostępu wprowadzone w hello ostatniego tygodnia.</span><span class="sxs-lookup"><span data-stu-id="2c576-125">hello **Just in time VM access** tile on hello **Security Center** blade shows hello number of VMs configured for just in time access and hello number of approved access requests made in hello last week.</span></span>

<span data-ttu-id="2c576-126">Wybierz hello **bezpośrednio w dostęp maszyny Wirtualnej** Kafelek i hello **bezpośrednio w dostęp maszyny Wirtualnej** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="2c576-126">Select hello **Just in time VM access** tile and hello **Just in time VM access** blade opens.</span></span>

![Tylko w czasie dostępu do maszyny Wirtualnej kafelka][2]

<span data-ttu-id="2c576-128">Witaj **bezpośrednio w dostęp do maszyny Wirtualnej czasu** blok zawiera informacje dotyczące stanu hello maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="2c576-128">hello **Just in time VM access** blade provides information on hello state of your VMs:</span></span>

- <span data-ttu-id="2c576-129">**Skonfigurowane** -maszyn wirtualnych, które zostały skonfigurowane toosupport na wszelki dostęp maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c576-129">**Configured** - VMs that have been configured toosupport just in time VM access.</span></span> <span data-ttu-id="2c576-130">dane Hello podane dotyczy hello w ostatnim tygodniu i zawiera dla każdej maszyny Wirtualnej hello liczby żądań zatwierdzonych, Data ostatniego dostępu i czas i użytkownika, który ostatnio.</span><span class="sxs-lookup"><span data-stu-id="2c576-130">hello data presented is for hello last week and includes for each VM hello number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="2c576-131">**Zalecane** -maszyn wirtualnych, które obsługują tylko w dostęp maszyny Wirtualnej, ale nie został skonfigurowany do.</span><span class="sxs-lookup"><span data-stu-id="2c576-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="2c576-132">Zaleca się włączenie tylko w kontroli dostępu wirtualna czasu dla tych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2c576-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="2c576-133">Zobacz [włączyć tylko w przypadku maszyn wirtualnych dostęp](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="2c576-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="2c576-134">**Brak rekomendacji** -przyczyn, które mogą spowodować maszyny Wirtualnej nie toobe zalecane są:</span><span class="sxs-lookup"><span data-stu-id="2c576-134">**No recommendation** - Reasons that can cause a VM not toobe recommended are:</span></span>
  - <span data-ttu-id="2c576-135">Brak grupy NSG - hello tylko w rozwiązaniu czasu wymaga toobe NSG w miejscu.</span><span class="sxs-lookup"><span data-stu-id="2c576-135">Missing NSG - hello just in time solution requires an NSG toobe in place.</span></span>
  - <span data-ttu-id="2c576-136">Klasycznym VM - Centrum zabezpieczeń na wszelki dostęp do maszyny Wirtualnej czasu aktualnie obsługuje tylko maszyn wirtualnych wdrożonych za pośrednictwem usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2c576-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="2c576-137">Wdrożenie klasyczne nie jest obsługiwany przez hello tylko w rozwiązaniu czasu.</span><span class="sxs-lookup"><span data-stu-id="2c576-137">A classic deployment is not supported by hello just in time solution.</span></span>
  - <span data-ttu-id="2c576-138">Inne - maszyny Wirtualnej jest w tej kategorii, jeśli hello tylko w czasie, które rozwiązanie jest wyłączona w zasadach zabezpieczeń hello hello subskrypcji lub grupy zasobów hello lub że hello maszyny Wirtualnej nie ma publicznego adresu IP i nie ma grupy NSG w miejscu.</span><span class="sxs-lookup"><span data-stu-id="2c576-138">Other - A VM is in this category if hello just in time solution is turned off in hello security policy of hello subscription or hello resource group, or that hello VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="2c576-139">Konfigurowanie tylko w czasie zasad dostępu</span><span class="sxs-lookup"><span data-stu-id="2c576-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="2c576-140">Witaj tooselect maszyn wirtualnych, które mają tooenable:</span><span class="sxs-lookup"><span data-stu-id="2c576-140">tooselect hello VMs that you want tooenable:</span></span>

1. <span data-ttu-id="2c576-141">Na powitania **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz hello **zalecane** kartę.</span><span class="sxs-lookup"><span data-stu-id="2c576-141">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Włącz tylko w czasie][3]

2. <span data-ttu-id="2c576-143">W obszarze **maszyn wirtualnych**, wybierz hello maszyn wirtualnych, które mają tooenable.</span><span class="sxs-lookup"><span data-stu-id="2c576-143">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="2c576-144">Spowoduje to umieszczenie znacznikiem wyboru tooa dalej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c576-144">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="2c576-145">Wybierz **włączyć JIT na maszynach wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="2c576-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="2c576-146">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="2c576-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="2c576-147">Porty domyślne</span><span class="sxs-lookup"><span data-stu-id="2c576-147">Default ports</span></span>

<span data-ttu-id="2c576-148">Widać hello domyślnych portów, które Centrum zabezpieczeń zaleca włączenie tylko w czasie.</span><span class="sxs-lookup"><span data-stu-id="2c576-148">You can see hello default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="2c576-149">Na powitania **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz hello **zalecane** kartę.</span><span class="sxs-lookup"><span data-stu-id="2c576-149">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Wyświetlanie domyślnych portów][6]

2. <span data-ttu-id="2c576-151">W obszarze **maszyn wirtualnych**, wybierz maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="2c576-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="2c576-152">Spowoduje to umieszczenie znacznikiem wyboru dalej toohello maszyny Wirtualnej i otwiera hello **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku.</span><span class="sxs-lookup"><span data-stu-id="2c576-152">This puts a checkmark next toohello VM and opens hello **JIT VM access configuration** blade.</span></span> <span data-ttu-id="2c576-153">Ten blok Wyświetla hello domyślnych portów.</span><span class="sxs-lookup"><span data-stu-id="2c576-153">This blade displays hello default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="2c576-154">Dodawanie portów</span><span class="sxs-lookup"><span data-stu-id="2c576-154">Add ports</span></span>

<span data-ttu-id="2c576-155">Z hello **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku można również dodać i skonfigurować nowy port, na którym ma zostać hello tooenable tylko w rozwiązaniu czasu.</span><span class="sxs-lookup"><span data-stu-id="2c576-155">From hello **JIT VM access configuration** blade, you can also add and configure a new port on which you want tooenable hello just in time solution.</span></span>

1. <span data-ttu-id="2c576-156">Na powitania **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2c576-156">On hello **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="2c576-157">Spowoduje to otwarcie hello **konfiguracji portów Dodaj** bloku.</span><span class="sxs-lookup"><span data-stu-id="2c576-157">This opens hello **Add port configuration** blade.</span></span>

  ![Konfiguracja portów][7]

2. <span data-ttu-id="2c576-159">Na **konfiguracji portów Dodaj** bloku, należy określić port hello typ protokołu dozwolone źródła adresów IP i maksymalny czas żądania.</span><span class="sxs-lookup"><span data-stu-id="2c576-159">On **Add port configuration** blade, you identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="2c576-160">Dozwolone źródła adresy IP są dostęp tooget dozwolonych zakresy IP hello na żądanie zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="2c576-160">Allowed source IPs are hello IP ranges allowed tooget access upon an approved request.</span></span>

  <span data-ttu-id="2c576-161">Czas żądania maksymalna jest hello maksymalny przedział czasu można otworzyć określonego portu.</span><span class="sxs-lookup"><span data-stu-id="2c576-161">Maximum request time is hello maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="2c576-162">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2c576-162">Select **OK**.</span></span>

## <a name="requesting-access-tooa-vm"></a><span data-ttu-id="2c576-163">Żąda dostępu tooa maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c576-163">Requesting access tooa VM</span></span>

<span data-ttu-id="2c576-164">toorequest tooa dostęp do maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="2c576-164">toorequest access tooa VM:</span></span>

1. <span data-ttu-id="2c576-165">Na powitania **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz hello **skonfigurowana** kartę.</span><span class="sxs-lookup"><span data-stu-id="2c576-165">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="2c576-166">W obszarze **maszyn wirtualnych**, wybierz hello maszyn wirtualnych, które mają tooenable dostępu.</span><span class="sxs-lookup"><span data-stu-id="2c576-166">Under **VMs**, select hello VMs that you want tooenable access.</span></span> <span data-ttu-id="2c576-167">Spowoduje to umieszczenie znacznikiem wyboru tooa dalej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c576-167">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="2c576-168">Wybierz **poprosić o dostęp**.</span><span class="sxs-lookup"><span data-stu-id="2c576-168">Select **Request access**.</span></span> <span data-ttu-id="2c576-169">Spowoduje to otwarcie hello **poprosić o dostęp** bloku.</span><span class="sxs-lookup"><span data-stu-id="2c576-169">This opens hello **Request access** blade.</span></span>

  ![Żądanie dostępu tooa maszyny Wirtualnej][4]

4. <span data-ttu-id="2c576-171">Na powitania **poprosić o dostęp** bloku, należy skonfigurować dla każdej maszyny Wirtualnej hello porty tooopen wraz z źródłowy adres IP hello, który hello port jest otwarte okno czasu hello tooand dla których hello port jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="2c576-171">On hello **Request access** blade, you configure for each VM hello ports tooopen along with hello source IP that hello port is opened tooand hello time window for which hello port is opened.</span></span> <span data-ttu-id="2c576-172">Możesz poprosić o dostęp tylko toohello porty, które zostały skonfigurowane w hello tylko w czasie zasad.</span><span class="sxs-lookup"><span data-stu-id="2c576-172">You can request access only toohello ports that are configured in hello just in time policy.</span></span> <span data-ttu-id="2c576-173">Każdy port ma maksymalny czas dozwolonych pochodną hello tylko w czasie zasad.</span><span class="sxs-lookup"><span data-stu-id="2c576-173">Each port has a maximum allowed time derived from hello just in time policy.</span></span>
5. <span data-ttu-id="2c576-174">Wybierz **otworzyć porty**.</span><span class="sxs-lookup"><span data-stu-id="2c576-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="2c576-175">Edytowanie tylko w czasie zasad dostępu</span><span class="sxs-lookup"><span data-stu-id="2c576-175">Editing a just in time access policy</span></span>

<span data-ttu-id="2c576-176">Można zmienić dla maszyny Wirtualnej istniejące tylko w czasie zasad przez dodanie i skonfigurowanie nowego tooopen port dla tej maszyny Wirtualnej lub zmieniając innych parametrów powiązanych tooan już chroniona portu.</span><span class="sxs-lookup"><span data-stu-id="2c576-176">You can change a VM's existing just in time policy by adding and configuring a new port tooopen for that VM, or by changing any other parameter related tooan already protected port.</span></span>

<span data-ttu-id="2c576-177">W celu tooedit istniejące tylko w zasadach czasu maszyny wirtualnej, hello **skonfigurowana** karta jest używana:</span><span class="sxs-lookup"><span data-stu-id="2c576-177">In order tooedit an existing just in time policy of a VM, hello **Configured** tab is used:</span></span>

1. <span data-ttu-id="2c576-178">W obszarze **maszyn wirtualnych**, wybierz tooadd wirtualna tooby portu, klikając hello trzy kropki w obrębie hello wiersza dla tej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c576-178">Under **VMs**, select a VM tooadd a port tooby clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="2c576-179">Spowoduje to otwarcie menu.</span><span class="sxs-lookup"><span data-stu-id="2c576-179">This opens a menu.</span></span>
2. <span data-ttu-id="2c576-180">Wybierz **Edytuj** hello menu.</span><span class="sxs-lookup"><span data-stu-id="2c576-180">Select **Edit** in hello menu.</span></span> <span data-ttu-id="2c576-181">Spowoduje to otwarcie hello **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku.</span><span class="sxs-lookup"><span data-stu-id="2c576-181">This opens hello **JIT VM access configuration** blade.</span></span>

  ![Edytowanie zasad][8]

3. <span data-ttu-id="2c576-183">Na powitania **Konfiguracja dostępu do maszyny Wirtualnej JIT** bloku, albo można edytować istniejące ustawienia hello port już chronione, klikając jej portu lub wybrać **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2c576-183">On hello **JIT VM access configuration** blade, you can either edit hello existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="2c576-184">Spowoduje to otwarcie hello **konfiguracji portów Dodaj** bloku.</span><span class="sxs-lookup"><span data-stu-id="2c576-184">This opens hello **Add port configuration** blade.</span></span>

  ![Dodaj port][7]

4. <span data-ttu-id="2c576-186">Na **konfiguracji portów Dodaj** bloku zidentyfikować hello portu, typ protokołu źródła dozwolonych adresów IP i czas maksymalny żądania.</span><span class="sxs-lookup"><span data-stu-id="2c576-186">On **Add port configuration** blade identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="2c576-187">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2c576-187">Select **OK**.</span></span>
6. <span data-ttu-id="2c576-188">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="2c576-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="2c576-189">Inspekcja tylko w czasie działania dostępu</span><span class="sxs-lookup"><span data-stu-id="2c576-189">Auditing just in time access activity</span></span>

<span data-ttu-id="2c576-190">Aby uzyskać wgląd w działania maszyny Wirtualnej przy użyciu wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="2c576-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="2c576-191">Dzienniki tooview:</span><span class="sxs-lookup"><span data-stu-id="2c576-191">tooview logs:</span></span>

1. <span data-ttu-id="2c576-192">Na powitania **bezpośrednio w dostęp do maszyny Wirtualnej czasu** bloku, wybierz hello **skonfigurowana** kartę.</span><span class="sxs-lookup"><span data-stu-id="2c576-192">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="2c576-193">W obszarze **maszyn wirtualnych**, wybierz informacji tooview maszyny Wirtualnej o klikając hello trzy kropki w obrębie hello wiersza dla tej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2c576-193">Under **VMs**, select a VM tooview information about by clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="2c576-194">Spowoduje to otwarcie menu.</span><span class="sxs-lookup"><span data-stu-id="2c576-194">This opens a menu.</span></span>
3. <span data-ttu-id="2c576-195">Wybierz **dziennik aktywności** hello menu.</span><span class="sxs-lookup"><span data-stu-id="2c576-195">Select **Activity Log** in hello menu.</span></span> <span data-ttu-id="2c576-196">Spowoduje to otwarcie hello **dziennik aktywności** bloku.</span><span class="sxs-lookup"><span data-stu-id="2c576-196">This opens hello **Activity log** blade.</span></span>

![Wybierz dziennik aktywności][9]

<span data-ttu-id="2c576-198">Witaj **dziennik aktywności** bloku udostępnia widok filtrowany poprzednich operacji dla tej maszyny Wirtualnej oraz czas, datę i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2c576-198">hello **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Wyświetl dziennik aktywności][5]

<span data-ttu-id="2c576-200">Można pobrać informacji dziennika hello wybierając **kliknij tutaj toodownload wszystkie elementy hello CSV jako**.</span><span class="sxs-lookup"><span data-stu-id="2c576-200">You can download hello log information by selecting **Click here toodownload all hello items as CSV**.</span></span>

<span data-ttu-id="2c576-201">Zmodyfikuj hello filtry i wybrać **Zastosuj** toocreate wyszukiwania i dziennika.</span><span class="sxs-lookup"><span data-stu-id="2c576-201">Modify hello filters and select **Apply** toocreate a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="2c576-202">Przy użyciu tylko w czasie dostępu do maszyny Wirtualnej za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c576-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="2c576-203">Upewnij się, masz hello w kolejności hello toouse tylko w rozwiązaniu czasu za pomocą programu PowerShell, [najnowsze](/powershell/azure/install-azurerm-ps) wersji programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c576-203">In order toouse hello just in time solution via PowerShell, make sure you have hello [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="2c576-204">Po wykonaniu czynności należy tooinstall hello [najnowsze](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Centrum zabezpieczeń Azure z galerii programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="2c576-204">Once you do, you need tooinstall hello [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from hello PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="2c576-205">Konfigurowanie tylko w zasadach czasu dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c576-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="2c576-206">tooconfigure tylko w zasadach czasu w odpowiedniej maszyny Wirtualnej, należy toorun tego polecenia w sesji programu PowerShell: ASCJITAccessPolicy zestawu.</span><span class="sxs-lookup"><span data-stu-id="2c576-206">tooconfigure a just in time policy on a specific VM, you need toorun this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="2c576-207">Wykonaj toolearn dokumentacji polecenia cmdlet hello więcej.</span><span class="sxs-lookup"><span data-stu-id="2c576-207">Follow hello cmdlet documentation toolearn more.</span></span>

### <a name="requesting-access-tooa-vm"></a><span data-ttu-id="2c576-208">Żąda dostępu tooa maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2c576-208">Requesting access tooa VM</span></span>

<span data-ttu-id="2c576-209">Witaj tooaccess określonej maszyny Wirtualnej, który jest chroniony za pomocą tylko w rozwiązaniu do czasu, należy toorun tego polecenia w sesji programu PowerShell: ASCJITAccess wywołania.</span><span class="sxs-lookup"><span data-stu-id="2c576-209">tooaccess a specific VM that is protected with hello just in time solution, you need toorun this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="2c576-210">Wykonaj toolearn dokumentacji polecenia cmdlet hello więcej.</span><span class="sxs-lookup"><span data-stu-id="2c576-210">Follow hello cmdlet documentation toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c576-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2c576-211">Next steps</span></span>
<span data-ttu-id="2c576-212">W tym artykule przedstawiono sposób tylko w czasie dostępu do maszyny Wirtualnej w Centrum zabezpieczeń ułatwia kontroli dostępu tooyour Azure maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2c576-212">In this article, you learned how just in time VM access in Security Center helps you control access tooyour Azure virtual machines.</span></span>

<span data-ttu-id="2c576-213">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2c576-213">toolearn more about Security Center, see hello following:</span></span>

- <span data-ttu-id="2c576-214">[Ustawianie zasad zabezpieczeń](security-center-policies.md) — Dowiedz się jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="2c576-214">[Setting security policies](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="2c576-215">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c576-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="2c576-216">[Monitorowanie kondycji zabezpieczeń](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c576-216">[Security health monitoring](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
- <span data-ttu-id="2c576-217">[Reagowanie na alerty toosecurity i zarządzanie nimi](security-center-managing-and-responding-alerts.md) — Dowiedz się jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="2c576-217">[Managing and responding toosecurity alerts](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
- <span data-ttu-id="2c576-218">[Monitorowanie rozwiązań partnerskich](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="2c576-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="2c576-219">[Często zadawane pytania dotyczące Centrum zabezpieczeń](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="2c576-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
- <span data-ttu-id="2c576-220">[Blog Azure Security](https://blogs.msdn.microsoft.com/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c576-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


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
