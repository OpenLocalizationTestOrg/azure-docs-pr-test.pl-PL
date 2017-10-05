---
title: "Konfigurowanie aplikacji SaaS do współpracy B2B w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Przykłady kodu i programu PowerShell dla usługi Azure Active Directory B2B współpracy"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 149a493f7b369415f0a2726dd6a576f0195c13d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="527c5-103">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="527c5-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="527c5-104">Azure współpracy B2B usługi Active Directory (Azure AD) współpracuje z większości aplikacji, które integrują się z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="527c5-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="527c5-105">W tej sekcji możemy przeprowadzenie instrukcje dotyczące konfigurowania niektórych popularnych aplikacji SaaS do użytku z B2B usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="527c5-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="527c5-106">Przed przyjrzymy się instrukcje specyficzne dla aplikacji, poniżej przedstawiono niektóre przyjąć reguł:</span><span class="sxs-lookup"><span data-stu-id="527c5-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="527c5-107">Dla większości aplikacji ustawienia użytkownika musi mieć miejsce, ręcznie.</span><span class="sxs-lookup"><span data-stu-id="527c5-107">For most of the apps, user setup needs to happen manually.</span></span> <span data-ttu-id="527c5-108">Oznacza to użytkownicy muszą być utworzone ręcznie w aplikacji, jak również.</span><span class="sxs-lookup"><span data-stu-id="527c5-108">That is, users must be created manually in the app as well.</span></span>

* <span data-ttu-id="527c5-109">Dla aplikacji, które obsługują automatyczne ustawienia, takie jak Dropbox zaproszeń do skorzystania z oddzielnych są tworzone za pomocą aplikacji.</span><span class="sxs-lookup"><span data-stu-id="527c5-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from the apps.</span></span> <span data-ttu-id="527c5-110">Użytkownicy muszą być koniecznie Zaakceptuj każde zaproszenie.</span><span class="sxs-lookup"><span data-stu-id="527c5-110">Users must be sure to accept each invitation.</span></span>

* <span data-ttu-id="527c5-111">Atrybuty użytkownika, aby uniknąć problemów z zniekształcone funkcja dysku profilu użytkownika (UPD) w gości, zawsze wartość **identyfikator użytkownika** do **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="527c5-111">In the user attributes, to mitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** to **user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="527c5-112">Dropbox biznesowa</span><span class="sxs-lookup"><span data-stu-id="527c5-112">Dropbox Business</span></span>

<span data-ttu-id="527c5-113">Aby umożliwić użytkownikom na logowanie przy użyciu konta organizacji, należy ręcznie skonfigurować skrzynki firm przy użyciu usługi Azure AD jako dostawcy tożsamości Security (Assertion Markup Language SAML).</span><span class="sxs-lookup"><span data-stu-id="527c5-113">To enable users to sign in using their organization account, you must manually configure Dropbox Business to use Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="527c5-114">Jeśli nie skonfigurowano firm Dropbox Aby to zrobić, nie może ona Monituj ani w przeciwnym razie użytkownicy mogą logować się za pomocą usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="527c5-114">If Dropbox Business has not been configured to do so, it cannot prompt or otherwise allow users to sign in using Azure AD.</span></span>

