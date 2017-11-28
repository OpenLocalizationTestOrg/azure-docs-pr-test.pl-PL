---
title: "aaaSSH obsługę aplikacji sieci Web usługi aplikacji Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Więcej informacji o korzystaniu z protokołu SSH z aplikacji sieci Web platformy Azure w systemie Linux."
keywords: "Usługa aplikacji Azure, aplikacji sieci web, linux, oss"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="35ce6-104">Obsługa protokołu SSH dla aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="35ce6-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="35ce6-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="35ce6-105">Overview</span></span>

<span data-ttu-id="35ce6-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) kryptograficznych protokół sieci bezpieczny sposób za pomocą usług sieciowych.</span><span class="sxs-lookup"><span data-stu-id="35ce6-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="35ce6-107">Toolog najczęściej używane do systemu zdalnie bezpieczny z wiersza polecenia i jest zdalnie wykonać poleceń administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="35ce6-107">It is most commonly used toolog into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="35ce6-108">Sieci Web aplikacji w systemie Linux zapewnia obsługę SSH do kontenera aplikacji hello z każdym hello wbudowanych Docker obrazami używanymi na potrzeby hello stosu środowiska uruchomieniowego nowych aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="35ce6-108">Web App on Linux provides SSH support into hello app container with each of hello built-in Docker images used for hello Runtime Stack of new web apps.</span></span> 

