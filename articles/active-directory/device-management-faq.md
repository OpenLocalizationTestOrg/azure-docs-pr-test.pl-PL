---
title: "Zarządzanie urządzeniami w usłudze Azure Active Directory — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Azure Active Directory Zarządzanie urządzeniami — często zadawane pytania."
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 2934b64c693f6505ddb389766374e31a5e6f249b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-device-management-faq"></a><span data-ttu-id="b1ec7-103">Zarządzanie urządzeniami w usłudze Azure Active Directory — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="b1ec7-103">Azure Active Directory device management FAQ</span></span>

<span data-ttu-id="b1ec7-104">**Pytanie: czy mogę ostatnio zarejestrowane urządzenia. Dlaczego nie widzę urządzenia w obszarze Moje informacje użytkownika w portalu Azure?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-104">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span></span>

<span data-ttu-id="b1ec7-105">**Odpowiedź:** urządzeń z systemem Windows 10, które są przyłączone do domeny z automatycznej rejestracji urządzeń nie są wyświetlane w obszarze informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under the USER info.</span></span>
<span data-ttu-id="b1ec7-106">Należy użyć programu PowerShell, aby wyświetlić wszystkie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-106">You need to use PowerShell to see all devices.</span></span> 

<span data-ttu-id="b1ec7-107">Informacje o użytkowniku należą następujące urządzenia:</span><span class="sxs-lookup"><span data-stu-id="b1ec7-107">Only the following devices are listed under the USER info:</span></span>

- <span data-ttu-id="b1ec7-108">Wszystkich urządzeń osobistych, które nie są przyłączone do przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="b1ec7-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="b1ec7-109">Wszystkie z systemem innym niż Windows 10 / Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b1ec7-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="b1ec7-110">Wszystkie urządzenia z systemem innym niż Windows</span><span class="sxs-lookup"><span data-stu-id="b1ec7-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="b1ec7-111">**Pytanie: Dlaczego nie można wyświetlić wszystkich urządzeń zarejestrowanych w usłudze Azure Active Directory w portalu Azure?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-111">**Q: Why can I not see all the devices registered in Azure Active Directory in the Azure portal?**</span></span> 

