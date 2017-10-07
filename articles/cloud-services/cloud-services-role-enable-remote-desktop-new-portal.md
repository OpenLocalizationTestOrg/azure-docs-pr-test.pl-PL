---
title: "aaaEnable Podłączanie pulpitu zdalnego dla roli w usług Azure Cloud Services | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure platformy azure w chmurze usługi połączeń pulpitu zdalnego tooallow aplikacji"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="d166b-103">Włączanie połączeń usług pulpitu zdalnego dla roli usług w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="d166b-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d166b-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d166b-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="d166b-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d166b-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="d166b-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d166b-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="d166b-107">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d166b-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="d166b-108">Pulpit zdalny umożliwia pulpitu hello tooaccess roli działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d166b-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="d166b-109">Można użyć tootroubleshoot połączenia pulpitu zdalnego i diagnozowanie problemów z aplikacją, jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="d166b-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="d166b-110">Umożliwia Podłączanie pulpitu zdalnego w roli podczas tworzenia przez uwzględnienie hello modułów usług pulpitu zdalnego w definicji usługi. można też tooenable pulpitu zdalnego za pośrednictwem hello rozszerzenia usług pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="d166b-110">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="d166b-111">Hello preferowana metoda się toouse hello pulpitu zdalnego rozszerzenie można włączyć pulpitu zdalnego, nawet po wdrożeniu aplikacji hello bez konieczności tooredeploy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d166b-111">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-portal"></a><span data-ttu-id="d166b-112">Konfigurowanie pulpitu zdalnego z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d166b-112">Configure Remote Desktop from hello Azure portal</span></span>
<span data-ttu-id="d166b-113">Hello portalu Azure używa hello podejście rozszerzenia usług pulpitu zdalnego, więc można włączyć pulpitu zdalnego, nawet po wdrożeniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d166b-113">hello Azure portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="d166b-114">Witaj **pulpitu zdalnego** bloku dla usługi w chmurze pozwala tooenable pulpitu zdalnego, zmiana konta administratora lokalnego hello używane maszyny wirtualne toohello tooconnect, hello certyfikat używany podczas uwierzytelniania i ustawić hello Data wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="d166b-114">hello **Remote Desktop** blade for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="d166b-115">Kliknij przycisk **usługi w chmurze**, kliknij nazwę hello hello usługi w chmurze, a następnie kliknij przycisk **pulpitu zdalnego**.</span><span class="sxs-lookup"><span data-stu-id="d166b-115">Click **Cloud Services**, click hello name of hello cloud service, and then click **Remote Desktop**.</span></span>

    ![Pulpit zdalny usługi w chmurze](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="d166b-117">Wybierz, czy tooenable pulpitu zdalnego dla poszczególnych ról lub dla wszystkich ról, a następnie zmienić wartości hello przełącznik hello zbyt**włączone**.</span><span class="sxs-lookup"><span data-stu-id="d166b-117">Choose whether you want tooenable Remote Desktop for an individual role or for all roles, then change hello value of hello switcher too**Enabled**.</span></span>

3. <span data-ttu-id="d166b-118">Wypełnij pola hello wymagane podanie nazwy użytkownika, hasła, wygaśnięcia i certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="d166b-118">Fill in hello required fields for user name, password, expiry, and certificate.</span></span>

    ![Pulpit zdalny usługi w chmurze](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="d166b-120">Wszystkie wystąpienia roli zostanie ponownie uruchomiony, gdy najpierw włączyć pulpitu zdalnego i kliknij przycisk OK (znacznikiem wyboru).</span><span class="sxs-lookup"><span data-stu-id="d166b-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="d166b-121">tooprevent ponowne uruchomienie komputera, hello certyfikatu używane tooencrypt hello hasło musi być zainstalowany na powitania roli.</span><span class="sxs-lookup"><span data-stu-id="d166b-121">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="d166b-122">tooprevent ponowne uruchomienie, [przekazywanie certyfikatu dla usługi w chmurze hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , a następnie wróć toothis okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d166b-122">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>
   >
   >
3. <span data-ttu-id="d166b-123">W **ról**, wybierz rolę hello tooupdate lub wybierz **wszystkie** dla wszystkich ról.</span><span class="sxs-lookup"><span data-stu-id="d166b-123">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>

4. <span data-ttu-id="d166b-124">Po zakończeniu aktualizacji konfiguracji, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="d166b-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="d166b-125">Potrwa kilka minut, zanim wystąpienia roli będą gotowe tooreceive połączenia.</span><span class="sxs-lookup"><span data-stu-id="d166b-125">It will take a few moments before your role instances are ready tooreceive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="d166b-126">Zdalne do wystąpień roli</span><span class="sxs-lookup"><span data-stu-id="d166b-126">Remote into role instances</span></span>
<span data-ttu-id="d166b-127">Włączenie pulpitu zdalnego na powitania ról, możesz zainicjować połączenie bezpośrednio z hello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="d166b-127">Once Remote Desktop is enabled on hello roles, you can initiate a connection directly from hello Azure Portal:</span></span>

1. <span data-ttu-id="d166b-128">Kliknij przycisk **wystąpień** tooopen hello **wystąpień** bloku.</span><span class="sxs-lookup"><span data-stu-id="d166b-128">Click **Instances** tooopen hello **Instances** blade.</span></span>
2. <span data-ttu-id="d166b-129">Wybierz wystąpienia roli, który ma pulpitu zdalnego skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="d166b-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="d166b-130">Kliknij przycisk **Connect** toodownload RDP plik hello wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="d166b-130">Click **Connect** toodownload an RDP file for hello role instance.</span></span>

    ![Pulpit zdalny usługi w chmurze](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="d166b-132">Kliknij przycisk **Otwórz** , a następnie **Connect** toostart hello Podłączanie pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="d166b-132">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="d166b-133">Usługi w chmurze jest działo za grupy NSG, może być konieczne toocreate reguł, które zezwalają na ruch na portach **3389** i **20000**.</span><span class="sxs-lookup"><span data-stu-id="d166b-133">If your cloud service is sitting behind an NSG, you may need toocreate rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="d166b-134">Pulpit zdalny używa portu **3389**.</span><span class="sxs-lookup"><span data-stu-id="d166b-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="d166b-135">Wystąpienia usługi chmury jest równoważone, więc nie można bezpośrednio kontrolować tooconnect wystąpienia, które do.</span><span class="sxs-lookup"><span data-stu-id="d166b-135">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="d166b-136">Witaj *RemoteForwarder* i *RemoteAccess* agentów zarządzania na ruch RDP i Zezwalaj na powitania klienta toosend pliku cookie protokołu RDP i określ tooconnect poszczególnych wystąpień do.</span><span class="sxs-lookup"><span data-stu-id="d166b-136">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="d166b-137">Witaj *RemoteForwarder* i *RemoteAccess* agentów wymagają tego portu **20000*** otwarty, które mogą być zablokowane, jeśli masz grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="d166b-137">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d166b-138">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d166b-138">Additional resources</span></span>

<span data-ttu-id="d166b-139">[Jak usługi w chmurze tooConfigure](cloud-services-how-to-configure.md)
[usług w chmurze — często zadawane pytania — pulpitu zdalnego](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="d166b-139">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
