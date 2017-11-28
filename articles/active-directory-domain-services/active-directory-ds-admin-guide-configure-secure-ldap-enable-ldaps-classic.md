---
title: "aaaConfigure bezpieczny protokół LDAP (LDAPS) w usługach domenowych Azure AD | Dokumentacja firmy Microsoft"
description: "Skonfiguruj zabezpieczenia protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="379a3-103">Konfigurowanie bezpiecznego protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD</span><span class="sxs-lookup"><span data-stu-id="379a3-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="379a3-104">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="379a3-104">Before you begin</span></span>
<span data-ttu-id="379a3-105">Upewnij się, przeprowadzisz [zadanie 2 - eksportu hello bezpiecznego tooa certyfikatu LDAP. Plik PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="379a3-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="379a3-106">Wybierz, czy toouse hello obsługi portalu Azure w wersji zapoznawczej lub hello Azure classic portal toocomplete to zadanie.</span><span class="sxs-lookup"><span data-stu-id="379a3-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="379a3-107">**Portalu Azure (wersja zapoznawcza)**: [Włącz bezpieczny protokół LDAP przy użyciu hello portalu Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="379a3-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="379a3-108">**Klasyczny portal Azure**: [Włącz bezpieczny protokół LDAP przy użyciu klasycznego portalu Azure hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="379a3-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a><span data-ttu-id="379a3-109">Zadanie 3 — Włączanie bezpiecznego protokołu LDAP do domeny zarządzanej hello przy użyciu klasycznego portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="379a3-109">Task 3 - enable secure LDAP for hello managed domain using hello classic Azure portal</span></span>
<span data-ttu-id="379a3-110">tooenable bezpieczny protokół LDAP, wykonaj następujące kroki konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="379a3-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="379a3-111">Przejdź toohello  **[klasycznego portalu Azure](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="379a3-111">Navigate toohello **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="379a3-112">Wybierz hello **usługi Active Directory** węzła w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="379a3-112">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="379a3-113">Wybierz katalog hello Azure AD (również określonego tooas "dzierżawy"), dla której włączono usługi domenowe Azure AD.</span><span class="sxs-lookup"><span data-stu-id="379a3-113">Select hello Azure AD directory (also referred tooas 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Wybieranie katalogu usługi Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="379a3-115">Kliknij przycisk hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="379a3-115">Click hello **Configure** tab.</span></span>

    ![Karta Konfigurowanie w katalogu](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="379a3-117">Przewiń w dół do sekcji toohello **usług domenowych w usłudze**.</span><span class="sxs-lookup"><span data-stu-id="379a3-117">Scroll down toohello section titled **domain services**.</span></span> <span data-ttu-id="379a3-118">Powinny pojawić się opcję o nazwie **bezpiecznego protokołu LDAP (LDAPS)** pokazane na powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="379a3-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in hello following screenshot:</span></span>

    ![Sekcja konfiguracji usług domenowych](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="379a3-120">Kliknij przycisk hello **Konfigurowanie certyfikatu...**  toobring przycisk zapasowej hello **Konfigurowanie certyfikatu protokołu Secure LDAP** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="379a3-120">Click hello **Configure certificate ...** button toobring up hello **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Konfigurowanie certyfikatu do bezpiecznego protokołu LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="379a3-122">Kliknij następujące ikony folderu hello **certyfikat z pliku PFX** pliku PFX hello toospecify, który zawiera certyfikat hello mają toouse dla bezpiecznej toohello dostępu LDAP zarządzane domeny.</span><span class="sxs-lookup"><span data-stu-id="379a3-122">Click hello folder icon following **PFX FILE WITH CERTIFICATE** toospecify hello PFX file, which contains hello certificate you wish toouse for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="379a3-123">Także wprowadzić hello hasło podczas eksportowania pliku PFX toohello certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="379a3-123">Also enter hello password you specified when exporting hello certificate toohello PFX file.</span></span> <span data-ttu-id="379a3-124">Następnie kliknij przycisk hello przycisk na dole hello gotowe.</span><span class="sxs-lookup"><span data-stu-id="379a3-124">Then, click hello done button on hello bottom.</span></span>

    ![Określ plik LDAP PFX bezpiecznego i hasło](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="379a3-126">Hello **usług domenowych w usłudze** sekcji hello **Konfiguruj** kartę uzyskać wygaszone i znajduje się w hello **oczekujących...**  stanu kilka minut.</span><span class="sxs-lookup"><span data-stu-id="379a3-126">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="379a3-127">W tym okresie hello LDAPS certyfikat został zweryfikowany dokładność i skonfigurowano bezpiecznego protokołu LDAP do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="379a3-127">During this period, hello LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![Bezpieczny protokół LDAP — stan oczekiwania](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="379a3-129">Trwa około 10 minut too15 tooenable bezpieczny protokół LDAP do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="379a3-129">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="379a3-130">Jeśli hello pod warunkiem, że bezpiecznego LDAP certyfikatu jest niezgodny hello wymagane kryteria, dla katalogu nie włączono bezpiecznego protokołu LDAP i zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="379a3-130">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="379a3-131">Na przykład nazwa domeny hello jest niepoprawna, hello certyfikat już wygasł lub wkrótce wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="379a3-131">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="379a3-132">Gdy pomyślnie włączono bezpiecznego protokołu LDAP do domeny zarządzanej, hello **oczekujących...**  powinien zniknąć wiadomości.</span><span class="sxs-lookup"><span data-stu-id="379a3-132">When secure LDAP is successfully enabled for your managed domain, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="379a3-133">Powinny pojawić się hello odcisk palca certyfikatu hello wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="379a3-133">You should see hello thumbprint of hello certificate displayed.</span></span>

    ![Bezpieczny protokół LDAP włączone](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a><span data-ttu-id="379a3-135">Zadanie 4 — Włączanie bezpiecznego dostępu LDAP za pośrednictwem hello internet</span><span class="sxs-lookup"><span data-stu-id="379a3-135">Task 4 - enable secure LDAP access over hello internet</span></span>
<span data-ttu-id="379a3-136">**Opcjonalne zadania** — Jeśli nie planujesz tooaccess hello domeny zarządzanej przy użyciu LDAPS ponad hello internet, pomiń to zadanie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="379a3-136">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="379a3-137">Przed rozpoczęciem tego zadania upewnij się, zostały ukończone hello czynności opisane w temacie [zadanie 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="379a3-137">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="379a3-138">Powinny pojawić się opcja zbyt**hello włączyć bezpieczny LDAP dostęp za pośrednictwem INTERNETU** w hello **usług domenowych w usłudze** sekcji hello **Konfiguruj** strony.</span><span class="sxs-lookup"><span data-stu-id="379a3-138">You should see an option too**ENABLE SECURE LDAP ACCESS OVER hello INTERNET** in hello **domain services** section of hello **Configure** page.</span></span> <span data-ttu-id="379a3-139">Ta opcja jest ustawiona zbyt**nr** domyślnie ponieważ zarządzana toohello dostęp do Internetu domeny za pośrednictwem bezpiecznego protokołu LDAP jest domyślnie wyłączona.</span><span class="sxs-lookup"><span data-stu-id="379a3-139">This option is set too**NO** by default since internet access toohello managed domain over secure LDAP is disabled by default.</span></span>

    ![Bezpieczny protokół LDAP włączone](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="379a3-141">Przełącz **hello włączyć bezpieczny LDAP dostęp za pośrednictwem INTERNETU** za**tak**.</span><span class="sxs-lookup"><span data-stu-id="379a3-141">Toggle **ENABLE SECURE LDAP ACCESS OVER hello INTERNET** too**YES**.</span></span> <span data-ttu-id="379a3-142">Kliknij przycisk hello **ZAPISAĆ** przycisk na powitania dolny panel.</span><span class="sxs-lookup"><span data-stu-id="379a3-142">Click hello **SAVE** button on hello bottom panel.</span></span>
    <span data-ttu-id="379a3-143">![Bezpieczny protokół LDAP włączone](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="379a3-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="379a3-144">Hello **usług domenowych w usłudze** sekcji hello **Konfiguruj** kartę uzyskać wygaszone i znajduje się w hello **oczekujących...**  stanu kilka minut.</span><span class="sxs-lookup"><span data-stu-id="379a3-144">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="379a3-145">Po pewnym czasie domeny zarządzanej tooyour dostęp do Internetu za pośrednictwem bezpiecznego protokołu LDAP jest włączone.</span><span class="sxs-lookup"><span data-stu-id="379a3-145">After some time, internet access tooyour managed domain over secure LDAP is enabled.</span></span>

    ![Bezpieczny protokół LDAP — stan oczekiwania](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="379a3-147">Trwa około 10 minut dostęp do Internetu tooenable za pośrednictwem bezpiecznego protokołu LDAP do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="379a3-147">It takes about 10 minutes tooenable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="379a3-148">Gdy bezpieczne tooyour dostępu LDAP zarządzane domeny przez internet został pomyślnie włączony hello, hello **oczekujących...**  powinien zniknąć wiadomości.</span><span class="sxs-lookup"><span data-stu-id="379a3-148">When secure LDAP access tooyour managed domain over hello internet is successfully enabled, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="379a3-149">Powinna zostać wyświetlona hello IP zewnętrznego adresu, który może być używane tooaccess katalogu za pośrednictwem LDAPS w polu hello **IP adres dla LDAPS dostępu zewnętrznego**.</span><span class="sxs-lookup"><span data-stu-id="379a3-149">You should see hello external IP address that can be used tooaccess your directory over LDAPS in hello field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![Bezpieczny protokół LDAP włączone](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="379a3-151">Zadanie 5 — konfigurowanie domeny zarządzanej hello tooaccess DNS z hello internet</span><span class="sxs-lookup"><span data-stu-id="379a3-151">Task 5 - configure DNS tooaccess hello managed domain from hello internet</span></span>
<span data-ttu-id="379a3-152">**Opcjonalne zadania** — Jeśli nie planujesz tooaccess hello domeny zarządzanej przy użyciu LDAPS ponad hello internet, pomiń to zadanie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="379a3-152">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="379a3-153">Przed rozpoczęciem tego zadania upewnij się, zostały ukończone hello czynności opisane w temacie [zadanie 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="379a3-153">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="379a3-154">Po włączeniu bezpiecznego dostępu LDAP za pośrednictwem Internetu hello potrzeby domeny zarządzanej, należy tooupdate DNS tak, aby komputery klienckie można znaleźć tej domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="379a3-154">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="379a3-155">Na końcu hello zadanie 4, zewnętrzny adres IP jest wyświetlany na powitania **Konfiguruj** karcie **IP adres dla LDAPS dostępu zewnętrznego**.</span><span class="sxs-lookup"><span data-stu-id="379a3-155">At hello end of task 4, an external IP address is displayed on hello **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="379a3-156">Konfigurowanie dostawcy usługi DNS zewnętrzne tej nazwy DNS hello hello zarządzane zewnętrzny adres IP toothis punktów domeny (na przykład "ldaps.contoso100.com").</span><span class="sxs-lookup"><span data-stu-id="379a3-156">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="379a3-157">W naszym przykładzie potrzebne są nam hello toocreate następującego wpisu DNS:</span><span class="sxs-lookup"><span data-stu-id="379a3-157">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="379a3-158">To wszystko — wszystko jest teraz gotowy tooconnect toohello zarządzane domeny przy użyciu bezpiecznego protokołu LDAP, za pośrednictwem hello internet.</span><span class="sxs-lookup"><span data-stu-id="379a3-158">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="379a3-159">Należy pamiętać, że komputery klienckie muszą ufać Witaj wystawca hello LDAPS certyfikatu toobe stanie tooconnect pomyślnie toohello zarządzane przy użyciu LDAPS domeny.</span><span class="sxs-lookup"><span data-stu-id="379a3-159">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="379a3-160">Jeśli korzystasz z urzędu certyfikacji przedsiębiorstwa lub publicznie zaufany urząd certyfikacji, nie trzeba toodo niczego, ponieważ komputery klienckie ufać tych wystawców certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="379a3-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="379a3-161">Jeśli używasz certyfikatu z podpisem własnym należy tooinstall hello publicznego część hello certyfikatu z podpisem własnym do magazynu zaufanych certyfikatów hello na komputerze klienckim hello.</span><span class="sxs-lookup"><span data-stu-id="379a3-161">If you are using a self-signed certificate, you need tooinstall hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="379a3-162">LDAPS blokowanie dostępu tooyour domeny zarządzanej za pośrednictwem hello internet</span><span class="sxs-lookup"><span data-stu-id="379a3-162">Lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="379a3-163">**Opcjonalne zadania** — Jeśli nie włączono LDAPS domeny zarządzanej toohello dostępu ponad hello internet, pomiń to zadanie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="379a3-163">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="379a3-164">Przed rozpoczęciem tego zadania upewnij się, zostały ukończone hello czynności opisane w temacie [zadanie 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="379a3-164">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="379a3-165">Udostępnianie domeny zarządzanej LDAPS dostępu za pośrednictwem hello internet reprezentuje zagrożenie bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="379a3-165">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="379a3-166">Witaj domeny zarządzanej jest dostępny z hello internet na powitania port używany do bezpiecznego protokołu LDAP (to znaczy port 636).</span><span class="sxs-lookup"><span data-stu-id="379a3-166">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="379a3-167">W związku z tym można toorestrict dostępu toohello zarządzane domeny toospecific znane adresy IP.</span><span class="sxs-lookup"><span data-stu-id="379a3-167">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="379a3-168">Ze względów bezpieczeństwa należy utworzyć grupę zabezpieczeń sieci (NSG) i powiązać ją z podsieci hello, w której włączono usługi domenowe Azure AD.</span><span class="sxs-lookup"><span data-stu-id="379a3-168">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="379a3-169">Witaj poniższej tabeli przedstawiono przykład grupy NSG można skonfigurować toolock dół bezpiecznego dostępu LDAP na powitania internet.</span><span class="sxs-lookup"><span data-stu-id="379a3-169">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="379a3-170">Hello NSG zawiera zestaw reguł, które zezwolić na przychodzący LDAPS dostęp za pośrednictwem portu TCP 636 tylko z określonego zestawu adresów IP.</span><span class="sxs-lookup"><span data-stu-id="379a3-170">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="379a3-171">Hello domyślne "DenyAll" reguła ma zastosowanie tooall pozostały przychodzący ruch z hello internet.</span><span class="sxs-lookup"><span data-stu-id="379a3-171">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="379a3-172">Witaj NSG reguły tooallow LDAPS dostęp za pośrednictwem hello internet z określonych adresów IP ma wyższy priorytet niż hello reguły DenyAll NSG.</span><span class="sxs-lookup"><span data-stu-id="379a3-172">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Przykład grupy NSG toosecure LDAPS dostęp za pośrednictwem hello internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="379a3-174">**Więcej informacji** - [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="379a3-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="379a3-175">Zawartość pokrewna</span><span class="sxs-lookup"><span data-stu-id="379a3-175">Related content</span></span>
* [<span data-ttu-id="379a3-176">Usługi domenowe AD Azure - Przewodnik wprowadzający</span><span class="sxs-lookup"><span data-stu-id="379a3-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="379a3-177">Administrowanie domeną zarządzaną usług Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="379a3-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="379a3-178">Administrowanie zasad grupy w domenie zarządzanej usług domenowych Azure AD</span><span class="sxs-lookup"><span data-stu-id="379a3-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="379a3-179">Sieciowe grupy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="379a3-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="379a3-180">Utwórz grupę zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="379a3-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
