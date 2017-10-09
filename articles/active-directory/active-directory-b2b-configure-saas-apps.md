---
title: "aplikacji SaaS aaaConfigure współpracy B2B w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a><span data-ttu-id="7c09a-103">Konfigurowanie aplikacji SaaS do współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7c09a-103">Configure SaaS apps for B2B collaboration</span></span>

<span data-ttu-id="7c09a-104">Azure współpracy B2B usługi Active Directory (Azure AD) współpracuje z większości aplikacji, które integrują się z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c09a-104">Azure Active Directory (Azure AD) B2B collaboration works with most apps that integrate with Azure AD.</span></span> <span data-ttu-id="7c09a-105">W tej sekcji możemy przeprowadzenie instrukcje dotyczące konfigurowania niektórych popularnych aplikacji SaaS do użytku z B2B usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c09a-105">In this section, we walk through instructions for configuring some popular SaaS apps for use with Azure AD B2B.</span></span>

<span data-ttu-id="7c09a-106">Przed przyjrzymy się instrukcje specyficzne dla aplikacji, poniżej przedstawiono niektóre przyjąć reguł:</span><span class="sxs-lookup"><span data-stu-id="7c09a-106">Before you look at app-specific instructions, here are some rules of thumb:</span></span>

* <span data-ttu-id="7c09a-107">Dla większości aplikacji hello Instalator użytkownik musi ręcznie toohappen.</span><span class="sxs-lookup"><span data-stu-id="7c09a-107">For most of hello apps, user setup needs toohappen manually.</span></span> <span data-ttu-id="7c09a-108">Oznacza to użytkownicy muszą być utworzone ręcznie w aplikacji hello również.</span><span class="sxs-lookup"><span data-stu-id="7c09a-108">That is, users must be created manually in hello app as well.</span></span>

* <span data-ttu-id="7c09a-109">Dla aplikacji, które obsługują automatyczne ustawienia, takie jak Dropbox zaproszeń do skorzystania z oddzielnych są tworzone na podstawie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="7c09a-109">For apps that support automatic setup, such as Dropbox, separate invitations are created from hello apps.</span></span> <span data-ttu-id="7c09a-110">Użytkownicy muszą być tooaccept się, że każde zaproszenie.</span><span class="sxs-lookup"><span data-stu-id="7c09a-110">Users must be sure tooaccept each invitation.</span></span>

* <span data-ttu-id="7c09a-111">Atrybuty użytkownika hello, toomitigate wszelkie problemy z zniekształcone funkcja dysku profilu użytkownika (UPD) w gości, zawsze wartość **identyfikator użytkownika** za**user.mail**.</span><span class="sxs-lookup"><span data-stu-id="7c09a-111">In hello user attributes, toomitigate any issues with mangled user profile disk (UPD) in guest users, always set **User Identifier** too**user.mail**.</span></span>


## <a name="dropbox-business"></a><span data-ttu-id="7c09a-112">Dropbox biznesowa</span><span class="sxs-lookup"><span data-stu-id="7c09a-112">Dropbox Business</span></span>

<span data-ttu-id="7c09a-113">tooenable toosign użytkowników w przy użyciu konta organizacji, należy ręcznie skonfigurować toouse skrzynki Business usługi Azure AD jako dostawcy tożsamości Security (Assertion Markup Language SAML).</span><span class="sxs-lookup"><span data-stu-id="7c09a-113">tooenable users toosign in using their organization account, you must manually configure Dropbox Business toouse Azure AD as a Security Assertion Markup Language (SAML) identity provider.</span></span> <span data-ttu-id="7c09a-114">Jeśli skrzynki firm nie został skonfigurowany toodo tak, go nie Monituj lub w przeciwnym razie zezwolić toosign użytkowników za pomocą usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c09a-114">If Dropbox Business has not been configured toodo so, it cannot prompt or otherwise allow users toosign in using Azure AD.</span></span>

