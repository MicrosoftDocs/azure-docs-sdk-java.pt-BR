---
title: Notas de versão de bibliotecas de gerenciamento do Azure para Java | Microsoft Docs
description: Veja o que há de novo e fique de olho em alterações significativas nas bibliotecas de gerenciamento do Azure para Java
keywords: Azure, Java, API, referência, anotações, atualizações, substituir, obsoleto
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 0aaa83ceb42192441decb5972baae56fed337fb2
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48898747"
---
# <a name="release-notes"></a>Notas de versão 

## <a name="october-5-2017---130"></a>5 de outubro de 2017 - 1.3.0 

A versão 1.3.0 é compatível com versões anteriores para serviços e uso de recursos que atingiram o estágio de disponibilidade geral (estável) em versões anteriores.

As alterações de última hora de versões de visualização para esses serviços são marcadas com a anotação @Beta.

Se você estiver migrando seu código para a versão 1.3.0, pode usar [estas notas](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) para preparar o seu código existente para a versão 1.3.

### <a name="generally-availabile-in-v13"></a>Geralmente disponível na V1.3

Algumas das APIs que ainda estavam em versões Beta anteriores estão agora na fase de Disponibilidade Geral (GA), em particular:

- métodos assíncronos
- todos os métodos na CDN que estavam anteriormente na versão Beta
- todos os métodos e interfaces no Gateway de Aplicativo que estavam anteriormente em versão Beta

  Algumas partes da biblioteca ainda estão em Versão Prévia. Consulte a tabela abaixo para saber o estado atual das bibliotecas:

Serviço ou recurso | Disponível como Disponibilidade Geral (GA) | Disponível como versão prévia 
---------|---------|---------|-
Computação  | Máquinas virtuais e extensões de VM, conjuntos de dimensionamento de máquina virtual, discos gerenciados   | Serviço de contêiner do Azure, registro de contêiner do Azure 
Armazenamento   |  Contas de armazenamento       |    Criptografia     
Banco de dados SQL  | Bancos de dados, firewalls, pools elásticos              
Rede    |  Redes virtuais, interfaces de rede, endereços IP, tabelas de roteamento, grupos de segurança de rede, DNS, gerenciadores de tráfego, gateways de aplicativo  |    Balanceadores de carga, Emparelhamento de rede, Gateway de Rede Virtual, Inspetores de rede 
Mais serviços    |  Gerenciador de Recursos, Cofre de Chaves, Redis, CDN, Lote       |  Aplicativos Web, Aplicativos de funções, Barramento de Serviço, Grafo RBAC, Cosmos DB, Pesquisar  
Conceitos básicos     |   Autenticação - núcleo, métodos assíncronos, identidade de serviço gerenciado      |      |

> Os recursos de visualização são marcados com uma anotação `@Beta` no nível de classe, interface ou método em bibliotecas. Esses recursos estão sujeitos a alterações. Eles podem ser modificados de alguma forma, ou até mesmo removidos, no futuro.

### <a name="import-with-maven"></a>Importar com Maven

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a>Obter ajuda e fazer comentários

Confira a comunidade de [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) para obter ajuda usando as bibliotecas em seu próprio código. Se você encontrar quaisquer bugs ou tiver sugestões para melhorar essas bibliotecas, arquive todas as questões através do [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).


