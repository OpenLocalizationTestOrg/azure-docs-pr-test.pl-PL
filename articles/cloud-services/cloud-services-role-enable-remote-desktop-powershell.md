---
title: "Włącz połączenia pulpitu zdalnego dla roli w usług Azure Cloud Services przy użyciu programu PowerShell"
description: "Konfigurowanie aplikacji usługi chmury azure przy użyciu programu PowerShell, aby umożliwić połączenia pulpitu zdalnego"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 171f27c92ee9de14301ebb664e9ba3bcd98c394d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="1f5c2-103">Włącz połączenia pulpitu zdalnego dla roli w usług Azure Cloud Services przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f5c2-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f5c2-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1f5c2-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="1f5c2-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1f5c2-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="1f5c2-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f5c2-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="1f5c2-107">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f5c2-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="1f5c2-108">Pulpit zdalny umożliwia dostęp do pulpitu z poziomu roli uruchomionej w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="1f5c2-109">Podłączanie pulpitu zdalnego umożliwia rozwiązywanie problemów i diagnozowanie problemów z aplikacją, gdy jest on uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="1f5c2-110">W tym artykule opisano, jak można włączyć pulpitu zdalnego na role usługi w chmurze przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-110">This article describes how to enable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="1f5c2-111">Zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) wymagań wstępnych wymagane dla tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span> <span data-ttu-id="1f5c2-112">Rozszerzenie usług pulpitu zdalnego korzysta z programu PowerShell, można włączyć pulpitu zdalnego, po wdrożeniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-112">PowerShell utilizes the Remote Desktop Extension so you can enable Remote Desktop after the application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="1f5c2-113">Konfigurowanie pulpitu zdalnego z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f5c2-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="1f5c2-114">[AzureServiceRemoteDesktopExtension zestaw](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) polecenie cmdlet pozwala na włączenie pulpitu zdalnego dla określonych ról lub wszystkich ról wdrożenia usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-114">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you to enable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="1f5c2-115">Polecenie cmdlet pozwala określić nazwę użytkownika i hasło dla użytkownika pulpitu zdalnego za pośrednictwem *poświadczeń* parametr, który akceptuje obiektu PSCredential.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-115">The cmdlet lets you specify the Username and Password for the remote desktop user through the *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="1f5c2-116">Jeśli używasz programu PowerShell interaktywnego, łatwo można ustawić obiektu PSCredential przez wywołanie metody [poświadczenia Get](https://technet.microsoft.com/library/hh849815.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-116">If you are using PowerShell interactively, you can easily set the PSCredential object by calling the [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="1f5c2-117">To polecenie wyświetla okno dialogowe umożliwia wprowadzenie nazwy użytkownika i hasła dla użytkownika zdalnego w bezpieczny sposób.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-117">This command displays a dialog box allowing you to enter the username and password for the remote user in a secure manner.</span></span>

<span data-ttu-id="1f5c2-118">Ponieważ PowerShell pomaga w scenariuszach automatyzacji, można również skonfigurować **PSCredential** obiektu w taki sposób, który nie wymaga interakcji z użytkownikiem.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-118">Since PowerShell helps in automation scenarios, you can also set up the **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="1f5c2-119">Najpierw należy skonfigurować bezpieczne hasło.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-119">First, you need to set up a secure password.</span></span> <span data-ttu-id="1f5c2-120">Rozpoczynać się od określenia hasła w postaci zwykłego tekstu przekonwertować go na bezpieczny ciąg przy użyciu [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f5c2-120">You begin with specifying a plain text password convert it to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="1f5c2-121">Obok należy konwertować za pomocą zaszyfrowanego ciągu standardowego to bezpieczny ciąg [ConvertFrom SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f5c2-121">Next you need to convert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="1f5c2-122">Teraz możesz zapisać ten zaszyfrowany ciąg standardowy w pliku za pomocą [zestawu zawartości](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f5c2-122">Now you can save this encrypted standard string to a file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="1f5c2-123">Można również utworzyć plik bezpieczne hasło, dzięki czemu nie trzeba wpisywać hasło zawsze.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-123">You can also create a secure password file so that you don't have to type in the password every time.</span></span> <span data-ttu-id="1f5c2-124">Ponadto plik bezpieczne hasło jest lepszym rozwiązaniem niż zwykły plik tekstowy.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="1f5c2-125">Można utworzyć pliku bezpieczne hasło, należy użyć następującego środowiska PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1f5c2-125">Use the following PowerShell to create a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="1f5c2-126">Przy ustawianiu hasła, upewnij się, że spełniają [wymagania dotyczące złożoności](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f5c2-126">When setting the password, make sure that you meet the [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="1f5c2-127">Do tworzenia obiektu poświadczenia z pliku bezpieczne hasło, należy odczytać zawartości pliku i przekonwertować je ponownie na bezpieczny ciąg przy użyciu [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f5c2-127">To create the credential object from the secure password file, you must read the file contents and convert them back to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="1f5c2-128">[AzureServiceRemoteDesktopExtension zestaw](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) polecenia cmdlet również akceptuje *wygaśnięcia* parametr, który określa **DateTime** , w którym wygaśnięciem konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-128">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which the user account expires.</span></span> <span data-ttu-id="1f5c2-129">Można na przykład ustawić konto wygasa za kilka dni od bieżącej daty i godziny.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-129">For example, you could set the account to expire a few days from the current date and time.</span></span>

<span data-ttu-id="1f5c2-130">W tym przykładzie programu PowerShell pokazuje, jak ustawić rozszerzenie usług pulpitu zdalnego dla usługi w chmurze:</span><span class="sxs-lookup"><span data-stu-id="1f5c2-130">This PowerShell example shows you how to set the Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="1f5c2-131">Opcjonalnie można określić miejsce wdrożenia i role, które chcesz włączyć pulpitu zdalnego na.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-131">You can also optionally specify the deployment slot and roles that you want to enable remote desktop on.</span></span> <span data-ttu-id="1f5c2-132">Jeśli nie podano tych parametrów, polecenie cmdlet umożliwia pulpitu zdalnego na wszystkich ról w **produkcji** miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-132">If these parameters are not specified, the cmdlet enables remote desktop on all roles in the **Production** deployment slot.</span></span>

<span data-ttu-id="1f5c2-133">Rozszerzenie usług pulpitu zdalnego jest powiązane z wdrożeniem.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-133">The Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="1f5c2-134">W przypadku utworzenia nowego wdrożenia usługi, należy włączyć pulpitu zdalnego w tym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-134">If you create a new deployment for the service, you have to enable remote desktop on that deployment.</span></span> <span data-ttu-id="1f5c2-135">Jeśli chcesz mieć włączoną usługą Pulpit zdalny, następnie należy rozważyć włączenie skryptów programu PowerShell do przepływu pracy wdrażania.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-135">If you always want to have remote desktop enabled, then you should consider integrating the PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="1f5c2-136">Pulpit zdalny do wystąpienia roli</span><span class="sxs-lookup"><span data-stu-id="1f5c2-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="1f5c2-137">[Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) polecenia cmdlet jest używane do zdalnego pulpitu do konkretnej roli wystąpienie usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-137">The [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used to remote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="1f5c2-138">Można użyć *LocalPath* parametr, aby pobrać protokołu RDP plików lokalnie.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-138">You can use the *LocalPath* parameter to download the RDP file locally.</span></span> <span data-ttu-id="1f5c2-139">Lub użyć *uruchamianie* parametr, aby bezpośrednio uruchomić okno dialogowe Podłączanie pulpitu zdalnego, dostęp wystąpienia roli usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-139">Or you can use the *Launch* parameter to directly launch the Remote Desktop Connection dialog to access the cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="1f5c2-140">Sprawdź, czy rozszerzenie Pulpit zdalny jest włączony w usłudze</span><span class="sxs-lookup"><span data-stu-id="1f5c2-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="1f5c2-141">[Get AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) polecenie cmdlet wyświetla który pulpitu zdalnego jest włączone lub wyłączone w ramach wdrożenia usługi.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-141">The [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="1f5c2-142">Polecenie cmdlet zwraca nazwę użytkownika dla użytkownika pulpitu zdalnego i role, które włączono rozszerzenie usług pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-142">The cmdlet returns the username for the remote desktop user and the roles that the remote desktop extension is enabled for.</span></span> <span data-ttu-id="1f5c2-143">Domyślnie dzieje się tak na miejsce wdrożenia i użytkownik może użyć miejsca przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-143">By default, this happens on the deployment slot and you can choose to use the staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="1f5c2-144">Usuń rozszerzenie Pulpit zdalny z usługą</span><span class="sxs-lookup"><span data-stu-id="1f5c2-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="1f5c2-145">Jeśli została już włączona rozszerzenia pulpitu zdalnego w ramach wdrożenia i należy zaktualizować ustawienia pulpitu zdalnego, najpierw usuń rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-145">If you have already enabled the remote desktop extension on a deployment, and need to update the remote desktop settings, first remove the extension.</span></span> <span data-ttu-id="1f5c2-146">I włącz ją ponownie przy użyciu nowych ustawień.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-146">And enable it again with the new settings.</span></span> <span data-ttu-id="1f5c2-147">Jeśli na przykład aby ustawić nowe hasło dla konta użytkownika zdalnego lub wygasłe konto.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-147">For example, if you want to set a new password for the remote user account, or the account expired.</span></span> <span data-ttu-id="1f5c2-148">W ten sposób jest wymagany na istniejące wdrożenia, które mają rozszerzenie usług pulpitu zdalnego włączone.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-148">Doing this is required on existing deployments that have the remote desktop extension enabled.</span></span> <span data-ttu-id="1f5c2-149">W przypadku nowych wdrożeń można po prostu zastosować rozszerzenia bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-149">For new deployments, you can simply apply the extension directly.</span></span>

<span data-ttu-id="1f5c2-150">Aby usunąć rozszerzenia usług pulpitu zdalnego z wdrożenia, można użyć [AzureServiceRemoteDesktopExtension Usuń](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-150">To remove the remote desktop extension from the deployment, you can use the [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="1f5c2-151">Opcjonalnie można określić miejsce wdrożenia i roli, z którego chcesz usunąć rozszerzenie usług pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-151">You can also optionally specify the deployment slot and role from which you want to remove the remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="1f5c2-152">Aby całkowicie usunąć Konfiguracja rozszerzenia, należy wywołać *Usuń* polecenia cmdlet z **UninstallConfiguration** parametru.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-152">To completely remove the extension configuration, you should call the *remove* cmdlet with the **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="1f5c2-153">**UninstallConfiguration** parametru odinstalowuje żadnej konfiguracji rozszerzenia, która jest stosowana do usługi.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-153">The **UninstallConfiguration** parameter uninstalls any extension configuration that is applied to the service.</span></span> <span data-ttu-id="1f5c2-154">Konfiguracja każdego rozszerzenia jest skojarzona z konfiguracją usługi.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-154">Every extension configuration is associated with the service configuration.</span></span> <span data-ttu-id="1f5c2-155">Wywoływanie *Usuń* polecenia cmdlet bez **UninstallConfiguration** Usuwa skojarzenia <mark>wdrożenia</mark> konfiguracji rozszerzenia, co powoduje wykluczenie rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-155">Calling the *remove* cmdlet without **UninstallConfiguration** disassociates the <mark>deployment</mark> from the extension configuration, thus effectively removing the extension.</span></span> <span data-ttu-id="1f5c2-156">Jednak konfiguracja rozszerzenia pozostaje skojarzony z usługą.</span><span class="sxs-lookup"><span data-stu-id="1f5c2-156">However, the extension configuration remains associated with the service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="1f5c2-157">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1f5c2-157">Additional resources</span></span>

<span data-ttu-id="1f5c2-158">[Jak skonfigurować usługi w chmurze](cloud-services-how-to-configure.md)
[usług w chmurze — często zadawane pytania — pulpitu zdalnego](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="1f5c2-158">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
