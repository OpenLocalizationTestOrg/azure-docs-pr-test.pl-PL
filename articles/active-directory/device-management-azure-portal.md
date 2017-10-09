---
title: "portal Azure — Witaj aaaManaging urządzeń przy użyciu wersji zapoznawczej | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello urządzeń toomanage portalu Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a><span data-ttu-id="f3798-103">Zarządzanie urządzeniami za pomocą hello Azure portal — wersja zapoznawcza</span><span class="sxs-lookup"><span data-stu-id="f3798-103">Managing devices using hello Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="f3798-104">Ta funkcja jest obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="f3798-104">This capability currently is in public preview.</span></span> <span data-ttu-id="f3798-105">Można przygotować toorevert lub Usuń wszystkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="f3798-105">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="f3798-106">Funkcja Hello jest dostępna w żadnych subskrypcji usługi Azure Active Directory (Azure AD) w publicznej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="f3798-106">hello feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="f3798-107">Gdy funkcja hello staje się ogólnie dostępna, niektórych aspektów funkcji hello mogą jednak wymagać subskrypcję usługi Azure Active Directory premium.</span><span class="sxs-lookup"><span data-stu-id="f3798-107">However, when hello feature becomes generally available, some aspects of hello feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="f3798-108">Z zarządzania urządzeniami w usłudze Azure Active Directory (Azure AD) można zapewnić, że użytkownicy uzyskują dostęp do zasobów z urządzeń, które spełniają standardy zabezpieczeń i zgodności.</span><span class="sxs-lookup"><span data-stu-id="f3798-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="f3798-109">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="f3798-109">This topic:</span></span>