1. <span data-ttu-id="527c5-115">Aby dodać aplikacja biznesowa Dropbox z usługą Azure AD, wybierz **aplikacje dla przedsiębiorstw** w okienku po lewej stronie, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="527c5-115">To add the Dropbox Business app into Azure AD, select **Enterprise applications** in the left pane, and then click **Add**.</span></span>

  ![Przycisk "Dodaj" na stronie aplikacji przedsiębiorstwa](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="527c5-117">W **dodać aplikację** okna, wprowadź **dropbox** w polu wyszukiwania, a następnie wybierz **Dropbox dla firm** na liście wyników.</span><span class="sxs-lookup"><span data-stu-id="527c5-117">In the **Add an application** window, enter **dropbox** in the search box, and then select **Dropbox for Business** in the results list.</span></span>

  ![Wyszukaj "dropbox" na stronie Dodawanie strony aplikacji](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="527c5-119">Na **logowanie jednokrotne** wybierz pozycję **logowanie jednokrotne** w okienku po lewej stronie, a następnie wprowadź **user.mail** w **identyfikator użytkownika** pole.</span><span class="sxs-lookup"><span data-stu-id="527c5-119">On the **Single sign-on** page, select **Single sign-on** in the left pane, and then enter **user.mail** in the **User Identifier** box.</span></span> <span data-ttu-id="527c5-120">(Jest ustawiona jako nazwy UPN domyślnie.)</span><span class="sxs-lookup"><span data-stu-id="527c5-120">(It's set as UPN by default.)</span></span>

  ![Konfigurowanie rejestracji jednokrotnej dla aplikacji](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="527c5-122">Aby pobrać certyfikat do użycia na potrzeby konfiguracji usługi Dropbox, wybierz **Konfigurowanie skrzynki**, a następnie wybierz **SAML pojedynczy znak na adres URL usługi** na liście.</span><span class="sxs-lookup"><span data-stu-id="527c5-122">To download the certificate to use for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in the list.</span></span>

  ![Pobieranie certyfikatu na potrzeby konfiguracji skrzynki](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="527c5-124">Zaloguj się do usługi Dropbox z logowania jednokrotnego adres URL z **logowanie jednokrotne** strony.</span><span class="sxs-lookup"><span data-stu-id="527c5-124">Sign in to Dropbox with the sign-on URL from the **Single sign-on** page.</span></span>

  ![Strona logowania usługi Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="527c5-126">W menu, wybierz **konsoli administracyjnej**.</span><span class="sxs-lookup"><span data-stu-id="527c5-126">On the menu, select **Admin Console**.</span></span>

  ![Łącze "Konsola administratora" w menu skrzynki](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="527c5-128">W **uwierzytelniania** okno dialogowe, wybierz opcję **więcej**, Przekaż certyfikat, a następnie w **Zaloguj się w adresie URL** wprowadź SAML pojedynczy adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="527c5-128">In the **Authentication** dialog box, select **More**, upload the certificate and then, in the **Sign in URL** box, enter the SAML single sign-on URL.</span></span>

  ![Link "Więcej" w oknie dialogowym zwinięte uwierzytelniania](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  !["Zaloguj się w adresie URL" w oknie dialogowym uwierzytelniania rozszerzonej](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="527c5-131">Aby skonfigurować ustawienia automatycznego użytkownika w portalu Azure, wybierz **inicjowania obsługi administracyjnej** w okienku po lewej stronie wybierz **automatyczne** w **inicjowania obsługi trybu** , a następnie wybierz **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="527c5-131">To configure automatic user setup in the Azure portal, select **Provisioning** in the left pane, select **Automatic** in the **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Konfigurowanie użytkownika automatycznego inicjowania obsługi w portalu Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="527c5-133">Po gościa lub element członkowski użytkowników są skonfigurowane w aplikacji Dropbox, otrzymują oddzielne zaproszenia z Dropbox.</span><span class="sxs-lookup"><span data-stu-id="527c5-133">After guest or member users have been set up in the Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="527c5-134">Aby korzystać z usługi Dropbox logowania jednokrotnego, zapraszane osoby musi zaakceptować zaproszenie, klikając łącze w nim.</span><span class="sxs-lookup"><span data-stu-id="527c5-134">To use Dropbox single sign-on, invitees must accept the invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="527c5-135">Box</span><span class="sxs-lookup"><span data-stu-id="527c5-135">Box</span></span>
<span data-ttu-id="527c5-136">Umożliwia użytkownikom uwierzytelnianie przy użyciu Federacji, która jest oparta na protokole SAML pole gości z użyciem konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="527c5-136">You can enable users to authenticate Box guest users with their Azure AD account by using federation that's based on the SAML protocol.</span></span> <span data-ttu-id="527c5-137">W ramach tej procedury należy przekazać do Box.com metadanych.</span><span class="sxs-lookup"><span data-stu-id="527c5-137">In this procedure, you upload metadata to Box.com.</span></span>

1. <span data-ttu-id="527c5-138">Dodaj aplikację pole z aplikacje przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="527c5-138">Add the Box app from the enterprise apps.</span></span>

2. <span data-ttu-id="527c5-139">Konfigurowanie rejestracji jednokrotnej w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="527c5-139">Configure single sign-on in the following order:</span></span>

  ![Konfiguruj okno rejestracji jednokrotnej](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="527c5-141">a.</span><span class="sxs-lookup"><span data-stu-id="527c5-141">a.</span></span> <span data-ttu-id="527c5-142">W **Zaloguj się na adres URL** Sprawdź, czy adres URL logowania jest odpowiednio ustawiony dla pola w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="527c5-142">In the **Sign on URL** box, ensure that the sign-on URL is set appropriately for Box in the Azure portal.</span></span> <span data-ttu-id="527c5-143">Ten adres URL jest adresem URL dzierżawy Box.com.</span><span class="sxs-lookup"><span data-stu-id="527c5-143">This URL is the URL of your Box.com tenant.</span></span> <span data-ttu-id="527c5-144">Należy stosować konwencji nazewnictwa *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="527c5-144">It should follow the naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="527c5-145">**Identyfikator** nie ma zastosowania do tej aplikacji, ale nadal jest widoczny jako pole obowiązkowe.</span><span class="sxs-lookup"><span data-stu-id="527c5-145">The **Identifier** does not apply to this app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="527c5-146">b.</span><span class="sxs-lookup"><span data-stu-id="527c5-146">b.</span></span> <span data-ttu-id="527c5-147">W **identyfikator użytkownika** wprowadź **user.mail** (na potrzeby logowania jednokrotnego dla konta gościa).</span><span class="sxs-lookup"><span data-stu-id="527c5-147">In the **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="527c5-148">c.</span><span class="sxs-lookup"><span data-stu-id="527c5-148">c.</span></span> <span data-ttu-id="527c5-149">W obszarze **certyfikat podpisywania SAML**, kliknij przycisk **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="527c5-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="527c5-150">d.</span><span class="sxs-lookup"><span data-stu-id="527c5-150">d.</span></span> <span data-ttu-id="527c5-151">Aby rozpocząć konfigurowanie dzierżawy Box.com przy użyciu usługi Azure AD jako dostawcy tożsamości, Pobierz plik metadanych, a następnie zapisz go na lokalny dysk.</span><span class="sxs-lookup"><span data-stu-id="527c5-151">To begin configuring your Box.com tenant to use Azure AD as an identity provider, download the metadata file and then save it to your local drive.</span></span>

 <span data-ttu-id="527c5-152">e.</span><span class="sxs-lookup"><span data-stu-id="527c5-152">e.</span></span> <span data-ttu-id="527c5-153">Przekazuj pliku metadanych do pola obsługuje zespół, który konfiguruje rejestracji jednokrotnej dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="527c5-153">Forward the metadata file to the Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="527c5-154">Ustawienia automatycznego użytkownika usługi Azure AD, w lewym okienku wybierz **inicjowania obsługi administracyjnej**, a następnie wybierz **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="527c5-154">For Azure AD automatic user setup, in the left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Zezwolić usłudze Azure AD connect do pola](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="527c5-156">Jak Dropbox zapraszane osoby pole zapraszane osoby muszą zrealizować ich zaproszenia od aplikacji Box.</span><span class="sxs-lookup"><span data-stu-id="527c5-156">Like Dropbox invitees, Box invitees must redeem their invitation from the Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="527c5-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="527c5-157">Next steps</span></span>

<span data-ttu-id="527c5-158">Na współpracy B2B usługi Azure AD, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="527c5-158">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="527c5-159">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="527c5-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="527c5-160">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="527c5-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="527c5-161">Dodawanie do roli użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="527c5-161">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="527c5-162">Delegowanie zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="527c5-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="527c5-163">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="527c5-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="527c5-164">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="527c5-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="527c5-165">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="527c5-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="527c5-166">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="527c5-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="527c5-167">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="527c5-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="527c5-168">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="527c5-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
