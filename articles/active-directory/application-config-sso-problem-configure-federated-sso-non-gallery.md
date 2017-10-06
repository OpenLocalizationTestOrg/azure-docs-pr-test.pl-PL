---
title: "Konfigurowanie federacyjnych logowanie jednokrotne dla aplikacji z systemem innym niż galerii aaaProblem | Dokumentacja firmy Microsoft"
description: "Niektóre hello typowych problemów, które można napotkać podczas konfigurowania federacyjnych pojedynczego logowania jednokrotnego tooyour niestandardową SAML aplikację, która nie jest wymieniony w galerii aplikacji usługi Azure AD hello adresów"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="befa0-103">Problem podczas konfiguracji federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="befa0-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="befa0-104">Jeśli napotkasz problem podczas konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="befa0-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="befa0-105">Sprawdź zostały wykonane wszystkie kroki hello w artykule hello [konfigurowania pojedynczego logowania jednokrotnego tooapplications, które nie znajdują się w galerii aplikacji hello Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="befa0-105">Verify you have followed all hello steps in hello article [Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-hello-application"></a><span data-ttu-id="befa0-106">Nie można dodać inne wystąpienie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="befa0-106">Can’t add another instance of hello application</span></span>

<span data-ttu-id="befa0-107">tooadd drugiego wystąpienia aplikacji, należy toobe stanie:</span><span class="sxs-lookup"><span data-stu-id="befa0-107">tooadd a second instance of an application, you need toobe able to:</span></span>

-   <span data-ttu-id="befa0-108">Skonfiguruj Unikatowy identyfikator hello drugie wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="befa0-108">Configure a unique identifier for hello second instance.</span></span> <span data-ttu-id="befa0-109">Nie można tego samego identyfikatora używane dla pierwszego wystąpienia hello powitalne tooconfigure stanie.</span><span class="sxs-lookup"><span data-stu-id="befa0-109">You won’t be able tooconfigure hello same identifier used for hello first instance.</span></span>

-   <span data-ttu-id="befa0-110">Skonfiguruj inny certyfikat niż hello używane jako hello pierwszego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="befa0-110">Configure a different certificate than hello one used for hello first instance.</span></span>

<span data-ttu-id="befa0-111">Jeśli hello aplikacji nie obsługuje żadnego z hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="befa0-111">If hello application doesn’t support any of hello above.</span></span> <span data-ttu-id="befa0-112">Następnie nie będzie możliwe tooconfigure drugiego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="befa0-112">Then, you won’t be able tooconfigure a second instance.</span></span>

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a><span data-ttu-id="befa0-113">Gdzie ustawić hello format EntityID (identyfikator użytkownika)</span><span class="sxs-lookup"><span data-stu-id="befa0-113">Where do I set hello EntityID (User Identifier) format</span></span>

<span data-ttu-id="befa0-114">Możesz nie być w formacie EntityID (identyfikator użytkownika) hello stanie tooselect usługi Azure AD wysyła toohello aplikacji hello odpowiedzi po uwierzytelnieniu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="befa0-114">You won’t be able tooselect hello EntityID (User Identifier) format that Azure AD sends toohello application in hello response after user authentication.</span></span>

<span data-ttu-id="befa0-115">Azure AD hello wybierz format dla atrybutu NameID hello (identyfikator użytkownika) oparte na wybranej wartości hello lub hello żądany przez aplikację hello w hello SAML AuthRequest format.</span><span class="sxs-lookup"><span data-stu-id="befa0-115">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="befa0-116">Aby uzyskać więcej informacji można znaleźć w artykule hello [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) sekcji hello NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="befa0-116">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy,</span></span>

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="befa0-117">Gdzie uzyskać metadanych aplikacji hello lub certyfikatu z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="befa0-117">Where do I get hello application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="befa0-118">metadane aplikacji hello toodownload lub certyfikatu z usługi Azure AD, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="befa0-118">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="befa0-119">Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="befa0-119">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="befa0-120">Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.</span><span class="sxs-lookup"><span data-stu-id="befa0-120">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="befa0-121">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="befa0-121">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="befa0-122">Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="befa0-122">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="befa0-123">Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="befa0-123">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="befa0-124">Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**</span><span class="sxs-lookup"><span data-stu-id="befa0-124">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="befa0-125">Wybierz aplikację hello skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="befa0-125">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="befa0-126">Po załadowaniu aplikacji hello, kliknij przycisk hello **logowanie jednokrotne** z menu nawigacji po lewej stronie powitania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="befa0-126">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="befa0-127">Przejdź za**certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="befa0-127">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="befa0-128">W zależności od tego, jakie aplikacji hello wymaga Konfigurowanie logowania jednokrotnego zobacz temat albo toodownload opcji hello hello XML metadanych lub hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="befa0-128">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

<span data-ttu-id="befa0-129">Usługi Azure AD nie udostępnia metadane hello tooget adresu URL.</span><span class="sxs-lookup"><span data-stu-id="befa0-129">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="befa0-130">można pobrać metadanych Hello jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="befa0-130">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a><span data-ttu-id="befa0-131">Nie wiadomo, jak toocustomize SAML oświadczenia wysyłane tooan aplikacji</span><span class="sxs-lookup"><span data-stu-id="befa0-131">Don't know how toocustomize SAML claims sent tooan application</span></span>

<span data-ttu-id="befa0-132">toolearn toocustomize hello SAML atrybutu oświadczenia wysyłane tooyour aplikacji, zobacz [oświadczeń mapowanie w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="befa0-132">toolearn how toocustomize hello SAML attribute claims sent tooyour application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="befa0-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="befa0-133">Next steps</span></span>
[<span data-ttu-id="befa0-134">Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="befa0-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
