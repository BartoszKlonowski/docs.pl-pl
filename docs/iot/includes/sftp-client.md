---
ms.openlocfilehash: 60e326af0d956ceb63b32e5d3ec2436fe09a7005
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2020
ms.locfileid: "96589976"
---
<span data-ttu-id="4b102-101">[Korzystając z klienta SFTP](https://www.raspberrypi.org/documentation/remote-access/ssh/sftp.md), skopiuj pliki z lokalizacji publikowania na komputerze deweloperskim do nowego folderu w Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4b102-101">[Using an SFTP client](https://www.raspberrypi.org/documentation/remote-access/ssh/sftp.md), copy the files from the publish location on the development computer to a new folder on the Raspberry Pi.</span></span>

<span data-ttu-id="4b102-102">Aby na przykład użyć `scp` polecenia do kopiowania plików z komputera deweloperskiego do Raspberry Pi, Otwórz wiersz polecenia i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4b102-102">For example, to use the `scp` command to copy files from the development computer to your Raspberry Pi, open a command prompt and execute the following:</span></span>

```console
scp -r /publish-location/* pi@raspberrypi:/home/pi/deployment-location/
```

<span data-ttu-id="4b102-103">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="4b102-103">Where:</span></span>

- <span data-ttu-id="4b102-104">`-r`Opcja powoduje, że `scp` Kopiowanie plików cyklicznie.</span><span class="sxs-lookup"><span data-stu-id="4b102-104">The `-r` option instructs `scp` to copy files recursively.</span></span>
- <span data-ttu-id="4b102-105">*/Publish-Location/* jest folderem opublikowanym w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="4b102-105">*/publish-location/* is the folder you published to in the previous step.</span></span>
- <span data-ttu-id="4b102-106">`pi@raspberypi` jest nazwą użytkownika i hosta w formacie `<username>@<hostname>` .</span><span class="sxs-lookup"><span data-stu-id="4b102-106">`pi@raspberypi` is the user and host names in the format `<username>@<hostname>`.</span></span>
- <span data-ttu-id="4b102-107">*/Home/pi/Deployment-Location/* jest nowym folderem na Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4b102-107">*/home/pi/deployment-location/* is the new folder on the Raspberry Pi.</span></span>

> [!TIP]
> <span data-ttu-id="4b102-108">Najnowsze wersje systemu Windows mają OpenSSH, w tym `scp` , wstępnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="4b102-108">Recent versions of Windows have OpenSSH, which includes `scp`, pre-installed.</span></span>
