---
title: zasoby aaaVariable automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Zmienna zasoby są wartości, które są dostępne tooall elementów runbook i konfiguracji DSC automatyzacji Azure.  W tym artykule opisano szczegóły hello zmiennych i w jaki sposób toowork z nimi w tworzeniu zarówno tekstową i graficznego."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="31553-104">Zasoby zmiennej usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="31553-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="31553-105">Zmienna zasoby są wartości, które są dostępne tooall elementów runbook i konfiguracji DSC na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="31553-105">Variable assets are values that are available tooall runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="31553-106">Można je utworzyć, zmodyfikować i pobierane z hello portalu Azure, programu Windows PowerShell, a za pomocą elementu runbook lub konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="31553-106">They can be created, modified, and retrieved from hello Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="31553-107">Zmienne automatyzacji to przydatne w przypadku hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="31553-107">Automation variables are useful for hello following scenarios:</span></span>

- <span data-ttu-id="31553-108">Udostępnienie wartości dla wielu elementów runbook lub konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="31553-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="31553-109">Udostępnienie wartości dla wielu zadań z hello konfiguracji DSC lub tego samego elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="31553-109">Share a value between multiple jobs from hello same runbook or DSC configuration.</span></span>

- <span data-ttu-id="31553-110">Zarządzanie wartością z portalu hello lub hello wiersz polecenia programu Windows PowerShell, który jest używany przez elementy runbook lub konfiguracji DSC, takiego jak zestaw wspólne elementy konfiguracji, takie jak określonej listy nazw maszyn wirtualnych określonej grupy zasobów, nazwa domeny usługi AD, itp.</span><span class="sxs-lookup"><span data-stu-id="31553-110">Manage a value from hello portal or from hello Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="31553-111">Zmienne automatyzacji są trwałe, dlatego nadal toobe dostępne nawet wtedy, gdy element runbook hello lub konfiguracji DSC nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="31553-111">Automation variables are persisted so that they continue toobe available even if hello runbook or DSC configuration fails.</span></span>  <span data-ttu-id="31553-112">Umożliwia to także toobe wartości, ustawione przez jeden element runbook, który następnie jest używany przez inny lub jest używany przez hello tego samego elementu runbook lub hello konfiguracji DSC następnym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="31553-112">This also allows a value toobe set by one runbook that is then used by another, or is used by hello same runbook or DSC configuration hello next time that it is run.</span></span>

<span data-ttu-id="31553-113">Po utworzeniu zmiennej możesz określić on być przechowywany zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="31553-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="31553-114">Gdy zmienna jest zaszyfrowana, jest bezpiecznie przechowywana w automatyzacji Azure i jego wartość nie można pobrać z hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) polecenia cmdlet, które wchodzi w skład hello modułu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31553-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of hello Azure PowerShell module.</span></span>  <span data-ttu-id="31553-115">Witaj jedynym sposobem można pobrać zaszyfrowaną wartość pochodzi z hello **Get-AutomationVariable** działania elementu runbook lub konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="31553-115">hello only way that an encrypted value can be retrieved is from hello **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="31553-116">Bezpiecznych zasobów w automatyzacji Azure obejmują poświadczeń, certyfikatów, połączeń i szyfrowane zmienne.</span><span class="sxs-lookup"><span data-stu-id="31553-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="31553-117">Te zasoby są szyfrowane i przechowywane w hello automatyzacji Azure za pomocą Unikatowy klucz, który jest generowany dla każdego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="31553-117">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="31553-118">Ten klucz jest zaszyfrowany za pomocą certyfikatu głównego i przechowywane w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="31553-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="31553-119">Przed zapisaniem zabezpieczonym zasobem, hello klucza dla konta automatyzacji hello jest odszyfrowywany za pomocą certyfikatu głównego hello i służyły tooencrypt hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="31553-119">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="31553-120">Typy zmiennych</span><span class="sxs-lookup"><span data-stu-id="31553-120">Variable types</span></span>

