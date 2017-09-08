---
title: "Notas de versão de bibliotecas de gerenciamento do Azure para Java | Microsoft Docs"
description: "Veja o que há de novo e fique de olho em alterações significativas nas bibliotecas de gerenciamento do Azure para Java"
keywords: "Azure, Java, API, referência, anotações, atualizações, substituir, obsoleto"
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: fc246d499b2f5f20a7efbaed16c4b4193d8d8e6c
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2017
---
# <a name="release-notes"></a>Notas de versão 

## <a name="june-30-2017---110"></a>30 de junho de 2017 - 1.1.0 

A V1.1 é retrocompatível com a V1.0 nas APIs destinadas a uso público que atingiram o estágio de disponibilidade geral (estável) na V1.0.

Algumas alterações foram introduzidas em APIs marcadas com a anotação @Beta na V.0

Se você estiver migrando seu código para a versão 1.1.0, você pode usar [estas notas](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) para preparar o seu código para a versão 1.1.0 a partir da versão 1.0.0.

### <a name="generally-availabile-in-v11"></a>Geralmente disponível na V1.1

Algumas das APIs que ainda estavam em versão Beta na V1.0 estão agora na fase de Disponibilidade Geral (GA) na V1.1, em particular:

- métodos assíncronos
- todos os métodos na CDN que estavam anteriormente na versão Beta
- todos os métodos e interfaces no Gateway de Aplicativo que estavam anteriormente em versão Beta

 Algumas partes da biblioteca ainda estão em Versão Prévia. Consulte a tabela abaixo para saber o estado atual das bibliotecas:

Serviço ou recurso | Disponível como Disponibilidade Geral (GA) | Disponível como Versão Prévia  | Em breve |
---------|---------|---------|---------|
Computação  | Máquinas virtuais e extensões de VM, conjuntos de dimensionamento de máquina virtual, discos gerenciados   | Serviço de contêiner do Azure, registro de contêiner do Azure |    |
Armazenamento   |  Contas de armazenamento       |         |   Criptografia      |
Banco de dados SQL  | Bancos de dados, firewalls, pools elásticos        |         |   Mais recursos      |
Rede    |  Redes virtuais, interfaces de rede, endereços IP, tabelas de roteamento, grupos de segurança de rede, DNS, gerenciadores de tráfego, gateways de aplicativo  |    Balanceadores de carga     |   VPN, observadores de rede   |
Mais serviços    |  Gerenciador de Recursos, Cofre de Chaves, Redis, CDN, Lote       |  Aplicativos Web, Aplicativos de Funções, Barramento de Serviço, Grafo RBAC, DocumentDB   | Monitor, Agendador, gerenciamento de Funções, Pesquisa, mais recursos do Grafo RBAC        |
Conceitos básicos     |   Autenticação - básica, assíncrona       |      |         |

### <a name="import-with-maven"></a>Importar com Maven

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a>Obter ajuda e fazer comentários

Confira a comunidade de [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) para obter ajuda usando as bibliotecas em seu próprio código. Se você encontrar quaisquer bugs ou tiver sugestões para melhorar essas bibliotecas, arquive todas as questões através do [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).

### <a name="migrate-from-previous-releases"></a>Migrar de versões anteriores

[Migrar da versão 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md) [Migrar da versão 1.1.0  ](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)