1. <span data-ttu-id="7c09a-115">aplikacja biznesowa skrzynki hello tooadd do usługi Azure AD, wybierz **aplikacje dla przedsiębiorstw** w lewym okienku hello, a następnie kliknij **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="7c09a-115">tooadd hello Dropbox Business app into Azure AD, select **Enterprise applications** in hello left pane, and then click **Add**.</span></span>

  ![przycisk "Dodaj" Hello na stronę aplikacji hello Enterprise](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. <span data-ttu-id="7c09a-117">W hello **dodać aplikację** okna, wprowadź **dropbox** w hello pole wyszukiwania, a następnie wybierz **Dropbox dla firm** hello listy wyników.</span><span class="sxs-lookup"><span data-stu-id="7c09a-117">In hello **Add an application** window, enter **dropbox** in hello search box, and then select **Dropbox for Business** in hello results list.</span></span>

  ![Wyszukaj "dropbox" na powitania Dodawanie strony aplikacji](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. <span data-ttu-id="7c09a-119">Na powitania **logowanie jednokrotne** wybierz pozycję **logowanie jednokrotne** w lewym okienku hello, a następnie wprowadź **user.mail** w hello **identyfikator użytkownika** pole.</span><span class="sxs-lookup"><span data-stu-id="7c09a-119">On hello **Single sign-on** page, select **Single sign-on** in hello left pane, and then enter **user.mail** in hello **User Identifier** box.</span></span> <span data-ttu-id="7c09a-120">(Jest ustawiona jako nazwy UPN domyślnie.)</span><span class="sxs-lookup"><span data-stu-id="7c09a-120">(It's set as UPN by default.)</span></span>

  ![Konfigurowanie rejestracji jednokrotnej dla aplikacji hello](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. <span data-ttu-id="7c09a-122">toodownload hello certyfikatu toouse dla konfiguracji usługi Dropbox, wybierz **Konfigurowanie skrzynki**, a następnie wybierz **SAML pojedynczy znak na adres URL usługi** hello liście.</span><span class="sxs-lookup"><span data-stu-id="7c09a-122">toodownload hello certificate toouse for Dropbox configuration, select **Configure DropBox**, and then select **SAML Single Sign On Service URL** in hello list.</span></span>

  ![Pobieranie certyfikatu hello konfiguracji skrzynki](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. <span data-ttu-id="7c09a-124">Logowanie tooDropbox z hello jednokrotnej adres URL z hello **logowanie jednokrotne** strony.</span><span class="sxs-lookup"><span data-stu-id="7c09a-124">Sign in tooDropbox with hello sign-on URL from hello **Single sign-on** page.</span></span>

  ![Strona Hello logowania usługi Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. <span data-ttu-id="7c09a-126">W hello menu, wybierz **konsoli administracyjnej**.</span><span class="sxs-lookup"><span data-stu-id="7c09a-126">On hello menu, select **Admin Console**.</span></span>

  ![łącze "Konsola administratora" Hello, w menu skrzynki hello](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. <span data-ttu-id="7c09a-128">W hello **uwierzytelniania** okno dialogowe, wybierz opcję **więcej**, Przekaż hello certyfikat, a następnie w hello **Zaloguj się w adresie URL** wprowadź adres URL hello SAML logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="7c09a-128">In hello **Authentication** dialog box, select **More**, upload hello certificate and then, in hello **Sign in URL** box, enter hello SAML single sign-on URL.</span></span>

  ![Witaj link "Więcej" w oknie dialogowym uwierzytelniania hello zwinięte](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Witaj "Adres URL logowania" w hello rozszerzona uwierzytelniania, okno dialogowe](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. <span data-ttu-id="7c09a-131">Ustawienia automatycznego użytkownika tooconfigure w hello portalu Azure, wybierz **inicjowania obsługi administracyjnej** wybierz w okienku po lewej stronie powitania **automatyczne** w hello **inicjowania obsługi trybu** , a następnie wybierz **Autoryzować**.</span><span class="sxs-lookup"><span data-stu-id="7c09a-131">tooconfigure automatic user setup in hello Azure portal, select **Provisioning** in hello left pane, select **Automatic** in hello **Provisioning Mode** box, and then select **Authorize**.</span></span>

  ![Konfigurowanie użytkownika automatycznego inicjowania obsługi w hello portalu Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

<span data-ttu-id="7c09a-133">Po gościa lub element członkowski użytkowników są skonfigurowane w aplikacji Dropbox hello, otrzymują oddzielne zaproszenia z Dropbox.</span><span class="sxs-lookup"><span data-stu-id="7c09a-133">After guest or member users have been set up in hello Dropbox app, they receive a separate invitation from Dropbox.</span></span> <span data-ttu-id="7c09a-134">toouse skrzynki rejestracji jednokrotnej, zapraszane osoby muszą zaakceptować zaproszenie hello, klikając łącze w nim.</span><span class="sxs-lookup"><span data-stu-id="7c09a-134">toouse Dropbox single sign-on, invitees must accept hello invitation by clicking a link in it.</span></span>

## <a name="box"></a><span data-ttu-id="7c09a-135">Box</span><span class="sxs-lookup"><span data-stu-id="7c09a-135">Box</span></span>
<span data-ttu-id="7c09a-136">Użytkownicy tooauthenticate pole gości z użyciem konta usługi Azure AD można włączyć, używając federacyjnego, który bazuje na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="7c09a-136">You can enable users tooauthenticate Box guest users with their Azure AD account by using federation that's based on hello SAML protocol.</span></span> <span data-ttu-id="7c09a-137">W tej procedurze możesz przekazać tooBox.com metadanych.</span><span class="sxs-lookup"><span data-stu-id="7c09a-137">In this procedure, you upload metadata tooBox.com.</span></span>

1. <span data-ttu-id="7c09a-138">Dodaj aplikację pole hello z hello aplikacje przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="7c09a-138">Add hello Box app from hello enterprise apps.</span></span>

2. <span data-ttu-id="7c09a-139">Konfigurowanie rejestracji jednokrotnej w następującej kolejności hello:</span><span class="sxs-lookup"><span data-stu-id="7c09a-139">Configure single sign-on in hello following order:</span></span>

  ![Konfiguruj okno rejestracji jednokrotnej](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 <span data-ttu-id="7c09a-141">a.</span><span class="sxs-lookup"><span data-stu-id="7c09a-141">a.</span></span> <span data-ttu-id="7c09a-142">W hello **Zaloguj się na adres URL** Sprawdź, czy hello adres URL logowania jest odpowiednio ustawiony dla pola w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7c09a-142">In hello **Sign on URL** box, ensure that hello sign-on URL is set appropriately for Box in hello Azure portal.</span></span> <span data-ttu-id="7c09a-143">Ten adres URL jest adresem URL hello dzierżawy Box.com.</span><span class="sxs-lookup"><span data-stu-id="7c09a-143">This URL is hello URL of your Box.com tenant.</span></span> <span data-ttu-id="7c09a-144">Należy stosować konwencję nazewnictwa hello *https://.box.com*.</span><span class="sxs-lookup"><span data-stu-id="7c09a-144">It should follow hello naming convention *https://.box.com*.</span></span>  
 <span data-ttu-id="7c09a-145">Witaj **identyfikator** nie ma zastosowania toothis aplikacji, ale nadal jest wyświetlany jako pole obowiązkowe.</span><span class="sxs-lookup"><span data-stu-id="7c09a-145">hello **Identifier** does not apply toothis app, but it still appears as a mandatory field.</span></span>

 <span data-ttu-id="7c09a-146">b.</span><span class="sxs-lookup"><span data-stu-id="7c09a-146">b.</span></span> <span data-ttu-id="7c09a-147">W hello **identyfikator użytkownika** wprowadź **user.mail** (na potrzeby logowania jednokrotnego dla konta gościa).</span><span class="sxs-lookup"><span data-stu-id="7c09a-147">In hello **User identifier** box, enter **user.mail** (for SSO for guest accounts).</span></span>

 <span data-ttu-id="7c09a-148">c.</span><span class="sxs-lookup"><span data-stu-id="7c09a-148">c.</span></span> <span data-ttu-id="7c09a-149">W obszarze **certyfikat podpisywania SAML**, kliknij przycisk **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="7c09a-149">Under **SAML Signing Certificate**, click **Create new certificate**.</span></span>

 <span data-ttu-id="7c09a-150">d.</span><span class="sxs-lookup"><span data-stu-id="7c09a-150">d.</span></span> <span data-ttu-id="7c09a-151">toobegin konfigurowanie Twojego Box.com toouse dzierżawy usługi Azure AD jako dostawcy tożsamości, Pobierz plik metadanych hello, a następnie zapisz tooyour dysku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="7c09a-151">toobegin configuring your Box.com tenant toouse Azure AD as an identity provider, download hello metadata file and then save it tooyour local drive.</span></span>

 <span data-ttu-id="7c09a-152">e.</span><span class="sxs-lookup"><span data-stu-id="7c09a-152">e.</span></span> <span data-ttu-id="7c09a-153">Przesyła hello metadanych pliku toohello pole zespołem pomocy technicznej, który konfiguruje rejestracji jednokrotnej dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="7c09a-153">Forward hello metadata file toohello Box support team, which configures single sign-on for you.</span></span>

3. <span data-ttu-id="7c09a-154">Ustawienia automatycznego użytkownika usługi Azure AD, w okienku po lewej stronie powitania, wybierz **inicjowania obsługi administracyjnej**, a następnie wybierz **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="7c09a-154">For Azure AD automatic user setup, in hello left pane, select **Provisioning**, and then select **Authorize**.</span></span>

  ![Autoryzowanie tooBox tooconnect usługi Azure AD](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

<span data-ttu-id="7c09a-156">Jak Dropbox zapraszane osoby pole zapraszane osoby muszą zrealizować ich zaproszenia od hello okno aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c09a-156">Like Dropbox invitees, Box invitees must redeem their invitation from hello Box app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c09a-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c09a-157">Next steps</span></span>

<span data-ttu-id="7c09a-158">Zobacz następujące artykuły dotyczące współpracy B2B usługi Azure AD hello:</span><span class="sxs-lookup"><span data-stu-id="7c09a-158">See hello following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="7c09a-159">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="7c09a-159">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="7c09a-160">Właściwości użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7c09a-160">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="7c09a-161">Dodawanie roli tooa użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7c09a-161">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="7c09a-162">Delegowanie zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7c09a-162">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="7c09a-163">Grupami dynamicznymi i współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7c09a-163">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="7c09a-164">Kod współpracy B2B i przykłady środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c09a-164">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="7c09a-165">Tokeny użytkownika współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7c09a-165">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="7c09a-166">Oświadczenia użytkowników współpracy B2B mapowania</span><span class="sxs-lookup"><span data-stu-id="7c09a-166">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="7c09a-167">Udostępnianie zewnętrzne w usłudze Office 365</span><span class="sxs-lookup"><span data-stu-id="7c09a-167">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="7c09a-168">Bieżące ograniczenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="7c09a-168">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