<span data-ttu-id="31553-121">Po utworzeniu zmiennej z hello portalu Azure, należy określić typ danych z listy rozwijanej hello tak hello portalu można wyświetlić hello odpowiednią kontrolkę dla wartości zmiennej hello.</span><span class="sxs-lookup"><span data-stu-id="31553-121">When you create a variable with hello Azure portal, you must specify a data type from hello drop-down list so hello portal can display hello appropriate control for entering hello variable value.</span></span> <span data-ttu-id="31553-122">Zmienna Hello nie jest ograniczone toothis danych typu, ale musisz ustawić zmiennej hello przy użyciu programu Windows PowerShell, jeśli chcesz, aby toospecify wartość innego typu.</span><span class="sxs-lookup"><span data-stu-id="31553-122">hello variable is not restricted toothis data type, but you must set hello variable using Windows PowerShell if you want toospecify a value of a different type.</span></span> <span data-ttu-id="31553-123">Jeśli określisz **nie zdefiniowano**, a następnie hello hello zmiennej zostanie ustawiona zbyt**$null**, i należy ustawić wartość hello z hello [AzureAutomationVariable zestaw](http://msdn.microsoft.com/library/dn913767.aspx) polecenia cmdlet lub **Set-AutomationVariable** działania.</span><span class="sxs-lookup"><span data-stu-id="31553-123">If you specify **Not defined**, then hello value of hello variable will be set too**$null**, and you must set hello value with hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="31553-124">Nie można utworzyć ani zmienić hello wartość dla typu zmienną złożone w portalu hello, ale można podać wartości typu przy użyciu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31553-124">You cannot create or change hello value for a complex variable type in hello portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="31553-125">Typy złożone zostaną zwrócone jako [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="31553-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="31553-126">Można przechowywać wiele wartości tooa pojedynczą zmienną, tworząc tablicy lub tablica skrótów i zapisać go toohello zmiennej.</span><span class="sxs-lookup"><span data-stu-id="31553-126">You can store multiple values tooa single variable by creating an array or hashtable and saving it toohello variable.</span></span>

<span data-ttu-id="31553-127">Witaj poniżej przedstawiono listę typów zmiennych, które są dostępne w automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="31553-127">hello following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="31553-128">Ciąg</span><span class="sxs-lookup"><span data-stu-id="31553-128">String</span></span>
* <span data-ttu-id="31553-129">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="31553-129">Integer</span></span>
* <span data-ttu-id="31553-130">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="31553-130">DateTime</span></span>
* <span data-ttu-id="31553-131">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="31553-131">Boolean</span></span>
* <span data-ttu-id="31553-132">Wartość null</span><span class="sxs-lookup"><span data-stu-id="31553-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="31553-133">Działania poleceń cmdlet i przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="31553-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="31553-134">polecenia cmdlet Hello w hello w poniższej tabeli są używane toocreate zmiennych i zarządzania nimi automatyzacji przy użyciu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31553-134">hello cmdlets in hello following table are used toocreate and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="31553-135">One dostarczane jako część hello [modułu Azure PowerShell](../powershell-install-configure.md) która jest dostępna na potrzeby automatyzacji elementów runbook i konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="31553-135">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="31553-136">Polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="31553-136">Cmdlets</span></span>|<span data-ttu-id="31553-137">Opis</span><span class="sxs-lookup"><span data-stu-id="31553-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="31553-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="31553-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="31553-139">Pobiera hello wartość istniejącej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="31553-139">Retrieves hello value of an existing variable.</span></span>|
|[<span data-ttu-id="31553-140">Nowe AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="31553-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="31553-141">Tworzy nową zmienną i ustawia jej wartość.</span><span class="sxs-lookup"><span data-stu-id="31553-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="31553-142">Usuń AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="31553-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="31553-143">Usuwa istniejącej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="31553-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="31553-144">Zestaw AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="31553-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="31553-145">Ustawia hello wartość istniejącej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="31553-145">Sets hello value for an existing variable.</span></span>|

<span data-ttu-id="31553-146">Hello działań przepływu pracy w poniższej tabeli hello są używane tooaccess zmienne automatyzacji w elemencie runbook.</span><span class="sxs-lookup"><span data-stu-id="31553-146">hello workflow activities in hello following table are used tooaccess Automation variables in a runbook.</span></span> <span data-ttu-id="31553-147">Są dostępne tylko dla elementu runbook lub konfiguracji DSC i nie są dostarczane jako część hello modułu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31553-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of hello Azure PowerShell module.</span></span>

|<span data-ttu-id="31553-148">Działania przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="31553-148">Workflow Activities</span></span>|<span data-ttu-id="31553-149">Opis</span><span class="sxs-lookup"><span data-stu-id="31553-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="31553-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="31553-150">Get-AutomationVariable</span></span>|<span data-ttu-id="31553-151">Pobiera hello wartość istniejącej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="31553-151">Retrieves hello value of an existing variable.</span></span>|
|<span data-ttu-id="31553-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="31553-152">Set-AutomationVariable</span></span>|<span data-ttu-id="31553-153">Ustawia hello wartość istniejącej zmiennej.</span><span class="sxs-lookup"><span data-stu-id="31553-153">Sets hello value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="31553-154">Należy unikać używania zmiennych w hello — Nazwa parametru **Get-AutomationVariable** runbook lub konfiguracji DSC, ponieważ może to skomplikować wykrywanie zależności między elementami runbook lub konfiguracji DSC automatyzacji zmienne w czasie projektowania.</span><span class="sxs-lookup"><span data-stu-id="31553-154">You should avoid using variables in hello –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="31553-155">Tworzenie nowej zmiennej automatyzacji</span><span class="sxs-lookup"><span data-stu-id="31553-155">Creating a new Automation variable</span></span>

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a><span data-ttu-id="31553-156">toocreate nową zmienną z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="31553-156">toocreate a new variable with hello Azure portal</span></span>

1. <span data-ttu-id="31553-157">Twoje konto usługi Automatyzacja kliknij hello **zasoby** Kafelek, a następnie na powitania **zasoby** bloku, wybierz opcję **zmienne**.</span><span class="sxs-lookup"><span data-stu-id="31553-157">From your Automation account, click hello **Assets** tile and then on hello **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="31553-158">Na powitania **zmienne** kafelka, wybierz opcję **dodać zmienną**.</span><span class="sxs-lookup"><span data-stu-id="31553-158">On hello **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="31553-159">Uzupełnij opcje hello na powitania **nową zmienną** bloku i kliknij przycisk **Utwórz** Zapisz nową zmienną hello.</span><span class="sxs-lookup"><span data-stu-id="31553-159">Complete hello options on hello **New Variable** blade and click **Create** save hello new variable.</span></span>

### <a name="toocreate-a-new-variable-with-windows-powershell"></a><span data-ttu-id="31553-160">toocreate nową zmienną za pomocą programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="31553-160">toocreate a new variable with Windows PowerShell</span></span>

<span data-ttu-id="31553-161">Witaj [AzureRmAutomationVariable nowy](https://msdn.microsoft.com/library/mt603613.aspx) polecenie cmdlet tworzy nową zmienną i ustawia wartość początkową.</span><span class="sxs-lookup"><span data-stu-id="31553-161">hello [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="31553-162">Można pobrać przy użyciu wartości hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="31553-162">You can retrieve hello value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="31553-163">Jeśli wartość hello jest typem prostym, zwracany jest tego samego typu.</span><span class="sxs-lookup"><span data-stu-id="31553-163">If hello value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="31553-164">Jeśli jest to typ złożony, a następnie **PSCustomObject** jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="31553-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="31553-165">Hello następujące przykładowe polecenia Pokaż jak toocreate zmiennej typu string, a następnie zwracają wartość.</span><span class="sxs-lookup"><span data-stu-id="31553-165">hello following sample commands show how toocreate a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="31553-166">Hello następujące przykładowe polecenia Pokaż jak toocreate zmiennej o złożony typem, a następnie zwracają jego właściwości.</span><span class="sxs-lookup"><span data-stu-id="31553-166">hello following sample commands show how toocreate a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="31553-167">W takim przypadku obiekt maszyny wirtualnej z **Get-AzureRmVm** jest używany.</span><span class="sxs-lookup"><span data-stu-id="31553-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="31553-168">Użycie zmiennej w element runbook lub konfiguracji DSC</span><span class="sxs-lookup"><span data-stu-id="31553-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="31553-169">Użyj hello **Set-AutomationVariable** działania tooset hello wartości zmiennej automatyzacji elementu runbook lub Konfiguracja DSC oraz hello **Get-AutomationVariable** tooretrieve go.</span><span class="sxs-lookup"><span data-stu-id="31553-169">Use hello **Set-AutomationVariable** activity tooset hello value of an Automation variable in a runbook or DSC configuration, and hello **Get-AutomationVariable** tooretrieve it.</span></span>  <span data-ttu-id="31553-170">Nie można używać hello **AzureAutomationVariable zestaw** lub **Get-AzureAutomationVariable** polecenia cmdlet w element runbook lub konfiguracji DSC, ponieważ są mniej wydajne niż hello działania przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="31553-170">You shouldn't use hello **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than hello workflow activities.</span></span>  <span data-ttu-id="31553-171">Również nie można pobrać wartości hello bezpiecznego zmiennych z **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="31553-171">You also cannot retrieve hello value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="31553-172">Witaj tylko sposób toocreate nową zmienną z wewnątrz elementu runbook lub konfiguracji DSC jest toouse hello [AzureAutomationVariable nowy](http://msdn.microsoft.com/library/dn913771.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31553-172">hello only way toocreate a new variable from within a runbook or DSC configuration is toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="31553-173">Przykłady tekstowy</span><span class="sxs-lookup"><span data-stu-id="31553-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="31553-174">Ustawianie i pobieranie prostych wartości zmiennych</span><span class="sxs-lookup"><span data-stu-id="31553-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="31553-175">Hello następujące przykładowe polecenia Pokaż jak tooset i pobierania zmiennej w elemencie runbook tekstową.</span><span class="sxs-lookup"><span data-stu-id="31553-175">hello following sample commands show how tooset and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="31553-176">W tym przykładzie zakłada się, że zmienne typu całkowitoliczbowego o nazwie *NumberOfIterations* i *NumberOfRunnings* oraz zmienna typu ciąg o nazwie *SampleMessage* zostały już utworzone.</span><span class="sxs-lookup"><span data-stu-id="31553-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="31553-177">Ustawianie i pobieranie obiekt złożony w zmiennej</span><span class="sxs-lookup"><span data-stu-id="31553-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="31553-178">Hello następujące przykładowy kod przedstawia sposób tooupdate zmiennej w tekstowy złożona wartość.</span><span class="sxs-lookup"><span data-stu-id="31553-178">hello following sample code shows how tooupdate a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="31553-179">W tym przykładzie maszyny wirtualnej platformy Azure są pobierane z **Get-AzureVM** i zapisane tooan istniejącej zmiennej automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="31553-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="31553-180">Zgodnie z objaśnieniem w [typy zmiennych](#variable-types), to jest przechowywana jako PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="31553-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="31553-181">W hello następującego kodu hello wartość jest pobierana z maszyny wirtualnej hello toostart zmiennej i używany hello.</span><span class="sxs-lookup"><span data-stu-id="31553-181">In hello following code, hello value is retrieved from hello variable and used toostart hello virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="31553-182">Ustawiania i pobierania kolekcję w zmiennej</span><span class="sxs-lookup"><span data-stu-id="31553-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="31553-183">Hello następujące przykładowy kod przedstawia sposób toouse zmienną z kolekcją złożonych wartości tekstowej elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="31553-183">hello following sample code shows how toouse a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="31553-184">W tym przykładzie wiele maszyn wirtualnych platformy Azure są pobierane z **Get-AzureVM** i zapisane tooan istniejącej zmiennej automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="31553-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="31553-185">Zgodnie z objaśnieniem w [typy zmiennych](#variable-types), to jest przechowywane jako zbiór PSCustomObjects.</span><span class="sxs-lookup"><span data-stu-id="31553-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="31553-186">W hello następującego kodu kolekcji hello są pobierane z hello zmiennej i używać toostart każdej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="31553-186">In hello following code, hello collection is retrieved from hello variable and used toostart each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="31553-187">Przykłady graficznym elementem runbook</span><span class="sxs-lookup"><span data-stu-id="31553-187">Graphical runbook samples</span></span>

<span data-ttu-id="31553-188">W graficznym elementem runbook, należy dodać hello **Get-AutomationVariable** lub **Set-AutomationVariable** hello zmiennej w okienku Biblioteka hello edytora graficznego usługi hello prawym przyciskiem myszy i wybierając hello działanie, które mają.</span><span class="sxs-lookup"><span data-stu-id="31553-188">In a graphical runbook, you add hello **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on hello variable in hello Library pane of hello graphical editor and selecting hello activity you want.</span></span>

![Dodawanie zmiennej toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="31553-190">Ustawianie wartości w zmiennej</span><span class="sxs-lookup"><span data-stu-id="31553-190">Setting values in a variable</span></span>
<span data-ttu-id="31553-191">Witaj poniższej ilustracji przedstawiono przykładowe działania tooupdate zmiennej z prostą wartością w graficznym elementem runbook.</span><span class="sxs-lookup"><span data-stu-id="31553-191">hello following image shows sample activities tooupdate a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="31553-192">W tym przykładzie jednej maszyny wirtualnej platformy Azure są pobierane z **Get-AzureRmVM** i nazwa komputera hello jest zapisywany tooan istniejącej zmiennej automatyzacji z typu String.</span><span class="sxs-lookup"><span data-stu-id="31553-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and hello computer name is saved tooan existing Automation variable with a type of String.</span></span>  <span data-ttu-id="31553-193">Nie ma znaczenia, czy hello [jest link potoku lub sekwencji](automation-graphical-authoring-intro.md#links-and-workflow) ponieważ oczekuje tylko jednego obiektu w danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="31553-193">It doesn't matter whether hello [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in hello output.</span></span>

![Zestaw prostej zmiennej](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="31553-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="31553-195">Next Steps</span></span>

* <span data-ttu-id="31553-196">Zobacz toolearn więcej informacji na temat łączenie działań w tworzeniu graficznego [łącza w tworzeniu graficznego](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="31553-196">toolearn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="31553-197">tooget wprowadzenie do graficznych elementów runbook, zobacz [Mój pierwszy graficznym elementem runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="31553-197">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

