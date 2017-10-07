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
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Obsługa protokołu SSH dla aplikacji sieci Web platformy Azure w systemie Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Omówienie

[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) kryptograficznych protokół sieci bezpieczny sposób za pomocą usług sieciowych. Toolog najczęściej używane do systemu zdalnie bezpieczny z wiersza polecenia i jest zdalnie wykonać poleceń administracyjnych.

Sieci Web aplikacji w systemie Linux zapewnia obsługę SSH do kontenera aplikacji hello z każdym hello wbudowanych Docker obrazami używanymi na potrzeby hello stosu środowiska uruchomieniowego nowych aplikacji sieci web. 

![Stosy środowiska wykonawczego](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

Za pomocą protokołu SSH i niestandardowe obrazy usługi Docker jako część obrazu hello w tym hello SSH serwera i jego konfigurowania, zgodnie z opisem w tym temacie.



## <a name="making-a-client-connection"></a>Połączenia klienta

toomake połączenie klienta SSH hello lokacji głównej musi być uruchomiona. 

Wklej hello końcowy zarządzania kontroli źródła (SCM) dla aplikacji sieci web w przeglądarce, za pomocą hello następującej postaci:

        https://<your sitename>.scm.azurewebsites.net/webssh/host

Jeśli nie są już uwierzytelniony, to wymagana tooauthenticate z tooconnect Twojej subskrypcji platformy Azure.

![Połączenie SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>Obsługa protokołu SSH z niestandardowymi obrazami Docker

Aby niestandardowe Docker obrazu toosupport SSH komunikacji między hello kontenera i powitania klienta w portalu Azure hello wykonaj następujące kroki dla obrazu Docker hello. 

Te kroki są są wyświetlane w hello repozytorium w usłudze Azure App Service jako przykład [tutaj](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).

1. Zawierają hello `openssh-server` instalacji w [ `RUN` instrukcji](https://docs.docker.com/engine/reference/builder/#run) w hello plik Dockerfile dla obrazu i ustawić hello hasło dla konta głównego hello także`"Docker!"`. 

    > [!NOTE] 
    > Ta konfiguracja nie zezwala na połączenia zewnętrzne toohello kontenera. SSH jest możliwy tylko za pośrednictwem hello Kudu / SCM lokacji, który jest uwierzytelniany przy użyciu hello poświadczeń publikowania.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. Dodaj [ `COPY` instrukcji](https://docs.docker.com/engine/reference/builder/#copy) toocopy plik Dockerfile toohello [sshd_config](http://man.openbsd.org/sshd_config) pliku toohello */itp/ssh/* katalogu. Plik konfiguracji powinny być oparte na naszych sshd_config plik w repozytorium GitHub usługi App hello [tutaj](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).

    > [!NOTE] 
    > Witaj *sshd_config* plik musi zawierać następujące hello lub hello połączenie nie powiedzie się: 
    > * `Ciphers`musi zawierać co najmniej jedną z następujących hello: `aes128-cbc,3des-cbc,aes256-cbc`.
    > * `MACs`musi zawierać co najmniej jedną z następujących hello: `hmac-sha1,hmac-sha1-96`.

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Dołączyć portu 2222 hello [ `EXPOSE` instrukcji](https://docs.docker.com/engine/reference/builder/#expose) dla hello plik Dockerfile. Chociaż hasła głównego hello jest znany, port 2222 jest niedostępny z hello internet. Jest wewnętrzny tylko port dostępny tylko przez kontenery w ramach hello mostek sieci wirtualnej sieci prywatnej.

    ```docker
    EXPOSE 2222 80
    ```

4. Upewnij się, toostart hello ssh usługi. przykład Witaj [tutaj](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) używa skryptu powłoki w */bin* katalogu.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Plik Dockerfile Hello używa hello [ `CMD` instrukcji](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello skryptu.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>Następne kroki
Zobacz hello następującego łącza Aby uzyskać więcej informacji dotyczących aplikacji sieci Web w systemie Linux. Pytania i uwagi można umieścić na [naszym forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Jak toouse Docker niestandardowego obrazu dla aplikacji sieci Web platformy Azure w systemie Linux](app-service-linux-using-custom-docker-image.md)
* [Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux](app-service-linux-using-nodejs-pm2.md)
* [W aplikacji sieci Web platformy Azure w systemie Linux przy użyciu platformy .NET Core](app-service-linux-using-dotnetcore.md)
* [W aplikacji sieci Web platformy Azure w systemie Linux przy użyciu Ruby](app-service-linux-ruby-get-started.md)
* [Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania](app-service-linux-faq.md)

