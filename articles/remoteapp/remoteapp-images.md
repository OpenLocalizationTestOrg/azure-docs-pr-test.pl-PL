---
title: "aaaWhat jest hello zawierają obrazy szablonów usługi Azure RemoteApp? | Microsoft Docs"
description: "Więcej informacji na temat hello obrazów szablonów dołączonych do usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a><span data-ttu-id="56c23-104">Co to jest hello zawierają obrazy szablonów usługi Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="56c23-104">What is in hello Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="56c23-105">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="56c23-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="56c23-106">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="56c23-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="56c23-107">Subskrypcja usługi Azure RemoteApp obejmuje trzy obrazy szablonów:</span><span class="sxs-lookup"><span data-stu-id="56c23-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="56c23-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="56c23-108">Windows Server 2012</span></span>
* <span data-ttu-id="56c23-109">Microsoft Office 365 ProPlus (wymagana jest subskrypcja usługi Office 365)</span><span class="sxs-lookup"><span data-stu-id="56c23-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="56c23-110">Microsoft Office 2013 Professional Plus (tylko wersja próbna)</span><span class="sxs-lookup"><span data-stu-id="56c23-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56c23-111">Subskrypcja usługi Azure RemoteApp daje dostęp toohello oprogramowania w obrazach hello, z wyjątkiem hello usługi Office 365 ProPlus, która wymaga oddzielnej subskrypcji, i Office 2013, którego nie można używać w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="56c23-111">Your Azure RemoteApp subscription grants you access toohello software in hello images, with hello exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="56c23-112">Oznacza to, że można udostępniać programy hello lub aplikacji na powitania obrazy szablonów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="56c23-112">This means that you can share hello programs or apps on hello template images with your users.</span></span> <span data-ttu-id="56c23-113">Na przykład utworzyć kolekcję, która używa obrazu systemu Windows Server 2012 R2 hello, można opublikować programu System Center Endpoint Protection dla użytkowników tooaccess za pośrednictwem usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="56c23-113">For example, if you create a collection that uses hello Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users tooaccess through RemoteApp.</span></span>
> 
> <span data-ttu-id="56c23-114">Zapoznaj się z hello [szczegółowe informacje o licencjonowaniu usługi RemoteApp](remoteapp-licensing.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="56c23-114">Check out hello [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="56c23-115">I [korzystanie z pakietu Office z usługą Azure RemoteApp](remoteapp-o365.md) dla hello informacji licencjonowania pakietu Office.</span><span class="sxs-lookup"><span data-stu-id="56c23-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for hello Office licensing info.</span></span>
> 
> 

<span data-ttu-id="56c23-116">Poniżej podano szczegółowe informacje o zawartości każdego obrazu.</span><span class="sxs-lookup"><span data-stu-id="56c23-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--hello-vanilla-image"></a><span data-ttu-id="56c23-117">Windows Server 2012 R2 ("Witaj obraz podstawowy)</span><span class="sxs-lookup"><span data-stu-id="56c23-117">Windows Server 2012 R2  ("hello vanilla image")</span></span>
<span data-ttu-id="56c23-118">Ten obraz jest oparty na system operacyjny Microsoft Windows Server 2012 R2 Datacenter i hello następujące role i funkcje zainstalował toomeet hello wymagania dotyczące obrazów szablonów usługi Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="56c23-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has hello following roles and features installed toomeet hello requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="56c23-119">.NET Framework 4.5, 3.5.1, 3.5</span><span class="sxs-lookup"><span data-stu-id="56c23-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="56c23-120">Środowisko pulpitu</span><span class="sxs-lookup"><span data-stu-id="56c23-120">Desktop Experience</span></span>
* <span data-ttu-id="56c23-121">Usługi dotyczące pisma ręcznego i odręcznego</span><span class="sxs-lookup"><span data-stu-id="56c23-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="56c23-122">Platforma Media Foundation</span><span class="sxs-lookup"><span data-stu-id="56c23-122">Media Foundation</span></span>
* <span data-ttu-id="56c23-123">Host sesji usług pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="56c23-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="56c23-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="56c23-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="56c23-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="56c23-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="56c23-126">Obsługa środowiska WoW64</span><span class="sxs-lookup"><span data-stu-id="56c23-126">WoW64 Support</span></span>

<span data-ttu-id="56c23-127">Ten obraz zawiera także hello następujące aplikacje zainstalowane:</span><span class="sxs-lookup"><span data-stu-id="56c23-127">This image also has hello following applications installed:</span></span>

* <span data-ttu-id="56c23-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="56c23-128">Adobe Flash Player</span></span>
* <span data-ttu-id="56c23-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="56c23-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="56c23-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="56c23-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="56c23-131">Microsoft Windows Media Player</span><span class="sxs-lookup"><span data-stu-id="56c23-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="56c23-132">Microsoft Office 365 ProPlus (wymagana jest subskrypcja)</span><span class="sxs-lookup"><span data-stu-id="56c23-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="56c23-133">Usługi Office 365 jest hello najbardziej pożądaną aplikacją, dlatego utworzyliśmy "niestandardowy" obraz dla Ciebie toowork z.</span><span class="sxs-lookup"><span data-stu-id="56c23-133">Office 365 is hello most requested application, so we created a "custom" image for you toowork with.</span></span>

<span data-ttu-id="56c23-134">Ten obraz jest rozszerzeniem obrazu podstawowego hello i ma hello zainstalowane następujące składniki programu Microsoft Office 365 ProPlus oprócz składników toohello zawartych w obrazie systemu Windows Server 2012 R2 hello:</span><span class="sxs-lookup"><span data-stu-id="56c23-134">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 365 ProPlus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="56c23-135">Dostęp</span><span class="sxs-lookup"><span data-stu-id="56c23-135">Access</span></span>
* <span data-ttu-id="56c23-136">Excel</span><span class="sxs-lookup"><span data-stu-id="56c23-136">Excel</span></span>
* <span data-ttu-id="56c23-137">Lync</span><span class="sxs-lookup"><span data-stu-id="56c23-137">Lync</span></span>
* <span data-ttu-id="56c23-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="56c23-138">OneNote</span></span>
* <span data-ttu-id="56c23-139">OneDrive dla firm (należy pamiętać, że agent synchronizacji hello nie jest obsługiwane do użycia z usługą Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="56c23-139">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="56c23-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="56c23-140">Outlook</span></span>
* <span data-ttu-id="56c23-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="56c23-141">PowerPoint</span></span>
* <span data-ttu-id="56c23-142">Word</span><span class="sxs-lookup"><span data-stu-id="56c23-142">Word</span></span>
* <span data-ttu-id="56c23-143">Narzędzia sprawdzające pakietu Office</span><span class="sxs-lookup"><span data-stu-id="56c23-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="56c23-144">Obraz powitania obejmuje również Visio Pro i Project Pro.</span><span class="sxs-lookup"><span data-stu-id="56c23-144">hello image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="56c23-145">I aplikacji, jak również następujące hello:</span><span class="sxs-lookup"><span data-stu-id="56c23-145">And hello following applications, as well:</span></span>

* <span data-ttu-id="56c23-146">SQL Native Client</span><span class="sxs-lookup"><span data-stu-id="56c23-146">SQL Native client</span></span>
* <span data-ttu-id="56c23-147">Sterownik ODBC</span><span class="sxs-lookup"><span data-stu-id="56c23-147">ODBC Driver</span></span>
* <span data-ttu-id="56c23-148">SQL Server Data Mining Client</span><span class="sxs-lookup"><span data-stu-id="56c23-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="56c23-149">MasterDataServices Client</span><span class="sxs-lookup"><span data-stu-id="56c23-149">MasterDataServices client</span></span>
* <span data-ttu-id="56c23-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="56c23-150">Microsoft Publisher</span></span>
* <span data-ttu-id="56c23-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="56c23-151">PowerQuery</span></span>
* <span data-ttu-id="56c23-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="56c23-152">PowerMap</span></span>

<span data-ttu-id="56c23-153">Pełna funkcjonalność aplikacji usługi Office 365 ProPlus jest dostępna tylko dla użytkowników, którzy posiadają plan usługi Office 365 ProPlus.</span><span class="sxs-lookup"><span data-stu-id="56c23-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="56c23-154">Więcej informacji o subskrypcji usługi Office 365 hello planów dla [plany usługi Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span><span class="sxs-lookup"><span data-stu-id="56c23-154">For more details on hello Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="56c23-155">Nadal masz pytania?</span><span class="sxs-lookup"><span data-stu-id="56c23-155">Still have questions?</span></span> <span data-ttu-id="56c23-156">Zapoznaj się z hello [usługi Office 365 + usługa RemoteApp](remoteapp-o365.md) informacji.</span><span class="sxs-lookup"><span data-stu-id="56c23-156">Check out hello [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="56c23-157">Zobacz także nowy artykuł hello [jak toouse subskrypcji usługi Office 365 z usługą Azure RemoteApp](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="56c23-157">Also check out hello new article, [How toouse your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="56c23-158">Należy pamiętać, że należy oddzielnie toolicense usługi Office 365 ProPlus, programu Visio Pro i Project Pro — każdy z nich ma własny licencji.</span><span class="sxs-lookup"><span data-stu-id="56c23-158">Note that you need toolicense Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="56c23-159">Microsoft Office 2013 Professional Plus (tylko wersja próbna)</span><span class="sxs-lookup"><span data-stu-id="56c23-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="56c23-160">Podczas hello bezpłatnym okresie próbnym można testować usługi hello z obrazem hello pakietu Office 2013.</span><span class="sxs-lookup"><span data-stu-id="56c23-160">During hello free trial period, you can test hello service with hello Office 2013 image.</span></span>

<span data-ttu-id="56c23-161">Ten obraz jest rozszerzeniem obrazu podstawowego hello i ma hello zainstalowane następujące składniki programu Microsoft Office 2013 Professional Plus oprócz składników toohello zawartych w obrazie systemu Windows Server 2012 R2 hello:</span><span class="sxs-lookup"><span data-stu-id="56c23-161">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 2013 Professional Plus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="56c23-162">Dostęp</span><span class="sxs-lookup"><span data-stu-id="56c23-162">Access</span></span>
* <span data-ttu-id="56c23-163">Excel</span><span class="sxs-lookup"><span data-stu-id="56c23-163">Excel</span></span>
* <span data-ttu-id="56c23-164">Lync</span><span class="sxs-lookup"><span data-stu-id="56c23-164">Lync</span></span>
* <span data-ttu-id="56c23-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="56c23-165">OneNote</span></span>
* <span data-ttu-id="56c23-166">OneDrive dla firm (należy pamiętać, że agent synchronizacji hello nie jest obsługiwane do użycia z usługą Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="56c23-166">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="56c23-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="56c23-167">Outlook</span></span>
* <span data-ttu-id="56c23-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="56c23-168">PowerPoint</span></span>
* <span data-ttu-id="56c23-169">Project</span><span class="sxs-lookup"><span data-stu-id="56c23-169">Project</span></span>
* <span data-ttu-id="56c23-170">Visio</span><span class="sxs-lookup"><span data-stu-id="56c23-170">Visio</span></span>
* <span data-ttu-id="56c23-171">Word</span><span class="sxs-lookup"><span data-stu-id="56c23-171">Word</span></span>
* <span data-ttu-id="56c23-172">Narzędzia sprawdzające pakietu Office</span><span class="sxs-lookup"><span data-stu-id="56c23-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56c23-173">**Informacje prawne:** ten obraz nie zawiera licencji pakietu Microsoft Office i *nie może być używany w środowisku produkcyjnym*.</span><span class="sxs-lookup"><span data-stu-id="56c23-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="56c23-174">Obraz pakietu Office 2013 Professional Plus Hello jest przeznaczony tylko do użycia próbnego.</span><span class="sxs-lookup"><span data-stu-id="56c23-174">hello Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="56c23-175">Jeśli chcesz toouse aplikacje pakietu Office w usłudze Azure RemoteApp w środowisku produkcyjnym należy obrazu usługi Office 365 ProPlus hello toouse.</span><span class="sxs-lookup"><span data-stu-id="56c23-175">If you want toouse Office apps in Azure RemoteApp for production, you need toouse hello Office 365 ProPlus image.</span></span> <span data-ttu-id="56c23-176">Aby uzyskać więcej szczegółowych informacji na temat licencjonowania usługi Office, zobacz temat [Korzystanie z usługi Office 365 z usługą Azure RemoteApp](remoteapp-o365.md)</span><span class="sxs-lookup"><span data-stu-id="56c23-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

