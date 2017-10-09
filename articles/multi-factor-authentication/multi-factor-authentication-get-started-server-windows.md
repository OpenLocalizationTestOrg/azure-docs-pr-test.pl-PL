---
title: "aaaWindows uwierzytelniania i serwera usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Jest to strona uwierzytelnianie wieloskładnikowe Azure hello przydatnej Wdrażanie uwierzytelniania systemu Windows i serwera usługi Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="18f36-103">Uwierzytelnianie systemu Windows i serwer usługi Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="18f36-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="18f36-104">Użyj sekcji uwierzytelnianie systemu Windows hello powitania serwera usługi Azure Multi-Factor Authentication tooenable i skonfiguruj uwierzytelnianie systemu Windows dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="18f36-104">Use hello Windows Authentication section of hello Azure Multi-Factor Authentication Server tooenable and configure Windows authentication for applications.</span></span> <span data-ttu-id="18f36-105">Przed skonfigurowaniem uwierzytelniania systemu Windows należy hello listy na uwadze następujące:</span><span class="sxs-lookup"><span data-stu-id="18f36-105">Before you set up Windows Authentication, keep hello following list in mind:</span></span>

* <span data-ttu-id="18f36-106">Po zakończeniu instalacji uruchom ponownie hello Azure Multi-Factor Authentication dla usług terminalowych tootake efektu.</span><span class="sxs-lookup"><span data-stu-id="18f36-106">After setup, reboot hello Azure Multi-Factor Authentication for Terminal Services tootake effect.</span></span>
* <span data-ttu-id="18f36-107">Jeśli zaznaczono opcję "Wymagaj Azure Multi-Factor Authentication dopasowania użytkownika" i nie jest hello listy użytkowników, nie będzie możliwe toolog na powitania maszynę po ponownym rozruchu.</span><span class="sxs-lookup"><span data-stu-id="18f36-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in hello user list, you will not be able toolog into hello machine after reboot.</span></span>
* <span data-ttu-id="18f36-108">Zaufanych adresów IP jest zależna od tego, czy aplikacja hello zapewniają powitania klienta IP z uwierzytelnianiem hello.</span><span class="sxs-lookup"><span data-stu-id="18f36-108">Trusted IPs is dependent on whether hello application can provide hello client IP with hello authentication.</span></span> <span data-ttu-id="18f36-109">Obecnie są obsługiwane wyłącznie usługi terminalowe.</span><span class="sxs-lookup"><span data-stu-id="18f36-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="18f36-110">Ta funkcja nie jest obsługiwane toosecure usług terminalowych w systemie Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="18f36-110">This feature is not supported toosecure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a><span data-ttu-id="18f36-111">toosecure aplikacji przy użyciu uwierzytelniania systemu Windows hello użyj następującej procedury.</span><span class="sxs-lookup"><span data-stu-id="18f36-111">toosecure an application with Windows Authentication, use hello following procedure.</span></span>
1. <span data-ttu-id="18f36-112">Kliknij ikonę uwierzytelnianie systemu Windows hello w powitania serwera usługi Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="18f36-112">In hello Azure Multi-Factor Authentication Server click hello Windows Authentication icon.</span></span>
   <span data-ttu-id="18f36-113">![Uwierzytelnianie systemu Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="18f36-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="18f36-114">Sprawdź hello **włączyć uwierzytelnianie systemu Windows** wyboru.</span><span class="sxs-lookup"><span data-stu-id="18f36-114">Check hello **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="18f36-115">Domyślnie to pole nie jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="18f36-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="18f36-116">Karta aplikacje Hello umożliwia tooconfigure administratora hello co najmniej jedna aplikacja uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="18f36-116">hello Applications tab allows hello administrator tooconfigure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="18f36-117">Wybierz serwer lub aplikacja — Określ, czy aplikacja serwera hello jest włączona.</span><span class="sxs-lookup"><span data-stu-id="18f36-117">Select a server or application – specify whether hello server/application is enabled.</span></span> <span data-ttu-id="18f36-118">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="18f36-118">Click **OK**.</span></span>
5. <span data-ttu-id="18f36-119">Kliknij pozycję **Dodaj...**</span><span class="sxs-lookup"><span data-stu-id="18f36-119">Click **Add…**</span></span>
6. <span data-ttu-id="18f36-120">Karta zaufanych adresów IP Hello umożliwia tooskip sesji Azure Multi-Factor Authentication dla systemu Windows, pochodzących z określonych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="18f36-120">hello Trusted IPs tab allows you tooskip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="18f36-121">Na przykład jeśli pracownicy korzystają z aplikacji hello hello biurze i w domu, mogą zdecydujesz, że nie chcesz ich dzwonienie na telefony Azure Multi-Factor Authentication przy jednoczesnym hello pakietu office.</span><span class="sxs-lookup"><span data-stu-id="18f36-121">For example, if employees use hello application from hello office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at hello office.</span></span> <span data-ttu-id="18f36-122">W tym celu należy określić podsieć biura hello jako wpis zaufanych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="18f36-122">For this, you would specify hello office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="18f36-123">Kliknij pozycję **Dodaj...**</span><span class="sxs-lookup"><span data-stu-id="18f36-123">Click **Add…**</span></span>
8. <span data-ttu-id="18f36-124">Wybierz **pojedynczy adres IP** Jeśli chcesz tooskip pojedynczego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="18f36-124">Select **Single IP** if you would like tooskip a single IP address.</span></span>
9. <span data-ttu-id="18f36-125">Wybierz **zakres adresów IP** Jeśli chcesz tooskip cały zakres adresów IP.</span><span class="sxs-lookup"><span data-stu-id="18f36-125">Select **IP Range** if you would like tooskip an entire IP range.</span></span> <span data-ttu-id="18f36-126">Na przykład: 10.63.193.1–10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="18f36-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="18f36-127">Wybierz **podsieci** Jeśli chcesz toospecify zakres adresów IP przy użyciu notacji podsieci.</span><span class="sxs-lookup"><span data-stu-id="18f36-127">Select **Subnet** if you would like toospecify a range of IPs using subnet notation.</span></span> <span data-ttu-id="18f36-128">Wprowadź początkowy IP podsieci hello i wybierz odpowiednią maskę sieciową hello z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="18f36-128">Enter hello subnet's starting IP and pick hello appropriate netmask from hello drop-down list.</span></span>
11. <span data-ttu-id="18f36-129">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="18f36-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18f36-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="18f36-130">Next steps</span></span>

- [<span data-ttu-id="18f36-131">Konfigurowanie urządzeń VPN innych firm dla serwera Azure MFA</span><span class="sxs-lookup"><span data-stu-id="18f36-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="18f36-132">Rozszerzyć istniejącą infrastrukturę uwierzytelniania z powitania serwera NPS rozszerzenia dla usługi Azure MFA</span><span class="sxs-lookup"><span data-stu-id="18f36-132">Augment your existing authentication infrastructure with hello NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
