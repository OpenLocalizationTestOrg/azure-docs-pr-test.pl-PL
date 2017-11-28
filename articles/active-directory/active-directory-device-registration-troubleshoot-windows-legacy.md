---
title: "komputery przyłączone aaaTroubleshooting hello automatyczną rejestrację domeny usługi Azure AD dla klientów niższego poziomu z systemem Windows | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z hello automatyczną rejestrację domeny usługi Azure AD komputerów przyłączonych do klientów niższego poziomu z systemem Windows."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a><span data-ttu-id="a6f51-103">Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD dla klientów niższego poziomu z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="a6f51-103">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span> 

<span data-ttu-id="a6f51-104">Ten temat jest stosowane tylko toohello od klientów:</span><span class="sxs-lookup"><span data-stu-id="a6f51-104">This topic is applicable only toohello following clients:</span></span> 

- <span data-ttu-id="a6f51-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="a6f51-105">Windows 7</span></span> 
- <span data-ttu-id="a6f51-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="a6f51-106">Windows 8.1</span></span> 
- <span data-ttu-id="a6f51-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="a6f51-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="a6f51-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a6f51-108">Windows Server 2012</span></span> 
- <span data-ttu-id="a6f51-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a6f51-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="a6f51-110">Dla systemu Windows 10 lub Windows Server 2016, zobacz [Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD — Windows 10 i Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="a6f51-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="a6f51-111">W tym temacie założono, że skonfigurowano automatyczną rejestrację urządzeń przyłączonych do domeny jako obramowane w opisanych w [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a6f51-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="a6f51-112">Ten temat zawiera rozwiązania wskazówki dotyczące sposobu tooresolve potencjalne problemy.</span><span class="sxs-lookup"><span data-stu-id="a6f51-112">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  
<span data-ttu-id="a6f51-113">Niektóre elementy toonote dla pomyślnych wyników:</span><span class="sxs-lookup"><span data-stu-id="a6f51-113">Some things toonote for successful outcomes:</span></span> 

- <span data-ttu-id="a6f51-114">Rejestracja tych klientów w usłudze Azure AD jest na użytkownika/urządzenie.</span><span class="sxs-lookup"><span data-stu-id="a6f51-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="a6f51-115">Na przykład: Jeśli jdoe i jharnett zalogować się w urządzeniu toothis, oddzielne rejestracji (DeviceID) jest tworzony dla każdego z tych użytkowników hello użytkownika informacje o karcie.</span><span class="sxs-lookup"><span data-stu-id="a6f51-115">As an example: If jdoe and jharnett log in toothis device, a separate registration (DeviceID) is created for each of these users in hello USER info tab.</span></span>  

- <span data-ttu-id="a6f51-116">Rejestracja tych klientów fabrycznej hello jest skonfigurowany tootry podczas logowania lub Zablokuj/Odblokuj i mogą występować opóźnienia 5 minut, że jest to wyzwalane za pomocą zadania harmonogramu zadań.</span><span class="sxs-lookup"><span data-stu-id="a6f51-116">Registration of these clients out of hello box is configured tootry at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="a6f51-117">Ponownie zainstaluj system operacyjny hello lub ręczne wyrejestrowanie i ponowne zarejestrowanie może utworzyć nowej rejestracji w usłudze Azure AD i spowoduje wiele wpisów hello użytkownika informacje o karcie w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f51-117">A re-install of hello operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="a6f51-118">Krok 1: Pobierz hello stan rejestracji</span><span class="sxs-lookup"><span data-stu-id="a6f51-118">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="a6f51-119">**Stan rejestracji hello tooverify:**</span><span class="sxs-lookup"><span data-stu-id="a6f51-119">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="a6f51-120">Witaj Otwórz wiersz polecenia jako administrator</span><span class="sxs-lookup"><span data-stu-id="a6f51-120">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="a6f51-121">Typ`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="a6f51-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="a6f51-122">To polecenie wyświetla okno dialogowe, która udostępnia szczegółowe informacje o stanie sprzężenia hello.</span><span class="sxs-lookup"><span data-stu-id="a6f51-122">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="a6f51-124">Krok 2: Ocena hello stan rejestracji</span><span class="sxs-lookup"><span data-stu-id="a6f51-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="a6f51-125">Jeśli sprzężenia hello zakończyła się niepowodzeniem, okno dialogowe hello zawiera szczegółowe informacje o problemie hello, który wystąpił.</span><span class="sxs-lookup"><span data-stu-id="a6f51-125">If hello join was not successful, hello dialog box provides you with details about hello issue that has occured.</span></span>

<span data-ttu-id="a6f51-126">**najbardziej typowe problemy Hello są:**</span><span class="sxs-lookup"><span data-stu-id="a6f51-126">**hello most common issues are:**</span></span>

- <span data-ttu-id="a6f51-127">Nieprawidłowej konfiguracji usług AD FS lub Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6f51-127">A misconfigured AD FS or Azure AD</span></span>

    ![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="a6f51-129">Użytkownik nie jest zarejestrowany jako użytkownik domeny</span><span class="sxs-lookup"><span data-stu-id="a6f51-129">You are not signed on as a domain user</span></span>

    ![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="a6f51-131">Osiągnięto limit przydziału</span><span class="sxs-lookup"><span data-stu-id="a6f51-131">A quota has been reached</span></span>

    ![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="a6f51-133">Usługa Hello nie odpowiada</span><span class="sxs-lookup"><span data-stu-id="a6f51-133">hello service is not responding</span></span> 

    ![Dołącz do miejsca pracy dla systemu Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="a6f51-135">Informacje o stanie hello również można znaleźć w dzienniku zdarzeń hello w obszarze **aplikacji i usług Log\Microsoft-dołączania**.</span><span class="sxs-lookup"><span data-stu-id="a6f51-135">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="a6f51-136">**Najczęstszymi przyczynami niepowodzenia rejestracji Hello są:**</span><span class="sxs-lookup"><span data-stu-id="a6f51-136">**hello most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="a6f51-137">Twój komputer nie jest w sieci wewnętrznej hello organizacji lub sieci VPN bez tooan połączenia lokalnego kontrolera domeny AD.</span><span class="sxs-lookup"><span data-stu-id="a6f51-137">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="a6f51-138">Użytkownik jest zalogowany tooyour komputera przy użyciu konta komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="a6f51-138">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="a6f51-139">Problemy z konfiguracją usługi:</span><span class="sxs-lookup"><span data-stu-id="a6f51-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="a6f51-140">Witaj serwer federacyjny został skonfigurowany toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="a6f51-140">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="a6f51-141">Nie ma żadnego obiektu punktu połączenia usługi, który wskazuje tooyour zweryfikowaną nazwę domeny w usłudze Azure AD w lesie hello AD, której należy komputer hello.</span><span class="sxs-lookup"><span data-stu-id="a6f51-141">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="a6f51-142">Użytkownik osiągnął limit hello urządzeń.</span><span class="sxs-lookup"><span data-stu-id="a6f51-142">A user has reached hello limit of devices.</span></span> <span data-ttu-id="a6f51-143">Zobacz wprowadzenie do rejestracji urządzeń usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a6f51-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6f51-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6f51-144">Next steps</span></span>

<span data-ttu-id="a6f51-145">Aby uzyskać więcej informacji, zobacz hello [automatycznej rejestracji urządzeń — często zadawane pytania](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="a6f51-145">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
