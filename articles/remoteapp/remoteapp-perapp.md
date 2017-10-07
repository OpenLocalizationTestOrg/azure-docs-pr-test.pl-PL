---
title: "aaaPublish aplikacji tooindividual użytkowników w kolekcji usługi Azure RemoteApp (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak opublikować aplikacje tooindividual użytkowników, a nie w zależności od grup w usłudze Azure RemoteApp."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a><span data-ttu-id="68736-103">Publikowanie aplikacji tooindividual użytkowników w kolekcji usługi Azure RemoteApp (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="68736-103">Publish applications tooindividual users in an Azure RemoteApp collection (Preview)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="68736-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="68736-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="68736-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="68736-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="68736-106">W tym artykule opisano sposób toopublish aplikacji tooindividual użytkowników w kolekcji usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="68736-106">This article explains how toopublish applications tooindividual users in an Azure RemoteApp collection.</span></span> <span data-ttu-id="68736-107">To jest nowa funkcja w usłudze Azure RemoteApp, obecnie w prywatnej wersji zapoznawczej i dostępne tooselect tylko pierwszych użytkowników do celów oceny.</span><span class="sxs-lookup"><span data-stu-id="68736-107">This is new functionality in Azure RemoteApp, currently in private preview and available only tooselect early adopters for evaluation purposes.</span></span>

<span data-ttu-id="68736-108">Pierwotnie usługa Azure RemoteApp obsługiwała tylko jeden sposób publikowania aplikacji: hello administrator publikował aplikacje z obrazu hello i będą one widoczne tooall użytkowników w kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="68736-108">Originally Azure RemoteApp enabled only one way of publishing applications: hello administrator would publish apps from hello image and they would be visible tooall users in hello collection.</span></span>

<span data-ttu-id="68736-109">Typowy scenariusz obejmuje tooinclude wiele aplikacji w jednej obrazu i wdrożenie jednej kolekcji w kolejności tooreduce zarządzania kosztów.</span><span class="sxs-lookup"><span data-stu-id="68736-109">A common scenario is tooinclude many applications in a single image and deploy one collection in order tooreduce management costs.</span></span> <span data-ttu-id="68736-110">Często nie wszystkie aplikacje są odpowiednie tooall użytkowników — Administratorzy woleliby toopublish aplikacji tooindividual użytkowników, aby nie były widoczne zbędne aplikacje w źródle aplikacji.</span><span class="sxs-lookup"><span data-stu-id="68736-110">Oftentimes not all applications are relevant tooall users – administrators would prefer toopublish apps tooindividual users so they don’t see unnecessary applications in their application feed.</span></span>

<span data-ttu-id="68736-111">Ta funkcja jest już dostępna w usłudze Azure RemoteApp, obecnie jako ograniczona funkcja wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="68736-111">This is now possible in Azure RemoteApp – currently as a limited preview feature.</span></span> <span data-ttu-id="68736-112">Oto krótkie podsumowanie nowej funkcji hello:</span><span class="sxs-lookup"><span data-stu-id="68736-112">Here is a brief summary of hello new functionality:</span></span>

1. <span data-ttu-id="68736-113">Kolekcję można ustawić w jeden z dwóch trybów:</span><span class="sxs-lookup"><span data-stu-id="68736-113">A collection can be set into one of two modes:</span></span>
   
   * <span data-ttu-id="68736-114">Hello oryginalny tryb kolekcji, gdzie wszyscy użytkownicy kolekcji widzą wszystkie opublikowane aplikacje.</span><span class="sxs-lookup"><span data-stu-id="68736-114">hello original collection mode, where all users in a collection can see all published applications.</span></span> <span data-ttu-id="68736-115">Jest to tryb domyślny hello.</span><span class="sxs-lookup"><span data-stu-id="68736-115">This is hello default mode.</span></span>
   * <span data-ttu-id="68736-116">Witaj nowy tryb aplikacji, którym użytkownicy widzą tylko aplikacje, które zostały jawnie przypisane toothem</span><span class="sxs-lookup"><span data-stu-id="68736-116">hello new application mode, where users only see applications that have been explicitly assigned toothem</span></span>
2. <span data-ttu-id="68736-117">W momencie hello tryb aplikacji hello można włączyć tylko przy użyciu poleceń cmdlet środowiska PowerShell usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="68736-117">At hello moment hello application mode can only be enabled using Azure RemoteApp PowerShell cmdlets.</span></span>
   
   * <span data-ttu-id="68736-118">Gdy Ustaw tryb tooapplication, przypisanie użytkownika w kolekcji hello nie mogą być zarządzane za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="68736-118">When set tooapplication mode, user assignment in hello collection cannot be managed through hello Azure portal.</span></span> <span data-ttu-id="68736-119">Przypisanie użytkownika musi toobe zarządzanych za pomocą poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68736-119">User assignment has toobe managed through PowerShell cmdlets.</span></span>
3. <span data-ttu-id="68736-120">Użytkownicy widzą tylko aplikacje hello bezpośrednio opublikowane toothem.</span><span class="sxs-lookup"><span data-stu-id="68736-120">Users will only see hello applications published directly toothem.</span></span> <span data-ttu-id="68736-121">Jednak może nadal być możliwe do toolaunch użytkownika hello inne aplikacje, które są dostępne w obrazie hello uzyskując dostęp do nich bezpośrednio w systemie operacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="68736-121">However, it may still be possible for a user toolaunch hello other applications available on hello image by accessing them directly in hello operating system.</span></span>
   
   * <span data-ttu-id="68736-122">Ta funkcja nie zapewnia bezpiecznej blokady aplikacji; lecz tylko ogranicza ich widoczność w źródle aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="68736-122">This feature does not provide a secure lockdown of applications; it only limits visibility in hello application feed.</span></span>
   * <span data-ttu-id="68736-123">Użytkownicy tooisolate z aplikacji, należy należy toouse oddzielne kolekcje dla tej.</span><span class="sxs-lookup"><span data-stu-id="68736-123">If you need tooisolate users from applications, you will need toouse separate collections for that.</span></span>

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a><span data-ttu-id="68736-124">Jak tooget poleceń cmdlet środowiska PowerShell usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="68736-124">How tooget Azure RemoteApp PowerShell cmdlets</span></span>
<span data-ttu-id="68736-125">tootry hello nowych wersji zapoznawczej funkcji, należy poleceń cmdlet programu Azure PowerShell toouse.</span><span class="sxs-lookup"><span data-stu-id="68736-125">tootry hello new preview functionality, you will need toouse Azure PowerShell cmdlets.</span></span> <span data-ttu-id="68736-126">Obecnie nie jest możliwe toouse hello Azure Management portal tooenable hello nowego trybu publikowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="68736-126">It is currently not possible toouse hello Azure Management portal tooenable hello new application publishing mode.</span></span>

<span data-ttu-id="68736-127">Najpierw upewnij się, że masz hello [modułu Azure PowerShell](/powershell/azure/overview) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="68736-127">First, make sure you have hello [Azure PowerShell module](/powershell/azure/overview) installed.</span></span>

<span data-ttu-id="68736-128">Następnie uruchom konsolę programu PowerShell hello w trybie administratora i hello uruchom następujące polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="68736-128">Then launch hello PowerShell console in administrator mode and run hello following cmdlet:</span></span>

        Add-AzureAccount

<span data-ttu-id="68736-129">Może zostać wyświetlony monit o podanie nazwy użytkownika i hasła platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68736-129">It will prompt you for your Azure user name and password.</span></span> <span data-ttu-id="68736-130">Po zalogowaniu można poleceń cmdlet usługi Azure RemoteApp stanie toorun względem subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="68736-130">Once signed in, you will be able toorun Azure RemoteApp cmdlets against your Azure subscriptions.</span></span>

## <a name="how-toocheck-which-mode-a-collection-is-in"></a><span data-ttu-id="68736-131">Jak toocheck trybu kolekcji jest w</span><span class="sxs-lookup"><span data-stu-id="68736-131">How toocheck which mode a collection is in</span></span>
<span data-ttu-id="68736-132">Uruchom następujące polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="68736-132">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppCollection <collectionName>

![Tryb kolekcji hello wyboru](./media/remoteapp-perapp/araacllelvel.png)

<span data-ttu-id="68736-134">Witaj właściwość AclLevel może mieć hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="68736-134">hello AclLevel property can have hello following values:</span></span>

* <span data-ttu-id="68736-135">Kolekcja: hello oryginalny Tryb publikowania.</span><span class="sxs-lookup"><span data-stu-id="68736-135">Collection: hello original publishing mode.</span></span> <span data-ttu-id="68736-136">Wszyscy użytkownicy widzą wszystkie opublikowane aplikacje.</span><span class="sxs-lookup"><span data-stu-id="68736-136">All users see all published apps.</span></span>
* <span data-ttu-id="68736-137">: Hello nowego trybu publikowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="68736-137">Application: hello new publishing mode.</span></span> <span data-ttu-id="68736-138">Użytkownicy widzą tylko hello aplikacje opublikowane bezpośrednio toothem.</span><span class="sxs-lookup"><span data-stu-id="68736-138">Users see only hello apps published directly toothem.</span></span>

## <a name="how-tooswitch-tooapplication-publishing-mode"></a><span data-ttu-id="68736-139">Jak tryb publikowania tooapplication tooswitch</span><span class="sxs-lookup"><span data-stu-id="68736-139">How tooswitch tooapplication publishing mode</span></span>
<span data-ttu-id="68736-140">Uruchom następujące polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="68736-140">Run hello following cmdlet:</span></span>

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

<span data-ttu-id="68736-141">Stan publikowania aplikacji zostanie zachowany: początkowo wszyscy użytkownicy będą widzieli wszystkie oryginalnie opublikowane aplikacje hello.</span><span class="sxs-lookup"><span data-stu-id="68736-141">Application publishing state will be preserved: initially all users will see all of hello original published apps.</span></span>

## <a name="how-toolist-users-who-can-see-a-specific-application"></a><span data-ttu-id="68736-142">Jak toolist użytkowników, którzy mogą przeglądać określonej aplikacji</span><span class="sxs-lookup"><span data-stu-id="68736-142">How toolist users who can see a specific application</span></span>
<span data-ttu-id="68736-143">Uruchom następujące polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="68736-143">Run hello following cmdlet:</span></span>

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

<span data-ttu-id="68736-144">Ta lista zawiera wszystkich użytkowników, którzy mogą przeglądać aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="68736-144">This lists all users who can see hello application.</span></span>

<span data-ttu-id="68736-145">Uwaga: Można wyświetlić aliasy aplikacji hello (o nazwie "app alias" w powyższej składni hello) systemem Get AzureRemoteAppProgram - CollectionName <collectionName>.</span><span class="sxs-lookup"><span data-stu-id="68736-145">Note: You can see hello application aliases (called "app alias" in hello syntax above) by running Get-AzureRemoteAppProgram -CollectionName <collectionName>.</span></span>

## <a name="how-tooassign-an-application-tooa-user"></a><span data-ttu-id="68736-146">Jak tooassign użytkownika tooa aplikacji</span><span class="sxs-lookup"><span data-stu-id="68736-146">How tooassign an application tooa user</span></span>
<span data-ttu-id="68736-147">Uruchom następujące polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="68736-147">Run hello following cmdlet:</span></span>

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

<span data-ttu-id="68736-148">Hello użytkownik zobaczy aplikacji hello w kliencie usługi Azure RemoteApp hello i będą mogli tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="68736-148">hello user will now see hello application in hello Azure RemoteApp client and will be able tooconnect tooit.</span></span>

## <a name="how-tooremove-an-application-from-a-user"></a><span data-ttu-id="68736-149">Jak tooremove aplikacji przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="68736-149">How tooremove an application from a user</span></span>
<span data-ttu-id="68736-150">Uruchom następujące polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="68736-150">Run hello following cmdlet:</span></span>

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a><span data-ttu-id="68736-151">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="68736-151">Providing feedback</span></span>
<span data-ttu-id="68736-152">Dziękujemy za Twoje opinie i sugestie dotyczące tej funkcji wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="68736-152">We appreciate your feedback and suggestions regarding this preview feature.</span></span> <span data-ttu-id="68736-153">Wypełnij hello [ankiety](http://www.instant.ly/s/FDdrb) toolet nam poznać Twoje zdanie.</span><span class="sxs-lookup"><span data-stu-id="68736-153">Please fill out hello [survey](http://www.instant.ly/s/FDdrb) toolet us know what you think.</span></span>

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a><span data-ttu-id="68736-154">Nie mam funkcja w wersji zapoznawczej hello tootry szansy?</span><span class="sxs-lookup"><span data-stu-id="68736-154">Haven't had a chance tootry hello preview feature?</span></span>
<span data-ttu-id="68736-155">Jeśli nie korzystasz w wersji zapoznawczej hello jeszcze, użyj tej [ankiety](http://www.instant.ly/s/AY83p) toorequest dostępu.</span><span class="sxs-lookup"><span data-stu-id="68736-155">If you have not participated in hello preview yet, please use this [survey](http://www.instant.ly/s/AY83p) toorequest access.</span></span>

