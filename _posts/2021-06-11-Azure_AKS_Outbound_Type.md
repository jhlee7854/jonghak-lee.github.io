---
layout: post
title: "AKS의 Outbound Type 요약"
date: 2021-06-11
categories: blog
tags: azure aks kubernetes
comments: true
---
AKS의 Worker Node는 Cluster의 생성, 업그레이드, 패치, 모니터링 등을 위한 kube-apiserver와의 통신, Node 생성을 위한 OS Image, Cluster 구성을 위한 Container Image 등이 필요하므로 Azure Global Service 및 클러스터 생생에 필요한 Service로의 Outbound가 필요하다.

AKS의 Outbound Type은 AKS를 생성할 때 지정할 수 있으며, `Load Balancer Type`과 `User Defined Route Type`으로 나뉜다.

Load Balancer Type의 경우 Cluster 생성 시 자동으로 Public IP와 Standard Load Balancer를 생성 및 설정하고 Outbound가 필요할 경우 이 경로를 이용한다.

User Defined Route Type의 경우 자동으로 Outbound 경로를 구성하지 않고 Worker Node가 위치한 Subnet의 UDR에 사용자가 직접 경로를 설정해야 한다.

## Load Balancer Type

AKS를 생성할 때 Outbound Type을 Load Balancer Type으로 설정하면 AKS는 자동으로 Public IP와 Standard Load Balancer를 생성하고 해당 경로를 통해 Worker Node의 Outbound를 처리한다.

AKS가 자동으로 Virtual Appliance(SLB)를 생성하고 Outbound 경로를 구성하므로 별다른 제약 조건이 없다면 간단하게 Stand Alone 형태로 AKS를 생성할 수 있다.

![Load Balancer type outbound for AKS]({{site.url}}/assets/images/aks-slb-outbound.png)

## User Defined Route Type

AKS를 생성할 때 Outbound Type을 User Defined Route Type으로 설정하면 AKS는  Load Balancer와 같은 Virtual Appliance를 자동으로 생성하지 않고 이미 생성되어 있다고 가정 하며, Worker Node가 위치한 Subnet의 UDR을 이용해 Outbound를 처리한다.

그러므로 AKS를 생성하기 전에 Outbound를 위한 별도의 Virtual Appliance가 필요하며, 해당 Virtual Appliance로 Outbound Traffic이 전달될 수 있도록 AKS의 Worker Node가 위치한 Subnet의 UDR을 사전에 설정해야 한다.

![클러스터 egress 트래픽에 대한 제한과 제어](https://docs.microsoft.com/en-us/azure/aks/media/limit-egress-traffic/aks-azure-firewall-egress.png)

또한 Virtual Appliance가 Azure Firewall이라면 모든 트랙픽이 Firewall을 통과해야 하므로 Firewall Policy에 AKS와 관련된 Outbound 정책 설정이 필요하다. 이와 관련된 내용은 다음 링크를 참조한다.

[AKS Cluster를 위한 필수 Outbound 네트워크 규칙 및 FQDN](https://docs.microsoft.com/en-us/azure/aks/limit-egress-traffic#required-outbound-network-rules-and-fqdns-for-aks-clusters)

## Load Balancer Type과 Azure Firewall

Azure Firewall을 사용하여 Outbound Traffic을 통제하는 네트워크에서 Outbound Type이 Load Balancer Type으로 생성된 AKS는 추가적인 네트워크 설정이 필요하다.

Load Balancer를 통해 Worker Node로 들어온 패킷은 응답할때 네트워크 통제를 위해 Firewall의 Private IP로 라우팅 된다. 이때 Azure Firewall은 세션의 상태를 관리하기 때문에 이처럼 다른 경로로 들어온 세션은 인지할 수 없어 패킷을 제거해 버리는 `비대칭 라우팅` 문제가 발생할 수 있다.

이러한 문제를 해결하기 위해 다음과 같이 Azure Firewall에서는 Load Balancer로 DNAT 설정을 해 주고, Worker Node가 있는 Subnet의 UDR에서는 Internet 트래픽에 대해 Azure Firewall의 Public IP로 라우팅 설정이 필요하다.

![Azure Firewall과 Standard Load Balancer 통합 - 비대칭 라우팅 문제 해결 방안](https://docs.microsoft.com/en-us/azure/firewall/media/integrate-lb/firewall-lb-asymmetric.png)

### References

[클러스터 egress 트래픽에 대한 제한과 제어](https://docs.microsoft.com/en-us/azure/aks/limit-egress-traffic#restrict-egress-traffic-using-azure-firewall)

[Egress에 사용자 정의 경로 사용하기](https://docs.microsoft.com/en-us/azure/aks/egress-outboundtype)

[Azure Firewall과 Standard Load Balancer 통합](https://docs.microsoft.com/en-us/azure/firewall/integrate-lb)
