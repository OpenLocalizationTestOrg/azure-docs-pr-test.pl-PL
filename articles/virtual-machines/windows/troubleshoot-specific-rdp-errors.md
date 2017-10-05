---
title: "Określone komunikaty o błędach protokołu RDP dla maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Zrozumienie określone komunikaty o błędach, które można napotkać podczas próby użycia Podłączanie pulpitu zdalnego do maszyny wirtualnej systemu Windows na platformie Azure"
keywords: "Błąd pulpitu zdalnego, błąd połączeń usług pulpitu zdalnego, nie można połączyć z maszyną wirtualną, rozwiązywania problemów pulpitu zdalnego"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: e7c049106726a15e96d4ebe7c7c0388a29c546c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-to-a-windows-vm-in-azure"></a><span data-ttu-id="cc8a7-104">Rozwiązywanie problemów z określone komunikaty o błędach protokołu RDP do maszyny Wirtualnej systemu Windows na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="cc8a7-104">Troubleshooting specific RDP error messages to a Windows VM in Azure</span></span>
<span data-ttu-id="cc8a7-105">W trakcie przy użyciu połączenia pulpitu zdalnego z maszyną wirtualną (VM) systemu Windows na platformie Azure może zostać wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-105">You may receive a specific error message when using Remote Desktop connection to a Windows virtual machine (VM) in Azure.</span></span> <span data-ttu-id="cc8a7-106">Ten artykuł zawiera szczegóły dotyczące niektórych bardziej typowe komunikaty o błędach napotkano wraz z czynności pozwalające rozwiązać je.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-106">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span> <span data-ttu-id="cc8a7-107">Jeśli występują problemy dotyczące nawiązywania połączenia z maszyną Wirtualną za pomocą protokołu RDP ale czy nie występują komunikat o błędzie, zobacz [Podręcznik rozwiązywania problemów dotyczących usług pulpitu zdalnego](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-107">If you are having issues connecting to your VM using RDP but do not encounter a specific error message, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="cc8a7-108">Aby uzyskać informacje na określone komunikaty o błędach zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="cc8a7-108">For information on specific error messages, see the following:</span></span>

* <span data-ttu-id="cc8a7-109">[Sesja zdalna została rozłączona, ponieważ nie nie zdalne serwery licencji usług pulpitu do dyspozycji licencji](#rdplicense).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-109">[The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license](#rdplicense).</span></span>
* <span data-ttu-id="cc8a7-110">[Pulpit zdalny nie może odnaleźć komputera "name"](#rdpname).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-110">[Remote Desktop can't find the computer "name"](#rdpname).</span></span>
* <span data-ttu-id="cc8a7-111">[Wystąpił błąd uwierzytelniania. Nie można skontaktować się z urzędu zabezpieczeń lokalnych](#rdpauth).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-111">[An authentication error has occurred. The Local Security Authority cannot be contacted](#rdpauth).</span></span>
* <span data-ttu-id="cc8a7-112">[Błąd zabezpieczeń systemu Windows: Twoje poświadczenia nie działają](#wincred).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-112">[Windows Security error: Your credentials did not work](#wincred).</span></span>
* <span data-ttu-id="cc8a7-113">[Ten komputer nie może połączyć się z komputerem zdalnym](#rdpconnect).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-113">[This computer can't connect to the remote computer](#rdpconnect).</span></span>

<a id="rdplicense"></a>

## <a name="the-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-to-provide-a-license"></a><span data-ttu-id="cc8a7-114">Sesja zdalna została rozłączona, ponieważ nie nie zdalne serwery licencji usług pulpitu do dyspozycji licencji.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-114">The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license.</span></span>
<span data-ttu-id="cc8a7-115">Przyczyna: 120-dniowy okres prolongaty licencjonowania dla roli serwera usług pulpitu zdalnego wygasł i musisz zainstalować licencji.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-115">Cause: The 120-day licensing grace period for the Remote Desktop Server role has expired and you need to install licenses.</span></span>

<span data-ttu-id="cc8a7-116">Jako obejście zapisać lokalną kopię pliku RDP z portalu i uruchom to polecenie w wierszu polecenia programu PowerShell do połączenia.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-116">As a workaround, save a local copy of the RDP file from the portal and run this command at a PowerShell command prompt to connect.</span></span> <span data-ttu-id="cc8a7-117">Ten krok powoduje wyłączenie Licencjonowanie tylko tego połączenia:</span><span class="sxs-lookup"><span data-stu-id="cc8a7-117">This step disables licensing for just that connection:</span></span>

        mstsc <File name>.RDP /admin

<span data-ttu-id="cc8a7-118">Jeśli nie potrzebujesz faktycznie więcej niż dwóch jednoczesnych połączeń usług pulpitu zdalnego do maszyny Wirtualnej, należy usunąć rolę serwera usług pulpitu zdalnego przy użyciu Menedżera serwera.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-118">If you don't actually need more than two simultaneous Remote Desktop connections to the VM, you can use Server Manager to remove the Remote Desktop Server role.</span></span>

<span data-ttu-id="cc8a7-119">Aby uzyskać więcej informacji, zobacz w blogu [maszyny Wirtualnej platformy Azure nie powiodło się "Nie serwerów usług pulpitu zdalnego licencji dostępnych"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-119">For more information, see the blog post [Azure VM fails with "No Remote Desktop License Servers available"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span></span>

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-the-computer-name"></a><span data-ttu-id="cc8a7-120">Pulpit zdalny nie może odnaleźć komputera "name".</span><span class="sxs-lookup"><span data-stu-id="cc8a7-120">Remote Desktop can't find the computer "name".</span></span>
<span data-ttu-id="cc8a7-121">Przyczyna: Klient pulpitu zdalnego na komputerze nie można rozpoznać nazwy komputera w ustawieniach pliku RDP.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-121">Cause: The Remote Desktop client on your computer can't resolve the name of the computer in the settings of the RDP file.</span></span>

<span data-ttu-id="cc8a7-122">Możliwe rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="cc8a7-122">Possible solutions:</span></span>

* <span data-ttu-id="cc8a7-123">Jeśli jesteś w intranecie firmy, upewnij się, że komputer ma dostęp do serwera proxy i może wysyłać ruch HTTPS do niej.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-123">If you're on an organization's intranet, make sure that your computer has access to the proxy server and can send HTTPS traffic to it.</span></span>
* <span data-ttu-id="cc8a7-124">Jeśli korzystasz z lokalnie przechowywanego pliku RDP, spróbuj użyć ten, który jest generowany przez portal.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-124">If you're using a locally stored RDP file, try using the one that's generated by the portal.</span></span> <span data-ttu-id="cc8a7-125">Ten krok zapewnia poprawną nazwę DNS maszyny wirtualnej lub usługi w chmurze i port punktu końcowego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-125">This step ensures that you have the correct DNS name for the virtual machine, or the cloud service and the endpoint port of the VM.</span></span> <span data-ttu-id="cc8a7-126">Oto przykładowy plik RDP, generowane przez portalu:</span><span class="sxs-lookup"><span data-stu-id="cc8a7-126">Here is a sample RDP file generated by the portal:</span></span>
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

<span data-ttu-id="cc8a7-127">Ma adres część tego pliku RDP:</span><span class="sxs-lookup"><span data-stu-id="cc8a7-127">The address portion of this RDP file has:</span></span>

* <span data-ttu-id="cc8a7-128">W pełni kwalifikowaną nazwę usługi w chmurze, która zawiera maszyny Wirtualnej ("tailspin-azdatatier.cloudapp.net" w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-128">The fully qualified domain name of the cloud service that contains the VM ("tailspin-azdatatier.cloudapp.net" in this example).</span></span>
* <span data-ttu-id="cc8a7-129">Port TCP zewnętrznego punktu końcowego dla ruchu pulpitu zdalnego (55919).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-129">The external TCP port of the endpoint for Remote Desktop traffic (55919).</span></span>

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-the-local-security-authority-cannot-be-contacted"></a><span data-ttu-id="cc8a7-130">Wystąpił błąd uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-130">An authentication error has occurred.</span></span> <span data-ttu-id="cc8a7-131">Nie można skontaktować się z urzędu zabezpieczeń lokalnych.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-131">The Local Security Authority cannot be contacted.</span></span>
<span data-ttu-id="cc8a7-132">Przyczyna: Docelowy maszyny Wirtualnej nie może zlokalizować urzędu zabezpieczeń w części zawierającej nazwę użytkownika poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-132">Cause: The target VM can't locate the security authority in the user name portion of your credentials.</span></span>

<span data-ttu-id="cc8a7-133">Jeśli nazwa użytkownika jest w formie *SecurityAuthority*\\*UserName* (przykład: CORP\User1), *SecurityAuthority* fragment jest nazwa komputera maszyny Wirtualnej (dla urzędu zabezpieczeń lokalnych) lub nazwy domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-133">When your user name is in the form *SecurityAuthority*\\*UserName* (example: CORP\User1), the *SecurityAuthority* portion is either the VM's computer name (for the local security authority) or an Active Directory domain name.</span></span>

<span data-ttu-id="cc8a7-134">Możliwe rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="cc8a7-134">Possible solutions:</span></span>

* <span data-ttu-id="cc8a7-135">Jeśli konto jest kontem lokalnym na maszynie wirtualnej, upewnij się, że nazwa maszyny Wirtualnej jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-135">If the account is local to the VM, make sure that the VM name is spelled correctly.</span></span>
* <span data-ttu-id="cc8a7-136">Jeśli konto znajduje się w domenie usługi Active Directory, Sprawdź pisownię nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-136">If the account is on an Active Directory domain, check the spelling of the domain name.</span></span>
* <span data-ttu-id="cc8a7-137">Jeśli konto domeny usługi Active Directory i nazwa domeny została wpisana poprawnie, sprawdź, czy kontroler domeny jest dostępny w tej domenie.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-137">If it is an Active Directory domain account and the domain name is spelled correctly, verify that a domain controller is available in that domain.</span></span> <span data-ttu-id="cc8a7-138">Jest typowym problemem w sieci wirtualnych platformy Azure, zawierających kontrolery domeny, że kontroler domeny jest niedostępna, ponieważ nie została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-138">It's a common issue in Azure virtual networks that contain domain controllers that a domain controller is unavailable because it hasn't been started.</span></span> <span data-ttu-id="cc8a7-139">Jako rozwiązanie alternatywne można użyć konta administratora lokalnego zamiast konta domeny.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-139">As a workaround, you can use a local administrator account instead of a domain account.</span></span>

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a><span data-ttu-id="cc8a7-140">Błąd zabezpieczeń systemu Windows: Twoje poświadczenia nie działają.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-140">Windows Security error: Your credentials did not work.</span></span>
<span data-ttu-id="cc8a7-141">Przyczyna: Docelowy maszyny Wirtualnej nie może zweryfikować nazwę konta i hasło.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-141">Cause: The target VM can't validate your account name and password.</span></span>

<span data-ttu-id="cc8a7-142">Komputer z systemem Windows można zweryfikować poświadczeń konta lokalnego lub konta domeny.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-142">A Windows-based computer can validate the credentials of either a local account or a domain account.</span></span>

* <span data-ttu-id="cc8a7-143">Dla kont lokalnych, użyj *ComputerName*\\*UserName* składni (przykład: SQL1\Admin4798).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-143">For local accounts, use the *ComputerName*\\*UserName* syntax (example: SQL1\Admin4798).</span></span>
* <span data-ttu-id="cc8a7-144">Dla kont domeny, użyj *DomainName*\\*UserName* składni (przykład: CONTOSO\peterodman).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-144">For domain accounts, use the *DomainName*\\*UserName* syntax (example: CONTOSO\peterodman).</span></span>

<span data-ttu-id="cc8a7-145">Jeśli zostały awansowane maszyny Wirtualnej do kontrolera domeny w nowym lesie usługi Active Directory, który podpisany przy użyciu konta administratora lokalnego jest konwertowana na równoważne konta z tego samego hasła w nowym lesie i domenie.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-145">If you have promoted your VM to a domain controller in a new Active Directory forest, the local administrator account that you signed in with is converted to an equivalent account with the same password in the new forest and domain.</span></span> <span data-ttu-id="cc8a7-146">Konto lokalne jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-146">The local account is then deleted.</span></span>

<span data-ttu-id="cc8a7-147">Na przykład jeśli jest zalogowany za pomocą konta lokalnego DC1\DCAdmin, a następnie podwyższony maszynę wirtualną jako kontroler domeny w nowym lesie dla domeny corp.contoso.com, konta lokalnego DC1\DCAdmin zostaje usunięta, a nowe konto domeny (CORP\DCAdmin) jest tworzony przy użyciu tego samego hasła.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-147">For example, if you signed in with the local account DC1\DCAdmin, and then promoted the virtual machine as a domain controller in a new forest for the corp.contoso.com domain, the DC1\DCAdmin local account gets deleted and a new domain account (CORP\DCAdmin) is created with the same password.</span></span>

<span data-ttu-id="cc8a7-148">Upewnij się, że nazwa konta jest nazwę maszyny wirtualnej można sprawdzić jako prawidłowe konto i że hasło jest prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-148">Make sure that the account name is a name that the virtual machine can verify as a valid account, and that the password is correct.</span></span>

<span data-ttu-id="cc8a7-149">Jeśli musisz zmienić hasło konta administratora lokalnego, zobacz [sposób resetowania hasła lub usługi pulpitu zdalnego dla maszyn wirtualnych systemu Windows](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-149">If you need to change the password of the local administrator account, see [How to reset a password or the Remote Desktop service for Windows virtual machines](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-to-the-remote-computer"></a><span data-ttu-id="cc8a7-150">Ten komputer nie może połączyć się z komputerem zdalnym.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-150">This computer can't connect to the remote computer.</span></span>
<span data-ttu-id="cc8a7-151">Przyczyna: Konto, które służy do łączenia nie ma pulpitu zdalnego logowania praw.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-151">Cause: The account that's used to connect does not have Remote Desktop sign-in rights.</span></span>

<span data-ttu-id="cc8a7-152">Każdy komputer z systemem Windows ma pulpitu zdalnego użytkownicy grupy lokalnej, która zawiera konta i grupy, które można zdalnie Zaloguj się do niego.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-152">Every Windows computer has a Remote Desktop users local group, which contains the accounts and groups that can sign into it remotely.</span></span> <span data-ttu-id="cc8a7-153">Członkowie grupy Administratorzy lokalni mają także dostęp, nawet jeśli te konta nie są wyświetlane w lokalnej grupie Użytkownicy pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-153">Members of the local administrators group also have access, even though those accounts are not listed in the Remote Desktop users local group.</span></span> <span data-ttu-id="cc8a7-154">W przypadku komputerów przyłączonych do domeny do lokalnej grupy administratorów zawiera także Administratorzy domeny w domenie.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-154">For domain-joined machines, the local administrators group also contains the domain administrators for the domain.</span></span>

<span data-ttu-id="cc8a7-155">Upewnij się, że konto, którego używasz nawiązać połączenia z uprawnieniami pulpitu zdalnego logowania.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-155">Make sure that the account you're using to connect with has Remote Desktop sign-in rights.</span></span> <span data-ttu-id="cc8a7-156">Jako obejście za pomocą domeny lub lokalnego konta administratora połączenia za pośrednictwem pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="cc8a7-156">As a workaround, use a domain or local administrator account to connect over Remote Desktop.</span></span> <span data-ttu-id="cc8a7-157">Aby dodać odpowiednie konto do lokalnej grupy użytkowników pulpitu zdalnego, należy użyć przystawki programu Microsoft Management Console (**Narzędzia systemowe > Użytkownicy i grupy lokalne > grupy > Użytkownicy pulpitu zdalnego**).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-157">To add the desired account to the Remote Desktop users local group, use the Microsoft Management Console snap-in (**System Tools > Local Users and Groups > Groups > Remote Desktop Users**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc8a7-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cc8a7-158">Next steps</span></span>
<span data-ttu-id="cc8a7-159">Jeśli żaden z tych błędów wystąpił i konieczne jest nieznany problem z połączeniem się przy użyciu protokołu RDP, zobacz [Podręcznik rozwiązywania problemów dotyczących usług pulpitu zdalnego](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-159">If none of these errors occurred and you have an unknown issue with connecting using RDP, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="cc8a7-160">Kroki podczas uzyskiwania dostępu do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów z dostępem do aplikacji uruchomionej na maszynie Wirtualnej platformy Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-160">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access to an application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="cc8a7-161">Jeśli występują problemy przy użyciu protokołu Secure Shell (SSH) do połączenia z maszyną wirtualną systemu Linux na platformie Azure, zobacz [połączeń Rozwiązywanie problemów z SSH z maszyną wirtualną systemu Linux na platformie Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc8a7-161">If you are having issues using Secure Shell (SSH) to connect to a Linux VM in Azure, see [Troubleshoot SSH connections to a Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

