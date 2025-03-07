---
title: Specify virtual network types (load testing)
description: Learn how to use a network mix to create a closer approximation of how end-users interact with your applications.
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords: 
  - load tests, scenarios
  - load tests, adding networks
  - load tests, removing networks
  - load tests, virtual networks
  - network mix
ms.assetid: 3c4f7874-081a-4ec4-9510-4d6d7d863a11
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
---
# Specify virtual network types in a load test scenario

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

The *network mix* gives you a way to simulate load more realistically in a load test scenario. Load is generated by using a heterogeneous mix of network types instead of one single network type. You create a closer approximation of how end-users interact with your applications.

A network mix specifies the probability of a virtual user running a given *network profile*. A network profile is a simulation of network bandwidth at the application layer. It does not simulate latency.

When you create a load test, you might want to simulate that load is being generated through more than one type of network connection. The network mix offers several network types. The different networks are simulated. When you choose an option such as `Cable-DSL 1.5Mbps`, wait times are injected into the test to simulate the selected bandwidth.

The network mix works like other mix options. A network type is selected randomly associated with a virtual user, based on network mix. That user's tests are run using a particular network type, based on the probability you specified in the mix.

After you have specified a network mix, you can add and remove network types. You can also change the distribution of the network mix using the mix control.

The mix control lets you easily adjust the distribution of networks in a scenario.

For more information, see [About the mix control](../test/specify-virtual-network-types-in-a-load-test-scenario.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## True network emulation

Visual Studio uses software-based true network emulation for all test types including load tests. True network emulation simulates network conditions by direct manipulation of the network packets. The true network emulator can emulate the behavior of both wired and wireless networks by using a reliable physical link, such as an Ethernet. The following network attributes are incorporated into true network emulation:

- Round-trip time over the network (latency)

- The amount of available bandwidth

- Queuing behavior

- Packet loss

- Reordering of packets

- Error propagations.

True network emulation also provides flexibility in filtering network packets based on IP addresses or protocols such as TCP, UDP, and ICMP.

True network emulation can be used by network-based application developers and testers to emulate a desired test environment, assess performance, predict the impact of change, or make decisions about technology optimization. When compared to hardware test beds, true network emulation is a much cheaper and more flexible solution.

## To add new networks to a scenario

1. During the process of specifying the network mix for a scenario, choose **Add**.

     A new network entry is added to the grid.

    > [!NOTE]
    > To display the **Edit Network Mix** dialog box, right-click an existing scenario and then choose **Edit Network Mix**.

2. In the **Network Type** column, choose the arrow for the new entry. Choose the desired network type.

3. (Optional) Adjust the mix control to specify the test distribution. For more information, see [About the mix control](../test/specify-virtual-network-types-in-a-load-test-scenario.md).

4. When you are finished adding networks, choose **OK**.

## To remove networks from a scenario

1. Open a load test.

2. Right-click the scenario from which you want to remove a network, and choose **Edit Network Mix**. The **Edit Network Mix** dialog box is displayed.

3. Select the network in the grid and then choose **Remove**.

4. (Optional) Adjust the mix control to specify the test distribution. For more information, see [About the mix control](../test/specify-virtual-network-types-in-a-load-test-scenario.md).

5. When you are finished removing networks, choose **OK**.

## About the mix control

The mix control lets you adjust the percentage of load that is distributed among tests, browser types, or network types in a load test scenario. To adjust the percentage values, move the sliders. Adjusting the mix for network types specifies the probability of a virtual user running a specific network profile in a load test scenario.

When you move a slider, the percentage values of all available items change. If you have more than two items, the amount you add or remove is distributed evenly among the other items. It is possible to override this behavior. If you select the check box in the lock column for a particular item, you lock the specified percentage value for that item. Then, when you move a slider, the amount you add or remove is only applied to any remaining unlocked items.

The **Distribute** button is used to allocate the percentage values equally among all items. For example, if you have three items, choosing **Distribute** sets the percentage values to 34, 33, and 33.

> [!WARNING]
> The **Distribute** button overrides any items that are locked.

It is also possible to type the percentage values directly into the **%** column instead of using the sliders. If you enter a percentage value directly, the other items will not adjust automatically.

> [!NOTE]
> The sliders are disabled when the total does not add up to 100%, or when the percentage values entered into the **%** column are decimals.

When you enter percentage values manually, you should make sure that the sum of all items is 100%. When you save a mix, if the sum is not 100%, you will be prompted to accept the percent values as they are, or to go back and adjust them. If you choose to accept them as they are, they will be prorated to 100%.  For example, if you have two items and you manually set them to 80% and 40%, the first item will be set to 66.67% (80 divided by 120) and the second item will be set to 33.33% (40 divided by 120).
