---
title: "aaaEnable Podłączanie pulpitu zdalnego dla roli w usług Azure Cloud Services przy użyciu programu PowerShell"
description: "Jak tooconfigure platformy azure w chmurze usługi aplikacji przy użyciu programu PowerShell tooallow obsługi połączeń pulpitu zdalnego"
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
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="650f9-103">Włącz połączenia pulpitu zdalnego dla roli w usług Azure Cloud Services przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="650f9-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="650f9-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="650f9-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="650f9-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="650f9-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="650f9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="650f9-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="650f9-107">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="650f9-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="650f9-108">Pulpit zdalny umożliwia pulpitu hello tooaccess roli działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="650f9-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="650f9-109">Można użyć tootroubleshoot połączenia pulpitu zdalnego i diagnozowanie problemów z aplikacją, jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="650f9-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="650f9-110">W tym artykule opisano sposób tooenable pulpitu zdalnego na role usługi w chmurze przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="650f9-110">This article describes how tooenable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="650f9-111">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) hello wymagania wstępne wymagane dla tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="650f9-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span> <span data-ttu-id="650f9-112">PowerShell korzysta hello rozszerzenia usług pulpitu zdalnego, więc można włączyć pulpitu zdalnego, po wdrożeniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="650f9-112">PowerShell utilizes hello Remote Desktop Extension so you can enable Remote Desktop after hello application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="650f9-113">Konfigurowanie pulpitu zdalnego z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="650f9-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="650f9-114">Witaj [AzureServiceRemoteDesktopExtension zestaw](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) polecenie cmdlet pozwala tooenable pulpitu zdalnego na określone role lub wszystkie role tego wdrożenia usługi chmury.</span><span class="sxs-lookup"><span data-stu-id="650f9-114">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you tooenable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="650f9-115">polecenia cmdlet Hello pozwala określić hello nazwy użytkownika i hasła dla hello użytkownika pulpitu zdalnego za pośrednictwem hello *poświadczeń* parametr, który akceptuje obiektu PSCredential.</span><span class="sxs-lookup"><span data-stu-id="650f9-115">hello cmdlet lets you specify hello Username and Password for hello remote desktop user through hello *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="650f9-116">Jeśli używasz programu PowerShell interaktywnego, łatwo można ustawić obiektu PSCredential hello przez wywołanie hello [poświadczenia Get](https://technet.microsoft.com/library/hh849815.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="650f9-116">If you are using PowerShell interactively, you can easily set hello PSCredential object by calling hello [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="650f9-117">To polecenie wyświetla okno dialogowe, dzięki czemu możesz tooenter hello username i hasło dla użytkownika zdalnego hello w bezpieczny sposób.</span><span class="sxs-lookup"><span data-stu-id="650f9-117">This command displays a dialog box allowing you tooenter hello username and password for hello remote user in a secure manner.</span></span>

<span data-ttu-id="650f9-118">Ponieważ PowerShell pomaga w scenariuszach automatyzacji, można również skonfigurować hello **PSCredential** obiektu w taki sposób, który nie wymaga interakcji z użytkownikiem.</span><span class="sxs-lookup"><span data-stu-id="650f9-118">Since PowerShell helps in automation scenarios, you can also set up hello **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="650f9-119">Najpierw należy tooset bezpieczne hasło.</span><span class="sxs-lookup"><span data-stu-id="650f9-119">First, you need tooset up a secure password.</span></span> <span data-ttu-id="650f9-120">Rozpoczynać się od określenia hasła w postaci zwykłego tekstu przekonwertować ciągu bezpiecznego tooa przy użyciu [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="650f9-120">You begin with specifying a plain text password convert it tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="650f9-121">Następnie tooconvert parametry te będą potrzebne bezpieczny do za pomocą zaszyfrowanego ciągu standardowego [ConvertFrom SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="650f9-121">Next you need tooconvert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="650f9-122">Teraz możesz zapisać ten zaszyfrowanego ciągu standardowego tooa plików przy użyciu [zestawu zawartości](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="650f9-122">Now you can save this encrypted standard string tooa file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="650f9-123">Można także utworzyć plik bezpieczne hasło, dzięki czemu nie trzeba tootype w haśle hello zawsze.</span><span class="sxs-lookup"><span data-stu-id="650f9-123">You can also create a secure password file so that you don't have tootype in hello password every time.</span></span> <span data-ttu-id="650f9-124">Ponadto plik bezpieczne hasło jest lepszym rozwiązaniem niż zwykły plik tekstowy.</span><span class="sxs-lookup"><span data-stu-id="650f9-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="650f9-125">Użyj hello następującego środowiska PowerShell toocreate pliku bezpieczne hasło:</span><span class="sxs-lookup"><span data-stu-id="650f9-125">Use hello following PowerShell toocreate a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="650f9-126">Przy ustawianiu hasła hello, upewnij się, że spełniają hello [wymagania dotyczące złożoności](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="650f9-126">When setting hello password, make sure that you meet hello [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="650f9-127">toocreate hello obiektu poświadczenia z hello pliku bezpieczne hasło, należy odczytać zawartości pliku hello i przekonwertować je wstecz tooa bezpieczny ciąg za pomocą [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="650f9-127">toocreate hello credential object from hello secure password file, you must read hello file contents and convert them back tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="650f9-128">Witaj [AzureServiceRemoteDesktopExtension zestaw](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) polecenia cmdlet również akceptuje *wygaśnięcia* parametr, który określa **DateTime** użytkownika hello wygaśnięciem konta.</span><span class="sxs-lookup"><span data-stu-id="650f9-128">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which hello user account expires.</span></span> <span data-ttu-id="650f9-129">Na przykład można ustawić tooexpire konta hello za kilka dni od hello bieżącą datę i godzinę.</span><span class="sxs-lookup"><span data-stu-id="650f9-129">For example, you could set hello account tooexpire a few days from hello current date and time.</span></span>

<span data-ttu-id="650f9-130">W tym przykładzie programu PowerShell pokazuje, jak tooset hello rozszerzenia usług pulpitu zdalnego na usługi w chmurze:</span><span class="sxs-lookup"><span data-stu-id="650f9-130">This PowerShell example shows you how tooset hello Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="650f9-131">Można również opcjonalnie określić hello miejsce wdrożenia i role, które mają tooenable pulpitu zdalnego na.</span><span class="sxs-lookup"><span data-stu-id="650f9-131">You can also optionally specify hello deployment slot and roles that you want tooenable remote desktop on.</span></span> <span data-ttu-id="650f9-132">Jeśli nie podano tych parametrów, polecenia cmdlet hello umożliwia pulpitu zdalnego na wszystkich ról w hello **produkcji** miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="650f9-132">If these parameters are not specified, hello cmdlet enables remote desktop on all roles in hello **Production** deployment slot.</span></span>

<span data-ttu-id="650f9-133">Witaj rozszerzenia usług pulpitu zdalnego jest powiązane z wdrożeniem.</span><span class="sxs-lookup"><span data-stu-id="650f9-133">hello Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="650f9-134">Jeśli utworzysz nowe wdrożenie usługi hello masz tooenable pulpitu zdalnego w tym wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="650f9-134">If you create a new deployment for hello service, you have tooenable remote desktop on that deployment.</span></span> <span data-ttu-id="650f9-135">Zawsze należy toohave pulpitu zdalnego włączyć następnie należy rozważyć włączenie hello skryptów programu PowerShell do przepływu pracy wdrażania.</span><span class="sxs-lookup"><span data-stu-id="650f9-135">If you always want toohave remote desktop enabled, then you should consider integrating hello PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="650f9-136">Pulpit zdalny do wystąpienia roli</span><span class="sxs-lookup"><span data-stu-id="650f9-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="650f9-137">Witaj [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) polecenia cmdlet jest używane tooremote pulpitu do konkretnej roli wystąpienie usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="650f9-137">hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used tooremote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="650f9-138">Można użyć hello *LocalPath* hello toodownload parametru RDP plików lokalnie.</span><span class="sxs-lookup"><span data-stu-id="650f9-138">You can use hello *LocalPath* parameter toodownload hello RDP file locally.</span></span> <span data-ttu-id="650f9-139">Możesz użyć hello *uruchamianie* parametru toodirectly uruchamiania hello Podłączanie pulpitu zdalnego w oknie dialogowym tooaccess hello wystąpienia roli usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="650f9-139">Or you can use hello *Launch* parameter toodirectly launch hello Remote Desktop Connection dialog tooaccess hello cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="650f9-140">Sprawdź, czy rozszerzenie Pulpit zdalny jest włączony w usłudze</span><span class="sxs-lookup"><span data-stu-id="650f9-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="650f9-141">Witaj [Get AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) polecenie cmdlet wyświetla który pulpitu zdalnego jest włączone lub wyłączone w ramach wdrożenia usługi.</span><span class="sxs-lookup"><span data-stu-id="650f9-141">hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="650f9-142">polecenie cmdlet Hello zwraca username hello hello użytkownika pulpitu zdalnego i hello ról, które rozszerzenia usług pulpitu zdalnego hello jest włączone dla.</span><span class="sxs-lookup"><span data-stu-id="650f9-142">hello cmdlet returns hello username for hello remote desktop user and hello roles that hello remote desktop extension is enabled for.</span></span> <span data-ttu-id="650f9-143">Domyślnie dzieje się tak na powitania miejsce wdrożenia i hello toouse przemieszczania miejsca zamiast tego można wybrać.</span><span class="sxs-lookup"><span data-stu-id="650f9-143">By default, this happens on hello deployment slot and you can choose toouse hello staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="650f9-144">Usuń rozszerzenie Pulpit zdalny z usługą</span><span class="sxs-lookup"><span data-stu-id="650f9-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="650f9-145">Jeśli została już włączona hello rozszerzenia usług pulpitu zdalnego w ramach wdrożenia i wymagają tooupdate hello ustawienia pulpitu zdalnego, należy najpierw usunąć hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="650f9-145">If you have already enabled hello remote desktop extension on a deployment, and need tooupdate hello remote desktop settings, first remove hello extension.</span></span> <span data-ttu-id="650f9-146">I włącz ją ponownie przy hello nowych ustawień.</span><span class="sxs-lookup"><span data-stu-id="650f9-146">And enable it again with hello new settings.</span></span> <span data-ttu-id="650f9-147">Na przykład jeśli chcesz, aby tooset nowe hasło dla konta użytkownika zdalnego hello, lub konta hello wygasł.</span><span class="sxs-lookup"><span data-stu-id="650f9-147">For example, if you want tooset a new password for hello remote user account, or hello account expired.</span></span> <span data-ttu-id="650f9-148">W ten sposób jest wymagany dla istniejącego wdrożenia, których hello zdalnego pulpitu rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="650f9-148">Doing this is required on existing deployments that have hello remote desktop extension enabled.</span></span> <span data-ttu-id="650f9-149">W przypadku nowych wdrożeń można po prostu zastosować rozszerzenia hello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="650f9-149">For new deployments, you can simply apply hello extension directly.</span></span>

<span data-ttu-id="650f9-150">tooremove hello zdalnego pulpitu rozszerzenie z wdrożenia hello, można użyć hello [AzureServiceRemoteDesktopExtension Usuń](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="650f9-150">tooremove hello remote desktop extension from hello deployment, you can use hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="650f9-151">Opcjonalnie można określić miejsce wdrożenia hello i roli, z którego mają rozszerzenia usług pulpitu zdalnego hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="650f9-151">You can also optionally specify hello deployment slot and role from which you want tooremove hello remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="650f9-152">Konfiguracja rozszerzenia hello Usuń toocompletely, należy wywołać hello *Usuń* polecenia cmdlet z hello **UninstallConfiguration** parametru.</span><span class="sxs-lookup"><span data-stu-id="650f9-152">toocompletely remove hello extension configuration, you should call hello *remove* cmdlet with hello **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="650f9-153">Witaj **UninstallConfiguration** parametru odinstalowuje żadnej konfiguracji rozszerzenia czyli zastosowane toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="650f9-153">hello **UninstallConfiguration** parameter uninstalls any extension configuration that is applied toohello service.</span></span> <span data-ttu-id="650f9-154">Konfiguracja każdego rozszerzenia jest skojarzona z konfiguracją usługi hello.</span><span class="sxs-lookup"><span data-stu-id="650f9-154">Every extension configuration is associated with hello service configuration.</span></span> <span data-ttu-id="650f9-155">Wywoływanie hello *Usuń* polecenia cmdlet bez **UninstallConfiguration** Usuwa skojarzenia hello <mark>wdrożenia</mark> hello rozszerzenia konfiguracji, co powoduje wykluczenie rozszerzenie Hello.</span><span class="sxs-lookup"><span data-stu-id="650f9-155">Calling hello *remove* cmdlet without **UninstallConfiguration** disassociates hello <mark>deployment</mark> from hello extension configuration, thus effectively removing hello extension.</span></span> <span data-ttu-id="650f9-156">Jednak konfiguracja rozszerzenia hello pozostaje skojarzony z usługą hello.</span><span class="sxs-lookup"><span data-stu-id="650f9-156">However, hello extension configuration remains associated with hello service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="650f9-157">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="650f9-157">Additional resources</span></span>

<span data-ttu-id="650f9-158">[Jak usługi w chmurze tooConfigure](cloud-services-how-to-configure.md)
[usług w chmurze — często zadawane pytania — pulpitu zdalnego](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="650f9-158">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
