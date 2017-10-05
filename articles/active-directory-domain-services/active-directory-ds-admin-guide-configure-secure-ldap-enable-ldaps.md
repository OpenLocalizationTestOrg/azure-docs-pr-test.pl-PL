---
title: "Skonfigurować bezpiecznego protokołu LDAP (LDAPS) w usługach domenowych Azure AD | Dokumentacja firmy Microsoft"
description: "Skonfiguruj zabezpieczenia protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 3b19f078b0d6dc3e02d951014056406fd1b099a8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="2635a-103">Konfigurowanie bezpiecznego protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD</span><span class="sxs-lookup"><span data-stu-id="2635a-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2635a-104">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="2635a-104">Before you begin</span></span>
<span data-ttu-id="2635a-105">Upewnij się, przeprowadzisz [zadanie 2 - wyeksportowany certyfikat bezpiecznego LDAP. Plik PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="2635a-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="2635a-106">Wybierz, czy użyć wersji zapoznawczej obsługi portalu Azure lub klasycznego portalu Azure do zakończenia tego zadania.</span><span class="sxs-lookup"><span data-stu-id="2635a-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2635a-107">**Portalu Azure (wersja zapoznawcza)**: [Włącz bezpieczny protokół LDAP przy użyciu portalu Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="2635a-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="2635a-108">**Klasyczny portal Azure**: [Włącz bezpieczny protokół LDAP przy użyciu klasycznego portalu Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="2635a-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview"></a><span data-ttu-id="2635a-109">Zadanie 3 — Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej przy użyciu portalu Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="2635a-109">Task 3 - enable secure LDAP for the managed domain using the Azure portal (Preview)</span></span>
<span data-ttu-id="2635a-110">Aby włączyć bezpiecznego protokołu LDAP, wykonaj następujące kroki konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="2635a-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="2635a-111">Przejdź do  **[portalu Azure](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="2635a-111">Navigate to the **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="2635a-112">Wyszukaj "usługi domeny" w **wyszukiwania zasobów** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2635a-112">Search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="2635a-113">Wybierz **usług domenowych Azure AD** z wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2635a-113">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="2635a-114">**Usług domenowych Azure AD** bloku wymieniono domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="2635a-114">The **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Znajdź zainicjowanie obsługi domeny zarządzanej](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="2635a-116">Kliknij nazwę domeny zarządzanej (na przykład "contoso100.com"), aby zobaczyć więcej szczegółów dotyczących domeny.</span><span class="sxs-lookup"><span data-stu-id="2635a-116">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Usług domenowych — stan inicjowania obsługi](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="2635a-118">Kliknij przycisk **Secure LDAP** w okienku nawigacji.</span><span class="sxs-lookup"><span data-stu-id="2635a-118">Click **Secure LDAP** on the navigation pane.</span></span>

    ![Usługi domenowe — blok bezpiecznego protokołu LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="2635a-120">Bezpieczny dostęp LDAP do domeny zarządzanej jest domyślnie wyłączona.</span><span class="sxs-lookup"><span data-stu-id="2635a-120">By default, secure LDAP access to your managed domain is disabled.</span></span> <span data-ttu-id="2635a-121">Przełącz **bezpieczny protokół LDAP** do **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="2635a-121">Toggle **Secure LDAP** to **Enable**.</span></span>

    ![Włącz bezpieczny protokół LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="2635a-123">Domyślnie bezpieczny dostęp LDAP do domeny zarządzanej za pośrednictwem Internetu jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="2635a-123">By default, secure LDAP access to your managed domain over the internet is disabled.</span></span> <span data-ttu-id="2635a-124">Przełącz **zapewnia bezpieczny dostęp LDAP w Internecie** do **włączyć**, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2635a-124">Toggle **Allow secure LDAP access over the internet** to **Enable**, if desired.</span></span> 

6. <span data-ttu-id="2635a-125">Kliknij ikonę następujący folder **. Plik PFX o bezpiecznego certyfikatu LDAP**.</span><span class="sxs-lookup"><span data-stu-id="2635a-125">Click the folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="2635a-126">Określ ścieżkę do pliku PFX z certyfikatu na potrzeby bezpiecznego dostępu LDAP do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="2635a-126">Specify the path to the PFX file with the certificate for secure LDAP access to the managed domain.</span></span>

7. <span data-ttu-id="2635a-127">Określ **hasła do odszyfrowywania. Plik PFX**.</span><span class="sxs-lookup"><span data-stu-id="2635a-127">Specify the **Password to decrypt .PFX file**.</span></span> <span data-ttu-id="2635a-128">Należy podać to samo hasło użyte podczas eksportowania certyfikatu do pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="2635a-128">Provide the same password you used when exporting the certificate to the PFX file.</span></span>

8. <span data-ttu-id="2635a-129">Gdy wszystko będzie gotowe, kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2635a-129">When you are done, click the **Save** button.</span></span>

9. <span data-ttu-id="2635a-130">Zobaczysz, że powiadomienie, które informuje, że bezpieczny protokół LDAP jest konfigurowany do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="2635a-130">You see a notification that informs you secure LDAP is being configured for the managed domain.</span></span> <span data-ttu-id="2635a-131">Do czasu ukończenia tej operacji nie można modyfikować inne ustawienia domeny.</span><span class="sxs-lookup"><span data-stu-id="2635a-131">Until this operation is complete, you cannot modify other settings for the domain.</span></span>

    ![Konfigurowanie bezpiecznego protokołu LDAP do domeny zarządzanej](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="2635a-133">Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej trwa około 10 – 15 minut.</span><span class="sxs-lookup"><span data-stu-id="2635a-133">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="2635a-134">Certyfikatu podanego LDAP bezpiecznego niezgodna kryteriów wymaganych dla katalogu nie włączono bezpiecznego protokołu LDAP i zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="2635a-134">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="2635a-135">Na przykład nazwa domeny jest nieprawidłowa, certyfikat już wygasł lub wkrótce wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="2635a-135">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span> <span data-ttu-id="2635a-136">W takim przypadku ponów próbę, używając prawidłowego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2635a-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="2635a-137">Zadanie 4 — Konfigurowanie systemu DNS w celu uzyskiwania dostępu do domeny zarządzanej z Internetu</span><span class="sxs-lookup"><span data-stu-id="2635a-137">Task 4 - configure DNS to access the managed domain from the internet</span></span>
> [!NOTE]
> <span data-ttu-id="2635a-138">**Opcjonalne zadania** — Jeśli nie ma dostępu do domeny zarządzanej przy użyciu LDAPS za pośrednictwem Internetu, pomiń to zadanie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2635a-138">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="2635a-139">Przed rozpoczęciem tego zadania upewnij się, zostały wykonane kroki opisane w temacie [zadanie 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="2635a-139">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="2635a-140">Po włączeniu bezpiecznego dostępu LDAP w Internecie dla domeny zarządzanej, musisz zaktualizować DNS tak, aby komputery klienckie można znaleźć tej domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="2635a-140">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="2635a-141">Na koniec zadanie 3 zewnętrzny adres IP jest wyświetlany na **właściwości** bloku w **IP adres dla LDAPS dostępu zewnętrznego**.</span><span class="sxs-lookup"><span data-stu-id="2635a-141">At the end of task 3, an external IP address is displayed on the **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="2635a-142">Tak, aby nazwa DNS domeny zarządzanej (na przykład "ldaps.contoso100.com") wskazuje to zewnętrzny adres IP, należy skonfigurować zewnętrznego dostawcy usługi DNS.</span><span class="sxs-lookup"><span data-stu-id="2635a-142">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="2635a-143">W tym przykładzie należy utworzyć następujący wpis DNS:</span><span class="sxs-lookup"><span data-stu-id="2635a-143">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="2635a-144">To wszystko — teraz można przystąpić do nawiązania połączenia domeny zarządzanej przy użyciu bezpiecznego protokołu LDAP, za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="2635a-144">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="2635a-145">Należy pamiętać, że komputery klienckie muszą ufać wystawcy certyfikatu LDAPS, aby można było pomyślnie nawiązać połączenie przy użyciu LDAPS domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="2635a-145">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="2635a-146">Jeśli używasz publicznie zaufany urząd certyfikacji, nie trzeba nic robić, ponieważ komputery klienckie ufać tych wystawców certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="2635a-146">If you are using a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="2635a-147">Jeśli używasz certyfikatu z podpisem własnym, należy zainstalować części publicznego certyfikatu z podpisem własnym do magazynu zaufanych certyfikatów na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="2635a-147">If you are using a self-signed certificate, install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="2635a-148">Zadanie 5 - blokowanie dostępu LDAPS do domeny zarządzanej za pośrednictwem Internetu</span><span class="sxs-lookup"><span data-stu-id="2635a-148">Task 5 - lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="2635a-149">**Opcjonalne zadania** — Jeśli nie włączono dostępu LDAPS do domeny zarządzanej za pośrednictwem Internetu, pomiń to zadanie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2635a-149">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="2635a-150">Przed rozpoczęciem tego zadania upewnij się, zostały wykonane kroki opisane w temacie [zadanie 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="2635a-150">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="2635a-151">Udostępnianie domeny zarządzanej LDAPS dostępu przez internet stanowi zagrożenie bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="2635a-151">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="2635a-152">Domeny zarządzanej jest dostępny z Internetu na port używany do bezpiecznego protokołu LDAP (to znaczy port 636).</span><span class="sxs-lookup"><span data-stu-id="2635a-152">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="2635a-153">W związku z tym można ograniczyć dostęp do domeny zarządzanej, aby określić adresy IP znane.</span><span class="sxs-lookup"><span data-stu-id="2635a-153">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="2635a-154">Ze względów bezpieczeństwa należy utworzyć grupę zabezpieczeń sieci (NSG) i powiązać ją z podsieci, w której włączono usługi domenowe Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2635a-154">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="2635a-155">W poniższej tabeli przedstawiono przykład grupy NSG można skonfigurować do blokowania bezpiecznego dostępu LDAP w Internecie.</span><span class="sxs-lookup"><span data-stu-id="2635a-155">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="2635a-156">Grupa NSG zawiera zestaw reguł, które zezwolić na przychodzący LDAPS dostęp za pośrednictwem portu TCP 636 tylko z określonego zestawu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="2635a-156">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="2635a-157">Domyślna reguła "DenyAll" dotyczy cały ruch przychodzący z Internetu.</span><span class="sxs-lookup"><span data-stu-id="2635a-157">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="2635a-158">Reguły NSG umożliwiają LDAPS dostęp przez internet z określonych adresów IP ma wyższy priorytet niż reguły DenyAll NSG.</span><span class="sxs-lookup"><span data-stu-id="2635a-158">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![Przykład grupy NSG bezpieczny dostęp do LDAPS w Internecie](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="2635a-160">**Więcej informacji** - [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="2635a-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="2635a-161">Zawartość pokrewna</span><span class="sxs-lookup"><span data-stu-id="2635a-161">Related content</span></span>
* [<span data-ttu-id="2635a-162">Usługi domenowe AD Azure - Przewodnik wprowadzający</span><span class="sxs-lookup"><span data-stu-id="2635a-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="2635a-163">Administrowanie domeną zarządzaną usług Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="2635a-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="2635a-164">Administrowanie zasad grupy w domenie zarządzanej usług domenowych Azure AD</span><span class="sxs-lookup"><span data-stu-id="2635a-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="2635a-165">Sieciowe grupy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="2635a-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="2635a-166">Utwórz grupę zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="2635a-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
