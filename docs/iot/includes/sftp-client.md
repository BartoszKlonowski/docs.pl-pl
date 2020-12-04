---
ms.openlocfilehash: 60e326af0d956ceb63b32e5d3ec2436fe09a7005
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2020
ms.locfileid: "96589976"
---
[Korzystając z klienta SFTP](https://www.raspberrypi.org/documentation/remote-access/ssh/sftp.md), skopiuj pliki z lokalizacji publikowania na komputerze deweloperskim do nowego folderu w Raspberry Pi.

Aby na przykład użyć `scp` polecenia do kopiowania plików z komputera deweloperskiego do Raspberry Pi, Otwórz wiersz polecenia i wykonaj następujące czynności:

```console
scp -r /publish-location/* pi@raspberrypi:/home/pi/deployment-location/
```

Gdzie:

- `-r`Opcja powoduje, że `scp` Kopiowanie plików cyklicznie.
- */Publish-Location/* jest folderem opublikowanym w poprzednim kroku.
- `pi@raspberypi` jest nazwą użytkownika i hosta w formacie `<username>@<hostname>` .
- */Home/pi/Deployment-Location/* jest nowym folderem na Raspberry Pi.

> [!TIP]
> Najnowsze wersje systemu Windows mają OpenSSH, w tym `scp` , wstępnie zainstalowane.