![Stosy środowiska wykonawczego](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="35ce6-110">Za pomocą protokołu SSH i niestandardowe obrazy usługi Docker jako część obrazu hello w tym hello SSH serwera i jego konfigurowania, zgodnie z opisem w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="35ce6-110">You can also use SSH with your custom Docker images by including hello SSH server as part of hello image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="35ce6-111">Połączenia klienta</span><span class="sxs-lookup"><span data-stu-id="35ce6-111">Making a client connection</span></span>

<span data-ttu-id="35ce6-112">toomake połączenie klienta SSH hello lokacji głównej musi być uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="35ce6-112">toomake an SSH client connection, hello main site must be started.</span></span> 

<span data-ttu-id="35ce6-113">Wklej hello końcowy zarządzania kontroli źródła (SCM) dla aplikacji sieci web w przeglądarce, za pomocą hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="35ce6-113">Paste hello Source Control Management (SCM) endpoint for your web app into your browser using hello following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="35ce6-114">Jeśli nie są już uwierzytelniony, to wymagana tooauthenticate z tooconnect Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="35ce6-114">If you are not already authenticated, you are required tooauthenticate with your Azure subscription tooconnect.</span></span>

![Połączenie SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="35ce6-116">Obsługa protokołu SSH z niestandardowymi obrazami Docker</span><span class="sxs-lookup"><span data-stu-id="35ce6-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="35ce6-117">Aby niestandardowe Docker obrazu toosupport SSH komunikacji między hello kontenera i powitania klienta w portalu Azure hello wykonaj następujące kroki dla obrazu Docker hello.</span><span class="sxs-lookup"><span data-stu-id="35ce6-117">In order for a custom Docker image toosupport SSH communication between hello container and hello client in hello Azure portal, perform hello following steps for your Docker image.</span></span> 

<span data-ttu-id="35ce6-118">Te kroki są są wyświetlane w hello repozytorium w usłudze Azure App Service jako przykład [tutaj](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="35ce6-118">These steps are are shown in hello Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="35ce6-119">Zawierają hello `openssh-server` instalacji w [ `RUN` instrukcji](https://docs.docker.com/engine/reference/builder/#run) w hello plik Dockerfile dla obrazu i ustawić hello hasło dla konta głównego hello także`"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="35ce6-119">Include hello `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile for your image and set hello password for hello root account too`"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="35ce6-120">Ta konfiguracja nie zezwala na połączenia zewnętrzne toohello kontenera.</span><span class="sxs-lookup"><span data-stu-id="35ce6-120">This configuration does not allow external connections toohello container.</span></span> <span data-ttu-id="35ce6-121">SSH jest możliwy tylko za pośrednictwem hello Kudu / SCM lokacji, który jest uwierzytelniany przy użyciu hello poświadczeń publikowania.</span><span class="sxs-lookup"><span data-stu-id="35ce6-121">SSH can only be accessed via hello Kudu / SCM Site, which is authenticated using hello publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="35ce6-122">Dodaj [ `COPY` instrukcji](https://docs.docker.com/engine/reference/builder/#copy) toocopy plik Dockerfile toohello [sshd_config](http://man.openbsd.org/sshd_config) pliku toohello */itp/ssh/* katalogu.</span><span class="sxs-lookup"><span data-stu-id="35ce6-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy a [sshd_config](http://man.openbsd.org/sshd_config) file toohello */etc/ssh/* directory.</span></span> <span data-ttu-id="35ce6-123">Plik konfiguracji powinny być oparte na naszych sshd_config plik w repozytorium GitHub usługi App hello [tutaj](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="35ce6-123">Your configuration file should be based on our sshd_config file in hello Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="35ce6-124">Witaj *sshd_config* plik musi zawierać następujące hello lub hello połączenie nie powiedzie się:</span><span class="sxs-lookup"><span data-stu-id="35ce6-124">hello *sshd_config* file must include hello following or hello connection fails:</span></span> 
    > * <span data-ttu-id="35ce6-125">`Ciphers`musi zawierać co najmniej jedną z następujących hello: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="35ce6-125">`Ciphers` must include at least one of hello following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="35ce6-126">`MACs`musi zawierać co najmniej jedną z następujących hello: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="35ce6-126">`MACs` must include at least one of hello following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="35ce6-127">Dołączyć portu 2222 hello [ `EXPOSE` instrukcji](https://docs.docker.com/engine/reference/builder/#expose) dla hello plik Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="35ce6-127">Include port 2222 in hello [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for hello Dockerfile.</span></span> <span data-ttu-id="35ce6-128">Chociaż hasła głównego hello jest znany, port 2222 jest niedostępny z hello internet.</span><span class="sxs-lookup"><span data-stu-id="35ce6-128">Although hello root password is known, port 2222 cannot be accessed from hello internet.</span></span> <span data-ttu-id="35ce6-129">Jest wewnętrzny tylko port dostępny tylko przez kontenery w ramach hello mostek sieci wirtualnej sieci prywatnej.</span><span class="sxs-lookup"><span data-stu-id="35ce6-129">It is an internal only port accessible only by containers within hello bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="35ce6-130">Upewnij się, toostart hello ssh usługi.</span><span class="sxs-lookup"><span data-stu-id="35ce6-130">Make sure toostart hello ssh service.</span></span> <span data-ttu-id="35ce6-131">przykład Witaj [tutaj](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) używa skryptu powłoki w */bin* katalogu.</span><span class="sxs-lookup"><span data-stu-id="35ce6-131">hello example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="35ce6-132">Plik Dockerfile Hello używa hello [ `CMD` instrukcji](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="35ce6-132">hello Dockerfile uses hello [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="35ce6-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="35ce6-133">Next steps</span></span>
<span data-ttu-id="35ce6-134">Zobacz hello następującego łącza Aby uzyskać więcej informacji dotyczących aplikacji sieci Web w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="35ce6-134">See hello following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="35ce6-135">Pytania i uwagi można umieścić na [naszym forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="35ce6-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="35ce6-136">Jak toouse Docker niestandardowego obrazu dla aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="35ce6-136">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="35ce6-137">Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="35ce6-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="35ce6-138">W aplikacji sieci Web platformy Azure w systemie Linux przy użyciu platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="35ce6-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="35ce6-139">W aplikacji sieci Web platformy Azure w systemie Linux przy użyciu Ruby</span><span class="sxs-lookup"><span data-stu-id="35ce6-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="35ce6-140">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="35ce6-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