- <span data-ttu-id="f3798-110">Przyjęto założenie, że czytelnik zna hello [wprowadzenie toodevice zarządzania w usłudze Azure Active Directory](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="f3798-110">Assumes that you are familiar with hello [introduction toodevice management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="f3798-111">Zapewnia możliwość hello o informacji na temat zarządzania urządzeniami przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f3798-111">Provides you with information about managing your devices using hello Azure portal</span></span>


<span data-ttu-id="f3798-112">toomanage urządzenia w portalu Azure hello, należy tooclick **urządzeń** w hello **Zarządzaj** sekcji hello hello **usługi Azure Active Directory** bloku.</span><span class="sxs-lookup"><span data-stu-id="f3798-112">toomanage devices in hello Azure portal, you need tooclick **Devices** in hello **Manage** section of hello hello **Azure Active Directory** blade.</span></span>

![Zarządzanie urządzeń w usłudze Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="f3798-114">Konfiguruj ustawienia urządzeń</span><span class="sxs-lookup"><span data-stu-id="f3798-114">Configure device settings</span></span>

<span data-ttu-id="f3798-115">toomanage swoje urządzenia za pomocą hello portalu Azure, potrzebują toobe zarejestrowany lub przyłączony tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="f3798-115">toomanage your devices using hello Azure portal, they need toobe either registered or joined tooAzure AD.</span></span> <span data-ttu-id="f3798-116">Jako administrator Aby precyzyjnie zdefiniować hello proces rejestracji i dołączenie urządzeń przez skonfigurowanie ustawienia urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="f3798-116">As an administrator, you can fine-tune hello process of registering and joining devices by configuring hello device settings.</span></span>

![Zarządzanie urządzeń w usłudze Intune](./media/device-management-azure-portal/22.png)


<span data-ttu-id="f3798-118">Blok ustawień urządzenia Hello umożliwia tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="f3798-118">hello device settings blade enables you tooconfigure:</span></span>

- <span data-ttu-id="f3798-119">**Użytkownicy mogą przyłączać urządzenia tooAzure AD** — to ustawienie włącza tooselect hello użytkowników, którzy może dołączać urządzenia tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="f3798-119">**Users may join devices tooAzure AD** - This settings enables you tooselect hello users who can join devices tooAzure AD.</span></span> <span data-ttu-id="f3798-120">Domyślnie Hello **wszystkich**.</span><span class="sxs-lookup"><span data-stu-id="f3798-120">hello default is **All**.</span></span>

- <span data-ttu-id="f3798-121">**Urządzeniach przyłączonych do kolejnych administratorów lokalnych na usługi Azure AD** — możesz wybrać hello użytkowników, którzy mają prawa administratora lokalnego na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="f3798-121">**Additional local administrators on Azure AD joined devices** - You can select hello users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="f3798-122">Użytkowników dodanych, w tym miejscu są dodawane toohello *Administratorzy urządzenia* roli w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3798-122">Users added here are added toohello *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="f3798-123">Administratorzy globalni w usłudze Azure AD i właścicielom urządzeń mają prawa administratora lokalnego domyślnie.</span><span class="sxs-lookup"><span data-stu-id="f3798-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="f3798-124">Ta opcja jest dostępna za pośrednictwem produktów, takich jak Azure AD Premium lub Enterprise Mobility Suite (EMS) hello możliwości wersji premium.</span><span class="sxs-lookup"><span data-stu-id="f3798-124">This option is a premium edition capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="f3798-125">**Użytkownicy mogą zarejestrować swoje urządzenia w usłudze Azure AD** — należy tooconfigure to ustawienie tooallow urządzeń toobe zarejestrowany z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3798-125">**Users may register their devices with Azure AD** - You need tooconfigure this setting tooallow devices toobe registered with Azure AD.</span></span> <span data-ttu-id="f3798-126">W przypadku wybrania **Brak**, urządzenia nie są dozwolone tooregister, jeśli nie są one usługi Azure AD przyłączone lub hybrydowego przyłączonych do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3798-126">If you select **None**, devices are not allowed tooregister when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="f3798-127">Rejestrowanie w usłudze Microsoft Intune lub zarządzania urządzeniami przenośnymi (MDM) dla usługi Office 365 wymaga rejestracji.</span><span class="sxs-lookup"><span data-stu-id="f3798-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="f3798-128">Jeśli skonfigurowano którąś z tych usług **wszystkie** jest zaznaczone i **Brak** nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="f3798-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="f3798-129">**Wymagaj uwierzytelniania wieloskładnikowego toojoin urządzeń** — możesz wybrać, czy użytkownicy są wymagane tooprovide drugiego uwierzytelniania dwuskładnikowego toojoin ich tooAzure urządzenia AD.</span><span class="sxs-lookup"><span data-stu-id="f3798-129">**Require Multi-Factor Auth toojoin devices** - You can choose whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="f3798-130">Domyślnie Hello **nr**.</span><span class="sxs-lookup"><span data-stu-id="f3798-130">hello default is **No**.</span></span> <span data-ttu-id="f3798-131">Firma Microsoft zaleca, wymagając uwierzytelniania wieloskładnikowego podczas rejestrowania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f3798-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="f3798-132">Przed włączeniem uwierzytelniania wieloskładnikowego dla tej usługi, pamiętaj, że skonfigurowano uwierzytelnianie wieloskładnikowe dla użytkowników hello, które rejestrują swoje urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f3798-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for hello users that register their devices.</span></span> <span data-ttu-id="f3798-133">Aby uzyskać więcej informacji dotyczących usług różnych uwierzytelnianie wieloskładnikowe platformy Azure, zobacz [wprowadzenie do korzystania z usługi Azure Multi-Factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f3798-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="f3798-134">**Maksymalna liczba urządzeń** — to ustawienie włącza tooselect hello maksymalną liczbę urządzeń, które użytkownik może mieć w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3798-134">**Maximum number of devices** - This setting enables you tooselect hello maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="f3798-135">Jeśli użytkownik osiągnie ten limit przydziału, nie są być stanie tooadd dodatkowych urządzeń dopóki jedna lub więcej hello istniejące urządzenia zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="f3798-135">If a user reaches this quota, they are not be able tooadd additional devices until one or more of hello existing devices are removed.</span></span> <span data-ttu-id="f3798-136">Oferta urządzenia Hello jest liczony dla wszystkich urządzeń, które są usługi Azure AD przyłączone lub usługi Azure AD, w obecnie zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="f3798-136">hello device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="f3798-137">Witaj, wartość domyślna to **20**.</span><span class="sxs-lookup"><span data-stu-id="f3798-137">hello default value is **20**.</span></span>

- <span data-ttu-id="f3798-138">**Użytkownicy mogą synchronizować ustawienia i dane aplikacji na urządzeniach** — domyślnie to ustawienie ma wartość zbyt**Brak**.</span><span class="sxs-lookup"><span data-stu-id="f3798-138">**Users may sync settings and app data across devices** - By default, this setting is set too**NONE**.</span></span> <span data-ttu-id="f3798-139">Wybranie określonych użytkowników lub grup lub wszystkich umożliwia toosync danych aplikacji i ustawień użytkownika hello na ich urządzeniach z systemem Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f3798-139">Selecting specific users or groups or ALL allows hello user’s settings and app data toosync across their Windows 10 devices.</span></span> <span data-ttu-id="f3798-140">Dowiedz się więcej informacji na temat sposobu synchronizacji działa w systemie Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f3798-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="f3798-141">Ta opcja jest dostępna za pośrednictwem produktów, takich jak Azure AD Premium lub Enterprise Mobility Suite (EMS) hello możliwości premium.</span><span class="sxs-lookup"><span data-stu-id="f3798-141">This option is a premium capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span>
 
    ![Zarządzanie urządzeń w usłudze Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="f3798-143">Znajdź urządzenia</span><span class="sxs-lookup"><span data-stu-id="f3798-143">Locate devices</span></span>

<span data-ttu-id="f3798-144">Jako administrator w hello portalu Azure, masz dwie opcje toolocate zarejestrowane i urządzeniach przyłączonych do:</span><span class="sxs-lookup"><span data-stu-id="f3798-144">As an administrator, in hello Azure portal, you have two options toolocate registered and joined devices:</span></span>

- <span data-ttu-id="f3798-145">**Wszystkie urządzenia** w hello **Zarządzaj** sekcji hello **urządzeń** bloku</span><span class="sxs-lookup"><span data-stu-id="f3798-145">**All devices** in hello **Manage** section of hello **Devices** blade</span></span>  

    ![Wszystkie urządzenia](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="f3798-147">**Urządzenia** w hello **Zarządzaj** sekcji **użytkownika** bloku</span><span class="sxs-lookup"><span data-stu-id="f3798-147">**Devices** in hello **Manage** section of a **User** blade</span></span>
 
    ![Wszystkie urządzenia](./media/device-management-azure-portal/43.png)



<span data-ttu-id="f3798-149">Obie opcje można uzyskać widoku tooa który:</span><span class="sxs-lookup"><span data-stu-id="f3798-149">With both options, you can get tooa view that:</span></span>


- <span data-ttu-id="f3798-150">Umożliwia toosearch urządzeń przy użyciu nazwy wyświetlanej hello jako filtr.</span><span class="sxs-lookup"><span data-stu-id="f3798-150">Enables you toosearch for devices using hello display name as filter.</span></span>

- <span data-ttu-id="f3798-151">Udostępnia szczegółowy przegląd urządzeń zarejestrowanych i połączone</span><span class="sxs-lookup"><span data-stu-id="f3798-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="f3798-152">Umożliwia tooperform typowych zadań zarządzania dla urządzenia</span><span class="sxs-lookup"><span data-stu-id="f3798-152">Enables you tooperform common device management tasks</span></span>
   

![Wszystkie urządzenia](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="f3798-154">Zadania dotyczące zarządzania urządzeniami</span><span class="sxs-lookup"><span data-stu-id="f3798-154">Device management tasks</span></span>

<span data-ttu-id="f3798-155">Jako administrator, można zarządzać hello zarejestrowany lub urządzenia do miejsca pracy.</span><span class="sxs-lookup"><span data-stu-id="f3798-155">As an administrator, you can manage hello registered or joined devices.</span></span> <span data-ttu-id="f3798-156">Ta sekcja zawiera informacje o typowych zadań zarządzania dla urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f3798-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="f3798-157">**Zarządzanie urządzeniem Intune** — Jeśli jesteś administratorem usługi Intune, możesz zarządzać urządzeniami oznaczona jako **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="f3798-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="f3798-158">Administrator może zobaczyć dodatkowe urządzenia</span><span class="sxs-lookup"><span data-stu-id="f3798-158">An administrator can see additional device</span></span> 

![Zarządzanie urządzeń w usłudze Intune](./media/device-management-azure-portal/31.png)


<span data-ttu-id="f3798-160">**Włączanie / wyłączanie urządzeń usługi Azure AD**</span><span class="sxs-lookup"><span data-stu-id="f3798-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="f3798-161">tooenable lub wyłącz urządzenie, należy toobe administratorem globalnym w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3798-161">tooenable or disable a device, you need toobe a global administrator in Azure  AD.</span></span> <span data-ttu-id="f3798-162">Wyłączenie urządzenia zapobiega urządzenia podczas uzyskiwania dostępu do zasobów usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3798-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="f3798-163">toodisable hello urządzenia, możesz kliknąć przycisk *...*</span><span class="sxs-lookup"><span data-stu-id="f3798-163">toodisable hello device, you can either click *…*</span></span> <span data-ttu-id="f3798-164">Kliknij urządzenie hello, aby uzyskać dodatkowe szczegóły.</span><span class="sxs-lookup"><span data-stu-id="f3798-164">click hello device for additional details.</span></span>

 
![Zarządzanie urządzeń w usłudze Intune](./media/device-management-azure-portal/33.png)

<span data-ttu-id="f3798-166">Wyłączenie urządzenia zmieni stan hello w hello **włączone** kolumny zbyt**nr**.</span><span class="sxs-lookup"><span data-stu-id="f3798-166">Disabling a device changes hello state in hello **ENABLED** column too**No**.</span></span>

![Wyłącz urządzenia](./media/device-management-azure-portal/32.png)


<span data-ttu-id="f3798-168">**Usuwanie urządzenia z systemem Azure AD** -toodelete urządzenie, należy toobe administratorem globalnym w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3798-168">**Delete an Azure AD device** - toodelete a device, you need toobe a global administrator in Azure AD.</span></span>  
<span data-ttu-id="f3798-169">Usuwanie urządzenia:</span><span class="sxs-lookup"><span data-stu-id="f3798-169">Deleting a device:</span></span>
 
- <span data-ttu-id="f3798-170">Zapobiega urządzenia podczas uzyskiwania dostępu do zasobów usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3798-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="f3798-171">Usuwa wszystkie szczegóły, które są dołączone toohello urządzenia, na przykład, klucze funkcji BitLocker dla urządzeń z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="f3798-171">Removes all details that are attached toohello device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="f3798-172">Reprezentuje nieodwracalny działania i nie jest zalecane, chyba że jest to wymagane</span><span class="sxs-lookup"><span data-stu-id="f3798-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="f3798-173">Jeśli urządzenie jest zarządzane przez inny urząd zarządzania (np. Microsoft Intune), upewnij się, czy urządzenie hello, zostały wyczyszczone / wycofane przed usunięciem hello urządzenia w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3798-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that hello device has been wiped / retired before deleting hello device in Azure AD.</span></span>

<span data-ttu-id="f3798-174">Możesz wybrać "..."</span><span class="sxs-lookup"><span data-stu-id="f3798-174">You can either select “…”</span></span> <span data-ttu-id="f3798-175">toodelete hello urządzenie lub urządzenia hello, aby uzyskać więcej informacji, kliknij polecenie</span><span class="sxs-lookup"><span data-stu-id="f3798-175">toodelete hello device or click on hello device for additional details</span></span>
 
![Usuwanie urządzenia](./media/device-management-azure-portal/34.png)


<span data-ttu-id="f3798-177">**Wyświetl lub skopiuj identyfikator urządzenia** — można użyć szczegóły identyfikator urządzenia identyfikator tooverify hello urządzenia na urządzeniu hello lub podczas rozwiązywania problemów przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3798-177">**View or copy device ID** - You can use a device ID tooverify hello device ID details on hello device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="f3798-178">tooaccess hello kopiowania kliknij przycisk hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f3798-178">tooaccess hello copy option, click hello device.</span></span>

![Wyświetl identyfikator urządzenia](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="f3798-180">**Wyświetl lub skopiować klucze funkcji BitLocker** — Jeśli jesteś administratorem, możesz wyświetlić hello kopiowania funkcji BitLocker kluczy lub toorecover użytkowników toohelp ich zaszyfrowanego dysku.</span><span class="sxs-lookup"><span data-stu-id="f3798-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy hello BitLocker keys toohelp users toorecover their encrypted drive.</span></span> <span data-ttu-id="f3798-181">Klucze te są dostępne tylko dla urządzeń z systemem Windows, które są szyfrowane i ich kluczy przechowywanych w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3798-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="f3798-182">Możesz skopiować te klucze podczas uzyskiwania dostępu do szczegółów hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f3798-182">You can copy these keys when accessing details of hello device.</span></span>
 
![Wyświetl klucze funkcji BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="f3798-184">Dzienniki inspekcji</span><span class="sxs-lookup"><span data-stu-id="f3798-184">Audit logs</span></span>


<span data-ttu-id="f3798-185">działania urządzenia Hello są dostępne za pośrednictwem hello Dzienniki aktywności.</span><span class="sxs-lookup"><span data-stu-id="f3798-185">hello device activities are available through hello activity logs.</span></span> <span data-ttu-id="f3798-186">Obejmuje to wyzwalane przez usługę rejestracji urządzeń hello lub przez użytkownika hello działania:</span><span class="sxs-lookup"><span data-stu-id="f3798-186">This includes activities triggered by hello device registration service or by hello user:</span></span>

- <span data-ttu-id="f3798-187">Tworzenie urządzenia i dodawanie użytkowników/właścicieli na urządzeniu hello</span><span class="sxs-lookup"><span data-stu-id="f3798-187">Device creation and adding owners/users on hello device</span></span>

- <span data-ttu-id="f3798-188">Zmiany ustawień toodevice</span><span class="sxs-lookup"><span data-stu-id="f3798-188">Changes toodevice settings</span></span>

- <span data-ttu-id="f3798-189">Urządzenie operacji, takich jak usuwanie lub aktualizowanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="f3798-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="f3798-190">Twoje toohello punktu wejścia inspekcja danych jest **dzienniki inspekcji** w hello **działania** sekcji hello **urządzeń* bloku.</span><span class="sxs-lookup"><span data-stu-id="f3798-190">Your entry point toohello auditing data is **Audit logs** in hello **Activity** section of hello **Devices* blade.</span></span>

![Dzienniki inspekcji](./media/device-management-azure-portal/61.png)


<span data-ttu-id="f3798-192">Dziennik inspekcji zawiera domyślny widok listy, który pokazuje:</span><span class="sxs-lookup"><span data-stu-id="f3798-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="f3798-193">Witaj Data i godzina wystąpienia hello</span><span class="sxs-lookup"><span data-stu-id="f3798-193">hello date and time of hello occurrence</span></span>

- <span data-ttu-id="f3798-194">obiekty docelowe Hello</span><span class="sxs-lookup"><span data-stu-id="f3798-194">hello targets</span></span>

- <span data-ttu-id="f3798-195">Witaj inicjatora / aktora (który) działania</span><span class="sxs-lookup"><span data-stu-id="f3798-195">hello initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="f3798-196">działanie Hello, (co)</span><span class="sxs-lookup"><span data-stu-id="f3798-196">hello activity (what)</span></span>

![Dzienniki inspekcji](./media/device-management-azure-portal/63.png)

<span data-ttu-id="f3798-198">Można dostosować widok listy hello klikając **kolumn** hello w pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="f3798-198">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>
 
![Dzienniki inspekcji](./media/device-management-azure-portal/64.png)


<span data-ttu-id="f3798-200">toonarrow dół hello zgłoszone poziom tooa danych czy działa dla Ciebie, dane można filtrować hello inspekcji przy użyciu hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f3798-200">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="f3798-201">Catergory</span><span class="sxs-lookup"><span data-stu-id="f3798-201">Catergory</span></span>
- <span data-ttu-id="f3798-202">Typ zasobu działania</span><span class="sxs-lookup"><span data-stu-id="f3798-202">Activity resource type</span></span>
- <span data-ttu-id="f3798-203">Działanie</span><span class="sxs-lookup"><span data-stu-id="f3798-203">Activity</span></span>
- <span data-ttu-id="f3798-204">Zakres dat</span><span class="sxs-lookup"><span data-stu-id="f3798-204">Date range</span></span>
- <span data-ttu-id="f3798-205">docelowy</span><span class="sxs-lookup"><span data-stu-id="f3798-205">Target</span></span>
- <span data-ttu-id="f3798-206">Zainicjowane przez (aktora)</span><span class="sxs-lookup"><span data-stu-id="f3798-206">Initiated By (Actor)</span></span>

<span data-ttu-id="f3798-207">Ponadto filtry toohello można wyszukiwać określone wpisy.</span><span class="sxs-lookup"><span data-stu-id="f3798-207">In addition toohello filters, you can search for specific entries.</span></span>

![Dzienniki inspekcji](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="f3798-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f3798-209">Next steps</span></span>

* [<span data-ttu-id="f3798-210">Wprowadzenie toodevice zarządzania w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3798-210">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