<span data-ttu-id="b1ec7-112">**Odpowiedź:** obecnie nie istnieje sposób, aby zobaczyć wszystkie zarejestrowane urządzenia w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-112">**A:** Currently, there is no way to see all registered devices in the Azure portal.</span></span> <span data-ttu-id="b1ec7-113">Przy użyciu programu Azure PowerShell można znaleźć wszystkie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-113">You can use Azure PowerShell to find all devices.</span></span> <span data-ttu-id="b1ec7-114">Aby uzyskać więcej informacji, zobacz [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-114">For more details, see the [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="b1ec7-115">**Pytanie: jak sprawdzić, co to jest stan rejestracji urządzenia klienta?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-115">**Q: How do I know what the device registration state of the client is?**</span></span>

<span data-ttu-id="b1ec7-116">**Odpowiedź:** zależy od stanu rejestracji urządzenia:</span><span class="sxs-lookup"><span data-stu-id="b1ec7-116">**A:** The device registration state depends on:</span></span>

- <span data-ttu-id="b1ec7-117">Co to jest urządzenia</span><span class="sxs-lookup"><span data-stu-id="b1ec7-117">What the device is</span></span>
- <span data-ttu-id="b1ec7-118">Jak został zarejestrowany</span><span class="sxs-lookup"><span data-stu-id="b1ec7-118">How it was registered</span></span> 
- <span data-ttu-id="b1ec7-119">Wszystkie szczegóły z nim związane.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-119">Any details related to it.</span></span> 
 

---

<span data-ttu-id="b1ec7-120">**Pytanie: Dlaczego jest to urządzenie I został usunięty w portalu Azure lub nadal przy użyciu programu Windows PowerShell wymienione w zarejestrowany?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-120">**Q: Why is a device I have deleted in the Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="b1ec7-121">**Odpowiedź:** to jest celowe.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-121">**A:** This is by design.</span></span> <span data-ttu-id="b1ec7-122">Urządzenie nie ma dostępu do zasobów w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-122">The device will not have access to resources in the cloud.</span></span> <span data-ttu-id="b1ec7-123">Jeśli chcesz usunąć urządzenie i ponownie zarejestrować akcji ręcznej musi być podejmowane na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-123">If you want to remove the device and register again, a manual action must be to be taken on the device.</span></span> 

<span data-ttu-id="b1ec7-124">Dla systemu Windows 10 i Windows Server 2016, które są lokalne AD przyłączonych do domeny:</span><span class="sxs-lookup"><span data-stu-id="b1ec7-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="b1ec7-125">Otwórz wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-125">Open the command prompt as an administrator.</span></span>

2.  <span data-ttu-id="b1ec7-126">Typ`dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="b1ec7-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="b1ec7-127">Wyloguj się i zaloguj się do wyzwolenia zaplanowane zadanie, które ponownie zarejestrowanie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-127">Sign out and sign in to trigger the scheduled task that registers the device again.</span></span> 

<span data-ttu-id="b1ec7-128">Dla innych platform systemu Windows, które znajdują się na obszarze AD przyłączonych do domeny:</span><span class="sxs-lookup"><span data-stu-id="b1ec7-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="b1ec7-129">Otwórz wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-129">Open the command prompt as an administrator.</span></span>
2.  <span data-ttu-id="b1ec7-130">Wpisz polecenie `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="b1ec7-131">Wpisz polecenie `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="b1ec7-132">**Pytanie: Dlaczego Zobacz urządzenia zduplikowanych wpisów w portalu Azure?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="b1ec7-133">**ODP.:**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-133">**A:**</span></span>

-   <span data-ttu-id="b1ec7-134">Dla systemu Windows 10 i Windows Server 2016 jeśli są one kolejnych nieudanych prób Odłączanie i dołączyć ponownie do tego samego urządzenia mogą istnieć zduplikowane wpisy.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-134">For Windows 10 and Windows Server 2016, if they are repeated attempts to unjoin and re-join the same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="b1ec7-135">Jeśli używasz konta Dodaj firmowego lub szkolnego każdego użytkownika systemu windows, który używa konta Dodaj firmowego lub szkolnego utworzy nowy rekord urządzenia z tę samą nazwę urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span></span>

-   <span data-ttu-id="b1ec7-136">Inne platformy systemu Windows, które znajdują się na obszarze AD przyłączonych do domeny za pomocą automatycznej rejestracji utworzy nowy rekord urządzenia o takiej samej nazwie urządzeń dla każdego użytkownika domeny, który loguje się do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span></span> 

-   <span data-ttu-id="b1ec7-137">Maszyny AADJ została wyczyszczona, ponowna instalacja i ponownie połączony z tej samej nazwie, zostaną wyświetlone jako inny rekord z tą samą nazwą urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-137">An AADJ machine that has been wiped, re-installed and re-joined with the same name, will show up as another record with the same device name.</span></span>

---

<span data-ttu-id="b1ec7-138">**Pytanie: Dlaczego użytkownik nadal dostęp do zasobów z urządzenia, które można wyłączyć w portalu Azure?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-138">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span></span>

<span data-ttu-id="b1ec7-139">**Odpowiedź:** może potrwać do godziny dla odwołania do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-139">**A:** It can take up to an hour for a revoke to be applied.</span></span>

>[!Note] 
><span data-ttu-id="b1ec7-140">Dla urządzeń utracone zaleca się czyszczenie urządzenia, aby upewnić się, że użytkownicy nie mogą uzyskać dostęp do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-140">For lost devices, we recommend wiping the device to ensure that users cannot access the device.</span></span> <span data-ttu-id="b1ec7-141">Aby uzyskać więcej informacji, zobacz [rejestrowanie urządzeń do zarządzania w usłudze Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="b1ec7-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="b1ec7-142">**Pytanie: Dlaczego Moi użytkownicy widzą "Nie można pobrać istnieje w tym miejscu"?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="b1ec7-143">**Odpowiedź:** Jeśli został skonfigurowany, niektóre zasady dostępu warunkowego będą musieli stanu określonego urządzenia, a urządzenie nie spełnia kryteriów, użytkownicy są blokowane, a ten komunikat zostanie wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-143">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span></span> <span data-ttu-id="b1ec7-144">Oszacowanie reguł i upewnij się, że urządzenie jest w stanie spełnia kryteria, aby uniknąć występowania tego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-144">Please evaluate the rules and ensure that the device is able to meet the criteria to avoid this message.</span></span>

---


<span data-ttu-id="b1ec7-145">**Pytanie: Zobacz rekordem urządzenia w obszarze informacje o użytkowniku w portalu Azure i można zobaczyć stan zarejestrowany na kliencie. Czy prawidłowo skonfigurować do korzystania z dostępu warunkowego?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-145">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="b1ec7-146">**Odpowiedź:** rekord urządzenia (deviceID) i stan w portalu Azure należy zgodny klient i spełniać żadnych kryteriów oceny dostępu warunkowego.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-146">**A:** The device record (deviceID) and state on the Azure portal must match the client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="b1ec7-147">Aby uzyskać więcej informacji, zobacz [wprowadzenie do rejestracji urządzeń usługi Azure Active Directory](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="b1ec7-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="b1ec7-148">**Pytanie: Dlaczego uzyskać komunikat "Nazwa użytkownika lub hasło jest niepoprawne" dla urządzenia, które tylko po dołączeniu do usługi Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span></span>

<span data-ttu-id="b1ec7-149">**Odpowiedź:** są typowe przyczyny tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="b1ec7-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="b1ec7-150">Poświadczenia użytkownika nie są już prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="b1ec7-151">Komputer nie może nawiązać połączenia z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-151">Your computer is unable to communicate with Azure Active Directory.</span></span> <span data-ttu-id="b1ec7-152">Sprawdź, czy wszystkie problemy z połączeniem sieciowym.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="b1ec7-153">Azure AD Join wymagania wstępne nie zostały spełnione.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-153">The Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="b1ec7-154">Upewnij się, że zostały wykonane kroki [rozszerzanie funkcji chmury na urządzeniach z systemem Windows 10 za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1ec7-154">Please ensure that you have followed the steps for [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="b1ec7-155">Logowania federacyjnego wymaga serwerze federacyjnym w celu obsługi aktywny punkt końcowy protokołu WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-155">Federated logins requires your federation server to support a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="b1ec7-156">**Pytanie: Dlaczego zobacz "Oops... Wystąpił błąd!" okna dialogowego podczas próby dołączenia komputera?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-156">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="b1ec7-157">**Odpowiedź:** jest to wynik konfigurowania rejestracji usługi Azure Active Directory z usługą Intune.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="b1ec7-158">Aby uzyskać więcej informacji, zobacz [Konfigurowanie zarządzania urządzeniami z systemem Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="b1ec7-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="b1ec7-159">**Pytanie: Dlaczego moja próby dołączenia komputera nie chociaż uzyskane informacje o błędzie?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-159">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="b1ec7-160">**Odpowiedź:** prawdopodobną przyczyną jest to, że użytkownik jest zalogowany do urządzenia przy użyciu wbudowanego konta administratora.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-160">**A:** A likely cause is that the user is logged in to the device using the built-in administrator account.</span></span> <span data-ttu-id="b1ec7-161">Utwórz konto lokalne różnych przed przy użyciu usługi Azure Active Directory Join, aby ukończyć instalację.</span><span class="sxs-lookup"><span data-stu-id="b1ec7-161">Please create a different local account before using Azure Active Directory Join to complete the setup.</span></span> 

---

<span data-ttu-id="b1ec7-162">**Pytanie: gdzie można znaleźć instrukcje do instalacji automatycznej rejestracji urządzeń?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-162">**Q: Where can I find instructions for the setup of automatic device registration?**</span></span>

<span data-ttu-id="b1ec7-163">**Odpowiedź:** szczegółowe instrukcje, zobacz [Konfigurowanie automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny w usłudze Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="b1ec7-163">**A:** For detailed instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="b1ec7-164">**Pytanie: gdzie mogę znaleźć, rozwiązywanie problemów z informacji o automatycznej rejestracji urządzeń?**</span><span class="sxs-lookup"><span data-stu-id="b1ec7-164">**Q: Where can I find troubleshooting information about the automatic device registration?**</span></span>

<span data-ttu-id="b1ec7-165">**Odpowiedź:** informacje dotyczące rozwiązywania problemów, zobacz:</span><span class="sxs-lookup"><span data-stu-id="b1ec7-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="b1ec7-166">Rozwiązywanie problemów z automatyczną rejestrację domeny komputery przyłączone do usługi Azure AD — Windows 10 i Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b1ec7-166">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="b1ec7-167">Rozwiązywanie problemów z automatyczną rejestrację domeny komputery przyłączone do usługi Azure AD dla klientów niższego poziomu z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="b1ec7-167">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

