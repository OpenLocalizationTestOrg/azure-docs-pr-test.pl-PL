---
title: "listy kontroli aaaManage dostępu do punktu końcowego platformy Azure | PowerShell | Klasycznym | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage listy kontroli dostępu przy użyciu programu PowerShell"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a><span data-ttu-id="1c312-103">Zarządzanie listami kontroli dostępu do punktu końcowego w hello klasycznego modelu wdrażania przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c312-103">Manage endpoint access control lists using PowerShell in hello classic deployment model</span></span>
<span data-ttu-id="1c312-104">Można tworzyć i zarządzać sieci listy kontroli dostępu (ACL) dla punktów końcowych przy użyciu programu Azure PowerShell lub w hello portalu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="1c312-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in hello Management Portal.</span></span> <span data-ttu-id="1c312-105">W tym temacie znajdziesz procedury ACL typowych zadań, które można wykonać przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c312-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="1c312-106">Listę hello programu Azure PowerShell zawiera polecenia cmdlet [poleceń cmdlet do zarządzania Azure](http://go.microsoft.com/fwlink/?LinkId=317721).</span><span class="sxs-lookup"><span data-stu-id="1c312-106">For hello list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="1c312-107">Aby uzyskać więcej informacji na temat listy kontroli dostępu, zobacz [co to jest sieć listy kontroli dostępu (ACL)?](virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="1c312-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="1c312-108">Toomanage Twojego listy ACL za pomocą portalu zarządzania hello, zobacz [jak tooSet się punkty końcowe tooa maszyny wirtualnej](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c312-108">If you want toomanage your ACLs by using hello Management Portal, see [How tooSet Up Endpoints tooa Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="1c312-109">Zarządzanie listy kontroli dostępu w sieci za pomocą programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c312-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="1c312-110">Można użyć toocreate poleceń cmdlet programu Azure PowerShell, usuwania i konfigurowania (set) sieci listy kontroli dostępu (ACL).</span><span class="sxs-lookup"><span data-stu-id="1c312-110">You can use Azure PowerShell cmdlets toocreate, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="1c312-111">Kilka przykładów niektórych hello sposobów konfigurowania listy ACL za pomocą środowiska PowerShell zostały włączone.</span><span class="sxs-lookup"><span data-stu-id="1c312-111">We've included a few examples of some of hello ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="1c312-112">tooretrieve pełną listę hello poleceń cmdlet programu PowerShell listy ACL, możesz użyć dowolnej z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="1c312-112">tooretrieve a complete list of hello ACL PowerShell cmdlets, you can use either of hello following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="1c312-113">Utwórz ACL sieci przy użyciu reguł, które zezwalają na dostęp z podsieci zdalnej</span><span class="sxs-lookup"><span data-stu-id="1c312-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="1c312-114">Hello w poniższym przykładzie przedstawiono sposób toocreate nowej listy ACL, który zawiera reguły.</span><span class="sxs-lookup"><span data-stu-id="1c312-114">hello example below illustrates a way toocreate a new ACL that contains rules.</span></span> <span data-ttu-id="1c312-115">Ta lista ACL jest następnie stosowany tooa punktu końcowego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1c312-115">This ACL is then applied tooa virtual machine endpoint.</span></span> <span data-ttu-id="1c312-116">reguły listy ACL Hello w poniższym przykładzie hello będzie zezwalał na dostęp z podsieci zdalnej.</span><span class="sxs-lookup"><span data-stu-id="1c312-116">hello ACL rules in hello example below will allow access from a remote subnet.</span></span> <span data-ttu-id="1c312-117">toocreate nową listę ACL sieci przy użyciu reguł zezwalania na dla podsieci zdalnej, Otwórz program Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="1c312-117">toocreate a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="1c312-118">Skopiuj i wklej skrypt hello poniżej, konfigurując skrypt hello z własne wartości, a następnie uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="1c312-118">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="1c312-119">Utwórz hello nowy obiekt listy ACL sieci.</span><span class="sxs-lookup"><span data-stu-id="1c312-119">Create hello new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="1c312-120">Ustaw regułę, która pozwala na dostęp z podsieci zdalnej.</span><span class="sxs-lookup"><span data-stu-id="1c312-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="1c312-121">W poniższym przykładzie hello, Ustaw regułę *100* (które mają pierwszeństwo przed reguły 200 lub nowszy) podsieci zdalnej hello tooallow *10.0.0.0/8* dostępu toohello punktu końcowego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1c312-121">In hello example below, you set rule *100* (which has priority over rule 200 and higher) tooallow hello remote subnet *10.0.0.0/8* access toohello virtual machine endpoint.</span></span> <span data-ttu-id="1c312-122">Zastąp wartości hello z wymaganiami konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1c312-122">Replace hello values with your own configuration requirements.</span></span> <span data-ttu-id="1c312-123">Nazwa Hello "Konfiguracji ACL programu SharePoint" należy zastąpić o przyjaznej nazwie hello mają toocall tej reguły.</span><span class="sxs-lookup"><span data-stu-id="1c312-123">hello name "SharePoint ACL config" should be replaced with hello friendly name that you want toocall this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="1c312-124">Dodatkowe reguły powtórz polecenie cmdlet hello, zastępując wartości hello z wymaganiami konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1c312-124">For additional rules, repeat hello cmdlet, replacing hello values with your own configuration requirements.</span></span> <span data-ttu-id="1c312-125">Należy się toochange hello reguły kolejności tooreflect hello kolejności w której ma zostać hello toobe zasady zastosowane.</span><span class="sxs-lookup"><span data-stu-id="1c312-125">Be sure toochange hello rule number Order tooreflect hello order in which you want hello rules toobe applied.</span></span> <span data-ttu-id="1c312-126">Witaj mniejszą liczbę reguł mają pierwszeństwo przed hello większą liczbę.</span><span class="sxs-lookup"><span data-stu-id="1c312-126">hello lower rule number takes precedence over hello higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="1c312-127">Następnie można utworzyć nowy punkt końcowy (Dodaj) lub ustawić hello listy ACL dla istniejącego punktu końcowego (Set).</span><span class="sxs-lookup"><span data-stu-id="1c312-127">Next, you can either create a new endpoint (Add) or set hello ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="1c312-128">W tym przykładzie dodamy, że nowy punkt końcowy maszyny wirtualnej o nazwie "web" oraz aktualizacji hello punktu końcowego maszyny wirtualnej z hello ustawień list ACL.</span><span class="sxs-lookup"><span data-stu-id="1c312-128">In this example, we will add a new virtual machine endpoint called "web" and update hello virtual machine endpoint with hello ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="1c312-129">Następnie połączyć polecenia cmdlet hello i uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="1c312-129">Next, combine hello cmdlets and run hello script.</span></span> <span data-ttu-id="1c312-130">Na przykład hello połączonych poleceń cmdlet będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="1c312-130">For this example, hello combined cmdlets would look like this:</span></span>
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="1c312-131">Usuń regułę listy ACL sieci, która pozwala na dostęp z podsieci zdalnej</span><span class="sxs-lookup"><span data-stu-id="1c312-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="1c312-132">Witaj w poniższym przykładzie przedstawiono sposób tooremove reguły listy ACL sieci.</span><span class="sxs-lookup"><span data-stu-id="1c312-132">hello example below illustrates a way tooremove a network ACL rule.</span></span>  <span data-ttu-id="1c312-133">tooremove reguły list kontroli dostępu w sieci za pomocą zezwolenia reguł dla podsieci zdalnej, Otwórz program Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="1c312-133">tooremove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="1c312-134">Skopiuj i wklej skrypt hello poniżej, konfigurując skrypt hello z własne wartości, a następnie uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="1c312-134">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="1c312-135">Pierwszym krokiem jest obiektu ACL sieci hello tooget hello punktu końcowego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1c312-135">First step is tooget hello Network ACL object for hello virtual machine endpoint.</span></span> <span data-ttu-id="1c312-136">Aby następnie usunąć hello reguły listy ACL.</span><span class="sxs-lookup"><span data-stu-id="1c312-136">You'll then remove hello ACL rule.</span></span> <span data-ttu-id="1c312-137">W takim przypadku możemy usunięcie go przez identyfikator reguły.</span><span class="sxs-lookup"><span data-stu-id="1c312-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="1c312-138">Identyfikator reguły hello 0 spowoduje usunięcie tylko ze hello listy ACL.</span><span class="sxs-lookup"><span data-stu-id="1c312-138">This will only remove hello rule ID 0 from hello ACL.</span></span> <span data-ttu-id="1c312-139">Nie powoduje usunięcia obiektu ACL hello z hello punktu końcowego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1c312-139">It does not remove hello ACL object from hello virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="1c312-140">Następnie należy zastosować punktu końcowego maszyny wirtualnej toohello obiektu ACL sieci hello i zaktualizować hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1c312-140">Next, you must apply hello Network ACL object toohello virtual machine endpoint and update hello virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="1c312-141">Usuń ACL sieci z punktu końcowego maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="1c312-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="1c312-142">W niektórych scenariuszach może być tooremove obiektu ACL sieci z punktu końcowego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1c312-142">In certain scenarios, you might want tooremove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="1c312-143">toodo, który Otwórz program Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="1c312-143">toodo that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="1c312-144">Skopiuj i wklej skrypt hello poniżej, konfigurując skrypt hello z własne wartości, a następnie uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="1c312-144">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="1c312-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1c312-145">Next steps</span></span>
[<span data-ttu-id="1c312-146">Co to jest sieć listy kontroli dostępu (ACL)?</span><span class="sxs-lookup"><span data-stu-id="1c312-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)

