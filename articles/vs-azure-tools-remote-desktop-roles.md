---
title: "Pulpit zdalny przy użyciu ról Azure aaaUsing | Dokumentacja firmy Microsoft"
description: "Przy użyciu pulpitu zdalnego z rolami systemu Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="f7383-103">Przy użyciu pulpitu zdalnego z rolami systemu Azure</span><span class="sxs-lookup"><span data-stu-id="f7383-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="f7383-104">Przy użyciu hello zestawu SDK platformy Azure i usługi pulpitu zdalnego, można uzyskać dostępu do ról platformy Azure i maszyn wirtualnych, które są obsługiwane przez platformę Azure.</span><span class="sxs-lookup"><span data-stu-id="f7383-104">By using hello Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="f7383-105">W programie Visual Studio można skonfigurować usługi pulpitu zdalnego z projektu usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="f7383-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="f7383-106">tooenable usług pulpitu zdalnego, musisz utworzyć projekt pracy, który zawiera co najmniej jedną rolę, a następnie opublikować go tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f7383-106">tooenable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it tooAzure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f7383-107">Możesz uzyskać dostęp Azure roli do rozwiązywania problemów lub tylko programowanie.</span><span class="sxs-lookup"><span data-stu-id="f7383-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="f7383-108">Witaj przeznaczenie każdej maszyny wirtualnej jest toorun konkretnej roli w aplikacji platformy Azure, nie toorun inne aplikacje klienckie.</span><span class="sxs-lookup"><span data-stu-id="f7383-108">hello purpose of each virtual machine is toorun a specific role in your Azure application, not toorun other client applications.</span></span> <span data-ttu-id="f7383-109">Jeśli chcesz toouse toohost Azure maszyny wirtualnej, która służy do celów, zobacz Uzyskiwanie dostępu do maszyn wirtualnych platformy Azure z poziomu Eksploratora serwera.</span><span class="sxs-lookup"><span data-stu-id="f7383-109">If you want toouse Azure toohost a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="f7383-110">tooenable i użyj pulpitu zdalnego dla roli Azure</span><span class="sxs-lookup"><span data-stu-id="f7383-110">tooenable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="f7383-111">W Eksploratorze rozwiązań Otwórz menu skrótów hello projekt usługi w chmurze, a następnie wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="f7383-111">In Solution Explorer, open hello shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="f7383-112">Witaj **publikowanie aplikacji platformy Azure** zostanie wyświetlony Kreator.</span><span class="sxs-lookup"><span data-stu-id="f7383-112">hello **Publish Azure Application** wizard appears.</span></span>
   
    ![Publikowanie polecenia dla projektu usługi w chmurze](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="f7383-114">U dołu hello **ustawień publikowania platformy Azure Microsoft** hello kreatora wybierz hello **Włącz pulpit zdalny** wszystkie pola wyboru ról.</span><span class="sxs-lookup"><span data-stu-id="f7383-114">At hello bottom of **Microsoft Azure Publish Settings** page of hello wizard, select hello **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="f7383-115">Witaj **konfigurację usług pulpitu zdalnego** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="f7383-115">hello **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="f7383-116">U dołu hello hello **konfigurację usług pulpitu zdalnego** oknie dialogowym Wybierz hello **więcej opcji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f7383-116">At hello bottom of hello **Remote Desktop Configuration** dialog box, choose hello **More Options** button.</span></span> 
   
    <span data-ttu-id="f7383-117">Zostaną wyświetlone pole listy rozwijanej, które można tworzyć lub wybrać certyfikat, dzięki czemu można zaszyfrować informacji poświadczeń przy nawiązywaniu połączeń za pośrednictwem pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="f7383-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="f7383-118">Z listy rozwijanej hello wybierz  **&lt;Utwórz >**, lub wybierz istniejący z listy hello.</span><span class="sxs-lookup"><span data-stu-id="f7383-118">In hello dropdown list, choose **&lt;Create>**, or choose an existing one from hello list.</span></span> 
   
    <span data-ttu-id="f7383-119">Jeśli wybierzesz istniejącego certyfikatu, Pomiń hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="f7383-119">If you choose an existing certificate, skip hello following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f7383-120">Hello certyfikaty, które należy do podłączania pulpitu zdalnego są inne niż hello certyfikaty, które są używane dla innych operacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f7383-120">hello certificates that you need for a remote desktop connection are different from hello certificates that you use for other Azure operations.</span></span> <span data-ttu-id="f7383-121">Witaj certyfikat dostępu zdalnego musi mieć klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="f7383-121">hello remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="f7383-122">Witaj **Tworzenie certyfikatu** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="f7383-122">hello **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="f7383-123">Podaj przyjazną nazwę dla nowego certyfikatu hello, a następnie wybierz hello **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f7383-123">Provide a friendly name for hello new certificate, and then choose hello **OK** button.</span></span> <span data-ttu-id="f7383-124">w polu listy rozwijanej hello pojawi się Hello nowego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="f7383-124">hello new certificate appears in hello dropdown list box.</span></span>
   2. <span data-ttu-id="f7383-125">W hello **konfigurację usług pulpitu zdalnego** okna dialogowego wprowadź nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="f7383-125">In hello **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="f7383-126">Nie można użyć istniejącego konta.</span><span class="sxs-lookup"><span data-stu-id="f7383-126">You can’t use an existing account.</span></span> <span data-ttu-id="f7383-127">Nie można określić administratora hello nazwy użytkownika dla nowego konta hello.</span><span class="sxs-lookup"><span data-stu-id="f7383-127">Don’t specify Administrator as hello user name for hello new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f7383-128">Jeśli hello hasło nie spełnia wymagań dotyczących złożoności hello, czerwona ikona pojawi się pole tekstowe hasła toohello dalej.</span><span class="sxs-lookup"><span data-stu-id="f7383-128">If hello password doesn’t meet hello complexity requirements, a red icon appears next toohello password text box.</span></span> <span data-ttu-id="f7383-129">Witaj hasło musi zawierać wielkie litery, małe litery i liczby lub symbole.</span><span class="sxs-lookup"><span data-stu-id="f7383-129">hello password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="f7383-130">Wybierz datę na konto, które hello wygasną i po którym połączeń pulpitu zdalnego zostanie zablokowana.</span><span class="sxs-lookup"><span data-stu-id="f7383-130">Choose a date on which hello account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="f7383-131">Po, które zostały podane hello wszystkie wymagane informacje, wybierz hello **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f7383-131">After you've provided all hello required information, choose hello **OK** button.</span></span>
      
       <span data-ttu-id="f7383-132">Wiele ustawień, które umożliwiają dostęp zdalny są dodawane toohello plików cscfg i csdef.</span><span class="sxs-lookup"><span data-stu-id="f7383-132">Several settings that enable Remote Access Services are added toohello .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="f7383-133">W hello **ustawień publikowania platformy Azure Microsoft** kreatora wybierz hello **OK** przycisku, gdy wszystko jest gotowe toopublish usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f7383-133">In hello **Microsoft Azure Publish Settings** wizard, choose hello **OK** button when you’re ready toopublish your cloud service.</span></span>
   
    <span data-ttu-id="f7383-134">Jeśli nie masz toopublish gotowe, wybierz hello **anulować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f7383-134">If you're not ready toopublish, choose hello **Cancel** button.</span></span> <span data-ttu-id="f7383-135">ustawienia konfiguracji Hello są zapisywane, a później można opublikować usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f7383-135">hello configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a><span data-ttu-id="f7383-136">Połącz tooan roli Azure przy użyciu pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="f7383-136">Connect tooan Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="f7383-137">Po opublikowaniu usługi w chmurze na platformie Azure umożliwia toolog Eksploratora serwera na powitania maszyny wirtualnej obsługującego Azure.</span><span class="sxs-lookup"><span data-stu-id="f7383-137">After you publish your cloud service on Azure, you can use Server Explorer toolog into hello virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="f7383-138">W Eksploratorze serwera rozwiń hello **Azure** węzeł, a następnie rozwiń węzeł hello usługi w chmurze i jeden z jej ról toodisplay listę wystąpień.</span><span class="sxs-lookup"><span data-stu-id="f7383-138">In Server Explorer, expand hello **Azure** node, and then expand hello node for a cloud service and one of its roles toodisplay a list of instances.</span></span>
2. <span data-ttu-id="f7383-139">Otwórz menu skrótów hello węzła wystąpienia, a następnie wybierz **połączyć za pomocą pulpitu zdalnego**.</span><span class="sxs-lookup"><span data-stu-id="f7383-139">Open hello shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Łączenie za pośrednictwem pulpitu zdalnego](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="f7383-141">Wprowadź hello nazwy użytkownika i hasła, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="f7383-141">Enter hello user name and password that you created previously.</span></span> <span data-ttu-id="f7383-142">Obecnie użytkownik jest zalogowany do sesji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="f7383-142">You are now logged into your remote session.</span></span>

