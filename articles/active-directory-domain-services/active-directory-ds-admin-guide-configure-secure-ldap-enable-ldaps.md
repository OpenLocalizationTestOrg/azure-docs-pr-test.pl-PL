---
title: "aaaConfigure bezpieczny protokół LDAP (LDAPS) w usługach domenowych Azure AD | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="2367c-103">Konfigurowanie bezpiecznego protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD</span><span class="sxs-lookup"><span data-stu-id="2367c-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2367c-104">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="2367c-104">Before you begin</span></span>
<span data-ttu-id="2367c-105">Upewnij się, przeprowadzisz [zadanie 2 - eksportu hello bezpiecznego tooa certyfikatu LDAP. Plik PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="2367c-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="2367c-106">Wybierz, czy toouse hello obsługi portalu Azure w wersji zapoznawczej lub hello Azure classic portal toocomplete to zadanie.</span><span class="sxs-lookup"><span data-stu-id="2367c-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2367c-107">**Portalu Azure (wersja zapoznawcza)**: [Włącz bezpieczny protokół LDAP przy użyciu hello portalu Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="2367c-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="2367c-108">**Klasyczny portal Azure**: [Włącz bezpieczny protokół LDAP przy użyciu klasycznego portalu Azure hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="2367c-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a><span data-ttu-id="2367c-109">Zadanie 3 — Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej hello przy użyciu hello portalu Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="2367c-109">Task 3 - enable secure LDAP for hello managed domain using hello Azure portal (Preview)</span></span>
<span data-ttu-id="2367c-110">tooenable bezpieczny protokół LDAP, wykonaj następujące kroki konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="2367c-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="2367c-111">Przejdź toohello  **[portalu Azure](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="2367c-111">Navigate toohello **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="2367c-112">Wyszukaj "usługi domeny" w hello **wyszukiwania zasobów** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2367c-112">Search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="2367c-113">Wybierz **usług domenowych Azure AD** z hello wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2367c-113">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="2367c-114">Witaj **usług domenowych Azure AD** bloku wymieniono domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="2367c-114">hello **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Znajdź zainicjowanie obsługi domeny zarządzanej](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="2367c-116">Kliknij nazwę hello toosee domeny (na przykład "contoso100.com") hello zarządzane więcej szczegółów na temat hello domeny.</span><span class="sxs-lookup"><span data-stu-id="2367c-116">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Usług domenowych — stan inicjowania obsługi](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="2367c-118">Kliknij przycisk **Secure LDAP** w okienku nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="2367c-118">Click **Secure LDAP** on hello navigation pane.</span></span>

    ![Usługi domenowe — blok bezpiecznego protokołu LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="2367c-120">Domyślnie jest wyłączona bezpiecznego LDAP dostępu tooyour domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="2367c-120">By default, secure LDAP access tooyour managed domain is disabled.</span></span> <span data-ttu-id="2367c-121">Przełącz **Secure LDAP** za**włączyć**.</span><span class="sxs-lookup"><span data-stu-id="2367c-121">Toggle **Secure LDAP** too**Enable**.</span></span>

    ![Włącz bezpieczny protokół LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="2367c-123">Domyślnie bezpiecznego tooyour dostępu LDAP zarządzane domeny przy użyciu hello internet jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="2367c-123">By default, secure LDAP access tooyour managed domain over hello internet is disabled.</span></span> <span data-ttu-id="2367c-124">Przełącz **Zezwalaj bezpiecznego dostępu LDAP za pośrednictwem hello internet** za**włączyć**, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2367c-124">Toggle **Allow secure LDAP access over hello internet** too**Enable**, if desired.</span></span> 

6. <span data-ttu-id="2367c-125">Kliknij następujące ikony folderu hello **. Plik PFX o bezpiecznego certyfikatu LDAP**.</span><span class="sxs-lookup"><span data-stu-id="2367c-125">Click hello folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="2367c-126">Określ plik PFX toohello ścieżka hello z certyfikatem hello w celu bezpiecznego LDAP dostępu toohello domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="2367c-126">Specify hello path toohello PFX file with hello certificate for secure LDAP access toohello managed domain.</span></span>

7. <span data-ttu-id="2367c-127">Określ hello **toodecrypt hasła. Plik PFX**.</span><span class="sxs-lookup"><span data-stu-id="2367c-127">Specify hello **Password toodecrypt .PFX file**.</span></span> <span data-ttu-id="2367c-128">Podaj hello samo hasło użyte podczas eksportowania pliku PFX toohello certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="2367c-128">Provide hello same password you used when exporting hello certificate toohello PFX file.</span></span>

8. <span data-ttu-id="2367c-129">Gdy wszystko będzie gotowe, kliknij przycisk hello **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2367c-129">When you are done, click hello **Save** button.</span></span>

9. <span data-ttu-id="2367c-130">Zostanie wyświetlone powiadomienie informujące, że dla domeny zarządzanej hello jest konfigurowany bezpiecznego protokołu LDAP.</span><span class="sxs-lookup"><span data-stu-id="2367c-130">You see a notification that informs you secure LDAP is being configured for hello managed domain.</span></span> <span data-ttu-id="2367c-131">Do czasu ukończenia tej operacji nie można modyfikować inne ustawienia hello domeny.</span><span class="sxs-lookup"><span data-stu-id="2367c-131">Until this operation is complete, you cannot modify other settings for hello domain.</span></span>

    ![Konfigurowanie bezpiecznego protokołu LDAP do domeny zarządzanej hello](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="2367c-133">Trwa około 10 minut too15 tooenable bezpieczny protokół LDAP do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="2367c-133">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="2367c-134">Jeśli hello pod warunkiem, że bezpiecznego LDAP certyfikatu jest niezgodny hello wymagane kryteria, dla katalogu nie włączono bezpiecznego protokołu LDAP i zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="2367c-134">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="2367c-135">Na przykład nazwa domeny hello jest niepoprawna, hello certyfikat już wygasł lub wkrótce wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="2367c-135">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span> <span data-ttu-id="2367c-136">W takim przypadku ponów próbę, używając prawidłowego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2367c-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="2367c-137">Zadanie 4 — konfigurowanie domeny zarządzanej hello tooaccess DNS z hello internet</span><span class="sxs-lookup"><span data-stu-id="2367c-137">Task 4 - configure DNS tooaccess hello managed domain from hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="2367c-138">**Opcjonalne zadania** — Jeśli nie planujesz tooaccess hello domeny zarządzanej przy użyciu LDAPS ponad hello internet, pomiń to zadanie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2367c-138">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="2367c-139">Przed rozpoczęciem tego zadania upewnij się, zostały ukończone hello czynności opisane w temacie [zadanie 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="2367c-139">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="2367c-140">Po włączeniu bezpiecznego dostępu LDAP za pośrednictwem Internetu hello potrzeby domeny zarządzanej, należy tooupdate DNS tak, aby komputery klienckie można znaleźć tej domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="2367c-140">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="2367c-141">Na końcu hello zadanie 3, zewnętrzny adres IP jest wyświetlany na powitania **właściwości** bloku w **IP adres dla LDAPS dostępu zewnętrznego**.</span><span class="sxs-lookup"><span data-stu-id="2367c-141">At hello end of task 3, an external IP address is displayed on hello **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="2367c-142">Konfigurowanie dostawcy usługi DNS zewnętrzne tej nazwy DNS hello hello zarządzane zewnętrzny adres IP toothis punktów domeny (na przykład "ldaps.contoso100.com").</span><span class="sxs-lookup"><span data-stu-id="2367c-142">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="2367c-143">W naszym przykładzie potrzebne są nam hello toocreate następującego wpisu DNS:</span><span class="sxs-lookup"><span data-stu-id="2367c-143">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="2367c-144">To wszystko — wszystko jest teraz gotowy tooconnect toohello zarządzane domeny przy użyciu bezpiecznego protokołu LDAP, za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="2367c-144">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="2367c-145">Należy pamiętać, że komputery klienckie muszą ufać Witaj wystawca hello LDAPS certyfikatu toobe stanie tooconnect pomyślnie toohello zarządzane przy użyciu LDAPS domeny.</span><span class="sxs-lookup"><span data-stu-id="2367c-145">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="2367c-146">Jeśli używasz publicznie zaufany urząd certyfikacji, nie trzeba toodo niczego, ponieważ komputery klienckie ufać tych wystawców certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="2367c-146">If you are using a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="2367c-147">Jeśli używasz certyfikatu z podpisem własnym, należy zainstalować hello publicznego część hello certyfikatu z podpisem własnym do magazynu zaufanych certyfikatów hello na komputerze klienckim hello.</span><span class="sxs-lookup"><span data-stu-id="2367c-147">If you are using a self-signed certificate, install hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="2367c-148">Zadanie 5 - LDAPS blokowanie dostępu tooyour zarządzane domeny za pośrednictwem hello internet</span><span class="sxs-lookup"><span data-stu-id="2367c-148">Task 5 - lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="2367c-149">**Opcjonalne zadania** — Jeśli nie włączono LDAPS domeny zarządzanej toohello dostępu ponad hello internet, pomiń to zadanie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2367c-149">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="2367c-150">Przed rozpoczęciem tego zadania upewnij się, zostały ukończone hello czynności opisane w temacie [zadanie 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="2367c-150">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="2367c-151">Udostępnianie domeny zarządzanej LDAPS dostępu za pośrednictwem hello internet reprezentuje zagrożenie bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="2367c-151">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="2367c-152">Witaj domeny zarządzanej jest dostępny z hello internet na powitania port używany do bezpiecznego protokołu LDAP (to znaczy port 636).</span><span class="sxs-lookup"><span data-stu-id="2367c-152">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="2367c-153">W związku z tym można toorestrict dostępu toohello zarządzane domeny toospecific znane adresy IP.</span><span class="sxs-lookup"><span data-stu-id="2367c-153">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="2367c-154">Ze względów bezpieczeństwa należy utworzyć grupę zabezpieczeń sieci (NSG) i powiązać ją z podsieci hello, w której włączono usługi domenowe Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2367c-154">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="2367c-155">Witaj poniższej tabeli przedstawiono przykład grupy NSG można skonfigurować toolock dół bezpiecznego dostępu LDAP na powitania internet.</span><span class="sxs-lookup"><span data-stu-id="2367c-155">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="2367c-156">Hello NSG zawiera zestaw reguł, które zezwolić na przychodzący LDAPS dostęp za pośrednictwem portu TCP 636 tylko z określonego zestawu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="2367c-156">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="2367c-157">Hello domyślne "DenyAll" reguła ma zastosowanie tooall pozostały przychodzący ruch z hello internet.</span><span class="sxs-lookup"><span data-stu-id="2367c-157">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="2367c-158">Witaj NSG reguły tooallow LDAPS dostęp za pośrednictwem hello internet z określonych adresów IP ma wyższy priorytet niż hello reguły DenyAll NSG.</span><span class="sxs-lookup"><span data-stu-id="2367c-158">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Przykład grupy NSG toosecure LDAPS dostęp za pośrednictwem hello internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="2367c-160">**Więcej informacji** - [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="2367c-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="2367c-161">Zawartość pokrewna</span><span class="sxs-lookup"><span data-stu-id="2367c-161">Related content</span></span>
* [<span data-ttu-id="2367c-162">Usługi domenowe AD Azure - Przewodnik wprowadzający</span><span class="sxs-lookup"><span data-stu-id="2367c-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="2367c-163">Administrowanie domeną zarządzaną usług Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="2367c-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="2367c-164">Administrowanie zasad grupy w domenie zarządzanej usług domenowych Azure AD</span><span class="sxs-lookup"><span data-stu-id="2367c-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="2367c-165">Sieciowe grupy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="2367c-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="2367c-166">Utwórz grupę zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="2367c-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
