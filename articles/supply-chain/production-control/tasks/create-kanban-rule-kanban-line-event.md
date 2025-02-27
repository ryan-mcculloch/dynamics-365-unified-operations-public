--- 
# required metadata 
 
title: Create a kanban rule using a kanban line event
description: This procedure creates a kanban rule by using the kanban line event setting to trigger pull from a process activity. 
author: ChristianRytt
ms.date: 08/29/2018
ms.topic: business-process 
ms.prod:  
ms.technology:  
 
# optional metadata 
 
ms.search.form: KanbanRules, LeanProductionFlowActivityLookup, SalesTableListPage, SalesCreateOrder, SalesTable   
audience: Application User 
# ms.devlang:  
ms.reviewer: kamaybac
# ms.tgt_pltfrm:  
# ms.custom:  
ms.search.region: Global
ms.search.industry: Manufacturing
ms.author: crytt
ms.search.validFrom: 2016-06-30 
ms.dyn365.ops.version: Version 7.0.0 
---
# Create a kanban rule using a kanban line event

[!include [banner](../../includes/banner.md)]

This procedure creates a kanban rule by using the kanban line event setting to trigger pull from a process activity. The kanban rule is triggered by a kanban process activity, with a quantity equal to or greater than 25 each. The demo data company used to create this task is USMF. This task is intended for the process engineer or the value stream manager, as they prepare production of a new or modified product in a lean environment.


## Create a kanban rule
1. Go to Product information management > Lean manufacturing > Kanban rules.
2. Click New.
3. In the Replenishment strategy field, select 'Event'.
    * This generates kanbans directly from demand. It is used to set up rules that define a make-to-order scenario.  
4. In the First plan activity field, enter or select a value.
    * Enter or select SpeakerAssemblyAndPolish. The first activity of a manufacturing kanban rule is a process activity in the production flow. When you select the activity, the validity dates of the activity are copied to the validity dates of the kanban rule.  
5. Expand the Details section.
6. In the Product field, type 'L0001'.
7. Expand the Events section.
8. In the Kanban line event field, select 'Automatic'.
    * This generates event kanbans on demand.  The field is used to configure kanban rules that replenish material that is required for a downstream process activity. When you select Automatic, the event kanbans are created with the demand. This setting is recommended if you expect to execute production on the same day.  
9. Set Minimum event quantity to '25'.
    * Event kanbans are generated when the demand quantity is equal to or more than this field. This is useful if you want to produce an order quantity less than this field on one machine and more than this field on another machine.  
10. Click Save.

## Create sales order and trigger kanban chain
1. Go to Sales and marketing > Sales orders > All sales orders.
2. Click New.
3. In the Customer account field, enter or select a value.
    * Select Customer account US-003, Forest Wholesales.  
4. Click OK.
5. In the Item number field, type 'L0001'.
    * L0001 is the item for which you created the kanban rule.  
6. Set Quantity to '27'.
    * Because 27 is higher than the minimum quantity of 25 on the kanban rule, this will trigger an event kanban.  
7. In the Site field, type '1'.
8. In the Warehouse field, enter or select a value.
    * Select warehouse 13.  
9. Click Save.

## View the kanban generated by the kanban rule
1. Go to Product information management > Lean manufacturing > Kanban rules.
2. In the list, find and select the desired record.
3. Expand the Kanbans section.
    * Notice that a kanban for 27 was created to process the  activity based on the created kanban rule.  
    * This is the last step.  



[!INCLUDE[footer-include](../../../includes/footer-banner.md)]